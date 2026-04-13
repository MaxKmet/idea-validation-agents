---
name: retention-predictor
description: Predicts retention potential by evaluating usage frequency, habit formation mechanics, and churn risk factors for a B2C app idea.
---

<!-- version: 0.1.0 | outputs: memory/ideas/<slug>/retention.json -->

# Skill: retention-predictor

## Purpose

Retention determines LTV. An app that churns users in week 1 can't build a business regardless of acquisition. This skill evaluates how sticky the idea is structurally — not based on feature lists, but on the underlying usage pattern and habit formation potential.

## Input

- Idea slug
- App concept description
- `memory/ideas/<slug>/desire_scores.json` (desire strength informs habit potential)
- `memory/ideas/<slug>/user_extraction.json` (usage frequency from pain map)

## Evaluation Factors

| Factor | High Retention Signal | Low Retention Signal |
|---|---|---|
| Usage frequency | Daily or multiple times/day | Weekly or less |
| External trigger | Clear real-world trigger (meal, workout, payday) | No natural trigger |
| Progress/reward loop | Clear progress visible over time | No feedback loop |
| Network effects | Gets better with more users | No network component |
| Data lock-in | User data accumulates | Nothing to lose by leaving |
| Habit stack | Fits into existing daily routine | Requires behavior change |

## Process

<!-- TODO: Add D1/D7/D30 retention benchmark database by app category -->
<!-- TODO: Add churn risk scoring rubric -->

1. Estimate natural usage frequency based on the problem (daily tooth brushing vs. annual tax filing).
2. Identify external triggers that would cue app usage.
3. Score habit formation potential (1–5) across the six factors above.
4. Estimate D1, D7, D30 retention benchmarks for the app category.
5. Flag high churn risk factors.

## Output

Write to `memory/ideas/<slug>/retention.json`:

```json
{
  "natural_usage_frequency": "multiple daily | daily | weekly | monthly | infrequent",
  "external_trigger": "",
  "habit_formation_score": 0,
  "churn_risk_factors": [],
  "estimated_retention": {
    "d1": 0,
    "d7": 0,
    "d30": 0
  },
  "churn_risk": "low | medium | high",
  "retention_verdict": "sticky | moderate | disposable"
}
```

## Notes

<!-- TODO: Cross-reference with desire_scores — survival/control desires = higher retention -->
