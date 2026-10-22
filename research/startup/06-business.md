# Business model

## Pricing

US base prices. Other regions get lower prices through the merchant of record's regional
pricing.

| Plan | Price | Includes |
|---|---|---|
| Free | $0 | Browser export 720p with "made with" watermark, 3 exports/month, MCP access |
| Creator | $19/mo ($15/mo annual) | 1080p, no watermark, unlimited browser exports, 50 GB storage, 30 cloud-render minutes |
| Pro | $39/mo ($29/mo annual) | 4K, premium templates, 5 brand kits, 150 cloud-render minutes |
| Studio (month 9) | $79/seat/mo | Team workspace, client brand kits, review links |
| Credits | Top-ups | Extra cloud-render minutes; optional generative B-roll later |

**Why these numbers:**
- Submagic charges $19 / $39 / $69, Descript $16–65, OpusClip $15–29 (see
  [01-market.md](01-market.md)).
- We match their entry prices but do the whole edit, graphics included.
- Test $19/$39 against $24/$49 during the beta.

### Founding-member offer (week 8)

- The first 100 users get ~$149/year, locked in for life.
- This brings cash early, rewards beta testers, and they become case studies.

## Unit economics

| Cost line | Per user per month |
|---|---|
| LLM | $0 (user's own AI via MCP) |
| Browser render + transcription | $0 |
| Proxy storage (assume 5–10 GB at ≈ $0.015/GB) | ≈ $0.08–$0.15 |
| Database, MCP calls, bandwidth | ≈ $0.05 at small scale |
| Payment fees (merchant of record, ~5% + fee) | ≈ $1–$2 |
| Cloud render | Paid by credits, priced at ≥ 5× compute cost |

**Target gross margin: 85%+.**

## Revenue math for the 12-month goal

| Target | Paying users needed at ~$25 blended ARPU |
|---|---|
| $1k MRR (month 2) | ~50 |
| $15k MRR (month 6) | ~600 |
| $50k MRR (month 12) | ~2,000 |

At a 4% free → paid conversion, 2,000 payers means about **50,000 free signups** in year one.
That is the number the growth plan in [07-growth.md](07-growth.md) has to hit.

## Budget: under $2k for 6 months

| Item | Cost |
|---|---|
| Domain + email | ~$60 |
| Cloudflare Workers paid plan + R2 | ~$100 |
| Database / auth | $0 (free tiers) |
| Cloud-render VPS (from month 2) | ~$100 |
| Trademark filing (1 class, if the name is clear) | ~$350 |
| Creator partner gifts / small boosts | ~$500 |
| Reserve | ~$800 |
| **Total** | **~$1,910** |

Assumed to be paid outside this budget: the founders' own AI coding subscriptions and
salaries.

## Payments and company setup (to decide in week 0)

- **Merchant of record** (Paddle, Lemon Squeezy or similar): sells globally, handles VAT/GST,
  supports regional prices.
- **Where to incorporate:** depends on where the founders live; see
  [09-open-questions.md](09-open-questions.md) questions 57–58.
- **Refund policy and terms of service:** needed before the first charge.
