---
name: user-background-interviewer
description: Conducts a deep background interview to understand what types of app ideas this specific user is most likely to succeed with based on their domain knowledge, networks, and skills.
---

<!-- version: 0.2.0 | outputs: memory/user_profile.md -->

# Skill: user-background-interviewer

## Purpose

Understand what types of ideas this specific user is most likely to succeed with. Surface hidden advantages, domain expertise, and natural distribution channels the user may not have considered.

## Input

- Fresh conversation (no prior context needed)
- Optional: existing `memory/user_profile.md` to extend

## Process

### Step 0 — Check for Existing Profile

Before showing the opening message, check if `memory/user_profile.md` already exists.

**If a profile exists**, present a summary and ask:

> I already have a profile on file for you:
>
> - **Domains:** <list strong_domains or selected_interest_domains>
> - **Technical level:** <technical_level, if present>
> - **Tier:** <icp_tier, if present>
> - **Mode last time:** <interview_mode>
>
> Would you like to:
> - **"Use it"** — Keep this profile and move on to idea generation.
> - **"Update"** — Run the interview again (full or short version) to refresh your profile.
> - **"Browse topics"** — Pick new topics to explore, keeping the rest of your profile.

**Routing (existing profile):**
- User says "use it", "keep it", "yes", "that's fine" or similar → keep the existing profile, proceed to the next skill in the workflow. Do not overwrite `user_profile.md`.
- User says "update" → proceed to the **Opening Message** below (full interview options).
- User says "browse topics" → go to **Browse Path** below. Merge `selected_interest_domains` into the existing profile (preserve other fields).

**If no profile exists**, proceed directly to the Opening Message.

### Opening Message

Before asking the first question, say exactly this:

> I'm going to ask you **10 questions** to understand your background, skills, and interests. This helps me find app ideas that genuinely fit you — not generic ideas, but ones where you have a real edge.
>
> Answer as freely as you'd like. There are no right or wrong answers.
>
> **Not sure where to start, or prefer not to answer questions?** No problem — pick one:
>
> - **"Browse topics"** — I'll show you real product domains people pay for. Pick 2–3 that interest you, and I'll generate ideas around those.
> - **"Short version"** — Just 4 quick questions instead of 10.
> - **"Skip"** — Jump straight to idea generation with generic recommendations.

**Routing:**
- User says "browse", "show me topics", "browse topics", "I have no idea", or similar → go to **Browse Path** below.
- User says "skip" → go to **Skip Path** below.
- User says "short version", "fast", "quick" or similar → go to **Fast Path** below.
- Otherwise → proceed with the **full interview**.

### Skip Path

If the user wants to skip entirely, still ask the mandatory technical ability question:

> No problem — I'll skip the interview. Just one quick question I need to generate relevant ideas:
>
> **What's your technical ability?** (no-code / beginner / intermediate / expert)

If the user refuses to answer even this, default to "beginner" and note it.

Then write a minimal profile:

```json
{
  "strong_domains": ["unknown"],
  "hidden_opportunities": [],
  "natural_problem_spaces": [],
  "distribution_advantages": [],
  "inner_circle_domains": [],
  "technical_level": "no-code | beginner | intermediate | expert",
  "fit_score_by_niche": {},
  "interview_summary": "User skipped the background interview. Technical level: <level>. Profile is generic — recommendations will not be personalized to domain fit or distribution advantages.",
  "interview_mode": "skipped",
  "all_questions_and_answers": []
}
```

Then proceed to the next skill in the workflow. Downstream skills will use default/neutral values when profile data is missing.

### Browse Path (Topic Picker)

When the user has no idea what they want to build or prefers not to answer personal questions, present product domains they can browse and pick from. These domains are organized around core human desires (from `memory/extra-context/core-human-desires.md`) but presented as concrete, relatable product categories — not psychology theory.

#### How it works

1. Show **Batch 1** (5 domains). Each domain has a plain-language name, a one-line "why people pay for this", and 3 concrete product examples.
2. After each batch, show a clear action prompt (see "After each batch" below).
3. The user picks domains by number or name. Selections accumulate across batches.
4. After each batch, the user either:
   - Says **"more"** (or similar) → show the next batch
   - Says **"continue"** / **"let's go"** / **"generate"** (or similar) → proceed with selected domains
5. Show up to 4 batches (20 domains total). If they haven't picked after all batches, ask: "None of these? Tell me in your own words what kind of problems or people interest you."
6. Once the user says "continue" with 2–3 domains selected, ask one quick follow-up: "Last question — what's your technical level? (no-code / beginner / intermediate / expert)"
7. Write the profile and proceed.

#### After each batch

After presenting each batch and receiving the user's response, show this status prompt:

> **Your picks so far:** <list selected domains, or "none yet">
>
> Pick **2–3 domains** total. Then:
> - Say **"more"** to see the next batch of topics
> - Say **"continue"** to start generating ideas with your selected topics

If the user already has 2–3 selections and says "more", show the next batch but remind them: "You've already picked <N> — feel free to swap any out, or say **continue** whenever you're ready."

If the user says "continue" with **fewer than 2** selections, prompt: "Pick at least one more — it helps me generate better ideas. Or say **more** to see another batch."

If the user says "continue" with **more than 3** selections, accept it but note: "That's a lot of ground to cover — I'll focus on the top 3 that produce the strongest signals."

#### Batch 1 — Health, Money & Daily Life

Present exactly this:

> Here are some real product spaces where people actually spend money. Look through them and **pick 2–3 that interest you** — you can select from this batch or say **"more"** to see another batch. When you're happy with your picks, say **"continue"**.
>
> **1. Health & Body** — People pay to feel healthier, track symptoms, and manage conditions.
> *Examples: calorie trackers, sleep monitors, symptom journals, medication reminders*
>
> **2. Personal Finance** — People pay to feel in control of their money and build wealth.
> *Examples: budget planners, expense trackers, investment portfolio dashboards, savings challenges*
>
> **3. Fitness & Movement** — People pay to get stronger, look better, and stay consistent.
> *Examples: workout trackers, running coaches, home exercise programs, gym log apps*
>
> **4. Food & Nutrition** — People pay to eat better without the mental load of planning.
> *Examples: meal planners, recipe organizers, grocery list builders, macro trackers*
>
> **5. Productivity & Focus** — People pay to get more done, reduce overwhelm, and feel organized.
> *Examples: task managers, time blockers, habit trackers, Pomodoro timers*

#### Batch 2 — Relationships, Status & Identity

> **6. Dating & Relationships** — People pay to find connection, improve relationships, and feel less alone.
> *Examples: dating profile coaches, couples check-in apps, communication skill builders*
>
> **7. Parenting & Family** — People pay to be better parents and manage family chaos.
> *Examples: baby trackers, chore schedulers, co-parenting coordinators, milestone journals*
>
> **8. Career & Professional Growth** — People pay to advance, earn more, and signal competence.
> *Examples: resume builders, interview prep tools, salary negotiation guides, skill trackers*
>
> **9. Social & Community** — People pay to belong, share interests, and not feel isolated.
> *Examples: local event finders, hobby matchmakers, accountability partner apps, group challenge platforms*
>
> **10. Personal Style & Image** — People pay to look good and express who they are.
> *Examples: outfit planners, wardrobe organizers, skincare routine trackers, haircut reference savers*

#### Batch 3 — Mind, Learning & Creativity

> **11. Mental Health & Stress** — People pay to feel calmer, manage anxiety, and process emotions.
> *Examples: mood trackers, guided journals, breathing exercises, therapy session notes*
>
> **12. Learning & Education** — People pay to acquire new skills and feel like they're growing.
> *Examples: language learning apps, flashcard systems, course trackers, reading habit builders*
>
> **13. Creative Tools** — People pay to make things — art, music, writing, video — and share them.
> *Examples: photo editors, beat makers, writing prompt generators, video thumbnail creators*
>
> **14. Journaling & Reflection** — People pay for structured self-awareness and personal narrative.
> *Examples: gratitude journals, daily reflection prompts, year-in-review generators, life timeline apps*
>
> **15. Hobbies & Collections** — People pay to organize, track, and deepen their hobbies.
> *Examples: plant care trackers, board game loggers, book lists, travel planners, wine journals*

#### Batch 4 — Home, Pets & Niche Needs

> **16. Home & Living** — People pay to manage their space, reduce maintenance stress, and improve their environment.
> *Examples: home maintenance schedulers, cleaning routines, moving checklists, interior design planners*
>
> **17. Pets & Animals** — People pay to take better care of their pets (and share cute photos).
> *Examples: pet health trackers, feeding schedulers, vet visit logs, pet photo journals*
>
> **18. Sustainability & Ethics** — People pay to live according to their values and reduce guilt.
> *Examples: carbon footprint trackers, ethical brand finders, waste reduction challenges, local farm finders*
>
> **19. Side Hustles & Freelancing** — People pay for tools that help them make more money independently.
> *Examples: invoice generators, client trackers, income dashboards, gig expense loggers*
>
> **20. Spirituality & Mindfulness** — People pay to find meaning, build rituals, and feel grounded.
> *Examples: meditation timers, prayer trackers, astrology journals, daily intention setters*

#### After selection — Mandatory technical ability question

Once the user picks 2–3 domains and says "continue" (or similar), you **must** ask this follow-up before proceeding. Do not skip it — technical level determines what kinds of ideas are feasible for this user:

> Great choices. Before I generate ideas, I need to know one thing:
>
> **What's your technical ability?**
> - **No-code** — I use tools like Bubble, Glide, or Zapier but don't write code
> - **Beginner** — I can follow tutorials and modify existing code
> - **Intermediate** — I can build a simple app from scratch on my own
> - **Expert** — I can build and ship production apps, including backend/infra

Wait for their answer. If they don't pick one of the four levels, map their response to the closest option (e.g., "I know some Python" → beginner or intermediate based on context). Then write the profile:

```json
{
  "strong_domains": ["unknown"],
  "hidden_opportunities": [],
  "natural_problem_spaces": [],
  "distribution_advantages": [],
  "inner_circle_domains": [],
  "inner_circle_testers_available": false,
  "fit_score_by_niche": {},
  "selected_interest_domains": ["<domain-1>", "<domain-2>", "<domain-3>"],
  "technical_level": "no-code | beginner | intermediate | expert",
  "interview_summary": "User browsed topic domains and selected: <domains>. Technical level: <level>. No background interview conducted — recommendations based on interest selection only.",
  "interview_mode": "browse",
  "all_questions_and_answers": []
}
```

The `selected_interest_domains` field is used by the orchestrator to guide `trend-analysis` (which niches to research) and `trend-to-product-mapper` (filter ideas to these domains). This replaces domain-fit scoring — instead of matching ideas to expertise, the system matches ideas to stated interest.

### Fast Path (4 questions)

Ask only these four questions (numbered [1/4] through [4/4]):

1. **[1/4]** — "What's your technical skill level? (no-code / beginner / intermediate / expert) And what domain or industry do you know best?"
2. **[2/4]** — "Do you have any existing audience, community, or content presence online? If yes, what topic and roughly how large?"
3. **[3/4]** — "What do your close friends or family do for work? Would any of them test an app or give you feedback regularly?"
4. **[4/4]** — "What are your constraints? Hours per week, monthly budget, and is this your main focus or a side project?"

Question [1/4] covers the mandatory technical ability question. If the user's answer to [1/4] only addresses domain and skips technical level, follow up: "Got it — and what's your technical level? (no-code / beginner / intermediate / expert)"

Apply the same validation rules as the full interview. Write the output using the same schema, filling in what's available and noting gaps.

### Handling Private or Resistant Users

If at any point the user resists a question or expresses discomfort:

1. Acknowledge it: "No problem — skip any question you're not comfortable with."
2. Do not pressure or re-ask. Mark the question as `"answer": "declined"` in the output.
3. If the user declines 3+ questions, gently suggest the fast path: "Would you prefer the short version instead? Just 4 quick questions."
4. If the user declines all questions, treat as a skip.

---

### Interview Questions

Ask each question one at a time. Show the counter format **[X/10]** at the start of each question. Do not ask the next question until the current answer is validated (see Validation Rules below).

---

**[1/10] — Technical Skills**

> What programming languages, platforms, or technical tools do you use regularly? For each one, tell me roughly how long you've been using it and whether you'd call yourself a beginner, intermediate, or expert.

*Covers: technical skills*

**[2/10] — Industry Experience & Inner Circle**

> What industry or professional domain have you spent the most time in? What do you understand about this space that most outsiders wouldn't?
>
> Also — think about your close friends, family members, or relatives. What do they do for work? Are any of them in industries you find interesting, and would they be willing to give you honest feedback, test an early version of an app, or help you understand their daily problems? (Even one person who'd answer your questions regularly is a massive advantage.)

*Covers: industry experience, domain access through personal network*

**[3/10] — Past Projects**

> Tell me about a project you've built or worked on — personal, professional, or a side project. What was it, what happened to it, and what's the single biggest thing you learned from it?

*Covers: past projects*

**[4/10] — Interests and Hobbies**

> What do you spend time on outside of work? Name 2–3 things you genuinely care about — things you'd seek out without anyone asking you to.

*Covers: interests and hobbies*

**[5/10] — What People Ask You**

> What do friends, colleagues, or people in your life regularly ask you for help with? What topics or problems do people treat you as the go-to person for?

*Covers: what people ask them*

**[6/10] — Communities**

> What online or offline communities are you part of — subreddits, Discord servers, forums, professional groups, local clubs? Which ones do you actively participate in vs. just observe?

*Covers: social patterns (communities)*

**[7/10] — Content You Consume**

> What content do you consume most obsessively — specific YouTube channels, newsletters, podcasts, subreddits, X accounts? What topics do you actively seek out or find yourself going down rabbit holes on?

*Covers: social patterns (content)*

**[8/10] — Core Strengths**

> Which of the following best describes your natural strengths? Pick your top 1–2:
>
> - Engineering / building
> - Design / UX
> - Marketing / growth
> - Sales / persuasion
> - Operations / systems thinking
> - Research / analysis

*Covers: strengths*

**[9/10] — Existing Audience or Content Creation**

> Have you created any content online — videos, articles, social posts, a newsletter — or built any kind of following or community? If yes: what topic, what platform, and roughly how large?

*Covers: content creation and distribution advantages*

**[10/10] — Constraints**

> What are your real constraints for building an app? Give me your best estimate for:
> - Available hours per week
> - Monthly budget for tools, ads, or subscriptions (in USD)
> - Is this a main focus or a side project?
> - How much risk are you comfortable with: low (I need it to work fast), medium, or high (I can experiment for months)?

*Covers: budget, time, risk tolerance*

---

### Validation Rules

After each answer, check before proceeding:

| Situation | Action |
|---|---|
| Answer is a single word or clearly too vague | Ask a targeted follow-up: "Can you be more specific? For example, [give a concrete example relevant to the question]." |
| Answer doesn't address the question | Rephrase gently: "I want to make sure I understand — [restate what you're looking for]." |
| Answer contradicts a previous answer | Flag and clarify: "Earlier you mentioned [X], but this suggests [Y] — which is more accurate?" |
| User says "I don't know" or "not sure" | Prompt with options: "Take your best guess — even a rough answer helps. For instance, [two or three concrete examples]." |
| Answer is clear and specific | Proceed to the next question immediately. |

Do not ask more than one follow-up per question. If the second attempt is still too vague, accept what was given and note the gap in the output.

## Output

Write to `memory/user_profile.md`:

```json
{
  "strong_domains": [],
  "hidden_opportunities": [],
  "natural_problem_spaces": [],
  "distribution_advantages": [],
  "inner_circle_domains": [],
  "inner_circle_testers_available": false,
  "selected_interest_domains": [],
  "technical_level": "",
  "fit_score_by_niche": {},
  "interview_summary": "",
  "interview_mode": "full | fast | browse | skipped",
  "all_questions_and_answers": []
}
```

## Notes

- The `inner_circle_domains` field captures industries accessible through the user's personal network. This is a high-signal input for trend-to-product-mapper — domain access through a friend or relative who'd give honest feedback is nearly as valuable as direct experience.
- When `interview_mode` = "skipped", downstream skills should treat all profile-dependent adjustments as neutral (no domain fit bonus, no distribution advantage, no tier adjustment).
- When `interview_mode` = "browse", the `selected_interest_domains` field drives niche selection in trend-analysis and idea filtering in trend-to-product-mapper. The system trades domain-fit precision for user engagement — a user who actively chose "Personal Finance" and "Side Hustles" is more motivated than one assigned those niches by an algorithm.
- The browse path domains are derived from `memory/extra-context/core-human-desires.md` but reframed as consumer product categories. The underlying desires (survival, status, belonging, etc.) inform why people pay — the domain labels are how users naturally think about what interests them.
