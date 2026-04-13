---
name: weakness-detection
description: Analyzes idea-scoring output to identify the weakest dimensions, root causes of low scores, and probable failure modes if the idea were pursued as-is.
---

<!-- version: 0.1.0 | outputs: memory/ideas/<slug>/weaknesses.json -->

# Skill: weakness-detection

## Purpose

Before triggering the pivot engine, understand WHY dimensions are weak. A low distribution score might mean "no viral loop" (fixable) or "fundamentally wrong category for organic growth" (structural). Surface the root cause, not just the symptom.

## Input

- Idea slug
- `memory/ideas/<slug>/scores.json` (required)
- All available dimension files in `memory/ideas/<slug>/`

## Weakness Classification

| Root Cause Type | Description | Fix Type |
|---|---|---|
| Structural | Inherent to the idea, can't be pivoted away | Drop or major pivot |
| Situational | Weak due to user's current constraints | Fixable (more time, budget) |
| Knowledge gap | Weak because data is missing | Run more research |
| Addressable | Weak but has a clear fix | Targeted pivot |

## Process

<!-- TODO: Add failure mode library by app category -->
<!-- TODO: Define threshold for "weak" (e.g., dimension score < 40) -->

1. Load scores.json, identify dimensions scoring below threshold.
2. For each weak dimension, read the source file to understand why.
3. Classify the root cause (structural / situational / knowledge gap / addressable).
4. Describe the failure mode if the idea proceeded without fixing this weakness.

## Output

Write to `memory/ideas/<slug>/weaknesses.json`:

```json
{
  "weak_dimensions": [
    {
      "dimension": "",
      "score": 0,
      "root_cause_type": "structural | situational | knowledge-gap | addressable",
      "root_cause_description": "",
      "failure_mode": ""
    }
  ],
  "critical_weaknesses": [],
  "addressable_weaknesses": [],
  "overall_weakness_severity": "fatal | major | minor"
}
```

## Notes

<!-- TODO: Define "fatal" vs "major" vs "minor" by combination of weak dimensions -->
