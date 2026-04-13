---
name: trend-to-product-mapper
description: Maps viral social content and trending topics to concrete app opportunities by extracting the underlying problem and validating monetization fit.
---

<!-- version: 0.3.0 | outputs: memory/ideas/<slug>/idea.md (up to 10 per run) -->

# Skill: trend-to-product-mapper

## Purpose

Surface app ideas from real-world signals rather than speculation. The pipeline is: viral content → extract problem → map to app → validate monetization. This skill bridges social listening and product ideation.

## User Interaction

Before executing, clarify which niche to analyze. Use available context to suggest options — don't ask blindly.

**Step 1 — Infer candidates from context:**

Check in this order:
1. `memory/market_insights/` — list any existing trend-analysis files; extract niche names from filenames (e.g., `nutrition-tiktok-2026-04.md` → "nutrition")
2. `memory/user_profile.md` — check for `domain`, `interests`, or `background` fields
3. The current conversation — did the user mention a topic or market earlier?

**Step 2 — Present options:**

If candidates were found from context:

> Which niche would you like to map to a product opportunity?
>
> Based on available research:
> - **[inferred niche]** _(trend data: [platform] [period])_
> - **[other inferred niches if any]**
>
> Or describe your own — e.g., "productivity tools for freelancers", "pet care", "language learning"

If no candidates were found:

> What niche or market category would you like to explore? A few starting points:
> - Fitness / nutrition / weight loss
> - Personal finance / investing
> - Mental health / mindfulness
> - Productivity / focus
> - Or describe your own in a few words

**Step 3 — Confirm:**

Once the user selects or describes a niche, confirm it back and proceed to Process.

## Input

- Target niche (e.g., "nutrition", "fitness", "personal finance")
- `memory/market_insights/<niche>-<platform>-<YYYY>-<MM>.md` — one or more trend-analysis output files for the niche. Read the full narrative (Part 2) from each file; do not rely solely on the YAML frontmatter.
- `memory/user_profile.md` to filter for user's domain fit and constraints

## Pipeline

```
trend-analysis output → scan for distinct opportunities → extract problem per opportunity → validate monetization → write up to 10 idea.md files
```

### What to Read from Trend-Analysis Output

| Section in trend-analysis file | What to extract |
|---|---|
| Emerging / Rising Trends | Fastest-moving problems and content angles |
| Financial Opportunities | Willingness-to-pay evidence and market size estimates |
| Key Hashtags / Subreddits / Keyword Clusters | Vocabulary the audience uses for the problem |
| Strategic Insights | Creator gaps and underserved segments |
| `monetization_evidence` (YAML frontmatter) | Quick-scan: is anyone already paying? |

Prefer signals that appear across **multiple platforms** — cross-platform resonance is a stronger product signal than single-platform virality.

## Process

1. Read available trend-analysis files relevant for the niche from `memory/market_insights/`.
2. Scan the full narrative of each file and identify **distinct** product opportunities — different underlying problems, different audience segments, or different app categories count as distinct. Do not list variations of the same idea.
3. Rank candidates by signal strength: weight cross-platform resonance and willingness-to-pay evidence most heavily. Drop candidates with no monetization signal.
4. Take the top 5–10 candidates (only include as many as have genuine signal — do not pad to reach 10).
5. For each candidate: extract the underlying problem (frustration or desire, not content topic), emotional trigger, audience vocabulary, app category, key features, key differentiator, and monetization evidence.
6. Assign a slug to each idea (kebab-case, max 40 chars, derived from the app concept).
7. Write one `idea.md` per idea to its own directory: `memory/ideas/<slug>/idea.md`.

## Output

For each identified opportunity, write to `memory/ideas/<slug>/idea.md`.

The file uses YAML frontmatter for machine-readable metadata and a full narrative body for human readability and downstream skill consumption.

### Frontmatter

```yaml
---
idea_slug: <slug>
status: candidate
created_at: <ISO date>
source_niche: <niche>
source_files: []        # memory/market_insights/ filenames read
platforms_covered: []   # e.g. ["tiktok", "reddit"]
trend_velocity: rising-fast | rising | stable | declining
cross_platform_resonance: true | false
monetization_validated: true | false
confidence: high | medium | low
---
```

### Body

Write the following sections in full prose or structured lists — no abbreviation:

```markdown
# <App Concept Name>

## The Problem
What specific frustration or unmet desire is this idea addressing? Describe it from the user's perspective — the emotional experience, not the feature gap. Include the exact vocabulary the audience uses.

**Emotional trigger:** <the core feeling driving the behavior — anxiety, FOMO, shame, aspiration, etc.>

**Audience vocabulary:** <3–5 exact phrases pulled from hashtags, post titles, or search queries>

## Market Signal Evidence
What trend data supports this? For each platform covered, cite the specific signal:

- **TikTok:** <hashtag, view count, content angle>
- **Reddit:** <subreddit, recurring post type, upvote pattern>
- **App Store:** <category trend, review complaint pattern, new entrant activity>
- **Web Search:** <rising query, search volume indicator>

**Trend velocity:** <rising-fast | rising | stable | declining>
**Cross-platform resonance:** <yes/no — does the same problem appear on 2+ platforms?>

## App Concept
What is the app? Describe it in 2–3 sentences as if pitching to a user, not an investor. Focus on what it does and who it's for.

**App category:** <e.g., habit tracker, AI coach, marketplace, tool>

## Key Features
The 3–5 core features that directly address the problem. Each feature should map to a specific pain point or desire from the Market Signal Evidence section.

1. **<Feature name>** — <what it does and why it matters>
2. ...

## Key Differentiator
What makes this meaningfully different from what already exists? Reference the saturation assessment from the trend-analysis Financial Opportunities section. One clear wedge — not a feature list.

## Monetization Evidence
What proof exists that people pay for solutions to this problem?

- <existing product / revenue signal / pricing evidence>
- ...

**Monetization validated:** <yes/no>

## Confidence Assessment
**Overall confidence:** <high | medium | low>

Reasoning: <1–2 sentences explaining the confidence level — what's strong, what's uncertain>
```

After writing all files, present a summary table to the user:

| # | Slug | App Concept | Confidence | Cross-Platform | Monetization |
|---|---|---|---|---|---|
| 1 | `<slug>` | ... | high/medium/low | yes/no | validated/unvalidated |
| ... | | | | | |

## Notes

<!-- TODO: Define what counts as "monetization validated" — IH revenue post? App Store paid app? -->
