# Product

## One engine, both editors

The founders want everything at once: Premiere-style editing, After Effects-style motion
graphics, short and long form. The **architecture supports all of it from day 1**. The
**feature depth ships in order**, so two people can actually finish it.

### Project format v2

Extends SceneWright v1 ([`src/project/schema.ts`](../../src/project/schema.ts)).

```
Project
├── settings      (resolution, fps, aspect: 9:16 / 16:9 / 1:1)
├── brand kit     (color tokens, fonts, logos)            ← exists in v1
├── assets        (footage proxies, images, audio, transcripts)
└── timeline
    ├── video track    → clips (source in/out, speed, transform, zoom, reframe)
    ├── audio track    → clips (volume, ducking, fades)
    ├── caption track  → words from transcript, styled by a caption template
    └── graphics track → composition clips
                          └── SceneWright scene graph (text, shapes, images, logos,
                              devices, particles, animations) ← exists in v1
                              (compositions can nest)
```

- **Premiere half:** tracks and clips.
- **After Effects half:** composition clips, i.e. SceneWright scenes nested on the timeline.

### Shipping order

| Order | Surface | Why first / later |
|---|---|---|
| 1 | Reels from talking-head footage (9:16) | What the first buyers post most; fastest to show value |
| 2 | Motion-graphics overlays on those reels | Our quality advantage; reuses the SceneWright engine |
| 3 | Long-form 16:9 YouTube edits | Same model, longer media; needs performance work |
| 4 | Keyframe tracks + full compositor (AE-style) | Pro depth for editors and agencies |

## Autopilot: the fully automatic path

One click (or one sentence to the user's AI) goes from raw footage to a finished reel.

| Step | Runs without AI (deterministic) | Uses the user's AI (via MCP) |
|---|---|---|
| Transcribe (in browser, word timestamps) | ✓ | |
| Cut silences, fillers, retakes | ✓ | Ambiguous retakes |
| Pick the hook (first 3 seconds) | Fallback: first strong sentence | ✓ |
| Captions in the chosen style | ✓ | |
| Punch-in zooms on emphasis + face-tracked 9:16 reframe | ✓ | Which moments to emphasise |
| Graphics callouts (lists, stats, lower thirds, chapter cards) | Fallback: none | ✓ Which points, what text |
| Music bed with ducking | ✓ | Mood choice |
| Quality lint, then fix | ✓ check | ✓ fix |
| Export 9:16 (+ 16:9) | ✓ | |

The deterministic column follows SceneWright's offline planner
([`src/ai/heuristic.ts`](../../src/ai/heuristic.ts)): the product still works when the user has
no AI connected.

## MCP tool surface

Remote MCP server with OAuth. Target clients: Claude, ChatGPT, Codex, Cursor.

| Group | Tools |
|---|---|
| Read | `list_projects`, `get_project_outline`, `get_transcript(range)`, `get_frames(times)` (contact-sheet images so the AI can *see* the cut), `list_templates`, `lint_project` |
| Write | `apply_ops([...])` with typed ops: cut, trim, move, caption style, add graphic (template + text + time), zoom, reframe, music, brand. Also `run_autopilot(preset)`, `undo`, `snapshot` |
| Output | `render_preview` (still or low-res clip), `export` (cloud render with credits; the free export runs in the browser app) |

**Rules:**
- Every write is a typed, validated operation: no free-form code and no raw JSON overwrites.
  Invalid ops are rejected with a reason the agent can act on.
- Every agent run creates a snapshot, so the user can revert the whole run.
- **MCP App UI:** an inline preview player with approve / revert, shown inside Claude and
  ChatGPT (MCP Apps, official since Jan 2026).

### Hard rule: bring-your-own AI

**Never** accept, store or proxy a user's Claude/ChatGPT login or subscription token. The only
path is the user adding our MCP connector in their AI client. AI providers' terms forbid
anything else, and it would be a security liability.

## Generative video: optional layer only

- Generated clips (Veo, Kling, Seedance, etc.) can come in later as **B-roll layers** on the
  timeline, paid with credits.
- They are always one editable layer among many, never the core of the product.
- Check each model's licence before adding an adapter (see SceneWright's
  [license audit](../LICENSE_AND_DEPENDENCY_AUDIT.md)).
