---
name: idea-validation
trigger: "User has a specific app idea and wants it validated"
entry_condition: "User has stated a concrete idea"
exit_output: "memory/ideas/<slug>/decision_memo.md"
---

# Workflow: Idea Validation

## Startup Announcement

When this workflow is triggered, **immediately** say this before doing anything else:

> **🔍 Starting: Idea Validation**
> I'll run a full validation on your idea across demand, competition, monetization, distribution, retention, and founder fit — and give you a scored verdict with a concrete next step.

Then proceed to step 1.

## Trigger

User expresses one of:
- "Validate my idea: [description]"
- "I want to build [idea] — is it worth it?"
- "Score this idea for me"
- Resuming after idea-generation selected a candidate

## Entry Conditions

1. Create `memory/ideas/<slug>/idea.md` with the raw idea description before starting the chain.
2. Idea slug = kebab-case derived from idea name (max 40 chars).

## Skill Chain

```
1. trend-analysis
   ↓ reads: topic derived from memory/ideas/<slug>/idea.md
   ↓ writes: memory/market_insights/<niche>-<platform>-<YYYY>-<MM>.md (one file per platform)
   → present: Share the top 3 trend signals found, trend velocity, and overall verdict (hot/warm/cool/cold). Full analysis at memory/market_insights/<niche>-<platform>-<YYYY>-<MM>.md

2. competitor-mapper
   ↓ reads: memory/ideas/<slug>/idea.md, memory/market_insights/<niche>-<platform>-<YYYY>-<MM>.md (one file per platform)
   ↓ writes: memory/ideas/<slug>/competitors.json
   → present: List the top 3 direct competitors with their pricing and top complaint, and state market saturation. Full landscape at memory/ideas/<slug>/competitors.json

3. desire-evaluator
   ↓ reads: memory/ideas/<slug>/idea.md, memory/market_insights/<niche>-<platform>-<YYYY>-<MM>.md (one file per platform)
   ↓ writes: memory/ideas/<slug>/desire_scores.json
   → present: State the primary desire driver, desire strength label, and virality potential. Full scores at memory/ideas/<slug>/desire_scores.json

4. pricing-and-wtp
   ↓ reads: memory/ideas/<slug>/user_extraction.json, memory/ideas/<slug>/competitors.json, memory/ideas/<slug>/desire_scores.json, memory/market_insights/<niche>-<platform>-<YYYY>-<MM>.md (one file per platform)
   ↓ writes: memory/ideas/<slug>/pricing.json
   → present: State the recommended pricing model, target WTP range, and estimated freemium conversion rate. Full model at memory/ideas/<slug>/pricing.json

5. distribution-analysis
   ↓ reads: memory/user_profile.md (if present), memory/ideas/<slug>/idea.md, memory/market_insights/<niche>-<platform>-<YYYY>-<MM>.md (one file per platform)
   ↓ writes: memory/ideas/<slug>/distribution.json
   → present: State the distribution verdict, recommended first acquisition channel, and whether a viral loop exists. Full analysis at memory/ideas/<slug>/distribution.json

6. retention-predictor
   ↓ reads: memory/ideas/<slug>/desire_scores.json, memory/ideas/<slug>/user_extraction.json
   ↓ writes: memory/ideas/<slug>/retention.json
   → present: State the retention verdict, natural usage frequency, and top churn risk factor. Full prediction at memory/ideas/<slug>/retention.json

7. cac-modeler
    ↓ reads: memory/user_profile.md (if present), memory/ideas/<slug>/pricing.json, memory/ideas/<slug>/distribution.json
    ↓ writes: memory/ideas/<slug>/cac.json
    → present: State the viability verdict, LTV:CAC ratio for the recommended channel, and payback period in months. Full model at memory/ideas/<slug>/cac.json

8. idea-scoring
    ↓ reads: memory/ideas/<slug>/weighted_signals.json, competitors.json, pricing.json, distribution.json, retention.json, desire_scores.json, cac.json
    ↓ writes: memory/ideas/<slug>/scores.json
    → present: Show the final score (X/100), verdict, top strength, and top weakness. Full breakdown at memory/ideas/<slug>/scores.json

9. decision-memo
    ↓ reads: memory/ideas/<slug>/scores.json + all dimension files
    ↓ writes: memory/ideas/<slug>/decision_memo.md
    → present: Share the complete decision memo in full. File also saved at memory/ideas/<slug>/decision_memo.md
```

## State Flow

| Step | Reads | Writes |
|---|---|---|
| competitor-mapper | `idea.md` | `competitors.json` |
| desire-evaluator | `user_extraction.json` (opt), `idea.md` | `desire_scores.json` |
| pricing-and-wtp | `user_extraction.json`, `competitors.json`, `desire_scores.json` | `pricing.json` |
| distribution-analysis | `user_profile.md`, `idea.md` | `distribution.json` |
| retention-predictor | `desire_scores.json`, `user_extraction.json` | `retention.json` |
| cac-modeler | `user_profile.md`, `pricing.json`, `distribution.json` | `cac.json` |
| idea-scoring | `weighted_signals.json`, `competitors.json`, `pricing.json`, `distribution.json`, `retention.json`, `desire_scores.json`, `cac.json` | `scores.json` |
| decision-memo | `scores.json` + all dimension files | `decision_memo.md` |

## Exit Output

`memory/ideas/<slug>/decision_memo.md` — the human-readable validation brief with:
- Verdict (pursue / test / pivot / drop)
- Final score
- Top 3 strengths with evidence
- Top 3 risks with evidence
- Recommended next step

If verdict is `pivot` or `drop`, offer to run `pivot-optimization` workflow.

## Notes

<!-- TODO: Define optional fast-path validation (skip steps 2–4 for quick gut-check) -->
<!-- TODO: Steps 2–5 have no inter-dependencies and can be parallelized -->
