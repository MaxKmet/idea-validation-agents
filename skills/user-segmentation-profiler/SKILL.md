---
name: user-segmentation-profiler
description: Classifies the user into an ICP tier (beginner/builder/growth) based on experience, constraints, and goals. Run once per user session before any workflow.
---

<!-- version: 0.1.0 | outputs: memory/user_profile.md -->

# Skill: user-segmentation-profiler

## Purpose

Classify the user into one of three ICP tiers and capture their constraints so all subsequent skills can tailor their output and recommendations appropriately.

## Input

- Conversation history or direct user answers about experience, budget, time, and goals.
- Optional: existing `memory/user_profile.md` (update if already exists)

## Process

<!-- TODO: Add full interview questions and scoring rubric -->

1. Ask the user about shipped apps (count, revenue, outcome).
2. Ask about available time per week and budget for ads/tools.
3. Ask about risk tolerance (need income vs. exploring).
4. Score against the tier rubric below.
5. Write output to `memory/user_profile.md`.

### Tier Rubric

| Tier | Criteria |
|---|---|
| `beginner` | No shipped apps, no audience, needs full guidance |
| `builder` | Some experience, weak GTM/validation skills |
| `growth` | Understands CAC/LTV, wants leverage and scale |

## Output

Write to `memory/user_profile.md` (merge with existing if present):

```json
{
  "icp_tier": "beginner | builder | growth",
  "budget_constraint": "low | medium | high",
  "time_per_week_hours": 0,
  "risk_tolerance": "low | medium | high",
  "strategy_recommendations": []
}
```

## Notes

<!-- TODO: Handle case where user refuses to answer questions -->
<!-- TODO: Define re-segmentation trigger (e.g., user reveals new info mid-session) -->
