---
prompt_for: web-search
placeholder: "[NICHE]"
usage: Replace [NICHE] with the target topic (e.g., "nutrition", "fitness", "personal finance") before invoking.
---

**Objective:**
Identify and analyze **current web search trends in the [NICHE] niche** using **credible, recent sources (published within the last 6 months)**.

---

**Instructions:**

1. **Source Criteria**

   * Use only **credible and recent sources (≤ 6 months old)**
   * At the beginning of the response, clearly state:
     **"Data observed as of [month/year]"**
   * Prioritize sources in this order:

     **Tier 1 — Search trend aggregators & daily coverage (cite SEO tool data + Google Trends)**
     * Search Engine Journal — daily coverage of search trends, keyword shifts, traffic changes; frequently cites Ahrefs, Semrush, Google Trends, and industry datasets
     * Search Engine Land — authoritative reporting on search behavior shifts, algorithm updates, and emerging query patterns
     * Search Engine Watch — trend analysis across organic and paid search; aggregates data from major SEO platforms

     Also search for **articles citing these sources** — when a marketing blog, trade press piece, or research report quotes Search Engine Journal, Search Engine Land, or Search Engine Watch data, it inherits the signal and often adds vertical-specific context.

     **Tier 2 — SEO authority blogs (original data analysis, closest to raw Ahrefs/Semrush exports)**
     * Ahrefs Blog — keyword demand studies, search volume trend analyses, click-through rate research, ranking factor breakdowns; based on Ahrefs' own index of billions of keywords
     * Semrush Blog — search demand trends, competitive traffic share, category-level keyword opportunity analyses; based on Semrush's proprietary dataset
     * Moz Blog — ranking factor studies, SERP feature trend analysis, domain authority benchmarks
     * Backlinko — large-scale keyword and ranking studies (e.g., "we analyzed X million search results"); turns Ahrefs/Semrush exports into insight narratives

     Also search for **articles citing Ahrefs, Semrush, or Moz data** — growth blogs, agency case studies, and niche SEO blogs that embed keyword charts or traffic breakdowns carry the same underlying signal.

     **Tier 3 — Trend aggregation & early signal platforms (data + narrative combined)**
     * Exploding Topics — surfaces search queries and topic categories growing faster than mainstream tools detect; combines Google Trends signals with proprietary scoring
     * CB Insights — market-level search demand signals in tech, health, fintech, and B2B; combines search data with funding and product signals

     **Tier 4 — Technical SEO & growth blogs (underrated, often very data-heavy)**
     * Content Marketing Institute — keyword opportunity analyses, content gap studies, traffic growth case studies; often based on Ahrefs/Semrush exports from real client data
     * Niche agency and growth blogs — look for posts that publish actual keyword lists, traffic breakdowns, or Ahrefs/Semrush screenshots from client campaigns; these often surface micro-trends before they reach mainstream SEO blogs

     **Tier 5 — Strategic synthesis layer (turns search insights into market direction)**
     * a16z Blog — interprets search and consumer behavior signals into broader market narratives and investment theses
     * CB Insights (also Tier 3) — synthesizes search demand data with funding trends to identify where markets are heading

---

2. **Trend Identification**
   Identify both:

   * **Established trends** (high stable search volume, dominant keyword clusters, entrenched SERP categories)
   * **Emerging / rising trends** (rapid growth in search volume, new query patterns, rising keyword clusters not yet served by established content)

---

3. **For EACH trend or keyword cluster, provide:**

**A. Basic Information**

* Trend / keyword cluster name
* Category (e.g., informational query, commercial intent, navigational shift, question-based, comparison-seeking, symptom/problem-driven, etc.)

**B. Description**

* What search queries and topics fall under this trend
* What user problem, desire, or intent is driving the searches
* Why it is gaining search volume (cultural shift, news event, product launch, algorithm change, seasonal pattern, etc.)

**C. Quantitative Metrics**

* Monthly search volume for core keywords (from Ahrefs, Semrush, or sources citing them)
* Search volume trend direction (stable / growing / declining)
* Keyword difficulty or competition level if available
* SERP feature presence (featured snippets, People Also Ask, shopping results, etc.) if relevant

**D. Growth Analysis**

* For **rising trends only**, include:

  * Growth rate (% increase in search volume over time OR absolute volume increase)
  * Timeframe (e.g., "+180% search volume over 12 months")
  * Velocity classification (slow / moderate / explosive)

---

4. **Structure the Output**
   Organize findings into clearly separated sections:

* **1. Executive Summary (Key Insights)**
* **2. Established Trends**
* **3. Emerging / Rising Trends**
* **4. Key Keyword Clusters (group related queries and intent types)**
* **5. Strategic Insights (Content, SEO & Marketing Takeaways)**

---

5. **Additional Analysis (Value Add)**
   Include:

* Pattern recognition (e.g., shift from informational to commercial intent, rise of question-based queries, emerging sub-topics or audience segments within [NICHE])
* SERP formats and content types driving visibility (e.g., long-form guides, comparison pages, video results, tools/calculators, Reddit/forum results surfacing in Google)
* Any **overhyped vs. genuinely growing** tension in trends (high-volume keywords with declining intent vs. low-volume keywords with explosive trajectory)
* Opportunities for content creators, SEO strategists, or product teams to capture underserved search demand

---

**Goal:**
Deliver a **data-backed, structured analysis** that not only lists search trends but explains **why they are growing, what intent sits behind them, and how they can be leveraged strategically** for content, product, and marketing.

---

6. **Financial Opportunities**
   Identify the **most monetarily interesting, not yet saturated search intent clusters** within the niche where people are **already searching with commercial or transactional intent** and spending money. Base conclusions on realistic data (search volume, keyword difficulty, CPC as proxy for advertiser willingness to pay, affiliate revenue, industry reports) — avoid speculative or wishful sizing.

   For each opportunity, provide:

   * **Search intent / high-commercial keyword cluster**: What specific queries indicate readiness to pay?
   * **Evidence of commercial value**: CPC data (high CPC = advertisers compete = money flows through this query), affiliate programs, products/services appearing in SERP ads, or existing content monetizing this traffic
   * **Saturation assessment**: How competitive is the SERP? Are there underserved angles, formats, or audience segments a new entrant could own?
   * **Realistic market size estimate**: Use bottoms-up reasoning where possible (e.g., "X,000 monthly searches × Y% click-through × Z% convert × $W average order = addressable revenue signal of $..."). Cite the data source.
   * **Why now**: What makes this keyword cluster timely — rising search volume, declining competition, new product category, regulatory change, or cultural shift?

   Prioritize opportunities that are:
   * Anchored in **commercial or transactional intent** (not purely informational)
   * **Specific enough** to be actionable (not "SEO is a $80B market")
   * **Emerging or underserved** — avoid keyword clusters already dominated by entrenched players with high-authority pages and no viable wedge

---

7. **Niche Risks**
   Identify the **most significant risks** that could undermine a product or business targeting this niche's search demand, based on signals from keyword data, SERP structure, and market trends. Base conclusions on data — not assumptions.

   For each risk, provide:

   * **Risk**: Short label (e.g., "AI Overviews killing organic traffic", "SERP dominated by incumbents", "Declining search intent")
   * **Signal**: Specific evidence from search data or SERP analysis that confirms this risk is real
   * **Severity**: Low / Medium / High
   * **Mitigation angle**: Is there a keyword cluster, content format, or distribution strategy that reduces exposure to this risk?

   Risk types to consider:
   * **AI search cannibalization** — are core keywords in this niche already being answered by Google AI Overviews, Perplexity, or ChatGPT in ways that eliminate the need to click through to an app or product? Look for zero-click SERP features dominating high-intent queries
   * **Incumbent moat** — are the top-ranking pages for primary keywords held by high-authority domains (WebMD, NerdWallet, Wikipedia, major brands) with no viable wedge for a new entrant? Check keyword difficulty and domain authority concentration
   * **Declining search intent** — is search volume trending down for core queries? Is demand migrating to other platforms (TikTok, Reddit, YouTube) where Google SEO provides no leverage?
   * **Query intent mismatch** — is the dominant search intent informational (people researching) rather than commercial or transactional (people ready to pay)? High volume with low CPC is a warning sign
   * **Regulatory or content policy risk** — are keywords in this niche subject to Google's sensitive topic classifications (health, finance, legal, supplements) that restrict advertising or suppress rankings without established authority?
   * **Seasonal demand cliff** — is the search volume driven by predictable seasonal spikes (New Year resolutions, tax season, back to school) that create boom-bust traffic patterns for products in this space?

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
