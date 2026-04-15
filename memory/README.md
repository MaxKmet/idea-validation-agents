# Memory System

This directory is the persistent state layer shared across all platform adapters and all skills. All skill outputs are written here. All skill inputs are read from here.

## Structure

```
memory/
  user_profile.md          # User background, ICP tier, strengths, constraints
  market_insights/         # Per-niche market intelligence (one file per niche + platform + period)
    README.md              # Index and naming convention
    <niche>-<platform>-<YYYY>-<MM>.md  # e.g. nutrition-tiktok-2026-04.md
  ideas/
    <idea-slug>/           # One directory per idea evaluated
      idea.md              # Idea description, trend evidence, metadata + status (written by trend-to-product-mapper or idea-generator)
      user_extraction.json
      signals.json
      weighted_signals.json
      keywords.json
      desire_scores.json
      competitors.json
      pricing.json
      cac.json
      market_size.json
      distribution.json
      retention.json
      complexity.json
      scores.json
      weaknesses.json
      pivot_options.json    # Structured pivot data for downstream re-scoring
      pivot_report.md       # Human-readable pivot brief (evidence, projections, recommendation)
      pivot_scores.json
      decision_memo.md
```

## Naming Convention

- Idea slugs: kebab-case, max 40 characters, derived from idea name
- Examples: `habit-tracker-climbers`, `nutrition-coach-glp1`, `freelance-invoice-ios`
- Market research slugs: prefix with `market-` (e.g., `market-nutrition-2026`)

## State Protocol

- **Skills WRITE** structured JSON or Markdown to their designated output files
- **Orchestrator READS** output files and provides relevant context when invoking the next skill
- Skills do NOT call each other — the orchestrator manages the chain

## Idea Lifecycle

Ideas are never deleted. Use `status` field in `idea.md` to track lifecycle:

| Status | Meaning |
|---|---|
| `candidate` | Generated but not yet validated |
| `in-validation` | Currently being analyzed |
| `scored` | Validation complete, has decision_memo |
| `active` | User is building this |
| `paused` | On hold |
| `dropped` | Decided not to pursue |

## Rules

1. Never delete idea directories — set `status: dropped` in idea.md instead
2. `user_profile.md` is updated incrementally — later skills append new fields
3. `market_insights/` grows over time — each new analysis is a new file, never overwrite an existing one
4. JSON files must be valid JSON (parseable by any adapter)
