---
name: desire-evaluator
description: Scores the strength of core human desire motivations (survival, status, belonging, control, curiosity) for a given app idea to predict user pull and retention potential.
---

<!-- version: 0.1.0 | outputs: memory/ideas/<slug>/desire_scores.json -->

# Skill: desire-evaluator

## Purpose

Apps that tap into primal human desires outperform apps that only solve functional problems. This skill scores how strongly an app idea connects to core motivational drivers, which predicts organic virality, retention, and pricing power.

## Input

- Idea slug
- App concept description
- Optional: `memory/ideas/<slug>/user_extraction.json` (identity driver)
- Use this file as reference of what drives core human desires `memory/extra-context/core-human-desires.md`

## Desire Dimensions

| Dimension | Description | Example App |
|---|---|---|
| Survival | Health, safety, financial security | Calorie tracker, budgeting app |
| Status | Looking good, achieving, winning | Fitness leaderboard, portfolio tracker |
| Belonging | Community, connection, not being alone | Group savings, running clubs |
| Control | Mastery, autonomy, reducing chaos | Task manager, habit tracker |
| Curiosity | Learning, discovery, novelty | Language app, quiz game |

## Process

<!-- TODO: Add scoring rubric with question bank per dimension -->
<!-- TODO: Define what score justifies proceeding (e.g., at least one dimension ≥ 4) -->

1. Score each dimension 1–5 based on how directly the app taps into it.
2. Identify the primary and secondary desire drivers.
3. Compute overall desire strength (weighted average).
4. Flag if no dimension scores ≥ 3 (weak desire signal → high churn risk).

## Output

Write to `memory/ideas/<slug>/desire_scores.json`:

```json
{
  "scores": {
    "survival": 0,
    "status": 0,
    "belonging": 0,
    "control": 0,
    "curiosity": 0
  },
  "primary_driver": "",
  "secondary_driver": "",
  "desire_strength": 0,
  "desire_strength_label": "strong | moderate | weak",
  "virality_potential": "high | medium | low",
  "notes": ""
}
```

## Notes

<!-- TODO: Add cross-reference with retention-predictor — desire strength should inform habit score -->
