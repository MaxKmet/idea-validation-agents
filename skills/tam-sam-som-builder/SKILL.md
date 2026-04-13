---
name: tam-sam-som-builder
description: Estimates TAM, SAM, and realistic SOM for a B2C app idea using triangulated bottom-up methodology anchored to market_insights trend data, competitor revenue proxies, and community size signals. Includes indie capture rate benchmarks and growth-rate adjustments by trend velocity.
---

<!-- version: 0.2.0 | outputs: memory/ideas/<slug>/market_size.json -->

# Skill: tam-sam-som-builder

## Purpose

Provide a realistic market size estimate that an indie developer can actually use for decisions. Most TAM estimates are useless because they use top-down analyst numbers designed to impress VCs, not to inform a solo builder deciding where to spend the next 6 months. This skill uses **triangulated bottom-up methodology** — multiple independent estimation approaches cross-checked against each other — anchored to real signals from `market_insights/` trend data.

## Input

- Idea slug (or market research slug for pre-idea deep dives)
- `memory/ideas/<slug>/keywords.json` (search volume estimates — if available)
- `memory/ideas/<slug>/competitors.json` (competitor scale and pricing signals)
- `memory/ideas/<slug>/pricing.json` (target price — if available)
- `memory/market_insights/<niche>-*-<YYYY>-<MM>.md` (trend analysis files — **use all available platform files for this niche**)

### Using Market Insights

Trend analysis files from `memory/market_insights/` provide critical calibration data. Extract the following from each available file's YAML frontmatter and narrative:

| Field | How it informs TAM/SAM/SOM |
|---|---|
| `trend_velocity` | Adjusts growth rate projections (see Step 5) |
| `top_signals` | Validates that real demand exists; calibrates bottom-up search volume estimates |
| `monetization_evidence` | Confirms WTP — if no monetization evidence exists across any platform, discount TAM by 30–50% |
| `overall_verdict` (hot/warm/cool/cold) | Sanity-check on whether the market is worth sizing at all |
| Platform narrative (Reddit pain points, TikTok engagement, App Store reviews) | Source for community size proxy estimation (see Approach B) |

If `overall_verdict` across platforms is "cold", flag the entire estimate as speculative and note that market demand is unvalidated.

## Methodology

### Approach A — Search Volume (primary when keywords.json available)

```
TAM = monthly_search_volume × 12 × intent_conversion_rate × annual_price
```

Where:
- `monthly_search_volume` = total from `keywords.json` across all relevant keywords
- `intent_conversion_rate` = % of searchers who have genuine purchase intent (see benchmarks below)
- `annual_price` = from `pricing.json` target WTP, annualized

**Intent conversion benchmarks by search type:**

| Search intent | Conversion rate | Example query |
|---|---|---|
| Direct solution search ("app to track X") | 8–15% | "habit tracker app", "budget planner iOS" |
| Problem-aware search ("how to X") | 3–8% | "how to save money", "how to build habits" |
| Category browsing ("best X apps") | 5–12% | "best workout apps 2026", "top meditation apps" |
| Tangential interest ("X tips") | 1–3% | "productivity tips", "healthy eating advice" |

### Approach B — Community Size Proxy (primary when market_insights available)

When keyword data is weak but trend analysis reveals active communities, estimate from community engagement:

```
TAM = active_community_members × platform_multiplier × annual_price
```

Where:
- `active_community_members` = sum of engaged users across platforms (subreddit subscribers, TikTok hashtag creators, App Store review volume)
- `platform_multiplier` = ratio of total interested population to active community members (see below)

**Platform multipliers** (how many silent interested people per active community member):

| Signal source | Multiplier | Rationale |
|---|---|---|
| Reddit subscribers in niche subreddit | 20–50× | ~2–5% of interested people join a subreddit |
| TikTok hashtag creators (not views) | 100–500× | Tiny fraction of interested people create content |
| App Store reviews for top competitor | 50–100× | ~1–2% of users leave reviews |
| Newsletter subscribers in niche | 10–30× | Email subscribers are a warmer proxy |

### Approach C — Competitor Revenue Proxy (supplementary)

Estimate from competitor data in `competitors.json`:

```
TAM = sum of estimated annual revenue across all mapped competitors × market_coverage_factor
```

Where:
- Estimate competitor revenue from: `estimated_users × competitor_price × 12 × estimated_conversion_rate`
- `market_coverage_factor` = 1.3–2.0× (competitors don't capture the full market). Use 1.3× for saturated markets, 2.0× for markets with few competitors.

### Triangulation

Run all available approaches and compare:
- If estimates agree within 2× → high confidence. Use the geometric mean.
- If estimates disagree by 2–5× → medium confidence. Use the most conservative estimate and note the range.
- If estimates disagree by > 5× → low confidence. Flag assumptions that cause the divergence.

Always report which approaches were used and their individual estimates in the output.

## SAM Filtering

SAM narrows TAM to the segment actually reachable by the app. Apply these filters in order:

### Geographic & Platform Filters

| Filter | How to apply | Data source |
|---|---|---|
| **Platform** | iOS-only → multiply TAM by iOS market share in target geography | See benchmarks below |
| **Geography** | English-only → US + UK + CA + AU + NZ + IE. Specific country → that country only | App concept language |
| **Age range** | If app targets a demographic (teens, 50+), apply population % | Idea description |
| **Income bracket** | If app requires disposable income for subscription, filter by income | Pricing model |

**iOS market share by region** (for iOS-only apps):

| Region | iOS share (approximate) |
|---|---|
| United States | 55–58% |
| United Kingdom | 50–53% |
| Canada | 53–56% |
| Australia | 55–58% |
| Western Europe (avg) | 30–35% |
| Global | 25–28% |
| Southeast Asia | 10–15% |
| India | 4–6% |
| Latin America | 12–18% |

For Android-only or cross-platform, apply the inverse or use 100%.

### Segment Filters

Beyond geography and platform, apply any filters that narrow the market to people who would actually consider this specific app:

- Niche focus (e.g., "fitness" → "climbing-specific fitness")
- Prerequisite behavior (e.g., "already tracks workouts" → subset of fitness app users)
- Tech-savviness requirement (if the app requires unusual setup, filter out casual users)

**SAM should typically be 10–40% of TAM.** If SAM > 50% of TAM, the filters are too loose. If SAM < 5% of TAM, the niche may be too narrow for viable economics.

## SOM Estimation

SOM is what an indie developer can realistically capture. This is where most estimates go wrong — indie builders don't have the resources to capture meaningful market share in crowded categories.

### SOM Capture Rate Benchmarks by Category

| App category | Year 1 capture rate | Year 3 capture rate | Notes |
|---|---|---|---|
| **Utility / tool** (calculator, converter, scanner) | 0.1–0.5% of SAM | 0.5–2.0% | Discoverable via ASO, many competitors |
| **Niche productivity** (specific workflow tool) | 0.5–2.0% | 2.0–5.0% | Smaller SAM but higher capture in the niche |
| **Health & fitness (niche)** | 0.3–1.5% | 1.0–4.0% | Loyal users if retention is strong |
| **Health & fitness (broad)** | 0.05–0.2% | 0.2–0.8% | Dominated by incumbents |
| **Social / community** | 0.01–0.1% | 0.1–0.5% | Network effects favor incumbents; cold start is brutal |
| **Content / media** | 0.1–0.5% | 0.5–2.0% | Depends heavily on content quality and curation |
| **Finance / budgeting** | 0.1–0.5% | 0.5–2.0% | High trust barrier, but sticky once adopted |
| **Creative tools** (photo, video, design) | 0.2–1.0% | 1.0–3.0% | Shareable output drives organic growth |
| **Education / learning** | 0.2–1.0% | 1.0–3.0% | Retention is the main challenge |
| **Lifestyle / habit** | 0.3–1.5% | 1.0–4.0% | Success varies wildly by habit loop quality |

Use the **lower end** of the range when:
- `market_saturation` from `competitors.json` is "high"
- Founder is beginner tier (from `user_profile.md`)
- No distribution advantage identified

Use the **upper end** when:
- Founder has an existing audience or distribution edge
- Strong ASO opportunity or viral loop exists
- Market is growing fast (trend_velocity = "rising-fast")

### SOM Calculation

```
SOM_year_1 = SAM × capture_rate_year_1
SOM_year_3 = SAM × capture_rate_year_3 × growth_multiplier
```

## Growth Rate Adjustment (from market_insights)

Trend velocity from market_insights directly affects the year-3 projection:

| Trend velocity | Growth multiplier (applied to year-3 SOM) | Rationale |
|---|---|---|
| `rising-fast` | 1.5–2.0× | Market is expanding — your share of a growing pie grows faster |
| `rising` | 1.2–1.5× | Moderate tailwind |
| `stable` | 1.0× | No adjustment — capture rate is the only growth driver |
| `declining` | 0.5–0.8× | Shrinking market — your absolute numbers may drop even if capture rate improves |

If multiple platform files have different velocities, use the **median** velocity.

## Reality Check Layer

Before finalizing, run these sanity checks:

| Check | Threshold | Action if triggered |
|---|---|---|
| **TAM inflation** | TAM > $10B for a niche indie app | Almost certainly using top-down numbers. Redo with bottom-up only. |
| **SAM too broad** | SAM > 50% of TAM | Filters are too loose. Add platform/geography/niche constraints. |
| **SOM fantasy** | SOM year 1 > $500K for a solo developer | Reality-check the capture rate. Most indie apps earn $0–$50K in year 1. |
| **No monetization evidence** | `monetization_evidence` from market_insights is empty across all platforms | Discount TAM by 30–50%. People may want this but not pay for it. |
| **Cold market** | All market_insights files show `overall_verdict` = "cold" or "cool" | Flag as speculative. Note that market demand is unvalidated. |

## Market Size Verdict Thresholds

Based on **SOM year 1** (the number that actually matters for an indie developer deciding whether to build):

| SOM year 1 | Verdict | Meaning for an indie dev |
|---|---|---|
| > $200K | **large** | Significant indie opportunity. Even partial execution could be life-changing. |
| $50K–$200K | **medium** | Viable as a primary project. Can sustain a solo developer if retention is good. |
| $10K–$50K | **niche** | Side-project scale. Viable if build cost is low and the founder has another income source. |
| < $10K | **micro-niche** | Hobby scale. Only worth building if the founder has a personal reason to build it or can expand the niche. |

## Process

1. Load all available inputs: `keywords.json`, `competitors.json`, `pricing.json`, and all matching `memory/market_insights/<niche>-*-<YYYY>-<MM>.md` files.
2. Extract calibration data from market_insights (trend velocity, top signals, monetization evidence, overall verdict).
3. Run Approach A (search volume) if `keywords.json` is available.
4. Run Approach B (community size proxy) if market_insights contain community signals.
5. Run Approach C (competitor revenue proxy) if `competitors.json` has user/pricing data.
6. Triangulate: compare estimates, determine confidence, select final TAM.
7. Apply SAM filters (geography, platform, demographics, niche).
8. Estimate SOM using category-appropriate capture rate benchmark.
9. Apply growth multiplier from trend velocity.
10. Run reality checks. Adjust if any are triggered.
11. Determine market size verdict from SOM year 1 thresholds.
12. Write output.

## Output

Write to `memory/ideas/<slug>/market_size.json`:

```json
{
  "methodology": "bottom-up | community-proxy | competitor-proxy | triangulated",
  "estimation_approaches": [
    {
      "approach": "search-volume | community-proxy | competitor-proxy",
      "tam_estimate": 0,
      "key_assumptions": []
    }
  ],
  "triangulation_confidence": "high | medium | low",
  "tam": {
    "value": 0,
    "currency": "USD",
    "period": "annual",
    "assumptions": []
  },
  "sam": {
    "value": 0,
    "filter_criteria": [],
    "sam_to_tam_ratio": 0
  },
  "som": {
    "year_1": 0,
    "year_3": 0,
    "capture_rate_year_1_pct": 0,
    "capture_rate_year_3_pct": 0,
    "growth_multiplier": 1.0,
    "growth_multiplier_source": ""
  },
  "market_insights_used": [],
  "trend_velocity_observed": "rising-fast | rising | stable | declining",
  "monetization_evidence_found": true,
  "reality_checks_triggered": [],
  "market_size_verdict": "large | medium | niche | micro-niche"
}
```

## Notes

- When used in the `market-deep-dive` workflow, `pricing.json` may not exist yet. In that case, use the median competitive price from `competitors.json` or a category benchmark ($3–$7/mo for typical B2C subscription apps).
- When used in `idea-validation` (if the orchestrator includes it), the output feeds into `idea-scoring`'s Monetization dimension. The `market_size_verdict` and SOM values are used alongside pricing and CAC data to assess overall monetization viability.
- Market_insights files have a `stale_after` date. If all available files are past their stale date, flag the estimates as potentially outdated and recommend re-running `trend-analysis` before making a build decision.
