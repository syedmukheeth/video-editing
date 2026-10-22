# Roadmap

## 8 weeks to first paying users

Two founders, full-time. Each week has a **gate**: if it isn't met, fix it before moving on.

| Week | Work | Gate |
|---|---|---|
| 0 (now) | Name + trademark/domain check. Create the private product repo, seeded from SceneWright. Interview 15–20 talking-head educators ([script](10-interview-script.md)). Answer [09-open-questions.md](09-open-questions.md) | 10+ educators show a specific pain plus real spend or a commitment (scoring in the script) |
| 1 | **Go/no-go spikes** (in the product repo): (a) Chrome/Edge decodes 10 min of 1080p, draws captions + graphics, exports a 60 s 1080p 9:16 MP4 **with AAC audio**; (b) Whisper WebGPU word timestamps on a 10-min file; (c) remote MCP + OAuth working in Claude **and** ChatGPT, with an MCP App preview | (a) export ≤ 1× real time; (b) word timing within ±100 ms; (c) one full agent edit round-trip |
| 2–3 | Timeline v2 model + multitrack UI; footage import + proxies; text-based editing (delete words = cut); silence/filler removal | 10-min raw video → clean cut in < 5 min of user time |
| 4 | Captions engine (10 designer styles, word highlight); punch-in zooms; face-tracked reframe; platform safe zones | A reel the motion-designer cofounder would post |
| 5 | Graphic overlays on the SceneWright engine (lower thirds, title cards, kinetic text, lists, stats, chapter cards); brand kit; 20 templates | Every template passes the quality lint |
| 6 | MCP tools + `apply_ops` + lint + MCP App preview; browser export; accounts, payments, credits | "Edit today's video into a reel in my style" works from Claude in one prompt |
| 7 | Private beta: 20–30 educators, onboarded by hand; daily build-in-public posts | 50% make a first export within 15 min |
| 8 | **Charge:** founding-member annual plan; cloud render beta; submit to Claude + ChatGPT directories | **First 30–50 paying users** |

### If a spike fails

| Spike | Fallback |
|---|---|
| Browser export too slow or AAC unavailable | Chrome/Edge only; Opus audio; cloud render becomes the default for long videos |
| Whisper WebGPU word timing unreliable | WASM path, or forced alignment on a small server for paid users only |
| MCP App UI blocked in one client | Launch with plain MCP tools + a preview link that opens our app |

### Cut list if behind (cut in this order)

1. Cloud render (browser export only at launch)
2. Music library
3. Long-form 16:9
4. Team features

## 12-month milestones

| Month | Ships | MRR target |
|---|---|---|
| 2 | Paid beta: reels from talking-head footage | $1k (≈50 payers) |
| 3 | Public launch, Claude/ChatGPT directories, Product Hunt | $3k |
| 6 | Long-form 16:9, music/SFX + ducking, template marketplace v1, optional generative B-roll layer | $15k |
| 9 | Studio seats for freelance editors and agencies, multilingual captions | $30k |
| 12 | Keyframe tracks / full compositor, public API | **$50k** (≈2,000 payers at ~$25 blended) |

**Check monthly.** If month-6 MRR is under $8k, stop building features and re-run customer
interviews.

## The billion-dollar path (honest version)

- A $1B company needs roughly **$50–100M ARR** that is still growing fast.
- Higgsfield's lesson: revenue moves from individual creators to **businesses** (see
  [01-market.md](01-market.md)).
- Our ladder:

| Stage | Customer | What they buy |
|---|---|---|
| 1 | Talking-head educators | Creator / Pro plans |
| 2 | Freelance editors and small agencies | Studio seats, client brand kits, review links |
| 3 | Brand and marketing teams | Brand governance, approvals, API, volume |
| 4 | Platform | Template marketplace + the agent-native project format as a standard |

Most startups never get there. The plan stays **profitable enough to survive without funding**
at every stage, so a slower path still works.
