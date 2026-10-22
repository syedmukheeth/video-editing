# License and Dependency Audit

_Date: 2026-10-22. This is an engineering audit, not legal advice. Have counsel review before
commercial distribution._

## 1. SceneWright's own license

**Apache-2.0.** Chosen because:

- it is permissive (companies and agencies can adopt and extend it, which the product needs),
- it includes an explicit patent grant (relevant in video/codec-adjacent software),
- it is compatible with every runtime dependency below (MIT, Apache-2.0, OFL fonts as separate
  files, Unlicense),
- it permits an open-core model: hosted services can be built on it without relicensing.

GPL/AGPL components (FFmpeg GPL builds, ComfyUI, Blender) are only ever used as **separate
programs** (subprocess or network service), never linked or imported, so they do not
impose their terms on SceneWright's source. See §4.

## 2. Production dependencies (verified from the installed tree)

Generated with `npm run licenses` (reads each installed package's `package.json`):

| License | Packages |
|---|---|
| MIT | `@napi-rs/canvas` (+ platform binaries), `hono`, `@hono/node-server`, `zod`, `react`, `react-dom`, `scheduler`, `tsx`, `esbuild` (tsx dependency), `@babel/runtime`, `json-schema-to-ts`, `ts-algebra`, `standardwebhooks`, `@stablelib/base64` |
| Apache-2.0 | `@anthropic-ai/sdk`, `@opentelemetry/api` (SDK dependency) |
| OFL-1.1 | `@fontsource/inter`, `@fontsource/space-grotesk`, `@fontsource/playfair-display` |
| Unlicense | `fast-sha256` (SDK dependency) |

23 production packages in total; no copyleft licenses, no "source-available" licenses, no
unknown licenses at the npm-package level.

Development-only dependencies (Vite, Vitest, TypeScript, Playwright, type packages) are MIT
or Apache-2.0 and are not shipped in the built app.

### Notes on specific dependencies

- **`@napi-rs/canvas`** is MIT, but its prebuilt binary statically includes Skia and other
  native libraries. The package ships a CycloneDX SBOM (`sbom.cdx.json`, 142 components). We
  read it: licenses include BSD-2/3-Clause, Apache-2.0, MIT, Zlib, ISC, ICU, **FTL**
  (FreeType), **IJG** (libjpeg-turbo), libpng-2.0, and **MPL-2.0** (Rust crates `cssparser`,
  `selectors`, `dtoa-short`). Nine components have no license recorded in the SBOM.
  _Action before binary redistribution (e.g. a desktop app or Docker image):_ include the
  SBOM-derived third-party notices; FTL and IJG require attribution in documentation. MPL-2.0
  is file-level copyleft and only obliges us to provide source for those (unmodified) files.
- **Fonts (OFL-1.1)**: may be bundled, embedded and used commercially; they may not be sold
  on their own, and modified versions must be renamed. Rendered videos are not subject to the
  OFL.
- **`@anthropic-ai/sdk`** (Apache-2.0): license covers the SDK code only. Use of the Claude
  API is governed by Anthropic's commercial terms, which are separate from this repository.

## 3. External programs (not npm dependencies)

| Program | License | How we use it | Obligations / risks |
|---|---|---|---|
| FFmpeg | LGPL-2.1+; builds with `--enable-gpl` (e.g. libx264, as in Ubuntu's package) are GPL | `ffmpeg`/`ffprobe` subprocess; user installs it | No obligation for SceneWright source. If **we** ever redistribute FFmpeg binaries (Docker image, desktop installer, `ffmpeg-static`), we must comply with the GPL/LGPL for those binaries (offer source, include license). H.264 encoding may also carry **patent licensing** questions (MPEG LA / Via LA pools) for commercial distribution of encoders — needs legal review before shipping a bundled encoder or a paid hosted renderer. |
| Chromium (Playwright) | BSD-3-Clause + others | E2E tests only | None for users. |

## 4. Projects researched but not integrated — license implications

| Project | License | Why it matters |
|---|---|---|
| Remotion | Remotion License (custom) | Free only for individuals, ≤3-employee companies, non-profits; others need a paid Company License; prohibits selling derivatives. **Incompatible with our open-core goal as a hard dependency.** |
| `@theatre/studio` | AGPL-3.0-only | Would force AGPL on network deployments if linked. |
| GSAP | "Standard no-charge license" (vendor terms) | Free but not OSI; terms controlled by vendor. |
| ComfyUI | GPL-3.0 | OK as a **separately deployed service** reached over HTTP; never import its code. |
| Blender | GPL | OK as a **subprocess**; scripts we pass to Blender that use `bpy` are arguably derivative works of Blender if distributed — keep them in a separate GPL-licensed plugin repo. |
| OpenChatCut | AGPL-3.0 (+ Remotion deps) | Not reusable in an Apache project. |
| react-video-editor (designcombo) | Custom "OpenVideo License" | Company tier — avoid. |

## 5. AI model and weight licenses (separate from software licenses)

SceneWright v0.1 bundles **no model weights**. LLM planning uses either a hosted API (user's
own key and terms) or a user-run local server. When generative image/video adapters are
added, each model's **weights license** must be checked independently of its code license:

| Model | Weights license (as stated in its GitHub repo) | Commercial use |
|---|---|---|
| Wan 2.1 / 2.2 | Apache-2.0 (README) | Yes, with attribution. |
| FLUX.1 [schnell] | Apache-2.0 (`model_licenses/LICENSE-FLUX1-schnell`) | Yes. |
| FLUX.1 [dev] | FLUX.1 [dev] Non-Commercial License v1.1.1 | **No** without a BFL license. |
| LTX-2.x | LTX-2.x Community License | Paid license required for entities with ≥ US$10M annual revenue. |
| LTX-Video 0.9.5 | OpenRAIL-M (linked from README; text hosted on Hugging Face, not verified here) | Use-based restrictions. |
| HunyuanVideo | Tencent Hunyuan Community License | **Not licensed in the EU, UK or South Korea**; other conditions. |
| CogVideoX-5B | "CogVideoX LICENSE" on Hugging Face (not verified here — HF blocked in this environment) | Unverified. |

Rule for future adapters: the adapter must declare the model's license id, and the UI must
show it before generation. Hosted (paid) generation must default to commercially licensed
models only.

## 6. Assets

- No third-party images, video, music or logos are committed. The example project uses only
  generated shapes, a generated placeholder UI and bundled OFL fonts.
- "Nova" in the example is a fictional product name chosen by the brief in the task
  description.
- Uploaded user assets stay in the user's data directory and are never sent to AI providers
  (only the text brief is sent).

## 7. Unresolved items before commercial deployment

1. H.264 patent licensing for a hosted/paid rendering service or a bundled encoder.
2. Third-party notices file for the `@napi-rs/canvas` native binary when redistributing
   binaries (desktop/Docker).
3. Trademark: check "SceneWright" for conflicts before public launch. Only two things were
   checked: the npm package name was unregistered, and `github.com/scenewright/scenewright`
   did not resolve as a public repository.
4. Weight licenses for any generative model adapter (§5), verified against the actual
   Hugging Face license files.
