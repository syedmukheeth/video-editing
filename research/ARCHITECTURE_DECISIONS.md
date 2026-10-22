# Architecture Decisions

This file records the decisions behind SceneWright v0.1 and the evidence behind them.
Each decision has a status, the alternatives that were considered, and what would make us
revisit it. Evidence is in [REPOSITORY_LANDSCAPE.md](REPOSITORY_LANDSCAPE.md) and
[LICENSE_AND_DEPENDENCY_AUDIT.md](LICENSE_AND_DEPENDENCY_AUDIT.md).

## Product thesis in one paragraph

Generative video models produce flattened pixels you cannot edit. Code-first motion
frameworks (Remotion, HyperFrames, Motion Canvas, Motionly) produce editable output, but
their AI workflows ask a model to **write executable code**. SceneWright has the model
produce **data**: a small, strictly validated storyboard. A deterministic compiler turns
that into a versioned project file, which a deterministic engine renders identically in the
browser preview and in the exported MP4. Every scene, element and animation stays editable,
and the engine works fully without AI.

## System overview

```
           ┌──────────────────────────── Browser (React editor) ───────────────────────────┐
 brief ──▶ │ New-project form ─▶ POST /api/projects ─┐                                      │
           │ Scene list · Inspector · Brand panel   │      ┌── engine/renderFrame ─▶ <canvas>│
           │      │ edits (pure reducers)           │      │   (same code as export)       │
           │      └─▶ project JSON ─ autosave PUT ──┼──────┘                               │
           └────────────────────────────────────────┼──────────────────────────────────────┘
                                                    ▼
           ┌──────────────────────────── Node server (Hono) ───────────────────────────────┐
           │ ai/  provider.plan(brief) ─▶ untrusted JSON ─▶ Storyboard schema (strict)       │
           │        └─ fail / no key ─▶ heuristic planner (deterministic fallback)          │
           │ storyboard/compile ─▶ Project (schema v1, strict) ─▶ storage/ (files on disk)  │
           │ render/ job queue ─▶ engine/renderFrame on @napi-rs/canvas ─▶ RGBA ─▶ ffmpeg   │
           │                                                     └─▶ ffprobe verification   │
           └───────────────────────────────────────────────────────────────────────────────┘
```

## Module boundaries (the seven interfaces)

| # | Interface | Location | Contract |
|---|---|---|---|
| 1 | Project specification | `src/project/schema.ts` | Zod schema for format `scenewright.project` v1; `parseProject(unknown)` returns a typed `Project` or structured issues. Strict objects: unknown keys are rejected. JSON Schema is exported to `docs/project.schema.json`. |
| 2 | Scene graph | `src/engine/timeline.ts` | Pure functions: scene start times with transition overlap, total duration, frame count, `scenesAt(time)`. |
| 3 | Animation primitives | `src/engine/animation.ts`, `src/engine/easing.ts` | `evaluateElement(element, localTime, sceneDuration)` → transform/opacity/reveal state. Each primitive is a pure function in a registry. |
| 4 | AI providers | `src/ai/types.ts` | `PlannerProvider.plan(request, signal)` returns `unknown`. The caller validates against `StoryboardSchema`; providers never construct projects. |
| 5 | Asset management | `src/engine/types.ts` (`AssetResolver`), `src/server/storage.ts` | Engine asks `assets.get(assetId)` for a drawable; browser and Node supply different loaders. Files live in `<project>/assets/` and are referenced by id. |
| 6 | Rendering engine | `src/engine/render.ts`, `src/render/` | `renderFrame(ctx, project, time, env)` draws onto any Canvas 2D context. `renderVideo(project, options)` validates, streams frames to FFmpeg, verifies with ffprobe. |
| 7 | Editor interface | `src/editor/` | React components operate on a `Project` via pure update functions (`src/project/edit.ts`) with undo/redo; persistence goes through the REST API. |

## ADR-001: Own a small declarative engine on Canvas 2D instead of adopting a code-first framework

**Status:** accepted.

**Context.** We need (a) browser preview, (b) server-side export that matches it, (c) a
project representation that a model can produce safely and a human can edit with forms.

**Options considered.**

| Option | Pros | Cons |
|---|---|---|
| Remotion | Most mature, huge ecosystem | Custom license: company license above 3 employees, ban on selling derivatives. Authoring = React code. Headless Chrome required for export. |
| HyperFrames | Apache-2.0, very active, deterministic | Authoring = HTML/CSS/JS written by an agent. v0.x with very high churn. Puppeteer + Chrome required. |
| Motion Canvas / Revideo | MIT, nice API | Motion Canvas effectively unmaintained since Dec 2024; Revideo low activity; authoring = TS generators. |
| editly | MIT, declarative JSON | No commits since Feb 2025; clip-oriented, not motion-graphics oriented. |
| **Own engine on Canvas 2D** | Data-only projects; same code in browser (native canvas) and Node (`@napi-rs/canvas`); no headless browser for export; small surface we fully control | We implement layout, animation and transitions ourselves. Canvas 2D has no 3D. |

**Decision.** Implement a ~1–2k line engine that evaluates a declarative scene graph and
draws with the Canvas 2D API. Reuse Skia via `@napi-rs/canvas` for server rasterisation and
FFmpeg for encoding. We are not building low-level infrastructure: rasterisation (Skia),
font shaping (Skia/browser), encoding (x264 via FFmpeg) and the UI framework (React) are all
reused. What we own is the domain model (scene graph, primitives, transitions), which is
the product.

**Evidence.** A spike registered `@fontsource` woff2 fonts in `@napi-rs/canvas`, drew a
gradient, glow and text, and piped 60 frames to `ffmpeg -c:v libx264`, producing a valid
640×360 H.264 file in ~0.6 s (ffprobe: 60 frames, 2.000 s).

**Revisit if** we need DOM/CSS layout fidelity, 3D, or complex text shaping (RTL, CJK
line-breaking) that Canvas 2D handles poorly — then add an *additional* backend (see
ADR-007) rather than replacing this one.

## ADR-002: The AI produces a storyboard, not a project and never code

**Status:** accepted.

The model's job is creative planning: choose scene kinds, write copy, pick a mood and
palette, allocate time. Layout and animation choreography are deterministic.

1. Provider returns `unknown` JSON (structured outputs are requested where supported).
2. `StoryboardSchema` (strict Zod) validates it: enumerated scene kinds, length-limited
   strings, hex colors, bounded durations, ≤ 12 scenes. Unknown keys are rejected.
3. `compileStoryboard()` maps each scene kind through a registered **scene-kind compiler**
   to concrete elements and animations that reference brand tokens (`@primary`, …).
4. The compiled project is validated again with the project schema before it is returned.

Why not let the model emit the full project? It could — the project schema is equally
strict — but the storyboard is ~10× smaller, much more reliable for small/local models,
and lets us improve layouts without re-prompting. Full-project editing by AI (e.g. "make
scene 3 faster") is on the roadmap as validated *patch operations*, not free-form code.

Text from the model is rendered with `fillText` only. There is no HTML, no `eval`, no
expressions, no URLs fetched from model output, and no file paths: assets are referenced by
opaque ids that must already exist in the project.

## ADR-003: Deterministic fallback planner

**Status:** accepted. A rule-based planner (`src/ai/heuristic.ts`) extracts product name,
duration, mood, colors, requested scene types and a call to action from the brief with
regular expressions and keyword tables, and reports requested capabilities that v0.1 cannot
do (3D, music, voice-over, generated footage). It is used when no provider is configured,
when a provider errors, refuses, times out or returns invalid data. The generation report
returned to the UI always states which planner produced the result and why.

## ADR-004: Provider adapters

`PlannerProvider` implementations shipped in v0.1:

- `heuristic` – always available.
- `anthropic` – official `@anthropic-ai/sdk`, `output_config.format` JSON schema, model
  configurable (default `claude-opus-5-5`), `fallbacks: "default"` for server-side refusal
  fallback, explicit handling of `stop_reason: "refusal"` and `"max_tokens"`.
- `openai-compatible` – plain `fetch` to `/v1/chat/completions` with
  `response_format: {type: "json_object"}`; works with Ollama, LM Studio, vLLM and hosted
  OpenAI-compatible APIs. No SDK dependency needed for a single endpoint.

Adding a provider = one file implementing `plan()` + one line in the registry.

## ADR-005: Project format — versioned JSON, normalised coordinates, brand tokens

- `format: "scenewright.project"`, `version: 1`. Loading a different version fails with a
  clear message; `src/project/migrate.ts` is the single place future migrations go.
- Positions and sizes are **fractions of the frame** (x, y, width relative to width; font
  size relative to height) so a project can be re-rendered at another resolution.
- Colors are hex or **brand tokens** (`@primary`, `@secondary`, `@accent`, `@background`,
  `@text`). Changing the brand color updates every element that references it.
- Fonts are an enum of bundled OFL families; this keeps renders reproducible because the
  same font files are used by the browser preview and the exporter.
- Scenes have explicit durations. A scene's `transition` overlaps the end of the previous
  scene (standard NLE semantics): `start[i] = start[i-1] + duration[i-1] - transition[i]`.
- "Out" animations are anchored to the element's end, so changing a scene's duration keeps
  exits at the end.
- Assets are stored next to the project file and referenced by id. **Export bundles**
  embed assets as base64 so a single `.scenewright.json` file is fully reproducible.

Full specification: [docs/PROJECT_FORMAT.md](../docs/PROJECT_FORMAT.md).

## ADR-006: Stack

| Concern | Choice | Rejected (and why) |
|---|---|---|
| Language | TypeScript everywhere | Python service for rendering: unnecessary second runtime |
| UI | React 19 + Vite 8 (SPA) | Next.js: no SSR/SEO need; adds a server model we don't use |
| API server | Hono on Node 22 | Express (28 deps), Fastify (15 deps) — both fine but heavier than needed |
| Validation | Zod 4 | Ajv + hand-written JSON Schema: worse TS inference |
| Persistence | JSON files under `DATA_DIR` | SQLite/Postgres: not needed for single-user local MVP; storage is behind `ProjectStore` interface |
| Jobs | In-process sequential queue | Redis/BullMQ: no multi-process requirement yet |
| Encoding | FFmpeg CLI (system binary, `FFMPEG_PATH` override) | `ffmpeg-static`: redistributes GPL binaries via npm; ffmpeg.wasm: slow |
| Tests | Vitest + Playwright (Chromium) | — |
| Containers | none in v0.1 | Docker adds nothing for a local app; can be added for cloud rendering |

TypeScript is pinned to 5.9 (not the 7.x native port) for compatibility with tooling.

## ADR-007: Future backends and integrations (not in v0.1)

- **3D**: `three.js` layer type. Preview in-browser; export via a headless-Chromium frame
  capture backend (Playwright is already a dev dependency) composited under the Canvas 2D
  layers. Blender as an optional out-of-process adapter for high-quality product renders.
- **HTML layer**: optional HyperFrames-based backend for users who want CSS layout, behind
  the same `renderVideo` interface.
- **Generated assets**: `AssetProvider` interface; first adapter talks to a user-run ComfyUI
  server over HTTP (keeps GPL code and GPUs out of the core).
- **Browser-only export**: Mediabunny + WebCodecs.
- **Audio**: soundtrack asset muxed by FFmpeg; beat markers to snap scene durations.

## ADR-008: Open core boundary

Everything required to create, edit, preview, render and export projects locally is in this
repository under Apache-2.0 and stays there. Potential hosted services (cloud rendering,
hosted AI credits, team storage/collaboration, premium template packs) plug in through the
same interfaces a self-hoster can implement: `PlannerProvider`, `ProjectStore`, a render
job runner, and template/scene-kind registries. The local app must never require a hosted
service, and no feature is removed from local mode to drive upgrades.

## Assumptions

- Single user, local machine, trusted network (the server binds to `127.0.0.1` by default
  and has no authentication).
- FFmpeg with libx264 is installed on the machine that renders.
- Target output is H.264 MP4 (yuv420p, so width and height must be even).
- Projects up to 10 minutes and 4K; render time is CPU-bound and roughly linear in frames.
