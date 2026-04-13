# Skills — Canonical Definitions

This directory contains the canonical, platform-agnostic skill definitions for the App Idea Validation Agent.

Each skill lives in its own subdirectory: `skills/<skill-name>/SKILL.md`

## Platform Adapters

Platform-specific adapters in `.claude/skills/`, `.codex/skills/`, and `.cursor/rules/` are thin stubs that reference these canonical definitions. When editing a skill, edit the canonical version here first, then update the platform adapter stub's frontmatter if needed.

## Skill Interface Contract

Every skill must:
1. Accept a defined **Input** (documented in the skill's `## Input` section)
2. Write structured output to `memory/` (documented in `## Output`)
3. Be invocable independently — no hidden dependencies beyond what is documented

## Output State Protocol

Skills communicate state through `memory/`. The orchestrator (Claude / Codex / Cursor) reads output files and passes relevant context when invoking the next skill in a workflow chain. Skills do NOT call each other directly.

## Adding a New Skill

1. Create `skills/<skill-name>/SKILL.md` with the standard frontmatter
2. Create `.claude/skills/<skill-name>/SKILL.md` stub
3. Create `.codex/skills/<skill-name>/SKILL.md` stub
4. Create `.cursor/rules/<skill-name>.mdc` stub
5. Add the skill to any relevant workflow in `workflows/`

## Skills Index

| Skill | Purpose | Output |
|---|---|---|
| `user-segmentation-profiler` | Classify user into ICP tier | `memory/user_profile.md` |
| `user-background-interviewer` | Deep user background interview | `memory/user_profile.md` |
| `trend-to-product-mapper` | Map trends to app opportunities | `memory/ideas/<slug>/idea.md` |
| `desire-evaluator` | Score desire motivations | `memory/ideas/<slug>/desire_scores.json` |
| `competitor-mapper` | Map competitive landscape | `memory/ideas/<slug>/competitors.json` |
| `pricing-and-wtp` | Model pricing and WTP | `memory/ideas/<slug>/pricing.json` |
| `cac-modeler` | Model CAC by channel | `memory/ideas/<slug>/cac.json` |
| `tam-sam-som-builder` | Estimate market size | `memory/ideas/<slug>/market_size.json` |
| `distribution-analysis` | Evaluate distribution options | `memory/ideas/<slug>/distribution.json` |
| `retention-predictor` | Predict retention and churn | `memory/ideas/<slug>/retention.json` |
| `pivot-engine` | Generate pivot options | `memory/ideas/<slug>/pivot_options.json` |
| `idea-scoring` | Score idea across all dimensions | `memory/ideas/<slug>/scores.json` |
| `decision-memo` | Write human-readable decision brief | `memory/ideas/<slug>/decision_memo.md` |
| `weakness-detection` | Identify weak dimensions | `memory/ideas/<slug>/weaknesses.json` |
| `trend-analysis` | Analyze market trends | `memory/market_insights/<niche>-<platform>-<YYYY>-<MM>.md` |
