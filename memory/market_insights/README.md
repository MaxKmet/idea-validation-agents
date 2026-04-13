---
description: Index and conventions for the market_insights directory
---

# Market Insights Directory

Each file in this directory is one completed market analysis. Files are written by the `trend-analysis` and `signal-aggregator` skills.

## Naming Convention

```
<niche>-<platform>-<YYYY>-<MM>.md
```

Examples:
- `nutrition-tiktok-2026-04.md` — TikTok nutrition trends, April 2026
- `fitness-reddit-2026-05.md` — Reddit fitness community analysis, May 2026
- `personal-finance-apps-2026-03.md` — App Store personal finance trends, March 2026
- `productivity-web-search-2026-06.md` — Web search trends for productivity, June 2026

For multi-platform analyses (no single platform focus):
```
<niche>-multi-<YYYY>-<MM>.md
```

## Frontmatter Schema

Each file must include:

```yaml
---
niche: <topic>
platform: tiktok | reddit | apps | web-search | multi
analyzed_at: YYYY-MM-DD
status: fresh | stale
stale_after: YYYY-MM-DD   # 6 months after analyzed_at
---
```

## Freshness Rule

Analyses older than 6 months should be flagged `status: stale`. Re-run `trend-analysis` to produce a new file — do not overwrite the old one.

## Files

| File | Niche | Platform | Period | Status |
|---|---|---|---|---|
| [nutrition-tiktok-2026-04.md](nutrition-tiktok-2026-04.md) | nutrition | tiktok | April 2026 | fresh |
