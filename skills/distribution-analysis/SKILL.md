---
name: distribution-analysis
description: Evaluates organic reach potential, paid feasibility, platform distribution advantages, creator economy fit, and founder edge for a B2C app idea. Includes viral coefficient estimation, ASO scoring rubric, and tier-adjusted verdicts.
---

<!-- version: 0.2.0 | outputs: memory/ideas/<slug>/distribution.json -->

# Skill: distribution-analysis

## Purpose

Distribution is the most underestimated factor in indie app success. A mediocre product with great distribution beats a great product with no distribution. This skill evaluates all realistic paths to users and adapts its verdict to the founder's tier — a channel that works for a growth-stage operator can be a trap for a beginner.

## Input

- Idea slug
- `memory/user_profile.md` (ICP tier, distribution advantages, budget constraint)
- `memory/ideas/<slug>/idea.md` (app concept, key features, differentiator)
- Optional: `memory/ideas/<slug>/competitors.json` (competitor distribution signals)

## Distribution Dimensions

| Dimension | Questions to Answer |
|---|---|
| Organic reach | Can this spread without paid spend? Is there a viral loop? What's the estimated viral coefficient? |
| Paid feasibility | Can paid ads break even at indie scale? What's the minimum viable budget? |
| Platform advantage | Is there an ASO moat? App Store featured potential? Category competitiveness? |
| Creator economy fit | Can influencers or creators promote this authentically? Does the app produce shareable output? |
| User's distribution edge | Does the user have an existing audience, community, or channel expertise? |

## Process

### Step 1 — Viral Coefficient Estimation

The viral coefficient (k-factor) predicts whether an app can grow organically through user referrals. Estimate k = i × c where:

- **i** = average number of invitations/shares per user
- **c** = conversion rate of each invitation

#### Viral loop identification

Evaluate the app concept against these loop types:

| Loop type | Description | Typical k-factor | Example |
|---|---|---|---|
| Inherent | Product is useless alone, requires inviting others | 0.5–1.5 | Multiplayer games, shared lists |
| Collaborative | Better with others but works solo | 0.2–0.6 | Workout trackers with friends, shared budgets |
| Word-of-mouth | Users talk about it because it's remarkable | 0.1–0.4 | Apps that produce "wow" output (AI art, unique insights) |
| Incentivized | Users get a reward for referring | 0.1–0.3 | Referral credits, unlocked features |
| Content-as-distribution | App output is inherently shareable on social platforms | 0.3–0.8 | Photo editors with watermarks, personality quizzes, wrapped/recap screens |
| None | No natural reason to share | 0.0–0.05 | Utility apps (calculators, timers) |

#### Estimation rubric

1. Identify which loop type(s) apply to the app concept.
2. Estimate **i** (invitations per user) — consider: does the core UX prompt sharing? How often? To how many people?
3. Estimate **c** (conversion per invitation) — consider: how compelling is the share artifact? Does the recipient need the app to view it?
4. Compute k = i × c.
5. Classify:

| k-factor | Classification |
|---|---|
| k ≥ 0.7 | **Viral growth engine** — organic growth is a primary acquisition channel |
| 0.3 ≤ k < 0.7 | **Viral assist** — referrals supplement other channels meaningfully |
| 0.1 ≤ k < 0.3 | **Marginal virality** — some word-of-mouth, not a growth driver |
| k < 0.1 | **Non-viral** — growth depends entirely on other channels |

> k ≥ 1.0 means every user brings in at least one more user on average — true exponential growth. This is rare for indie apps; be skeptical of estimates above 0.8 unless the app has an inherent or content-as-distribution loop.

### Step 2 — ASO Potential Scoring

App Store Optimization is the highest-leverage free channel for indie developers. Score ASO opportunity on a 3-tier rubric:

#### ASO scoring rubric

| Factor | High (3 pts) | Medium (2 pts) | Low (1 pt) |
|---|---|---|---|
| **Category competition** | Niche category, top 10 achievable with <500 ratings | Moderate category, top 50 achievable | Saturated category, dominated by incumbents with 100K+ ratings |
| **Keyword opportunity** | High-volume keywords with low-rated top results (< 4.2 stars, < 1K ratings) | Keywords exist but top results are solid (4.5+ stars) | All relevant keywords dominated by well-known brands |
| **Search intent match** | Users actively search for this exact solution (tool/utility intent) | Users search for the category but not this specific angle | Discovery-dependent — users don't know they want this |
| **Review velocity potential** | App has natural prompt moments for asking reviews (completed task, achievement) | Some prompt moments but not in core loop | No natural review prompt; must interrupt to ask |
| **Visual differentiation** | App icon and screenshots can stand out (unique aesthetic, bold output previews) | Decent but similar to competitors | Looks like every other app in the category |

**ASO score**: Sum of all factors (5–15 points).

| Total | ASO opportunity |
|---|---|
| 12–15 | **high** — ASO should be primary acquisition channel |
| 8–11 | **medium** — ASO is viable but won't be the sole driver |
| 5–7 | **low** — ASO alone won't generate meaningful installs |

#### Featured potential checklist

An app has App Store featured potential if it meets **3+ of these 5 criteria**:

1. Uses a newly released Apple/Google platform feature (widgets, Live Activities, visionOS, AI APIs)
2. Has exceptional design quality (would look good in an editorial story)
3. Serves an underrepresented audience or emerging cultural moment
4. Has a clear positive-impact or wellness angle
5. Is a premium/indie app (Apple editorially favors paid apps and small teams)

### Step 3 — Creator Economy Fit Assessment

Evaluate whether influencers and creators can authentically promote the app. Not all apps are "creator-friendly" — forcing influencer marketing on a utility app wastes money.

#### Creator fit criteria

| Factor | Score: High | Score: Medium | Score: Low |
|---|---|---|---|
| **Content generation** | App produces visual or shareable output that IS the content (before/after, results, transformations) | App experience is interesting to narrate/demonstrate | App is invisible — nothing to show on camera |
| **Audience alignment** | Clear niche creator communities already talk about this problem space | Adjacent creator communities exist | No creator community maps to this product |
| **Demo-ability** | Can be demonstrated in a 30–60 second clip with visible value | Needs 2–3 minute explanation to convey value | Requires hands-on usage over days to appreciate |
| **Authenticity** | Creator would genuinely use the app (not just shill for money) | Creator could plausibly use it occasionally | Feels forced — creator has no real use case |
| **Affiliate/monetization fit** | App has a price point that supports affiliate commissions ($5+/mo or $20+ one-time) | Freemium with conversion — harder to attribute | Free app with no monetization — no creator incentive |

**Scoring**: Count High/Medium/Low across all 5 factors.
- **high fit**: 3+ factors scored High
- **medium fit**: 2 factors High, or 3+ Medium
- **low fit**: 2+ factors Low, or no factors High

### Step 4 — Paid Channel Feasibility

Assess whether paid acquisition can work within indie budget constraints.

| Budget tier | Monthly ad spend | Viable paid strategies |
|---|---|---|
| **Micro** (< $200/mo) | Testing only | One platform, 2–3 ad creatives, learn CPM/CPI before scaling. Not a primary channel. |
| **Light** (< $500/mo) | Targeted campaigns | One platform with lookalike audiences. Can work if CPI < $2 and LTV > $6. |
| **Moderate** (< $2000/mo) | Real optimization | Multi-creative testing, retargeting. Viable if LTV:CAC > 3:1 on at least one platform. |

If `budget_constraint` from user profile is "low", cap paid feasibility at "marginal" regardless of other factors — the user cannot sustain the learning curve of paid acquisition.

### Step 5 — Founder Distribution Edge

Cross-reference `user_profile.md` to identify whether the founder has a pre-existing distribution advantage:

| Advantage type | Impact |
|---|---|
| Existing audience (newsletter, social, YouTube) | Direct launch channel — reduces cold-start risk significantly |
| Community membership (active in relevant subreddits, Discord, forums) | Warm audience for validation and early adopters |
| Content creation skills (video, writing, design) | Can execute organic content channels without outsourcing |
| Technical SEO / ASO experience | Can capitalize on search-driven channels faster |
| Industry relationships | Potential for partnerships, cross-promotion, press |
| None identified | Must rely on product-led or paid growth — harder path |

### Step 6 — Distribution Verdict

Compute the overall verdict by evaluating all dimensions together, then **adjust for founder tier**.

#### Raw verdict logic

| Condition | Raw verdict |
|---|---|
| k-factor ≥ 0.5 OR (ASO = high AND creator_fit = high) OR founder has existing audience | **strong** |
| k-factor ≥ 0.2 AND at least one other dimension scores medium+ | **moderate** |
| All dimensions low/marginal, no organic path, paid not viable at budget | **weak** |

#### Tier adjustment

The same distribution profile means different things to different founders. Apply this adjustment:

| Founder tier | Adjustment |
|---|---|
| **beginner** | Downgrade verdict by one level if the only viable channels require technical skill (SEO, paid optimization, ASO keyword research). Beginners need channels with fast feedback loops: TikTok organic, community posting, referral-based growth. Flag complex channels as "aspirational — learn first." |
| **builder** | No adjustment. Builders can execute most channels with some learning curve. Flag paid channels > $500/mo as risky given typical builder budgets. |
| **growth** | Upgrade verdict by one level if paid channels are viable and the founder has optimization experience. Growth-tier founders can unlock channels that are traps for beginners. |

If `user_profile.md` is unavailable, skip tier adjustment and note it as a gap.

## Output

Write to `memory/ideas/<slug>/distribution.json`:

```json
{
  "organic_reach_potential": "high | medium | low",
  "viral_loop_exists": false,
  "viral_loop_type": "inherent | collaborative | word-of-mouth | incentivized | content-as-distribution | none",
  "viral_loop_description": "",
  "k_factor_estimate": 0.0,
  "k_factor_classification": "viral-growth-engine | viral-assist | marginal | non-viral",
  "paid_feasibility": "viable | marginal | not-viable",
  "minimum_paid_budget_monthly": 0,
  "paid_feasibility_rationale": "",
  "platform_advantage": {
    "aso_opportunity": "high | medium | low",
    "aso_score_breakdown": {
      "category_competition": 0,
      "keyword_opportunity": 0,
      "search_intent_match": 0,
      "review_velocity_potential": 0,
      "visual_differentiation": 0,
      "total": 0
    },
    "featured_potential": false,
    "featured_criteria_met": []
  },
  "creator_economy_fit": "high | medium | low",
  "creator_fit_rationale": "",
  "creator_fit_breakdown": {
    "content_generation": "high | medium | low",
    "audience_alignment": "high | medium | low",
    "demo_ability": "high | medium | low",
    "authenticity": "high | medium | low",
    "affiliate_fit": "high | medium | low"
  },
  "user_distribution_advantage": "",
  "user_advantage_type": "audience | community | content-skills | seo-aso | relationships | none",
  "recommended_first_channel": "",
  "recommended_first_channel_rationale": "",
  "channels_ranked": [
    { "channel": "", "viability": "high | medium | low", "time_to_first_100_users": "" }
  ],
  "distribution_verdict": "strong | moderate | weak",
  "tier_adjustment_applied": "",
  "distribution_verdict_rationale": ""
}
```

## Notes

- The `recommended_first_channel` should always be the highest-viability channel the founder can realistically execute given their tier. Don't recommend "TikTok organic" to someone who has never made a video; don't recommend "ASO" to someone who doesn't know what keywords are.
- If `competitors.json` is available, check competitor distribution strategies — an app succeeding via a channel the founder can replicate is a strong positive signal.
- k-factor estimates are inherently speculative pre-launch. Treat them as directional, not precise. Flag any estimate above 0.5 as "optimistic until validated."
