---
name: pivot-engine
description: Generates structured pivot options for a scored idea based on weak dimensions, market_insights signals, and founder constraints. Includes scoring simulation, minimum viable pivot criteria, effort estimation, and indie buildability filtering.
---

<!-- version: 0.2.0 | outputs: memory/ideas/<slug>/pivot_options.json -->

# Skill: pivot-engine

## Purpose

When an idea scores poorly in one or more dimensions, generate concrete pivot options rather than abandoning the idea entirely. A pivot is a deliberate change in **one variable** to improve the weakest dimension — not a complete restart. The best pivots preserve what's already strong while fixing what's broken, and they're grounded in real market signals, not wishful thinking.

## Input

- Idea slug
- `memory/ideas/<slug>/scores.json` (current scores — required)
- `memory/ideas/<slug>/weaknesses.json` (weak dimensions with root causes — required, run weakness-detection first)
- `memory/ideas/<slug>/idea.md` (current concept)
- `memory/ideas/<slug>/competitors.json` (positioning gaps, competitor complaints)
- `memory/ideas/<slug>/distribution.json` (current channel assessment)
- `memory/ideas/<slug>/pricing.json` (current pricing model and WTP)
- `memory/ideas/<slug>/retention.json` (current retention assessment)
- `memory/user_profile.md` (ICP tier, budget, time, distribution advantages)
- `memory/market_insights/<niche>-*-<YYYY>-<MM>.md` (trend data — **use all available platform files**)

### Using Market Insights

Market insights are essential for generating pivots grounded in real demand rather than theory. Extract:

| Field | How it informs pivots |
|---|---|
| `top_signals` | Identify adjacent niches or audience segments with validated demand. A trending subreddit or TikTok hashtag near the idea's space suggests a viable audience pivot target. |
| `trend_velocity` | If the current niche is "declining", pivoting within it is futile — pivot to an adjacent rising niche. If "rising-fast", the problem may be execution (distribution, pricing), not the market. |
| `monetization_evidence` | If monetization is weak but market_insights show competitors successfully charging in the space, the issue is pricing model or positioning, not WTP. Pivot the model, not the idea. |
| Platform narratives (Reddit complaints, TikTok trends, App Store gaps) | Source specific pivot targets: underserved segments mentioned in Reddit threads, content angles trending on TikTok, App Store categories with stale top results. |

## Pivot Types

| Pivot type | What changes | What stays | When to use |
|---|---|---|---|
| **Audience narrowing** | Target user segment | Core problem and solution | Demand is broad but shallow; CAC too high because targeting is diffuse |
| **Audience expansion** | Broaden from niche to adjacent segment | Core solution mechanics | Market is too small (micro-niche verdict); SOM < $10K |
| **Feature simplification** | Scope and complexity | Core value proposition | Complexity too high; time-to-MVP exceeds founder capacity |
| **Feature pivot** | Core feature emphasis | Target audience and problem | Current feature set doesn't match what users actually want (review mining signals) |
| **Niche pivot** | Problem space subcategory | Solution approach | Competition too high in broad category; narrow to underserved niche |
| **Pricing pivot** | Pricing model or price point | Product and audience | WTP mismatch; wrong model for usage pattern; competitive pricing gap |
| **Distribution pivot** | Primary acquisition channel | Product and audience | Current channel is unviable; founder lacks skills/budget for assumed channel |
| **Platform pivot** | Target platform (iOS → web, mobile → desktop) | Core idea and audience | Wrong platform for audience behavior or market dynamics |
| **Monetization pivot** | Revenue model (B2C → B2C2B, app → content, product → service) | Core domain expertise | Direct monetization unviable but the domain has other revenue paths |
| **Problem pivot** | Which problem to solve | Target audience and domain | Audience is right but the specific pain point is weak; adjacent problem is stronger |

## Minimum Viable Pivot Criteria

A pivot must be different enough to change the score but similar enough to preserve existing work and insights. Apply the **Same Idea Test**:

### A valid pivot must meet ALL of these:

1. **Changes exactly 1–2 variables** from the list above. Changing 3+ variables is a new idea, not a pivot — create a new idea slug instead.
2. **Preserves at least one strong dimension** (score ≥ 60 in the original). A pivot that abandons all strengths is a restart.
3. **Has evidence** — the pivot direction is supported by at least one concrete signal (market_insights data, competitor gap, user complaint, trend).
4. **Addressable root cause** — the weakness it targets has `root_cause_type` of "addressable" or "situational" in `weaknesses.json`. Pivots cannot fix structural weaknesses unless the pivot changes the core mechanic (which usually means it's a new idea).

### A pivot is NOT valid if:

- It requires the founder to acquire a skill set they don't have and can't learn in < 4 weeks
- It targets a completely different audience AND a different problem (that's a new idea)
- The only evidence is "maybe this would work" with no supporting signal
- It makes the idea harder to build without a proportional improvement in market viability

## Process

### Step 1 — Load and assess weakness landscape

1. Load `weaknesses.json`. Identify all weak dimensions and their root causes.
2. Separate weaknesses into:
   - **Addressable** (`root_cause_type` = "addressable" or "situational") → these are pivot targets
   - **Knowledge gaps** (`root_cause_type` = "knowledge-gap") → these need more research, not a pivot
   - **Structural** (`root_cause_type` = "structural") → only fixable by major pivot or new idea
3. If `overall_weakness_severity` = "fatal" and all weaknesses are structural, recommend dropping rather than pivoting. Note this in the output.

### Step 2 — Map weak dimensions to pivot types

Use this mapping to identify which pivot types are most likely to improve each weak dimension:

| Weak dimension | Primary pivot types | Secondary pivot types |
|---|---|---|
| **Demand** (< 40) | Problem pivot, audience narrowing | Niche pivot |
| **Competition** (< 40) | Niche pivot, audience narrowing | Feature pivot, platform pivot |
| **Monetization** (< 40) | Pricing pivot, monetization pivot | Audience narrowing (higher-WTP segment) |
| **Distribution** (< 40) | Distribution pivot, platform pivot | Audience narrowing (more reachable segment) |
| **Retention** (< 40) | Feature pivot, feature simplification | Problem pivot (pick a stickier problem) |
| **Founder-Market Fit** (< 40) | Niche pivot (toward founder's domain), feature simplification | Platform pivot (to founder's strongest platform) |

If multiple dimensions are weak, prioritize the one with the lowest score AND an addressable root cause.

### Step 3 — Generate pivot options using market_insights

For each applicable pivot type (from Step 2), generate a concrete option:

1. **Pull evidence from market_insights**:
   - For audience pivots: look for specific user segments mentioned in Reddit discussions or TikTok content
   - For niche pivots: identify adjacent niches with rising trend_velocity
   - For distribution pivots: check which channels show actual activity for the niche in market_insights
   - For pricing pivots: reference monetization_evidence and competitor pricing from `competitors.json`

2. **Be specific, not generic**:
   - Bad: "Narrow the audience"
   - Good: "Target freelance designers who use Figma (150K+ active in r/FigmaDesign) instead of all designers. This segment has higher WTP ($8–12/mo based on competitor pricing), active Reddit communities for organic distribution, and specific pain points around invoice management that existing tools ignore."

3. **Generate 2–3 options**, ranked by expected impact. Each option must pass the Minimum Viable Pivot Criteria.

### Step 4 — Scoring simulation

For each pivot option, simulate the expected score change by projecting how each dimension would shift. This gives the orchestrator enough information to decide whether a full re-score is warranted.

#### Simulation method

For the dimension(s) the pivot targets, estimate the new score range based on:
- The pivot direction and its evidence strength
- Category benchmarks from the rubrics in `idea-scoring`
- What the market_insights data suggests about the pivot target

For dimensions the pivot doesn't target, assume they remain unchanged **unless** there's a clear secondary effect:
- Audience narrowing typically improves Distribution (+5 to +15) but may reduce Demand (-5 to -10) and Market Size
- Feature simplification typically improves Founder-Market Fit (+10 to +20) but may reduce Retention (-5 to -10) if features drove stickiness
- Pricing pivots can affect Distribution (freemium → more installs) and Retention (subscription → commitment)

#### Projected score calculation

```
projected_score = sum of (projected_dimension_scores × weights) × projected_floor_penalty
```

Use the same weights and floor penalty logic from `idea-scoring`. This is an estimate — the actual re-score (step 4 of the pivot-optimization workflow) will be definitive.

Report as a range: `projected_score_range: { low: X, high: Y }`.

### Step 5 — Effort estimation

Each pivot has an execution cost. Estimate it relative to the founder's tier:

| Effort level | Definition | Typical timeline |
|---|---|---|
| **Low** | Can be done in a weekend. Changes copy, positioning, pricing, or targeting — no code changes. | 1–3 days |
| **Medium** | Requires feature changes or new content. Some development work. | 1–3 weeks |
| **High** | Significant rebuild. New core feature, new platform, or new audience requiring fresh research. | 1–3 months |

#### Tier adjustment on effort

| Founder tier | Adjust |
|---|---|
| **Beginner** | Upgrade effort by one level (what's "medium" for a builder is "high" for a beginner) |
| **Builder** | No adjustment |
| **Growth** | Downgrade effort by one level (what's "medium" for a builder is "low" for growth) |

A pivot with "high" effort for the founder's tier should be flagged as risky — the time investment may not be justified unless the projected score improvement is substantial (≥ 20 points).

### Step 6 — Indie buildability filter

Before finalizing, verify each pivot option passes these constraints:

| Constraint | Fails if |
|---|---|
| **Solo buildable** | Pivot requires a team (e.g., marketplace requiring both supply and demand side simultaneously) |
| **Budget feasible** | Pivot requires spend exceeding founder's budget tier (e.g., "run paid social" for a Bootstrap founder) |
| **Time feasible** | Pivot requires > 3 months of work for the founder's tier |
| **Skill feasible** | Pivot requires skills the founder doesn't have and can't learn in 4 weeks (e.g., "build an ML model" for a no-code beginner) |
| **No enterprise creep** | Pivot moves the idea toward B2B enterprise, custom sales, or long sales cycles — fundamentally not an indie B2C play |

If a pivot fails any constraint, either modify it to fit or discard it and note why.

### Step 7 — Select recommended pivot

Rank remaining options by: `(projected_score_improvement / effort_level)` — the best pivot is the one with the highest score impact per unit of effort.

Tie-breakers:
1. Stronger evidence from market_insights
2. Lower risk (fewer dimensions negatively affected)
3. Preserves more of the original idea's strengths

## Output

Write to `memory/ideas/<slug>/pivot_options.json`:

```json
{
  "original_score": 0,
  "original_verdict": "",
  "triggered_by_weaknesses": [
    {
      "dimension": "",
      "score": 0,
      "root_cause_type": "",
      "root_cause_description": ""
    }
  ],
  "structural_weaknesses_unpivotable": [],
  "pivot_options": [
    {
      "pivot_id": "pivot-1",
      "pivot_type": "",
      "description": "",
      "specific_change": "",
      "evidence": "",
      "evidence_source": "",
      "meets_minimum_viable_pivot": true,
      "scoring_simulation": {
        "dimensions_improved": [
          { "dimension": "", "current": 0, "projected_low": 0, "projected_high": 0 }
        ],
        "dimensions_worsened": [
          { "dimension": "", "current": 0, "projected_low": 0, "projected_high": 0 }
        ],
        "dimensions_unchanged": [],
        "projected_score_range": { "low": 0, "high": 0 },
        "projected_verdict_range": ""
      },
      "effort": {
        "level": "low | medium | high",
        "tier_adjusted_level": "low | medium | high",
        "timeline": "",
        "what_changes": "",
        "what_stays": ""
      },
      "indie_buildability": {
        "passes": true,
        "constraints_checked": ["solo_buildable", "budget_feasible", "time_feasible", "skill_feasible", "no_enterprise_creep"],
        "failed_constraints": []
      },
      "trade_offs": [],
      "variables_changed": 0
    }
  ],
  "recommended_pivot": "",
  "recommended_pivot_rationale": "",
  "drop_recommendation": false,
  "drop_rationale": "",
  "market_insights_sources_used": []
}
```

## Notes

- If `overall_weakness_severity` = "fatal" and all weaknesses are structural, set `drop_recommendation` = true and explain why no pivot can save this idea. Still generate 1 option as a "Hail Mary" if the founder wants to try, but be honest about the odds.
- When generating niche pivots, always check `competitors.json` for `positioning_gaps` — an identified gap with evidence is the strongest pivot foundation.
- Pivot options that combine two small changes (e.g., audience narrowing + pricing change) are allowed as a single option if both changes are "low" effort. Call this out as a **compound pivot** and flag the higher risk.
- The `pivot_id` field is used by `idea-scoring` to link re-scores in `pivot_scores.json` back to the specific option.
- If market_insights files are past their `stale_after` date, note that pivot evidence may be outdated and recommend refreshing trend analysis before committing to a pivot direction.
