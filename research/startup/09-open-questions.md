# Open questions (week 0)

The first 20 founder questions are answered in [README.md](README.md). These 84 are next. Tick
each one off and write the answer under it, or link to where it is answered.

## Customer (talking-head educators)

- [ ] 1. Which 3 niches first (finance, fitness, tech, language, coaching, medicine)?
- [ ] 2. How many videos a week do they post, and on which platforms?
- [ ] 3. Do they edit themselves, pay an editor, or use CapCut/Submagic?
- [ ] 4. What do they pay today for editing (tools + people)?
- [ ] 5. What is the most painful part: cutting, captions, graphics, or turning one video into many?
- [ ] 6. Do they film long videos and cut reels from them, or film reels directly?
- [ ] 7. What makes them say an edit looks "cheap" or like AI?
- [ ] 8. Do they have brand kits (fonts, colors, logo)?
- [ ] 9. Which non-English languages matter to their audiences?
- [ ] 10. Who are 20 named educators we can interview this week?

## Product and editor

- [ ] 11. What is the maximum footage length at launch (10 min? 60 min?)?
- [ ] 12. Which aspect ratios ship first: 9:16 only, or 9:16 + 1:1 + 16:9?
- [ ] 13. Is text-based editing the default view, or is the timeline?
- [ ] 14. Which 10 caption styles come first (named and designed)?
- [ ] 15. Which 20 graphic templates come first?
- [ ] 16. Is there a music library on day 1? Which license source?
- [ ] 17. Will we have SFX, whooshes and transition packs?
- [ ] 18. B-roll: stock (which provider and license) or the user's own clips only?
- [ ] 19. Do we need green-screen or background removal?
- [ ] 20. Will multi-cam (2 angles) be needed for podcasts or interviews later?
- [ ] 21. What does undo/version history look like (snapshots per agent run)?
- [ ] 22. Should there be a mobile view for approving edits on a phone?

## Agent and MCP

- [ ] 23. Which AI client is tested first: Claude or ChatGPT?
- [ ] 24. Exact `apply_ops` operation list for v1 (aim for ~25 ops)?
- [ ] 25. How do we show the AI the video: contact sheets, keyframes, or short GIFs?
- [ ] 26. Maximum context we send per call (transcript chunk size)?
- [ ] 27. Should the agent see quality-lint errors and auto-fix them?
- [ ] 28. What happens when two edits conflict (user editing while the agent edits)?
- [ ] 29. Do we publish agent "skills"/prompts (e.g., "educator reel style") users can install?
- [ ] 30. Do MCP connectors work on free Claude/ChatGPT plans? (Verify; it affects the funnel.)
- [ ] 31. Codex/Cursor users: do we need a local stdio MCP too, or is remote enough?
- [ ] 32. Rate limits per user for MCP calls?

## Quality ("not slop")

- [ ] 33. Who signs off on every template (the motion-designer cofounder)?
- [ ] 34. What are the written rules of the house style (type scale, motion timing, colors)?
- [ ] 35. Which lint checks block an export, and which only warn?
- [ ] 36. How do we test taste: blind A/B against Submagic/Captions outputs with real creators?
- [ ] 37. Will there be per-platform presets (TikTok vs Reels vs Shorts safe zones)?
- [ ] 38. Pacing rules: maximum seconds without a visual change?
- [ ] 39. Do we forbid certain cheap effects entirely?
- [ ] 40. Do creators pick a style once, or per video?

## Technology

- [ ] 41. Minimum browser and hardware we support (GPU required?)
- [ ] 42. Proxy settings (resolution, bitrate, codec)?
- [ ] 43. How do we handle 4K HEVC iPhone footage in the browser?
- [ ] 44. Is AAC encoding available in WebCodecs on Windows/macOS Chrome? What is the fallback (Opus)?
- [ ] 45. Where does the canonical project live: local-first with sync, or server-first?
- [ ] 46. Offline support?
- [ ] 47. Cloud render: which VPS/region? Do we upload originals only for cloud renders, and when do we delete them?
- [ ] 48. Database choice: Postgres or D1?
- [ ] 49. Monitoring/error tracking on a free tier (Sentry free)?
- [ ] 50. What gets open-sourced, if anything (e.g., the format spec for MCP clients)?

## Business and pricing

- [ ] 51. Final US prices: test $19/$39 against $24/$49?
- [ ] 52. Regional price table (India, Brazil, SEA, EU)?
- [ ] 53. Annual-plan discount size?
- [ ] 54. Founding-member deal: price and how many seats?
- [ ] 55. How many credits per cloud-render minute, and what does a credit cost?
- [ ] 56. Refund policy?
- [ ] 57. Which merchant of record, and in which country is the company incorporated?
- [ ] 58. Company structure (e.g., US C-corp via Stripe Atlas vs local entity) and cost?
- [ ] 59. When to add bundled AI credits, if ever?
- [ ] 60. When to sell to agencies (Studio plan)?

## Growth

- [ ] 61. Which founder is on camera, and on which platforms?
- [ ] 62. Posting cadence and content pillars?
- [ ] 63. The first 20 creator partners: names, follower counts, offer?
- [ ] 64. Affiliate percentage and duration?
- [ ] 65. Waitlist now, before the product exists?
- [ ] 66. Launch date for Product Hunt?
- [ ] 67. Which SEO pages first (e.g., "Hormozi-style captions", "lower third template")?
- [ ] 68. Community: Discord, or none until 500 users?
- [ ] 69. Referral program (free credits per referral)?
- [ ] 70. What is the one demo video that sells it in 30 seconds?

## Legal and operations

- [ ] 71. Product name: trademark search in the US/EU/India?
- [ ] 72. Terms of service + privacy policy (footage handling, AI usage)?
- [ ] 73. Copyright of user footage and templates (who owns exports)?
- [ ] 74. Music/SFX licensing for commercial use on social platforms?
- [ ] 75. H.264 patent licensing for cloud rendering: get advice?
- [ ] 76. GDPR basics (EU users from day 1)?
- [ ] 77. Data deletion and retention policy for uploads?
- [ ] 78. Founder agreement: equity split, vesting, IP assignment of SceneWright?

## Team and funding

- [ ] 79. Who owns what: product/engineering vs design/growth?
- [ ] 80. Founder salaries: how long can you go without?
- [ ] 81. At what MRR do you hire the first person, and for what role?
- [ ] 82. Will you apply to an accelerator later (YC, a16z speedrun), and when?
- [ ] 83. At $50k MRR: raise to accelerate, or stay bootstrapped?
- [ ] 84. What is the "kill or pivot" signal, and the date to check it?
