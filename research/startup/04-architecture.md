# Architecture

The budget is under $2k for six months, so the main design rule is: **the user's AI thinks,
the user's browser renders, we only store and coordinate.**

## Who pays for what

| Work | Runs on | Cost to us |
|---|---|---|
| Planning, judgment, copywriting | User's AI (Claude / ChatGPT / Codex via MCP) | $0 |
| Transcription | User's browser (Whisper, WebGPU / WASM) | $0 |
| Preview + standard export | User's browser (WebCodecs) | $0 |
| Face tracking for reframe | User's browser (MediaPipe) | $0 |
| Project data, proxies, transcripts | Our storage (R2 + database) | ≈ $0.015 per GB-month |
| Cloud render (automatic / 4K / no browser open) | Our container, on demand | Paid by user credits (priced ≥ 5× cost) |

## Stack

| Concern | Choice | Why |
|---|---|---|
| Editor | React 19 + Vite (from SceneWright) + new multitrack timeline | Reuse existing code |
| Decode / encode / mux | WebCodecs + **Mediabunny** (MPL-2.0) | $0 render cost. Avoid Remotion packages (company license required) |
| Compositing | SceneWright engine on Canvas 2D; move the hot path to WebGL/WebGPU only if 1080p preview stutters | Same code for preview and export |
| Transcription | Whisper via transformers.js on WebGPU, WASM fallback | $0. Week-1 spike checks word timestamps (transformers.js #820) |
| Reframe / face tracking | MediaPipe in browser (Apache-2.0) | $0 |
| Footage handling | Originals stay on the user's disk (File System Access / OPFS); upload only 720p proxies, transcripts, thumbnails | Storage ≈ $0; fast uploads |
| API + MCP server | Hono (already used) on Cloudflare Workers; remote MCP with OAuth; same Zod schemas | One codebase; free or cheap tier |
| Database / files | Postgres free tier (Neon or Supabase) or Cloudflare D1; R2 for files (no egress fees) | < $10/month |
| Cloud render (paid) | SceneWright [`src/render/`](../../src/render/) (Skia + FFmpeg) in a container on a cheap VPS, on demand | Only paying jobs cost money |
| Payments | Merchant of record (Paddle, Lemon Squeezy or similar) | Handles global VAT/GST and regional prices |
| Auth | Better Auth (self-hosted) or a Clerk free tier | $0 |

## Data flow

```
 User's disk (original 4K footage)
      │  decode in browser (WebCodecs)
      ▼
 Browser app ── transcript, 720p proxy, thumbnails ──▶ R2 / database
      │  preview + export (WebCodecs → MP4)                │
      ▼                                                    ▼
 Final MP4 on user's disk                Remote MCP server (Cloudflare Workers)
                                                           ▲
                                     user's Claude / ChatGPT / Codex calls tools
                                     (apply_ops, get_frames, lint_project, …)

 Paid path: originals uploaded → render container (Skia + FFmpeg) → MP4 → deleted after N days
```

## What to reuse from SceneWright

Copy these into the **new private product repo** (not into this research repo):

| SceneWright code | Becomes |
|---|---|
| [`src/project/schema.ts`](../../src/project/schema.ts) + [`migrate.ts`](../../src/project/migrate.ts) | Format v2 (tracks, clips, compositions) with a v1→v2 migration |
| [`src/project/edit.ts`](../../src/project/edit.ts) | The pure edit operations behind `apply_ops` |
| [`src/engine/`](../../src/engine/) (animation, easing, draw, text, timeline, render) | The composition renderer |
| [`src/storyboard/scene-kinds.ts`](../../src/storyboard/scene-kinds.ts), [`moods.ts`](../../src/storyboard/moods.ts), [`templates.ts`](../../src/storyboard/templates.ts) | The first graphic templates |
| [`src/ai/heuristic.ts`](../../src/ai/heuristic.ts), [`src/ai/generate.ts`](../../src/ai/generate.ts) | Autopilot fallback, and the validate-or-fall-back pattern for every MCP input |
| [`src/render/`](../../src/render/), [`src/server/jobs.ts`](../../src/server/jobs.ts) | Cloud render worker and queue |
| [`src/editor/`](../../src/editor/) | Editor shell, inspector, brand panel |
| [`tests/`](../../tests/), [`e2e/`](../../e2e/) | Testing discipline (Vitest + Playwright) |

**Changes from SceneWright:**
- The built-in Anthropic/OpenAI planners become optional. MCP is the main path.
- The server gains auth and per-user isolation; SceneWright's server is single-user and
  localhost-only.
- File storage moves behind the existing `ProjectStore` interface to R2 + database.

## Legal and licensing notes

| Item | Status |
|---|---|
| SceneWright code already published | Stays Apache-2.0 forever for anyone who copied it |
| New product code | Can be closed: the founders own SceneWright and write the new code |
| SceneWright README / CLAUDE.md | Update to say "archived research" once the product repo exists |
| Mediabunny (MPL-2.0) | Fine in a closed product if its files aren't modified (or modifications are published) |
| Remotion packages | Avoid: company license required |
| H.264 patents | Browser export uses the OS/browser encoder. Cloud rendering with x264 needs advice before charging |
| Product name | Trademark search needed (US, EU, India) before launch |
| Generative model adapters | Check each model's weights/terms licence before adding |

Open items carried over from SceneWright's
[license audit §7](../LICENSE_AND_DEPENDENCY_AUDIT.md) still apply.
