# Positioning

## The line

> **The pro editor your AI can drive.** Premiere + After Effects in the browser for talking-head
> educators. Every caption, zoom and graphic stays editable, and nothing looks like AI slop.

## Who it's for first

**Talking-head educators:** coaches, finance, tech, fitness and language creators who film
themselves.
- They post short-form often (Reels, Shorts, TikTok), and often long-form too.
- Today they pay an editor, or spend hours in CapCut, Submagic or Descript.
- They need: clean cuts, captions that look designed, punch-in zooms, on-screen graphics
  (lists, stats, chapter cards), brand consistency and speed.

## Where we sit

| | Generative video (Higgsfield, Veo, Kling) | MCP editors (invideo, Clueso, OpusClip, Cardboard) | Caption tools (Submagic, Captions) | **Us** |
|---|---|---|---|---|
| Output | New pixels | Edited footage | Captioned clips | Edited footage + designed motion graphics |
| Editable afterwards | No | Partly | Captions only | **Every layer, every property** |
| Brand-exact | No | Varies | Templates | **Brand kit tokens across every layer** |
| AI cost to vendor | High (GPU) | Medium–high | Medium | **≈ $0 (user's AI via MCP, user's browser)** |
| Quality control | Prompting | Prompting | Presets | **Designer templates + quality lint gate** |

## Moat, most defensible first

1. **Taste encoded as data.**
   - The motion-designer cofounder makes caption styles, motion presets and graphic templates.
   - A deterministic **quality lint** must pass before export.
   - The agent composes only from vetted parts, so it can't produce slop.
   - Competitors can copy features, but not years of craft decisions held in a template library.
2. **Agent-native project format.**
   - A typed timeline with nested compositions. Agents change it only through validated edit
     operations.
   - This is SceneWright's rule: the AI emits **data, never code**.
   - Every agent edit is undoable, diffable and previewable.
3. **Near-zero marginal cost.**
   - The user's AI does the thinking; the user's browser renders and transcribes.
   - We can price below rivals and still keep 85%+ gross margin.
4. **Later: network effects.**
   - A template marketplace (designers sell styles).
   - Brand kits and team workspaces that agencies don't want to leave.

## The "not slop" quality system

| Part | What it is | Owner |
|---|---|---|
| Caption styles | ~10 at launch: type, size, word-highlight motion, safe placement | Motion designer |
| Motion presets | Easing curves, durations, stagger, entrances/exits: one house motion language | Motion designer |
| Graphic templates | ~20 at launch: lower thirds, title cards, kinetic text, lists, stat callouts, chapter cards | Motion designer |
| Brand kit | Colors, fonts, logos as tokens (`@primary` etc., already in SceneWright) | User |
| Quality lint | Platform safe zones, text overflow, contrast, caption line length, pacing (max seconds without a visual change), clipped faces | Engineering |
| Export gate | Errors block export; warnings show to user and agent; the agent is asked to fix them | Engineering |

**Rule:** if a template or preset can make something the motion designer wouldn't post, it
doesn't ship.

## What we are not

- Not a generative-footage company. Generated clips are an **optional layer**, never the core.
- Not a "prompt → finished video, no edits" toy. Every output opens in a full editor.
- Not an AI reseller. Users bring their own AI. Bundled AI credits come later, and only if
  conversion needs them.
