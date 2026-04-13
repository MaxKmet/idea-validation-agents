---
name: market-deep-dive
trigger: "User wants to understand a market or category before committing to an idea"
entry_condition: "User specifies a market category or topic"
exit_output: "memory/market_insights/<niche>-<platform>-<YYYY>-<MM>.md (new file) + per-idea dimension files"
---

# Workflow: Market Deep Dive

## Startup Announcement

When this workflow is triggered, **immediately** say this before doing anything else:

> **📊 Starting: Market Deep Dive**
> I'll analyze the market you're interested in — trends across platforms, competitive landscape, market size, and how people actually acquire users in this space.

Then proceed to step 1.

## Trigger

User expresses one of:
- "Tell me about the [category] market"
- "What's happening in [space]?"
- "Is [category] a good market to enter?"
- Used as a prerequisite before idea-generation in a specific category

## Entry Conditions

- User specifies a topic or category (e.g., "nutrition apps", "B2B invoicing tools")
- No idea is required — this is pre-idea market research
- Create a temporary slug for the research context (e.g., `market-nutrition-2026`)

## Skill Chain

```
1. trend-analysis
   ↓ reads: topic from user
   ↓ writes: memory/market_insights/<niche>-<platform>-<YYYY>-<MM>.md (one file per platform)
   → present: Share top 3 trend signals, trend velocity, and overall verdict (hot/warm/cool/cold). Full analysis at memory/market_insights/<niche>-<platform>-<YYYY>-<MM>.md

2. competitor-mapper
   ↓ reads: topic, memory/market_insights/<niche>-*-<YYYY>-<MM>.md (from step 1)
   ↓ writes: memory/ideas/<slug>/competitors.json
   → present: List the top 3 direct competitors with pricing and top complaint, and state market saturation level. Full landscape at memory/ideas/<slug>/competitors.json

3. tam-sam-som-builder
   ↓ reads: memory/market_insights/<niche>-*-<YYYY>-<MM>.md (search volume proxy), memory/ideas/<slug>/competitors.json
   ↓ writes: memory/ideas/<slug>/market_size.json
   → present: State TAM, SAM, realistic SOM for year 1, and market size verdict. Full estimates at memory/ideas/<slug>/market_size.json

4. distribution-analysis
   ↓ reads: memory/user_profile.md, topic
   ↓ writes: memory/ideas/<slug>/distribution.json
   → present: State the distribution verdict, recommended first acquisition channel, and whether a viral loop exists in this market. Full analysis at memory/ideas/<slug>/distribution.json
```

## State Flow

| Step | Reads | Writes |
|---|---|---|
| trend-analysis | topic from user | `memory/market_insights/<niche>-<platform>-<YYYY>-<MM>.md` |
| competitor-mapper | topic, `market_insights/<niche>-*` | `competitors.json` |
| tam-sam-som-builder | `market_insights/<niche>-*`, `competitors.json` | `market_size.json` |
| distribution-analysis | `user_profile.md`, topic | `distribution.json` |

## Exit Output

The user receives a market intelligence report synthesized from:
- New `memory/market_insights/<niche>-<platform>-deep-dive-<YYYY>-<MM>.md` file
- `market_size.json` — TAM/SAM/SOM estimates
- `competitors.json` — competitive landscape
- `distribution.json` — how people acquire users in this market


## Notes

<!-- TODO: Add option to run trend-analysis only (quick version without full competitor map) -->
