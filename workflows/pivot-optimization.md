---
name: pivot-optimization
trigger: "Idea scored poorly (verdict: pivot or drop) or user is questioning current direction"
entry_condition: "memory/ideas/<slug>/scores.json must exist"
exit_output: "memory/ideas/<slug>/pivot_options.json + pivot_scores.json"
---

# Workflow: Pivot Optimization

## Startup Announcement

When this workflow is triggered, **immediately** say this before doing anything else:

> **🔄 Starting: Pivot Optimization**
> I'll dig into why your idea scored the way it did, identify the root causes of weak dimensions, and generate concrete pivot options — each with a projected score improvement and effort estimate.

Then proceed to step 1.

## Trigger

User expresses one of:
- "Should I pivot?"
- "This isn't working — what should I change?"
- Automatically offered when idea-validation returns verdict: `pivot` or `drop`

## Entry Conditions

- `memory/ideas/<slug>/scores.json` must exist (run `idea-validation` first if not)
- User specifies which idea to pivot (by slug or name)

## Skill Chain

```
1. idea-scoring (re-read existing scores)
   ↓ reads: all dimension files in memory/ideas/<slug>/
   ↓ confirms: memory/ideas/<slug>/scores.json is current
   → present: Confirm the current score (X/100) and verdict. State which dimensions are weakest to set context for the pivot analysis. Full scores at memory/ideas/<slug>/scores.json

2. weakness-detection
   ↓ reads: memory/ideas/<slug>/scores.json + all dimension files + related market insights files
   ↓ writes: memory/ideas/<slug>/weaknesses.json
   → present: State the 2–3 weakest scoring dimensions, their root causes, and the most critical failure mode. Full analysis at memory/ideas/<slug>/weaknesses.json

3. pivot-engine
   ↓ reads: memory/ideas/<slug>/weaknesses.json + scores.json
   ↓ writes: memory/ideas/<slug>/pivot_options.json + memory/ideas/<slug>/pivot_report.md
   → present: Share the full pivot_report.md inline. Files also saved at memory/ideas/<slug>/pivot_options.json and memory/ideas/<slug>/pivot_report.md

4. idea-scoring (re-score recommended pivot variant)
   ↓ reads: pivot_options.json + existing dimension files (adjusted for pivot)
   ↓ writes: memory/ideas/<slug>/pivot_scores.json
   → present: Show the projected score for the recommended pivot variant vs. the original score. State whether the pivot crosses the 50-point threshold. Full projection at memory/ideas/<slug>/pivot_scores.json
```

## State Flow

| Step | Reads | Writes |
|---|---|---|
| idea-scoring (existing) | all dimension files | `scores.json` (confirms current) |
| weakness-detection | `scores.json` + dimension files | `weaknesses.json` |
| pivot-engine | `weaknesses.json`, `scores.json` | `pivot_options.json` |
| idea-scoring (pivot) | `pivot_options.md` + adjusted dimensions | `pivot_scores.json` |

## Exit Output

- `memory/ideas/<slug>/pivot_report.md` — human-readable pivot brief with evidence-backed options, score projections, trade-offs, and recommended first action
- `memory/ideas/<slug>/pivot_options.json` — structured pivot data for downstream re-scoring
- `memory/ideas/<slug>/pivot_scores.json` — projected score for the recommended pivot

If the recommended pivot scores ≥ 50 → suggest running full `idea-validation` on the pivot variant (create new idea slug).

If the recommended pivot still scores < 30 → recommend dropping the idea.

## Notes

<!-- TODO: Define when to create a new idea slug vs. updating the existing one for a pivot -->
<!-- TODO: Add "micro-pivot" path for small adjustments (pricing only, audience only) -->
