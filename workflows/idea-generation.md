---
name: idea-generation
trigger: "User has no app idea and wants to discover one"
entry_condition: "memory/user_profile.md may not exist"
exit_output: "memory/ideas/<slug>/scores.json"
---

# Workflow: Idea Generation

## Startup Announcement

When this workflow is triggered, **immediately** say this before doing anything else:

> **💡 Starting: Idea Generation**
> I'll help you find an app idea worth building. We'll cover your background, explore trending markets, and surface the best opportunities for you specifically.

Then proceed to step 1.

## Trigger

User expresses one of:
- "I don't have an idea yet"
- "Help me find an app idea"
- "What should I build?"
- No prior context in memory

## Entry Conditions

- **Always start with step 1** (user-background-interviewer). It is the mandatory entry point for every idea-generation run.
- If `memory/user_profile.md` already exists, the skill will detect it and offer to reuse the existing profile (see step 1 condition below).
- The user always has the option to re-interview, browse topics, use the fast path, or skip.

## Skill Chain

```
1. user-background-interviewer
   ↓ writes: memory/user_profile.md
   ↓ condition: ALWAYS runs as the first step, even if user_profile.md exists.
   |   If user_profile.md exists → the skill presents the existing profile summary and asks:
   |     "Use existing profile" → keep current profile, proceed to step 2 (or step 3 if browse/skipped mode).
   |     "Update" → run full or fast interview to refresh the profile.
   |     "Browse topics" → run browse path to add/replace selected_interest_domains.
   |   If user_profile.md does not exist → the skill shows the standard opening message with all options.
   |   Routes:
   |     Full interview (interview_mode: "full") → proceeds to step 2.
   |     Fast path (interview_mode: "fast") → proceeds to step 2.
   |     Browse topics (interview_mode: "browse") → proceeds to step 3.
   |     Skip (interview_mode: "skipped") → proceeds to step 3.
   |     Use existing profile → proceeds to step 2 (or step 3 if prior mode was browse/skipped).
   → present: Confirm the key background captured — strong domains, distribution advantages, inner circle domains, and constraints. If browsed, confirm selected domains. If skipped, note that recommendations will be generic. Full profile at memory/user_profile.md

2. user-segmentation-profiler
   ↓ condition: Skip this step if interview_mode = "skipped" or "browse" (not enough data to segment). Default to icp_tier = "beginner" and proceed.
   ↓ writes: memory/user_profile.md (adds icp_tier, constraints)
   → present: State the ICP tier assigned (beginner/builder/growth) and top strategy recommendations. Full profile at memory/user_profile.md

3. trend-analysis
   ↓ reads: memory/user_profile.md (to infer niche candidates)
   ↓ reads: memory/market_insights/ (check for existing trend data)
   ↓ condition: If interview_mode = "browse", use selected_interest_domains directly as niche candidates (no need to infer or ask).
   |   Otherwise, infer niche from user_profile.md or existing market_insights/ files; ask user to confirm or describe their own.
   |   Ask which platforms to include; if a relevant file already exists for the niche, present it and ask whether to skip or refresh; if missing, run trend-analysis.
   ↓ writes: memory/market_insights/<niche>-<platform>-<YYYY>-<MM>.md (one file per platform; skip if up-to-date file exists)
   → present: Share top 3 trend signals per platform, trend velocity, and overall verdict (hot/warm/cool/cold). Full analysis at memory/market_insights/<niche>-<platform>-<YYYY>-<MM>.md

4. trend-to-product-mapper
   ↓ reads: memory/user_profile.md (domain fit filter)
   ↓ reads: memory/market_insights/<niche>-*-<YYYY>-<MM>.md (from step 3)
   ↓ writes: memory/ideas/<idea-slug-1>/idea.md ... memory/ideas/<idea-slug-N>/idea.md (7–10 files)
   → present: Show the summary table of all mapped idea candidates (slug, app concept, confidence, cross-platform resonance, monetization status). Full idea files at memory/ideas/<slug>/idea.md

5. idea-scoring
   ↓ reads: available dimension files per candidate
   ↓ writes: memory/ideas/<slug>/scores.json (quick score for each candidate)
   → present: Show all candidates ranked by final score with verdict labels. Highlight the top recommendation with rationale. Full scores at memory/ideas/<slug>/scores.json
```

## State Flow

| Step | Reads | Writes |
|---|---|---|
| user-background-interviewer | (conversation) | `memory/user_profile.md` |
| user-segmentation-profiler | `memory/user_profile.md` | `memory/user_profile.md` (extended) |
| trend-analysis | `memory/user_profile.md`, `memory/market_insights/` | `memory/market_insights/<niche>-<platform>-<YYYY>-<MM>.md` |
| trend-to-product-mapper | `memory/user_profile.md`, `memory/market_insights/<niche>-*` | `memory/ideas/<slug>/idea.md` (7–10 files) |
| idea-scoring | all available dimension files | `memory/ideas/<slug>/scores.json` |

## Exit Output

The user receives:
- All scored idea candidates ranked by `final_score`
- Top candidate recommended with rationale
- A file link list for all ideas, formatted as:

  ```
  📄 memory/ideas/<slug-1>/idea.md  (score: XX/100)
  📄 memory/ideas/<slug-2>/idea.md  (score: XX/100)
  📄 memory/ideas/<slug-3>/idea.md  (score: XX/100)
  ...
  ```

- Prompt to run `idea-validation` on the chosen idea

## Notes

- When the interview is skipped, the workflow still works — trend-analysis infers niches from the user's message or asks directly, and trend-to-product-mapper generates ideas without domain-fit filtering. Results will be generic but still valuable.
- When the user browses topics, the `selected_interest_domains` become the niche candidates for trend-analysis. This is a better starting point than a full skip — the user has actively chosen what interests them, which provides stronger filtering for idea generation even without a background interview.
- When the interview is skipped or browsed, user-segmentation-profiler is also skipped since there's insufficient data. The system defaults to `icp_tier: "beginner"` which is the most conservative setting (simpler channels recommended, lower budget assumed). The user can correct this later.
- If the user skipped or browsed initially but later wants to personalize, they can say "run the interview" at any time. The system will run user-background-interviewer, update user_profile.md, and re-run downstream skills that depend on it.
