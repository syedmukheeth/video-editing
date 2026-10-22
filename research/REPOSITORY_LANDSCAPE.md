# Repository Landscape

_Research date: 2026-10-22. Author: SceneWright core team._

## How this was researched (and what was not possible)

Every repository below was verified in this session by **shallow-cloning it from GitHub**
(`git clone --depth 1 --filter=blob:none`) and reading files at `HEAD`: the license file,
`README.md`, and package manifests. Activity was measured with
`git fetch --shallow-since=2026-04-22` and `git rev-list --count`. Release tags were read with
`git ls-remote --tags`. npm versions, licenses and publish dates come from
`registry.npmjs.org`.

Limitations, stated plainly:

- **The GitHub REST API (`api.github.com`) was blocked** by this environment's network policy
  (HTTP 403), so **star counts, issue counts and GitHub "Releases" pages were not collected**.
  We do not quote star numbers anywhere in this document.
- **huggingface.co was blocked**, so model-weight licenses were verified only where the
  license text or license statement is shipped inside the GitHub repository. Where it is
  not, this is marked _unverified_.
- "Commits in last 6 months" counts commits on the default branch since 2026-04-22. For
  very large monorepos the number includes bot and release commits; treat it as an activity
  signal, not a quality measure.
- Feature descriptions are taken from each project's own README unless otherwise stated.
  We did not run every project.

## Summary table

| Project | URL | What it is | Lang | License (verified file) | Last commit | Commits since 2026-04-22 |
|---|---|---|---|---|---|---|
| Remotion | https://github.com/remotion-dev/remotion | React components → video via headless Chrome + FFmpeg | TS | **Remotion License** (custom, source-available; company license above 3 employees) | 2026-10-22 | 7,628 |
| HyperFrames | https://github.com/heygen-com/hyperframes | HTML/CSS + seekable animations → deterministic MP4 via headless Chrome + FFmpeg; agent skills | TS | Apache-2.0 | 2026-10-21 | 5,422 |
| Motion Canvas | https://github.com/motion-canvas/motion-canvas | Generator-based TS animation library + editor | TS | MIT | 2026-07-02 | 1 (npm `@motion-canvas/core` 3.17.2 published 2024-12-14) |
| Revideo | https://github.com/redotvideo/revideo | Motion Canvas fork with headless render API + React player | TS | MIT | 2026-07-15 | 19 |
| Manim (3b1b) | https://github.com/3b1b/manim | Python math animation engine (OpenGL) | Python | MIT | 2026-09-09 | n/a |
| Manim Community | https://github.com/ManimCommunity/manim | Community fork of Manim | Python | MIT | 2026-10-20 | 127 |
| Theatre.js | https://github.com/theatre-js/theatre | Keyframe animation library + visual studio for web/three.js | TS | core Apache-2.0, **studio AGPL-3.0-only** | 2024-04-11 | 0 |
| three.js | https://github.com/mrdoob/three.js | WebGL/WebGPU 3D library | JS | MIT | 2026-10-22 | active (r186 tag) |
| React Three Fiber | https://github.com/pmndrs/react-three-fiber | React renderer for three.js | TS | MIT | 2026-10-14 | active |
| Blender | https://github.com/blender/blender | Full 3D suite with Python API and headless rendering | C/C++/Py | GPL (COPYING → GPL) | 2026-10-22 | active (v5.2.x tags) |
| FFmpeg | https://github.com/FFmpeg/FFmpeg | Encode/decode/filter/mux everything | C | LGPL-2.1+ with optional GPL parts | 2026-10-22 | active |
| MLT | https://github.com/mltframework/mlt | Multimedia framework behind Shotcut/Kdenlive | C/C++ | LGPL-2.1 | 2026-10-21 | active |
| libopenshot | https://github.com/OpenShot/libopenshot | Video editing library behind OpenShot | C++ | LGPL-3.0 | 2026-10-21 | active |
| Shotcut | https://github.com/mltframework/shotcut | Desktop NLE | C++/Qt | GPL-3.0 | 2026-10-21 | active |
| Kdenlive | https://github.com/KDE/kdenlive | Desktop NLE | C++/Qt | GPL-3.0 | 2026-10-22 | active |
| Olive | https://github.com/olive-editor/olive | Desktop NLE (rewrite) | C++ | GPL-3.0 | 2024-12-05 | — (stalled) |
| Natron | https://github.com/NatronGitHub/Natron | Node-based compositor | C++ | GPL-2.0 | 2026-07-24 | low |
| editly | https://github.com/mifi/editly | Declarative JSON → video via Node + FFmpeg | TS | MIT | 2025-02-20 | 0 |
| Diffusion Studio Core | https://github.com/diffusionstudio/core | Browser video composition engine (WebCodecs) | TS | MPL-2.0 | 2025-11-18 | 0 |
| Mediabunny | https://github.com/Vanilagy/mediabunny | Pure-TS media muxing/demuxing/WebCodecs toolkit | TS | MPL-2.0 | 2026-10-20 | 420 |
| ffmpeg.wasm | https://github.com/ffmpegwasm/ffmpeg.wasm | FFmpeg compiled to WebAssembly | TS/C | MIT wrapper (FFmpeg core keeps its own license) | 2025-09-16 | — |
| @napi-rs/canvas | https://github.com/Brooooooklyn/canvas | Skia-backed Canvas 2D API for Node, prebuilt binaries | Rust/TS | MIT | 2026-10-21 | 129 |
| skia-canvas | https://github.com/samizdatco/skia-canvas | Skia Canvas 2D for Node | Rust/TS | MIT | 2026-10-12 | 331 |
| node-canvas | https://github.com/Automattic/node-canvas | Cairo-backed Canvas for Node | C++/JS | MIT (per npm; no root LICENSE file at HEAD) | 2026-10-19 | active |
| PixiJS | https://github.com/pixijs/pixijs | 2D WebGL/WebGPU renderer | TS | MIT | 2026-10-10 | active |
| Konva | https://github.com/konvajs/konva | Canvas 2D scene graph | TS | MIT | 2026-10-14 | active |
| Fabric.js | https://github.com/fabricjs/fabric.js | Interactive canvas object model | TS | MIT | 2026-10-21 | active |
| lottie-web | https://github.com/airbnb/lottie-web | After Effects (Bodymovin) JSON player | JS | MIT | 2024-11-19 | — (low) |
| GSAP | https://github.com/greensock/GSAP | Tweening/timeline library | JS | **"Standard no-charge license"** (not OSI) | 2026-04-13 | low |
| Motion | https://github.com/motiondivision/motion | React/JS animation library | TS | MIT | 2026-10-22 | active |
| ComfyUI | https://github.com/comfyanonymous/ComfyUI | Node-graph inference UI/server for diffusion models | Python | GPL-3.0 | 2026-10-21 | 1,134 |
| diffusers | https://github.com/huggingface/diffusers | PyTorch diffusion pipelines (image/video) | Python | Apache-2.0 | 2026-10-22 | active |
| LTX-Video | https://github.com/Lightricks/LTX-Video | Video generation model code (superseded by LTX-2) | Python | code Apache-2.0 | 2026-01-06 | 0 |
| LTX-2 | https://github.com/Lightricks/LTX-2 | Audio+video generation model | Python | **LTX-2.x Community License** (paid license above US$10M revenue) | 2026-10-18 | active |
| Wan 2.1 / 2.2 | https://github.com/Wan-Video/Wan2.2 | Open-weight text/image-to-video | Python | Apache-2.0 (README states models are Apache-2.0) | 2026-09-21 | active |
| HunyuanVideo | https://github.com/Tencent/HunyuanVideo | Text-to-video model | Python | **Tencent Hunyuan Community License** (excludes EU, UK, South Korea) | 2026-10-08 | active |
| CogVideo | https://github.com/THUDM/CogVideo | CogVideoX models | Python | code Apache-2.0; 2B weights Apache-2.0; 5B weights "CogVideoX LICENSE" (_text not verifiable here_) | 2025-11-04 | 0 |
| Mochi | https://github.com/genmoai/mochi | Mochi 1 video model | Python | Apache-2.0 (repo) | 2026-10-06 | active |
| Open-Sora | https://github.com/hpcaitech/Open-Sora | Open video generation training/inference | Python | Apache-2.0 | 2026-04-09 | low |
| FLUX | https://github.com/black-forest-labs/flux | Image generation inference code | Python | code Apache-2.0; **FLUX.1 [dev] weights Non-Commercial**; FLUX.1 [schnell] weights Apache-2.0 | 2025-07-31 | — |
| Ollama | https://github.com/ollama/ollama | Local LLM runtime with OpenAI-compatible API | Go | MIT | 2026-10-21 | active |
| Motionly / Motify | https://github.com/COPPSARY/Motionly | AI-assisted HTML + GSAP motion graphics editor | TS/Svelte | Apache-2.0 (depends on GSAP's non-OSI license) | 2026-10-21 | active |
| OpenChatCut | https://github.com/0xsline/OpenChatCut | Agent-driven multitrack video editor (MCP) | TS | AGPL-3.0 (and depends on Remotion packages) | 2026-10-21 | active |
| SynthCut | https://github.com/Relo-video/SynthCut | Multitrack editor exposed as an MCP server, FFmpeg backend | TS | GPL-3.0 | 2026-07-21 | — |
| OpenCut | https://github.com/OpenCut-app/OpenCut | Web/desktop video editor, **being rewritten** in Rust | Rust/TS | MIT (per README badge; LICENSE begins "Copyright 2026 OpenCut") | 2026-09-24 | — |
| MoneyPrinterTurbo | https://github.com/harry0703/MoneyPrinterTurbo | Topic → script + stock footage + subtitles + music short videos | Python | MIT | 2026-10-21 | 646 |
| react-video-editor (designcombo) | https://github.com/designcombo/react-video-editor | React timeline editor UI | TS | **"OpenVideo License"** (custom, company tier) | 2026-06-29 | 1 |

## Category analysis

### A. Motion graphics and programmatic animation

**Remotion** is the most mature "code → video" system in the JavaScript ecosystem and by far
the most active (7.6k commits in six months). Its authoring model is React components; it
renders by driving headless Chrome frame-by-frame and encoding with FFmpeg. **It is not
open-source in the OSI sense.** We read `LICENSE.md` at HEAD: free use is limited to
individuals, for-profit organisations with up to 3 employees, non-profits and evaluation;
everyone else needs a paid Company License, and "it is not allowed to copy or modify
Remotion code for the purpose of selling, renting, licensing, relicensing, or sublicensing
your own derivate of Remotion". The file also announces license changes for Remotion 5.0.
For an open-core product that wants agencies and companies as users, making Remotion a hard
dependency would push every company user above three employees into a Remotion purchase.
_Role: reference design only, not a dependency._

**HyperFrames** (HeyGen, Apache-2.0) is the strongest permissively licensed renderer in this
space. Its README states compositions are HTML files with data attributes, the renderer
"seeks each frame in headless Chrome and encodes the result with FFmpeg", and it requires
Node 22+ and FFmpeg. Packages inspected: `engine` (Puppeteer + FFmpeg), `producer`,
`player`, `studio`, `lint`, cloud adapters for AWS Lambda and GCP Cloud Run. Very high churn
(5.4k commits in six months; v0.8.x). Its contract is that **an AI agent writes HTML/CSS/JS**;
the README describes skills that teach agents to "write valid HTML, wire seekable
animations". That is the opposite of our security requirement that model output is data,
never code. _Role: strong candidate for a future optional "HTML layer" backend or export
target; not the core engine for v0.1._

**Motion Canvas** (MIT) has an excellent generator-based API, but the last npm release of
`@motion-canvas/core` is 3.17.2 from 2024-12-14 and there was one commit to the default
branch in the last six months. **Revideo** (MIT fork) adds headless rendering but has low
activity (19 commits). Both are code-authoring tools (TypeScript generators), again
requiring code generation rather than data generation. _Role: design inspiration (signals,
tweening API); not adopted._

**Manim** (MIT, Python) is mature and active but is specialised for mathematical
animation and would introduce a Python runtime and LaTeX/Cairo/OpenGL dependencies.
_Not adopted._

**Theatre.js**: no commits since 2024-04-11. Its `@theatre/studio` package is
`AGPL-3.0-only` (verified in `theatre/studio/package.json`) while `@theatre/core` is
Apache-2.0. _Not adopted; the keyframe-sequencing idea is on our roadmap._

**GSAP**: the repository has no LICENSE file; `package.json` says
`"Standard 'no charge' license: https://gsap.com/standard-license"`. Free to use but not an
OSI license, with terms controlled by a single vendor. _Not adopted._

**lottie-web** (MIT): last commit 2024-11-19. Lottie JSON is still a valuable interchange
format. _Roadmap: Lottie import as a layer type._

### B. 3D graphics and rendering

**three.js** (MIT, extremely active) is the obvious choice for in-browser 3D.
**React Three Fiber** (MIT) makes it ergonomic in React. The hard part for a video product
is *server-side, deterministic* 3D rendering: three.js needs WebGL, which in Node means
headless Chrome (or `headless-gl`). **Blender** (GPL) can render headlessly via
`blender -b` and a Python script, as a **subprocess**, which keeps our code license-clean
(we would not link against it), but it is a ~300 MB+ install with GPU-sensitive render
times. _Decision: no 3D in v0.1. Planned path: a `three` layer type rendered in-browser for
preview and via a headless-Chromium frame capture backend for export; Blender only as an
optional out-of-process "render farm" adapter later._

### C. Video processing and compositing

**FFmpeg** is unavoidable and the right tool for encoding, muxing audio and probing. We
invoke the `ffmpeg`/`ffprobe` binaries as subprocesses (verified locally: FFmpeg 6.1.1 with
libx264). We do not link to FFmpeg libraries and do not redistribute binaries, which keeps
the GPL/LGPL obligations on the distributor of the binary (the OS package manager), not on us.

**MLT / libopenshot / Shotcut / Kdenlive / Natron / Olive** are full C++ NLE stacks under
LGPL/GPL. They are the right tools for long-form clip editing but bring heavy native builds
and do not provide a programmable motion-graphics model. _Not adopted._

**editly** (MIT) is conceptually close to us — declarative JSON → video with Node + FFmpeg
and Canvas/Fabric layers — but has had no commits since 2025-02-20. _Reference for the
"declarative spec" idea; not a dependency._

**Diffusion Studio Core** (MPL-2.0, no commits since 2025-11) and **Mediabunny**
(MPL-2.0, very active, pure TypeScript muxers/WebCodecs) enable in-browser encoding.
_Roadmap: Mediabunny for a "render in the browser" export path that needs no server._
MPL-2.0 is file-level copyleft and compatible with an MIT/Apache app as long as the MPL
files themselves stay under MPL.

**Canvas 2D in Node**: we compared `@napi-rs/canvas` (MIT, 0 npm dependencies, prebuilt
Skia binaries, 129 commits in six months, v1.0.13 published 2026-10-21), `skia-canvas`
(MIT, 3 deps, v4.0.0) and `node-canvas` (Cairo, requires system libraries on some
platforms). We spiked `@napi-rs/canvas`: it registered `@fontsource` **woff2** files,
rendered gradients, shadow-glow and text, and streamed 60 RGBA frames into FFmpeg producing
a valid 640×360 H.264 file in ~0.6 s. _Adopted._

### D. AI video and image generation

**ComfyUI** (GPL-3.0, very active) is the de-facto open orchestration server for diffusion
image/video models, with an HTTP + WebSocket API and workflow JSON. Because it is GPL, we
talk to it **only over its network API as a separately deployed service** — no code import.
_Roadmap: `ComfyUIAssetProvider` that submits a workflow and imports resulting images/clips
as assets._

**diffusers** (Apache-2.0) is the library-level alternative; it would require us to operate a
Python GPU service. _Deferred; ComfyUI covers the same need with less code from us._

Open-weight video models (software license vs. weights license — these differ):

| Model | Code license | Weights license (as stated in the GitHub repo) | Commercial notes |
|---|---|---|---|
| Wan 2.1 / 2.2 | Apache-2.0 | README: "The models in this repository are licensed under the Apache 2.0 License" | Most permissive of the strong models. |
| LTX-Video (≤0.9.x) | Apache-2.0 | README links to an OpenRAIL-M license for 0.9.5 (hosted on HF, _not verified here_) | Use-based restrictions (OpenRAIL). |
| LTX-2.x | LTX Community License (`LICENSE`, `LICENSE-2_x`) | Same | Commercial entities with annual revenue ≥ US$10M need a paid license. |
| HunyuanVideo | Tencent Hunyuan Community License | Same | **Does not apply in the EU, UK, South Korea**; extra MAU thresholds. |
| CogVideoX | Apache-2.0 | 2B: Apache-2.0; 5B: "CogVideoX LICENSE" on HF (_not verified here_) | Check before use. |
| Mochi 1 | Apache-2.0 | README describes an open model; _weights license not verified here_ | Check before use. |
| FLUX.1 [dev] | Apache-2.0 | `model_licenses/LICENSE-FLUX1-dev`: **Non-Commercial License v1.1.1** | Not for commercial use without BFL license. |
| FLUX.1 [schnell] | Apache-2.0 | `model_licenses/LICENSE-FLUX1-schnell`: Apache-2.0 | OK. |

Hardware: all of these require a CUDA GPU (typically 12–80 GB VRAM depending on model and
resolution). None is appropriate as a mandatory dependency of a local MVP.

**LLM providers for planning**: the Anthropic Messages API (official
`@anthropic-ai/sdk`, Apache-2.0) supports JSON-schema-constrained structured output;
**Ollama** (MIT) and most local servers expose an OpenAI-compatible
`/v1/chat/completions` endpoint, which lets users run planning fully locally.

### E. Existing open-source AI creative applications

- **Motionly / Motify** (Apache-2.0): the closest product to our vision. README: HTML
  compositions + GSAP timelines are the project source; visual editor; deterministic scrub;
  H.264 export; "AI generation and editing" in its cloud mode; bundled agent skills that
  write compositions. Runtime dependency on GSAP (non-OSI license) and analytics SDKs
  (`@datadog/browser-rum`, `posthog-js`, `@vercel/analytics` in `dependencies`).
- **OpenChatCut** (AGPL-3.0): agent + multitrack timeline + MCP; depends on `remotion`,
  `@remotion/renderer` etc., so it inherits Remotion's license terms in addition to AGPL.
- **SynthCut** (GPL-3.0): editor exposed as an MCP server with FFmpeg processing.
- **OpenCut** (MIT): popular editor, currently being rewritten (README: "being rewritten from
  the ground up"; classic version in `opencut-app/opencut-classic`).
- **MoneyPrinterTurbo** (MIT, Python): topic → script → stock footage → subtitles → music.
  A pipeline for faceless short-form videos, not an editable motion-graphics tool.
- **react-video-editor** (designcombo): custom "OpenVideo License" with a company tier.

## Shortlist and roles in SceneWright

| Need | Selected | Integration style | Why |
|---|---|---|---|
| Frame rasterisation (server) | `@napi-rs/canvas` | npm dependency | MIT, zero deps, prebuilt, same Canvas 2D API as browsers, spike passed |
| Frame rasterisation (preview) | Browser Canvas 2D | built-in | Same engine code as export |
| Encoding / muxing / probing | FFmpeg CLI | subprocess | Universal; no linking |
| Schema + validation | Zod 4 | npm dependency | MIT, zero deps, emits JSON Schema |
| HTTP API | Hono + @hono/node-server | npm dependency | MIT, zero deps, tiny |
| Editor UI | React 19 + Vite | npm dependency | MIT, standard, no SSR needed |
| LLM planning | `@anthropic-ai/sdk`; OpenAI-compatible HTTP | adapter | Structured output; local models via Ollama |
| Fonts | `@fontsource/*` (OFL-1.1) | npm dependency | Same woff2 files in browser and Skia |
| Generative image/video (later) | ComfyUI | separate service over HTTP | Keeps GPL and GPU out of core |
| 3D (later) | three.js | npm dependency + headless Chromium capture | MIT, ubiquitous |
| Browser-side export (later) | Mediabunny | npm dependency | Active, MPL-2.0 |
