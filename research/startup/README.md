# Startup research: agentic motion-graphics video editor

_Working name: TBD · Research date: 2026-10-22 · Status: planning (week 0)_

> **Confidential.** This folder holds company strategy, pricing and positioning. The
> `syedmukheeth/video-editing` repository is **public**. Do not commit or push this folder
> until the repository is private, or keep it out of git.

## In one line

**The pro editor your AI can drive:** Premiere + After Effects in the browser for talking-head
educators. Every caption, zoom and graphic stays editable, and nothing looks like AI slop.

## The idea in five points

1. **What it is.** A cloud, Adobe-level video editor (timeline + motion-graphics compositor) that
   runs fully agentic and fully automatic.
2. **Who drives it.** Users connect their own Claude, ChatGPT, Codex or Cursor through an
   **MCP connector**. Their AI calls our editing tools. We pay nothing for LLM usage.
3. **Why it isn't slop.** It is built from designer-made caption styles, motion presets and
   templates, and an automatic quality lint has to pass before export.
4. **Why it's cheap to run.** Rendering and transcription run in the user's browser. Only
   optional cloud renders cost us money.
5. **Where it comes from.** SceneWright (this repository) already turns a brief into a
   validated, editable scene graph and renders the same frames in preview and export. That
   engine is the seed.

## Decisions (20 founder questions, answered 2026-10-22)

| Area | Decision |
|---|---|
| Team | 2 cofounders, both full-time; skills cover full-stack TypeScript, video/graphics engineering, motion design, marketing |
| SceneWright | Ours. The product goes closed in a new private repo; SceneWright stays as research |
| First buyer | Social media creators, starting with **talking-head educators** |
| Product | Cloud "Adobe-level" editor: short + long form + motion graphics, **all surfaces in one engine** |
| BYO AI | **MCP connector only** (user's Claude / ChatGPT / Codex drives the editor) |
| Generative video | **Optional layer only**; real footage + crafted graphics are the core |
| Pricing model | Subscription + render credits |
| Price level | Regional pricing (US base, lower prices by region) |
| Funding | Bootstrap to revenue |
| Growth | Build in public, creator partnerships, template marketplace, Claude/ChatGPT directories |
| Budget | Under $2k cash for the first 6 months (excluding salaries) |
| Time | Both founders full-time now |
| Market | Global English from day 1 |
| Open source | Closed product; SceneWright stays public research |
| Rendering | Browser first (free to us); cloud render is paid with credits |
| First revenue | Paying users by **week 8** |
| 12-month goal | **$50k+ MRR** |

## Files

| File | What's inside |
|---|---|
| [01-market.md](01-market.md) | Higgsfield numbers, MCP video-editor competitors, talking-head tool prices |
| [02-positioning.md](02-positioning.md) | Positioning, moat, the "not slop" quality system |
| [03-product.md](03-product.md) | One engine for both editors, format v2, Autopilot, MCP tool surface |
| [04-architecture.md](04-architecture.md) | Stack, cost logic, what to reuse from SceneWright, legal notes |
| [05-roadmap.md](05-roadmap.md) | 8-week plan with gates, cut list, 12-month milestones |
| [06-business.md](06-business.md) | Pricing, founding offer, unit economics, budget |
| [07-growth.md](07-growth.md) | Getting the first 1,000 creators with no ad budget |
| [08-risks.md](08-risks.md) | Risks, mitigations, verification gates |
| [09-open-questions.md](09-open-questions.md) | 84 open questions to answer during week 0 |
| [10-interview-script.md](10-interview-script.md) | Week-0 educator interview script, outreach DMs, note template, go/no-go scoring |

## How to use this folder

- **Week 0:** work through [09-open-questions.md](09-open-questions.md) and tick off answers.
  Interview 15–20 educators with [10-interview-script.md](10-interview-script.md) before
  writing product code.
- **Week 1:** run the three go/no-go spikes in [05-roadmap.md](05-roadmap.md). Do them in the new
  private product repo, **not** here; this repository holds research markdown only.
- **Monthly:** compare MRR with the milestones in [05-roadmap.md](05-roadmap.md) and update the
  risk table in [08-risks.md](08-risks.md).
