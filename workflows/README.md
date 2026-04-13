# Workflows

Each workflow file is a complete orchestration spec for a user intent. The orchestrator (Claude Code, Codex, or Cursor) reads the spec and executes each skill in sequence, passing state through `memory/`.

Workflows are **not code** — they are specifications. No skill calls another skill directly. The orchestrator reads each skill's output from `memory/` before invoking the next.

---

## Workflow Index

| Workflow | Trigger | Skill Chain | Exit Output |
|---|---|---|---|
| [`idea-generation`](idea-generation.md) | No idea yet | interviewer → segmenter → trend → mapper → scoring | `memory/ideas/<slug>/scores.json` |
| [`idea-validation`](idea-validation.md) | Has a specific idea | trend → competitors → desire → pricing → distribution → retention → CAC → scoring → memo | `memory/ideas/<slug>/decision_memo.md` |
| [`market-deep-dive`](market-deep-dive.md) | Wants market research | trend → competitors → market size → distribution | `memory/market_insights/<niche>-<platform>-<YYYY>-<MM>.md` |
| [`pivot-optimization`](pivot-optimization.md) | Idea scored poorly | re-score → weakness detection → pivot engine → re-score pivot | `memory/ideas/<slug>/pivot_options.json` |

---

## How Workflows Execute

1. **Startup Announcement** — the orchestrator outputs the workflow's `## Startup Announcement` section **in bold** before any skill runs. This tells the user clearly what has started.
2. **Skill invocation** — skills run in the order defined in the `## Skill Chain` section. Each skill has a `↓ reads` (inputs from `memory/`) and `↓ writes` (output to `memory/`), followed by `→ present` (what to surface inline to the user).
3. **Context passing** — the orchestrator reads each skill's output from `memory/` and provides relevant context when invoking the next skill. Skills never call each other.
4. **Exit output** — the workflow ends when the final artifact is written and presented.

---

## Workflow Files

Each workflow spec contains:

| Section | Purpose |
|---|---|
| `## Startup Announcement` | The exact text to output in bold before any action |
| `## Trigger` | Example user phrases that activate this workflow |
| `## Entry Conditions` | What must exist in memory before the workflow starts |
| `## Skill Chain` | Ordered skill invocations with reads, writes, and presentation instructions |
| `## State Flow` | Summary table of memory dependencies across steps |
| `## Exit Output` | The final artifact(s) the user receives |
| `## Notes` | Edge cases, TODOs, and optional paths |

---

## State Directory Convention

All per-idea state is written to `memory/ideas/<idea-slug>/`. Use kebab-case slugs, max 40 characters.

Example: `habit-tracker-for-climbers`

Ideas are never deleted from memory — set `status: dropped` in `idea.md` instead.
