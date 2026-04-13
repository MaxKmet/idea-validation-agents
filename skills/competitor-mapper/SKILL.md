---
name: competitor-mapper
description: Maps the full competitive landscape — direct, indirect, substitute, and emerging competitors — with positioning gap analysis, review mining, and market_insights-calibrated saturation scoring. Feeds into idea-scoring, cac-modeler, pricing-and-wtp, and tam-sam-som-builder.
---

<!-- version: 0.2.0 | outputs: memory/ideas/<slug>/competitors.json -->

# Skill: competitor-mapper

## Purpose

Understand what the user is actually competing against — not just other apps, but also spreadsheets, habits, free alternatives, and human services. The goal is not an exhaustive list but a **strategic map**: who owns the space, where the gaps are, and whether this idea can occupy a position that incumbents can't easily copy.

## Input

- Idea slug
- `memory/ideas/<slug>/idea.md` (app concept, key features, differentiator)
- `memory/market_insights/<niche>-*-<YYYY>-<MM>.md` (trend analysis files — **use all available platform files for this niche**)

### Using Market Insights

Trend analysis files are a primary research source for competitor mapping. Extract the following:

| Platform file | What to extract for competitor mapping |
|---|---|
| **Apps** (`<niche>-apps-*.md`) | Category rankings, new entrants, top apps by downloads/revenue, review complaint patterns, pricing models in use |
| **Reddit** (`<niche>-reddit-*.md`) | Apps and tools users mention by name (both praised and hated), non-software workarounds users describe, recurring complaints about existing solutions |
| **TikTok** (`<niche>-tiktok-*.md`) | Apps featured in viral content (free marketing = distribution advantage), creator-promoted tools, "alternatives to X" content trends |
| **Web Search** (`<niche>-web-search-*.md`) | Top-ranking apps for category keywords, "best X apps" list winners, SEO-dominant competitors |
| `monetization_evidence` (from any platform) | Which competitors are actively monetizing (proves the market supports revenue, identifies pricing benchmarks) |
| `trend_velocity` | Rising-fast markets attract new entrants quickly — flag that emerging threats will increase |

If no market_insights files exist, note this as a gap and rely on direct research only.

## Competitor Categories

| Category | Definition | Why it matters | Examples |
|---|---|---|---|
| **Direct** | Same solution, same audience | Head-to-head competition for the same users | Apps solving the exact same problem on the same platform |
| **Indirect** | Different solution, same problem | User might choose this instead, even though it works differently | A meditation app competing with a journaling app for "stress relief" |
| **Substitute** | Non-software solution the user currently employs | The real baseline — what happens if the user never installs any app | Spreadsheets, pen-and-paper, hiring a person, doing nothing, a WhatsApp group |
| **Emerging** | New entrants, beta products, or announced features from incumbents | Future competitive pressure — the landscape 6–12 months from now | YC-backed startups, Product Hunt launches, Apple/Google adding native features |

## Process

### Step 1 — Research Checklist by Category

#### Direct competitors (find 3–8)

Search these sources in order:

1. **App Store / Play Store category browse**: Search the primary category and 2–3 keyword variations. Record the top 10 results for each search.
2. **"Best X apps" articles**: Search Google for `best [category] apps 2026`. The top 3 listicle results typically capture the market leaders.
3. **Product Hunt**: Search the category. Sort by most upvoted. Focus on launches from the past 18 months (recent entrants).
4. **Market insights (Apps file)**: If `<niche>-apps-*.md` exists, extract any competitors named in the narrative.
5. **Market insights (Reddit file)**: If `<niche>-reddit-*.md` exists, extract apps users mention by name in discussions.
6. **AlternativeTo.net**: Search the closest existing app. Lists adjacent competitors you may have missed.

For each direct competitor, record:
- Name, platform(s), pricing model and price
- Estimated user base (from App Store ratings count × 50–100, or from market_insights narrative)
- App Store rating (stars + review count)
- Last updated date (stale = opportunity)
- Top 3 features
- Top 3 complaints (from review mining — see Step 3)

#### Indirect competitors (find 2–5)

Ask: "What else might someone use to solve the same underlying problem, even if the approach is completely different?"

Sources:
- Reddit threads where users describe their current workflow for this problem
- "How to [solve problem]" search results — the solutions that appear ARE the indirect competition
- Market insights narratives that describe alternative approaches to the same pain

#### Substitutes (find 2–4)

Ask: "What is the user doing RIGHT NOW, before they know this app exists?"

Common substitute categories:
- **Manual process**: Spreadsheet, notes app, pen-and-paper, calendar reminders
- **Human service**: Coach, therapist, accountant, personal trainer
- **Social workaround**: Group chat, Facebook group, Discord server
- **Inaction**: Doing nothing (this is the strongest competitor for low-urgency problems)

Record the estimated cost and friction of each substitute — this is the switching-cost baseline the app must beat.

#### Emerging threats (find 1–3)

Sources:
- Product Hunt launches in the past 6 months
- YC / startup accelerator demo day lists
- Apple WWDC / Google I/O feature announcements that could obviate the app
- If `trend_velocity` = "rising-fast" in market_insights, note that new entrants are likely

Flag any emerging competitor that has raised funding — they have resources to move fast.

### Step 2 — App Store Search Methodology

The App Store is the most important research surface for B2C apps. Use this systematic approach:

1. **Primary keyword search**: The most obvious term a user would search (e.g., "habit tracker").
2. **Problem keyword search**: The problem statement (e.g., "build better habits").
3. **Audience keyword search**: The target user + need (e.g., "ADHD planner").
4. **Adjacent keyword search**: Related but broader terms (e.g., "daily routine", "productivity").

For each search, record:
- Number of results that are clearly relevant (not spam/unrelated)
- Rating and review count of the top 3 results
- Whether the top result has > 50K ratings (signals an entrenched incumbent)
- Date of last update for top 5 results (stale apps = opportunity to displace)

### Step 3 — Review Mining for Positioning Gaps

Competitor reviews are the richest source of positioning gaps. Mine them systematically:

#### 1-star reviews (frustration signals)

These reveal what users hate about existing solutions. Look for patterns:
- Bugs and reliability complaints (opportunity: "the one that actually works")
- Missing features that users expected (opportunity: build the feature they want)
- Pricing complaints (opportunity: better value or different model)
- Privacy/data concerns (opportunity: privacy-first positioning)
- UX complexity complaints (opportunity: simpler alternative)

#### 3-star reviews (unmet expectation signals)

These are often more valuable than 1-star reviews. 3-star reviewers liked the app enough to keep using it but something important is missing:
- "Great app BUT..." — the "but" is the positioning gap
- "Would be perfect IF..." — the "if" is the feature opportunity
- "Works for X but not for Y" — the "Y" is the underserved segment

#### 5-star reviews (what's defensible)

Read competitor 5-star reviews to understand what they do well. These strengths are hard to compete against directly — don't try. Instead, find the **orthogonal angle** that the incumbent's strength doesn't cover.

#### Mining process

For each direct competitor (top 3–5):
1. Read the 20 most recent 1-star reviews
2. Read the 20 most recent 3-star reviews
3. Read 10 recent 5-star reviews
4. Categorize complaints into themes (max 5 themes per competitor)
5. Identify the **most common complaint shared across 2+ competitors** — this is the strongest gap signal

### Step 4 — Positioning Gap Analysis

A positioning gap is a real user need that no current competitor serves well. Classify each gap:

| Gap type | Description | Defensibility |
|---|---|---|
| **Audience gap** | No competitor targets this specific user segment | Medium — easy to copy if proven |
| **Feature gap** | A commonly requested feature that no competitor has built | Low — incumbents can add it |
| **Experience gap** | Existing solutions work but the UX is painful | Medium — hard for bloated incumbents to simplify |
| **Price gap** | All competitors are expensive; a free or cheap alternative would win | Low — race to the bottom |
| **Philosophy gap** | Existing solutions have a fundamentally different worldview (e.g., "gamified" vs. "minimalist") | High — incumbents can't pivot their core identity |
| **Platform gap** | No good solution exists on a specific platform (e.g., iOS-only need, Apple Watch, visionOS) | Medium — temporary, but first-mover advantage is real |
| **Trust gap** | Users don't trust existing solutions (privacy, data ownership, ads) | High — trust is hard to build retroactively |

Prioritize **philosophy gaps** and **trust gaps** — these are the hardest for incumbents to copy and the most defensible for an indie developer.

### Step 5 — Market Saturation Scoring

Saturation reflects how crowded the space is and how difficult it will be to get noticed.

| Factor | Low (1 pt) | Medium (2 pts) | High (3 pts) |
|---|---|---|---|
| **Direct competitor count** | 0–2 relevant apps | 3–6 relevant apps | 7+ relevant apps |
| **Incumbent dominance** | No app has > 10K ratings | 1–2 apps have 10K–100K ratings | An app has > 100K ratings |
| **Funding in space** | No funded competitors | 1–2 funded startups | Multiple funded companies or a FAANG player |
| **App Store keyword saturation** | Primary keywords show few relevant results | Moderate results, some quality variance | Top results are all high-quality, well-maintained apps |
| **Content saturation** | Few "best X apps" articles exist | Some articles, moderate SEO competition | Many SEO-optimized listicles, hard to rank |

**Total score** (5–15 points):

| Total | Saturation level |
|---|---|
| 5–7 | **low** — Blue ocean. Few competitors, clear opportunity to establish position. |
| 8–11 | **medium** — Competitive but gaps exist. Success requires clear differentiation. |
| 12–15 | **high** — Red ocean. Dominated by well-funded or well-established players. Indie success requires a genuinely novel angle or underserved niche. |

## Output

Write to `memory/ideas/<slug>/competitors.json`:

```json
{
  "direct_competitors": [
    {
      "name": "",
      "platform": "",
      "estimated_users": "",
      "app_store_rating": 0,
      "review_count": 0,
      "last_updated": "",
      "pricing": "",
      "pricing_model": "",
      "top_features": [],
      "top_complaints": [],
      "complaint_themes": [],
      "distribution_channels_observed": []
    }
  ],
  "indirect_competitors": [
    {
      "name": "",
      "approach": "",
      "why_users_choose_it": ""
    }
  ],
  "substitutes": [
    {
      "description": "",
      "cost": "",
      "friction_level": "low | medium | high",
      "switching_cost_to_app": ""
    }
  ],
  "emerging_threats": [
    {
      "name": "",
      "stage": "beta | launched | announced",
      "funded": false,
      "threat_level": "low | medium | high",
      "notes": ""
    }
  ],
  "review_mining_summary": {
    "most_common_complaint_across_competitors": "",
    "strongest_gap_signal": "",
    "competitors_mined": 0
  },
  "positioning_gaps": [
    {
      "gap_type": "audience | feature | experience | price | philosophy | platform | trust",
      "description": "",
      "defensibility": "low | medium | high",
      "evidence": ""
    }
  ],
  "saturation_score": {
    "direct_competitor_count": 0,
    "incumbent_dominance": 0,
    "funding_in_space": 0,
    "keyword_saturation": 0,
    "content_saturation": 0,
    "total": 0
  },
  "market_saturation": "low | medium | high",
  "differentiation_opportunities": [],
  "market_insights_sources_used": []
}
```

## Notes

- The `most_common_complaint_across_competitors` from review mining is one of the highest-signal data points in the entire validation system. If the same complaint appears in 3+ competitor review sets, it's a validated pain point — the market is telling you what to build.
- `distribution_channels_observed` for each competitor helps downstream skills (distribution-analysis, cac-modeler) understand which channels actually work in this category.
- If market_insights show `trend_velocity` = "rising-fast", note in `emerging_threats` that the competitor landscape will shift quickly. Rising markets attract builders.
- Substitutes with `friction_level` = "low" are the hardest to displace — if doing nothing or using a spreadsheet is easy enough, the app must provide dramatically more value to justify the download.
