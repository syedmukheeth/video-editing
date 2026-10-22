# Market check

_Research date: 2026-10-22. Revenue and valuation figures are company-reported or from secondary
coverage, not audited. Re-check before using them in a pitch._

## Higgsfield: proof the category is big

| Metric | Figure | Source |
|---|---|---|
| Valuation, Jan 2026 | $1.3B ($80M Series A extension) | [YourStory](https://yourstory.com/ai-story/how-higgsfield-ai-became-a-54-billion-ai-video-startup) |
| Valuation, Aug 2026 | **$5.4B** ($400M Series B, led by DST Global) | [TheNextWeb](https://thenextweb.com/news/higgsfield-series-b-400m-5-4bn-valuation-700m-revenue) |
| Annualised revenue, Aug 2026 | ~$700M (vs ~$20M a year earlier) | [TheNextWeb](https://thenextweb.com/news/higgsfield-series-b-400m-5-4bn-valuation-700m-revenue) |
| Annualised revenue, Sep 2026 | ~$1B run rate (secondary summary of a CEO interview; trailing 4 weeks × 13) | [Dealroom](https://dealroom.co/news/talk-jszn8rFtxm4-burning-4m-a-month-inside-higgsfields-dash-to-a-1b-arr/) |
| Annualised revenue, Jan 2026 | ~$200M–$230M (sources differ) | [Sacra](https://sacra.com/research/higgsfield-at-230m-arr/) |
| Users, Jan 2026 | 15M | TechCrunch, via the sources above |
| Revenue mix | Business customers are now the majority of revenue (under a quarter in January) | FT, via TheNextWeb |

**What it tells us:**
- Creators will pay for AI video at large scale.
- The money then shifts to **business** use.
- Higgsfield sells *generated pixels*. Its strength is photoreal and stylised footage.
- It doesn't target what business videos need most: exact typography, brand-accurate layouts,
  and edits that can be changed later and come out the same every time.

## "Edit video with your AI over MCP" is already crowded

| Product | What it does (vendor claims) | Date / stage | Source |
|---|---|---|---|
| invideo MCP | External agents drive invideo's browser editor: timeline, color, audio, generation | Launched 2026-09-30 | [invideo](https://invideo.io/news/introducing-invideo-mcp/) |
| Clueso MCP | Claude/ChatGPT plan, script, voice and assemble videos; results stay editable | Product Hunt, Sep 2026 | [Product Hunt](https://www.producthunt.com/p/clueso/clueso-mcp-2) |
| OpusClip MCP | Long video → captioned, reframed short clips from Claude | Live | [OpusClip](https://www.opus.pro/blog/claude-video-editing-mcp) |
| Valmera | MCP server for editing your own footage: silence removal, captions, reframing, export | Live | [MCP Market](https://mcpmarket.com/server/valmera) |
| Cardboard | Agentic browser editor for growth teams; first cuts from raw footage | YC W26 | [NeuronFeed](https://neuronfeed.com/startups/cardboard) |
| Palmier | Open-source video editor built for AI agents; 2-person team | YC S24 | [eesel](https://www.eesel.ai/blog/what-is-palmier-ai-video-editor) |
| Descript, Riverside, Tella | Listed as agentic editors drivable by Claude/ChatGPT/Codex/Cursor | Live | [Tella roundup](https://www.tella.com/blog/best-agentic-video-editors) (written by a competitor) |

**What it tells us:** by our launch, MCP support is a **basic requirement, not a moat**. We have
to win on output quality, editability and focus on one niche.

## Talking-head tools and what creators pay

| Tool | Price (third-party listings, check vendor pages) | Strength |
|---|---|---|
| Submagic | $19 / $39 / $69 per month ($12 / $23 / $41 billed yearly) | Captions and polish on short clips |
| Descript | From $16/month (annual) up to ~$65/month; free tier 60 min/month | Text-based editing of recordings |
| OpusClip | From ~$15/month (150 min) up to ~$29/month; 60 min/month free | Automatic clip selection from long videos |
| Captions / Mirage | Raised $75M growth round (Mar 2026); AI Edit for videos up to 10 min | Mobile-first captions, avatars |

Sources: [Costbench (Submagic)](https://costbench.com/software/ai-video-editing-saas/submagic/),
[Castmagic (OpusClip alternatives)](https://www.castmagic.io/blog/opus-clip-alternatives),
[Captions/Mirage](https://yespress.io/products/captions.md).

**What it tells us:** creators already pay **$15–$70/month** for single-purpose tools (captions,
clipping, text editing). A tool that does the whole edit, with graphics, at $19–$39 fits that
budget.

## Building blocks we can use

| Need | Available today | Note | Source |
|---|---|---|---|
| Render in the browser at $0 server cost | WebCodecs + **Mediabunny** (MPL-2.0) | Remotion's web renderer is experimental, and its packages need a company license; avoid them | [Remotion blog](https://www.remotion.dev/blog/mediabunny), [web renderer docs](https://www.remotion.dev/docs/web-renderer/) |
| Transcription in the browser at $0 | Whisper via transformers.js (WebGPU, WASM fallback) | Word timestamps on WebGPU are a known gap; spike first | [transformers.js #820](https://github.com/huggingface/transformers.js/issues/820), [Remotion whisper-webgpu](https://remotion.dev/docs/whisper-webgpu) |
| UI inside Claude and ChatGPT | **MCP Apps**, official MCP extension since Jan 2026 | Directory submission rules change often; check official docs | [Alpic](https://alpic.ai/blog/mcp-apps-goes-official-claude-chatgpt-support), [Sunpeak](https://sunpeak.ai/blogs/claude-connectors-vs-claude-apps/) |

## Gaps in this research

- No hands-on testing of any competitor.
- Competitor pricing came from third-party listings.
- Not yet found: Hera, Jitter or other AI motion-graphics startups; MCP availability on free
  Claude/ChatGPT plans; official directory submission rules.
- These are listed in [09-open-questions.md](09-open-questions.md).

For the open-source landscape (Remotion, HyperFrames, Motionly, OpenChatCut…), see SceneWright's
own [COMPETITIVE_ANALYSIS.md](../COMPETITIVE_ANALYSIS.md).
