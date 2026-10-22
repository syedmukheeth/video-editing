# Risks and verification

## Top risks

| # | Risk | Impact | What we do about it |
|---|---|---|---|
| 1 | **Crowded MCP-editor market** (invideo, Clueso, OpusClip, Descript, Cardboard, Palmier) | Users see us as "another one" | Win on craft + quality lint for one niche. Every demo shows the visible quality gap |
| 2 | **Scope:** "all at once" with 2 people | Nothing ships well | One unified format; depth shipped in order; weekly gates; cut list in [05-roadmap.md](05-roadmap.md) |
| 3 | **Browser limits:** WebCodecs on Safari/Firefox, memory for long 4K, AAC encoding support | Export fails for some users | Chrome/Edge first; cloud render as fallback; week-1 spike |
| 4 | **Users without a paid AI plan, or MCP setup friction** | Lower activation | Autopilot's deterministic steps work with no AI; one-click connector setup guide; bundled AI credits later if conversion needs it |
| 5 | **Platform risk:** Claude/ChatGPT directory rules change; CapCut or Descript add strong agents | Distribution or differentiation loss | Own the editor, template library and project format, not just the connector |
| 6 | **Budget under $2k** | Can't buy growth or GPUs | All compute on the user's side; growth from content and partners |
| 7 | **Legal:** H.264 patents for cloud rendering; trademark; music licensing; generative-model licences | Fines or forced rename | Advice before charging for cloud render; trademark search in week 0; licensed music only |
| 8 | **Strategy leaks:** this research sits in a public repo | Competitors read the plan | Don't push `research/startup/` until the repo is private |
| 9 | **Founder risk:** two founders, no written agreement | Disputes over equity or SceneWright IP | Founder agreement with vesting and IP assignment in week 0 |

## Verification gates

### Technical

| Gate | Pass condition | When |
|---|---|---|
| Browser export spike | 60 s 1080p 9:16 MP4 with AAC, export ≤ 1× real time on Chrome/Edge | Week 1 |
| Transcription spike | Word timestamps within ±100 ms on a 10-min file, in browser | Week 1 |
| MCP spike | One full agent edit round-trip in Claude **and** ChatGPT | Week 1 |
| Automated tests | Vitest + Playwright cover format v2, edit ops and quality lint | From week 2 |
| End-to-end test | Raw talking-head file → Autopilot → MCP edit → export → check codec, duration, safe zones | Week 6 |

### Product

| Gate | Pass condition | When |
|---|---|---|
| Problem confirmed | 10+ of 15–20 interviewed educators score pain ≥ 4 and (spend ≥ 3 or a commitment); see [10-interview-script.md](10-interview-script.md) | Week 0 |
| Activation | 50% of beta users export within 15 minutes | Week 7 |
| Willingness to pay | 30–50 paying users | Week 8 |
| Retention | 60% of payers still active after month 1 | Month 3 |

### Business

| Gate | Pass condition | When |
|---|---|---|
| MRR on track | Within 30% of the milestone table in [05-roadmap.md](05-roadmap.md) | Monthly |
| Pivot check | If month-6 MRR is under $8k, stop feature work and re-interview customers | Month 6 |
