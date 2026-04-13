---
name: cac-modeler
description: Models LTV, CAC by channel, LTV:CAC ratios, and payback period for an indie developer. Uses market_insights to calibrate channel CPMs and competitive intensity. Includes indie budget tier definitions and viability thresholds.
---

<!-- version: 0.2.0 | outputs: memory/ideas/<slug>/cac.json -->

# Skill: cac-modeler

## Purpose

Determine whether this indie developer can realistically acquire users profitably given their budget and the competitive landscape. Many ideas fail not because of bad products but because CAC exceeds LTV at indie scale. This skill builds a complete unit economics picture: LTV from retention and pricing, CAC from channel benchmarks calibrated by market_insights signals, and a payback timeline that tells the founder how long they need to fund growth before the business sustains itself.

## Input

- Idea slug
- `memory/user_profile.md` (budget constraint, ICP tier)
- `memory/ideas/<slug>/pricing.json` (target price → revenue per user)
- `memory/ideas/<slug>/retention.json` (D30 retention, churn risk → estimated lifespan)
- `memory/ideas/<slug>/distribution.json` (viable channels, k-factor, ASO opportunity, creator fit)
- `memory/ideas/<slug>/competitors.json` (competitor pricing and scale signals — optional)
- `memory/market_insights/<niche>-*-<YYYY>-<MM>.md` (trend data — **use all available platform files**)

### Using Market Insights

Trend analysis files provide critical calibration for CAC estimates. Extract the following:

| Field | How it informs CAC |
|---|---|
| `trend_velocity` | Rising markets have lower organic CAC (more discovery demand) but higher paid CAC (more advertisers bidding). Declining markets have the inverse. |
| `top_signals` (TikTok hashtags, Reddit threads, App Store categories) | Validate which organic channels have real activity — a niche trending on TikTok means TikTok organic CAC is at the lower end of the range |
| `monetization_evidence` | If competitors are already running ads (visible in trend narratives), paid CPMs in that niche are likely elevated. Adjust paid CAC estimates upward. |
| Platform narrative (Reddit pain points, creator engagement) | Identifies which communities are already activated — lower cost to reach an audience that's already discussing the problem |

## LTV Estimation

LTV is the foundation. Without an accurate LTV, CAC ratios are meaningless.

### LTV Formula

```
LTV = ARPU_monthly × average_lifespan_months
```

Where:
- **ARPU_monthly** (Average Revenue Per User per month):
  - Subscription: `target_price × (1 - churn_rate_monthly)`
  - Freemium: `target_price × freemium_conversion_estimate`
  - One-time purchase: `price / 12` (annualized for comparison)
  - Consumables: `average_monthly_spend` (estimate from category)

- **average_lifespan_months** (derived from retention.json):

| D30 retention | Estimated avg lifespan | Rationale |
|---|---|---|
| ≥ 25% | 12–18 months | Strong retention; users who survive D30 tend to stay long |
| 15–24% | 6–12 months | Decent; typical for well-executed niche apps |
| 8–14% | 3–6 months | Below average; expect significant churn in months 2–3 |
| < 8% | 1–3 months | Disposable; most users gone within a billing cycle |

If `retention.json` is unavailable, use category median D30 benchmarks:

| Category | Median D30 |
|---|---|
| Social / messaging | 15–25% |
| Health & fitness | 10–18% |
| Finance / budgeting | 12–20% |
| Productivity / tools | 8–15% |
| Games (casual) | 5–12% |
| Education | 6–12% |
| Lifestyle / habit | 10–18% |
| Creative tools | 12–20% |

### LTV Confidence

| Data available | Confidence |
|---|---|
| `pricing.json` + `retention.json` with D30 data | High |
| `pricing.json` only (using category median retention) | Medium |
| Neither (using category defaults for both) | Low — flag prominently |

## CAC by Channel

### Indie Budget Tiers

Define the founder's budget context before estimating per-channel CAC:

| Tier | Monthly ad/marketing spend | Who this is | Implication |
|---|---|---|---|
| **Bootstrap** | $0–$100/mo | Beginner or side-project builder | Paid channels are off the table. Must rely entirely on organic. |
| **Lean** | $100–$500/mo | Builder with some runway | Can test one paid channel with tight creative constraints. |
| **Moderate** | $500–$2,000/mo | Growth-tier or funded builder | Can run proper paid campaigns with A/B testing on one platform. |
| **Serious** | > $2,000/mo | Rare for indie; growth stage | Multi-platform paid, retargeting, influencer budgets. |

Map from `user_profile.md`: `budget_constraint` = "low" → Bootstrap. "medium" → Lean. "high" → Moderate or Serious (ask if ambiguous).

### Channel CAC Estimation

For each channel, estimate CAC using the funnel model:

```
CAC = cost_per_impression / (CTR × install_rate × activation_rate)
```

For organic channels, "cost" is time-valued at $0 but the skill reports the **effective CAC** — the opportunity cost of the founder's time, normalized per acquired user.

#### Channel benchmarks with market_insights adjustments

| Channel | Base CAC range | Adjust down if | Adjust up if |
|---|---|---|---|
| **ASO organic** | $0.50–$3.00 | ASO opportunity = "high" (from distribution.json); niche category with low competition | Saturated category; `market_saturation` = "high" from competitors.json |
| **Content / SEO** | $1.00–$8.00 | Niche has high search volume with low-quality top results; `rising` or `rising-fast` trend velocity | Competitive keywords dominated by established brands |
| **TikTok organic** | $0.50–$5.00 | Niche is trending on TikTok (visible in market_insights top_signals); app produces shareable output (content-as-distribution loop) | Low TikTok engagement for this category; no visual hook |
| **Reddit / community** | $0.50–$4.00 | Active communities discussing this problem (from Reddit market_insights); founder is an active community member | Small or inactive communities; product is hard to discuss authentically |
| **Paid social (Meta)** | $3.00–$40.00 | Broad audience, visual product, low CPM niche | Competitive niche with high CPMs; narrow targeting required |
| **Paid social (TikTok)** | $2.00–$25.00 | Trending niche (lower CPMs due to content volume); strong creative hook | Niche with limited content; poor demo-ability |
| **Influencer / creator** | $2.00–$25.00 | Creator economy fit = "high" (from distribution.json); micro-influencers available in niche | Low creator fit; only macro-influencers relevant (expensive) |
| **Word of mouth / referral** | $0.00–$2.00 | k-factor ≥ 0.3 (from distribution.json); inherent or collaborative viral loop | k-factor < 0.1; no natural sharing mechanic |
| **Press / Product Hunt** | $0.00–$5.00 | Novel concept with clear narrative; uses new platform feature | Crowded launch day; "me too" product |

> Press/Product Hunt provides a one-time spike, not sustained acquisition. Model it as a fixed user cohort (typically 500–5,000 installs), not a recurring channel.

### Channel Relevance Filter

Not all channels apply to every idea. Skip channels that score "not applicable":

| Skip condition | Channels to exclude |
|---|---|
| App has no visual output or demo hook | TikTok organic, influencer |
| `budget_constraint` = "low" (Bootstrap tier) | Paid social (both), influencer (unless micro/barter) |
| No relevant online communities exist | Reddit / community |
| `viral_loop_exists` = false AND k_factor < 0.1 | Word of mouth / referral |
| Utility app with no narrative angle | Press / Product Hunt |

## LTV:CAC Ratio Thresholds

After computing LTV and per-channel CAC, classify each channel:

| LTV:CAC ratio | Classification | Meaning |
|---|---|---|
| ≥ 5:1 | **Excellent** | Strong unit economics. Scale this channel aggressively. |
| 3:1–5:1 | **Healthy** | Viable and sustainable. Standard target for indie apps. |
| 2:1–3:1 | **Marginal** | Barely works. Viable only if the founder can optimize over time or retention improves. |
| 1:1–2:1 | **Unprofitable** | Losing money after overhead. Not viable unless LTV increases significantly. |
| < 1:1 | **Cash burn** | Every user costs more than they ever return. Do not use this channel. |

A minimum of **one channel at ≥ 3:1** is required for the overall viability verdict to be "viable."

## Payback Period Calculation

Payback period answers: "How many months until a user has paid back their acquisition cost?"

```
payback_months = CAC / ARPU_monthly
```

Report the payback period for the **recommended first channel** and any channel with LTV:CAC ≥ 3:1.

| Payback period | Assessment |
|---|---|
| ≤ 1 month | Excellent — cash flow positive almost immediately |
| 1–3 months | Good — sustainable for a funded indie builder |
| 3–6 months | Acceptable — requires patience and runway |
| 6–12 months | Risky — the founder needs alternative income during this period |
| > 12 months | Dangerous — cash flow negative for over a year. Not viable at indie scale unless lifetime deal covers upfront cost. |

For **Bootstrap tier** founders, any payback period > 3 months is a red flag — they likely can't sustain the cash gap.

## Viability Verdict

| Condition | Verdict |
|---|---|
| At least 2 channels with LTV:CAC ≥ 3:1, at least one organic | **viable** |
| Exactly 1 channel with LTV:CAC ≥ 3:1, OR organic channels at 2:1–3:1 with improvement potential | **marginal** |
| No channel achieves LTV:CAC ≥ 2:1, OR only paid channels viable but founder is Bootstrap tier | **not-viable** |

If market_insights show `trend_velocity` = "rising-fast", add a note that organic CAC may improve as the market grows (more search volume, more platform promotion of trending content). This is speculative but worth flagging.

## Process

1. Load all inputs: `pricing.json`, `retention.json`, `distribution.json`, `competitors.json`, `user_profile.md`, and all matching `memory/market_insights/<niche>-*-<YYYY>-<MM>.md` files.
2. Extract market_insights calibration signals (trend velocity, platform activity, monetization evidence, competitor ad activity).
3. Determine founder's budget tier from `user_profile.md`.
4. Compute LTV using the formula, pricing data, and retention data. Note confidence level.
5. For each applicable channel (after relevance filter), estimate CAC using benchmarks adjusted by market_insights and distribution.json signals.
6. Compute LTV:CAC ratio per channel. Classify each.
7. Compute payback period for viable channels.
8. Rank channels by LTV:CAC ratio. Select recommended first channel — must be executable by this founder at their budget tier.
9. Determine viability verdict.
10. Write output.

## Output

Write to `memory/ideas/<slug>/cac.json`:

```json
{
  "ltv": {
    "estimated_ltv": 0,
    "arpu_monthly": 0,
    "average_lifespan_months": 0,
    "ltv_confidence": "high | medium | low",
    "ltv_assumptions": []
  },
  "founder_budget_tier": "bootstrap | lean | moderate | serious",
  "cac_by_channel": {
    "aso_organic": { "cac": 0, "ltv_cac_ratio": 0, "classification": "", "payback_months": 0 },
    "content_seo": { "cac": 0, "ltv_cac_ratio": 0, "classification": "", "payback_months": 0 },
    "tiktok_organic": { "cac": 0, "ltv_cac_ratio": 0, "classification": "", "payback_months": 0 },
    "reddit_community": { "cac": 0, "ltv_cac_ratio": 0, "classification": "", "payback_months": 0 },
    "paid_social_meta": { "cac": 0, "ltv_cac_ratio": 0, "classification": "", "payback_months": 0 },
    "paid_social_tiktok": { "cac": 0, "ltv_cac_ratio": 0, "classification": "", "payback_months": 0 },
    "influencer": { "cac": 0, "ltv_cac_ratio": 0, "classification": "", "payback_months": 0 },
    "word_of_mouth": { "cac": 0, "ltv_cac_ratio": 0, "classification": "", "payback_months": 0 },
    "press_product_hunt": { "cac": 0, "ltv_cac_ratio": 0, "classification": "", "payback_months": 0, "one_time_cohort_estimate": 0 }
  },
  "skipped_channels": [],
  "viable_channels": [],
  "marginal_channels": [],
  "non_viable_channels": [],
  "recommended_first_channel": "",
  "recommended_first_channel_rationale": "",
  "payback_period_months": 0,
  "market_insights_adjustments": [],
  "viability_verdict": "viable | marginal | not-viable",
  "viability_verdict_rationale": ""
}
```

## Notes

- The `recommended_first_channel` must be achievable by the founder at their current tier. Don't recommend paid social to a Bootstrap founder. Don't recommend Reddit community marketing to someone with no community presence. Cross-reference `user_profile.md` distribution advantages.
- If `retention.json` is unavailable, LTV confidence drops to medium at best. Flag this prominently — CAC ratios are only as good as the LTV estimate, and LTV depends entirely on retention.
- When `distribution.json` shows a strong viral loop (k-factor ≥ 0.3), the effective CAC for word-of-mouth should account for the viral multiplier: `effective_CAC = base_CAC / (1 / (1 - k))`. A k-factor of 0.5 halves the effective CAC.
- Press/Product Hunt is not a channel strategy — it's a launch event. Model it as a one-time cohort (estimate 500–5,000 installs) and do not include it in recurring channel viability.
- If all market_insights files are past their `stale_after` date, note that CAC benchmarks may have shifted and recommend refreshing trend analysis.
