---
prompt_for: apps
placeholder: "[CATEGORY]"
usage: Replace [CATEGORY] with the target app category (e.g., "nutrition", "fitness", "personal finance") before invoking, bes specific.
---

**Objective:**
Identify and analyze **current trends in the [CATEGORY] app category** (covering both **mobile apps and web apps**) using **credible, recent sources (published within the last 6 months)**.

---

**Instructions:**

1. **Source Criteria**

   * Use only **credible and recent sources (≤ 6 months old)**
   * At the beginning of the response, clearly state:
     **"Data observed as of [month/year]"**
   * Prioritize sources in this order:

     **Tier 1 — Direct analytics platform blogs (highest fidelity, actual paid data repackaged for free)**
     * Sensor Tower Blog — mobile app downloads/revenue, category deep dives, market shifts
     * data.ai Blog — downloads, revenue, engagement benchmarks, category reports
     * Appfigures Blog — App Store/Play Store ranking trends, monetization data
     * Similarweb Blog — web traffic trends, audience behavior, category-level web app benchmarks, referral and engagement data

     Also search for **articles and reports that cite Tier 1 sources** — tech press, trade publications, and research reports that quote or reference Sensor Tower, data.ai, Appfigures, or Similarweb data inherit their fidelity and often add interpretive context. Examples: TechCrunch, Business of Apps, Axios, The Verge, Wired, and Statista reports covering app or web market data.

     **Tier 2 — Search & SEO intelligence blogs (web app demand signal)**
     * Ahrefs Blog — organic search demand, keyword trends, content gap analysis; useful for surfacing high-intent web app categories
     * Semrush Blog — search volume trends, competitive landscape, traffic share by category; strong signal for web-first products
     * Exploding Topics — emerging app and web product categories, early-stage trend detection before mainstream coverage

     Also search for **articles citing Ahrefs, Semrush, or Exploding Topics data** — marketing and growth blogs that embed their keyword charts or trend graphs carry the same signal.

     **Tier 3 — AI & emerging tool directories (early discovery signal)**
     * Futurepedia — AI tool directory tracking new entrants, categories, and user adoption signals
     * There's An AI For That — AI app/tool landscape, category clustering, use case mapping; useful for spotting emerging AI-native app niches

     **Tier 4 — Growth & product blogs (analytical interpretation layer)**
     * Lenny's Newsletter — growth loops behind breakout apps, product strategy case studies
     * a16z Blog — consumer behavior shifts, emerging app categories, investment signals
     * First Round Review — product and growth case studies from early-stage winners
     * TechCrunch — app launches, funding rounds, breakout consumer and B2B products, market coverage

     **Tier 5 — Trend aggregation & funding intelligence**
     * CB Insights — AI, health, fintech app trends; funding signals; category reports
     * Morning Brew (Emerging Tech sections) — mainstream-crossing trends, consumer app culture

     **Tier 6 — Mobile growth & ASO blogs (tactical, often reveals micro-trends early)**
     * Phiture Blog — App Store ranking insights, keyword trends, conversion optimization
     * MobileAction Blog — ASO keyword trends, category movement
     * Gummicube Blog — App Store visibility tactics, early keyword signal

     **Tier 7 — Indie hacker / builder ecosystem (earliest signal, often pre-blog)**
     * X (Twitter) — follow builders sharing "we hit 100k users," revenue dashboards, growth experiments
     * Reddit (r/startups, r/androidapps, r/iosapps, r/SideProject, r/webdev) — real user sentiment, breakout app discovery

---

2. **Trend Identification**
   Identify both:

   * **Established trends** (high download/traffic/revenue volume, stable category dominance)
   * **Emerging / rising trends** (rapid growth in downloads, DAU, web traffic, search interest, or funding)

   Where relevant, distinguish whether a trend is **mobile-native**, **web-native**, or **cross-platform**.

---

3. **For EACH trend or app category, provide:**

**A. Basic Information**

* Trend / category name
* Platform focus (mobile / web / cross-platform)
* Type (e.g., new app category, monetization shift, UX pattern, platform behavior, audience segment, feature trend)

**B. Description**

* What kinds of apps or products fall under this trend
* What user problem or desire it addresses
* Why it is gaining traction (cultural, technological, or platform drivers)

**C. Quantitative Metrics**

* Mobile: downloads, DAU/MAU, revenue figures, or category growth rates (preferably from Tier 1 mobile sources)
* Web: monthly visits, traffic growth, engagement benchmarks (preferably from Similarweb or sources citing it)
* Search demand: keyword search volume or trend trajectory (from Ahrefs, Semrush, or Exploding Topics)
* App Store / Play Store ranking movement if available

**D. Growth Analysis**

* For **rising trends only**, include:

  * Growth rate (% increase over time OR absolute increase in downloads/traffic/revenue)
  * Timeframe of growth (e.g., "+85% downloads in 60 days," "+200% organic search volume YoY")
  * Velocity classification (slow / moderate / explosive)

---

4. **Structure the Output**
   Organize findings into clearly separated sections:

* **1. Executive Summary (Key Insights)**
* **2. Established Trends**
* **3. Emerging / Rising Trends**
* **4. Key Categories & Signals by Cluster (group related app types or behaviors)**
* **5. Strategic Insights (Product & Marketing Takeaways)**

---

5. **Additional Analysis (Value Add)**
   Include:

* Pattern recognition (e.g., shift toward specific app types, monetization models, platform preferences, or audience segments within [CATEGORY])
* UX / product formats driving retention and growth (e.g., streaks, AI personalization, social loops, paywall positioning, web-to-app funnels)
* Any **overhyped vs. genuinely growing** tension in trends (what looks big but isn't, what looks niche but is compounding)
* Opportunities for indie developers, product teams, or investors

---

**Goal:**
Deliver a **data-backed, structured analysis** that not only lists trends but explains **why they are growing, what is driving retention and monetization, and how they can be leveraged strategically** — across both mobile and web.

---

6. **Financial Opportunities**
   Identify the **most monetarily interesting, not yet saturated problems or high-intent interests** within the category that users are **already actively paying to solve**. Base conclusions on realistic market data (App Store revenue, web subscription benchmarks, category reports from Sensor Tower / data.ai / Similarweb, search demand from Ahrefs/Semrush, funding rounds, etc.) — avoid speculative or wishful sizing.

   For each opportunity, provide:

   * **Problem / high-intent interest**: What specifically are users paying to solve or satisfy?
   * **Evidence of willingness to pay**: Existing apps or web products, subscription tiers, or in-app purchases with proven revenue
   * **Saturation assessment**: Is the market crowded, or are there underserved segments / entry angles for a new player?
   * **Realistic market size estimate**: Use bottoms-up reasoning where possible (e.g., "X million MAU/monthly visitors in category × Y% convert to paid × $Z/mo = addressable revenue pool of $..."). Cite the data source behind the estimate.
   * **Why now**: What technological shift, platform change, or cultural moment makes this opportunity timely?

   Prioritize opportunities that are:
   * Backed by **existing spending behavior** (not hypothetical demand)
   * **Specific enough** to be actionable (not "the app market is $500B")
   * **Emerging or underserved** — avoid opportunities already dominated by entrenched players with no viable wedge

---

7. **Niche Risks**
   Identify the **most significant risks** that could undermine a new app entering this category, based on signals from app store data, download trends, revenue patterns, and market structure. Base conclusions on data — not assumptions.

   For each risk, provide:

   * **Risk**: Short label (e.g., "Platform policy change", "Market saturation", "Big tech entry")
   * **Signal**: Specific evidence from app store data, analytics sources, or market reports that confirms this risk is real
   * **Severity**: Low / Medium / High
   * **Mitigation angle**: Is there a sub-segment, platform, or positioning approach that reduces exposure to this risk?

   Risk types to consider:
   * **Market saturation** — is the category crowded with near-identical products, making differentiation extremely difficult? Are top charts dominated by entrenched players with large rating moats?
   * **Platform dependency risk** — is the category heavily dependent on App Store or Google Play policy, featuring algorithms, or review guidelines that could change without warning?
   * **Race to zero pricing** — is the category trending toward free (ad-supported or freemium with no paid conversion), compressing monetization for new entrants?
   * **Big tech entry risk** — is Apple, Google, or another platform player already building native features that would replace third-party apps in this category?
   * **Retention / engagement cliff** — does category data show high download volumes but poor retention (suggesting the pain is not deep enough to sustain daily use)?
   * **Regulatory exposure** — are apps in this category facing legal scrutiny, data privacy regulation, or health/financial compliance requirements that raise the barrier to entry?
   * **AI disruption risk** — is AI commoditizing the core feature of apps in this category, making it hard to maintain a defensible product moat?

---

8. **Sources**
   At the end of the document, include a **"Sources" section** listing all URLs referenced during research as markdown hyperlinks:

   ```
   ## Sources
   - [Publication / Page Title](https://url.com)
   - [Publication / Page Title](https://url.com)
   ```

   * Include every source consulted, even if not directly quoted
   * Use the actual page title or publication name as the link label
   * Do not omit sources — completeness is required
