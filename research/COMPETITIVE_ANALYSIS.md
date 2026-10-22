# Competitive Analysis

_Research date: 2026-10-22._

**Evidence standard.** We say a product "does X" only when its own repository or
documentation says so, and we cite the source. We do **not** say a product lacks a
feature unless we checked its source; where we only have third-party claims we label them
as such. Proprietary products were not used hands-on in this research.

## 1. Proprietary AI video platforms

### Higgsfield (proprietary, hosted)

What we could verify from public pages (search results; vendor pages are self-reported):

- Vendor FAQ (https://geo.higgsfield.ai/higgsfield-ai-features-faq) lists Soul Cast
  (character consistency), Cinema Studio, Click-to-Ad (ads from product URLs),
  Higgsfield Audio, style transfer and motion effects.
- A third-party comparison (https://blog.segmind.com/higgsfield-ai-vs-runway-key-differences/)
  describes multi-model generation (Seedance, Kling, Wan, Flux and others) and states that
  output is a generated file. A competitor's blog (https://ltx.studio/blog/best-higgsfield-alternatives)
  claims it lacks storyboarding and editing; **this is a competitor's claim and we did not
  verify it.**

Positioning: Higgsfield is a generation platform built on diffusion video models. Its
strength is photoreal and stylised footage, which SceneWright does not attempt in v0.1.
Our wedge is the *other* half of a launch video: typography, brand-accurate layouts,
product screenshots, logo reveals and transitions that must be exact, editable and
reproducible. Long term these combine: generated clips become assets inside an editable
SceneWright project.

## 2. Open-source projects closest to SceneWright

| Product | License | Source of truth | AI authoring model | Editable afterwards | Export path |
|---|---|---|---|---|---|
| **Motionly / Motify** | Apache-2.0 (runtime depends on GSAP standard no-charge license) | README at HEAD | Agent skills write `composition.html` + `timeline.js`; cloud mode has chat-based "AI generation and editing" | Yes (visual editor over HTML; position/scale/rotation/opacity/text) | In-browser, H.264 MP4 (`mp4-muxer` in deps) |
| **HyperFrames** | Apache-2.0 | README + package manifests | Agent writes HTML/CSS + seekable animations; linter checks it | Yes, by editing HTML (studio package exists) | Headless Chrome + FFmpeg, local/Docker/Lambda/Cloud Run |
| **Remotion** (+ AI prompts) | Remotion License (source-available) | LICENSE.md | Model writes React/TSX | Yes, by editing code | Headless Chrome + FFmpeg |
| **OpenChatCut** | AGPL-3.0 + Remotion deps | README, package.json | Agents drive a multitrack timeline (MCP) | Yes (tracks, clips, captions) | Remotion renderer + FFmpeg |
| **SynthCut** | GPL-3.0 | README | MCP client drives 85 editor tools (README) | Yes | FFmpeg |
| **MoneyPrinterTurbo** | MIT | README | LLM writes script; stock footage matched | Limited (regenerate) | MoviePy/FFmpeg |
| **editly** | MIT | README | None built in | JSON spec | FFmpeg, inactive since 2025-02 |

## 3. Unmet needs SceneWright targets

These are gaps relative to the specific projects above, stated precisely.

1. **AI output as validated data, not code.** Motionly, HyperFrames and Remotion-based
   workflows (per their READMEs) have the model write HTML/JS/TSX that is then executed in
   a browser. That is powerful but makes the AI path a code-execution path, requires linting
   / sandboxing, and makes results hard to edit for non-developers. SceneWright's model
   output is a strict storyboard; nothing the model writes is executed.
2. **Form-based editing of every generated property.** Because the project is a typed scene
   graph, the editor exposes text, colors, timing, easing and animation parameters as
   controls — no code view required for the core workflow.
3. **Brand tokens.** Elements reference `@primary` / `@accent` etc., so "change the brand
   color" is one edit that updates every scene. (We did not find an equivalent concept in
   the READMEs of the projects above; we have not exhaustively checked their docs, so we do
   not claim they lack it.)
4. **Works with no AI key and no GPU.** A deterministic planner produces a usable
   multi-scene project from a brief offline; local LLMs via OpenAI-compatible servers are
   first-class.
5. **Permissive core with no non-OSI runtime dependencies.** Every runtime dependency is
   MIT, Apache-2.0 or OFL (fonts). No Remotion company license, no GSAP license, no
   analytics SDKs in the app.
6. **Same engine for preview and export without a headless browser.** Export runs on Skia
   in Node; no Chrome download is needed to render.
7. **Honest capability reporting.** Requests the planner cannot honour (3D, music sync,
   generated footage in v0.1) are listed in the generation report instead of silently
   ignored.

## 4. Where competitors are ahead (and what we do about it)

| Area | Who is ahead | Our plan |
|---|---|---|
| Expressiveness | HyperFrames/Remotion/Motionly — anything HTML/React can do | Grow the primitive set; add an optional HTML layer backend later (ADR-007) |
| Generated footage | Higgsfield and other hosted platforms | ComfyUI asset provider; generated clips become editable layers |
| Timeline editing of clips/audio | OpenChatCut, SynthCut, Kdenlive, Shotcut | Scene-based editor first; multitrack and audio in later milestones |
| Cloud rendering at scale | HyperFrames (Lambda/Cloud Run packages), Remotion Lambda | Render backend interface allows a hosted runner later |
| Community & templates | Remotion | Template/scene-kind registry designed for contributions |

## 5. Target users for v0.1

- Indie founders and small marketing teams who need a 10–30 s launch/promo video with
  exact product copy and brand colors.
- Developers who want a scriptable, open, reproducible motion-graphics renderer
  (`npm run render -- project.json out.mp4`).
- Agencies that want an open, self-hostable base they can extend with their own templates.
