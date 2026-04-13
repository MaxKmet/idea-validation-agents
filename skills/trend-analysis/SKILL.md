---
name: trend-analysis
description: Analyzes market trends across platforms (TikTok, Reddit, App Store, Google Trends) for a given topic or category. Writes a new file to memory/market_insights/.
---

<!-- version: 0.1.0 | outputs: memory/market_insights/<niche>-<platform>-<YYYY>-<MM>.md | prompts: skills/trend-analysis/prompts/ -->

# Skill: trend-analysis

## Purpose

Build a comprehensive, multi-platform view of what is trending in a market category. Used in the market-deep-dive workflow and as a standalone research tool. Output is appended to the shared market intelligence file.

## Input

- Topic or category to analyze (e.g., "nutrition apps", "personal finance", "fitness")
- Platform prompt templates from `skills/trend-analysis/prompts/` (see Prompts section below)

## User Interaction

Before executing, ask the user which platforms to include in the analysis. Present the options clearly and wait for their answer before proceeding.

**Prompt to user:**

> Which sources would you like to include in this analysis? (select one or more)
>
> 1. **TikTok** — hashtag trends, viral content angles, creator gaps
> 2. **Reddit** — community pain points, recurring complaints, unmet needs
> 3. **App Store** — category rankings, new entrants, top review complaints
> 4. **Web Search (Google)** — search volume trends, rising queries, SEO demand
> 5. **All of the above** — full multi-platform analysis (recommended for a new niche)

Wait for the user's selection. Accept answers like "1, 3", "TikTok and Reddit", "all", or "just App Store". Map their answer to the corresponding prompt files before continuing.

If the user selects multiple platforms, run each one sequentially and produce a separate output file per platform. Do not combine platforms into a single file unless explicitly asked.

## Prompts Directory

Per-platform analyst prompt templates live in `skills/trend-analysis/prompts/`. Each contains a structured research brief with source tiers, output sections, and a `[NICHE]` or `[CATEGORY]` placeholder to fill before invoking:

| File | Platform | Placeholder |
|---|---|---|
| `prompts/tiktok.md` | TikTok hashtag & trend analysis | `[NICHE]` |
| `prompts/reddit.md` | Reddit community & pain-point analysis | `[NICHE]` |
| `prompts/apps.md` | App Store & web app category analysis | `[CATEGORY]` |
| `prompts/web-search.md` | Google/SEO keyword trend analysis | `[NICHE]` |

Completed analyses are stored as individual files in `memory/market_insights/` following the naming convention `<niche>-<platform>-<YYYY>-<MM>.md`. See `memory/market_insights/README.md` for the full schema.

## Platform Coverage

| Platform | Signal | Tool/Source |
|---|---|---|
| TikTok | Hashtag views, viral content, creator angles | TikTok Creative Center |
| Reddit | Subreddit growth, post volume, pain language | Reddit search + analytics |
| App Store | Category rankings, new entrants, review trends | Sensor Tower, data.ai, AppFollow |
| Google Search | Search volume trends, rising queries | Google Trends, Ahrefs |

## Process

1. Load the platform prompt from `prompts/<platform>.md` and replace `[NICHE]` / `[CATEGORY]` with the target topic.
2. Execute the prompt: research the platform using the source tiers and output structure defined in the prompt.
3. Score trend velocity: rising-fast / rising / stable / declining.
4. Identify the strongest creator/content angle and any monetization evidence.
5. Write findings to a new file: `memory/market_insights/<niche>-<platform>-<YYYY>-<MM>.md`.

One file per platform run. To cover all platforms, run this skill once per platform and produce four files.

## Output

Write to `memory/market_insights/<niche>-<platform>-<YYYY>-<MM>.md`.

The file has two parts:

### Part 1 — YAML Frontmatter (machine-readable summary)

```yaml
---
niche: <topic>
platform: tiktok | reddit | apps | web-search | multi
analyzed_at: YYYY-MM-DD
status: fresh
stale_after: YYYY-MM-DD   # 6 months after analyzed_at
trend_velocity: rising-fast | rising | stable | declining
overall_verdict: hot | warm | cool | cold
key_insight: "<one-sentence takeaway>"
top_signals: []           # 3–5 bullet strings: top hashtags, subreddits, queries, or app categories
monetization_evidence: [] # 1–3 strings: existing products/revenue that confirm willingness to pay
---
```

### Part 2 — Full Narrative Analysis (long-form Markdown)

Follow the output structure mandated by the platform prompt template exactly

The narrative must be self-contained — a downstream skill reading only this file should have everything it needs to map trends to product opportunities.

