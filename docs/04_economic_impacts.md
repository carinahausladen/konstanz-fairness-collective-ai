---
layout: default
title: "Economic Impacts of AI"
permalink: /economics/
---

# The Economics of AI Fairness

*Who benefits, who loses, and what we are measuring when we say AI is "transforming work."*

Two things are happening at once. On the one hand, AI is a general-purpose technology diffusing unevenly across occupations, skill clusters, countries, and income levels — a pattern that may echo the "great divergence" of earlier GPTs like electrification. On the other, AI production itself depends on a new global labor market: human-grade training data sourced through precarious gig platforms. Most existing readings cover the first story and not the second. This week we do both.

---

## 1. Why might AI produce economic harms? — a conceptual frame

Before measuring AI's effects, it helps to be explicit about what mechanisms could *produce* harm in the first place. Acemoglu's "Harms of AI" (2021) is the standing conceptual reference for this course. His claim: **the harms are not inherent to AI technology — they flow from how AI is developed and deployed**, specifically to empower firms and governments against workers and citizens. Three broad domains:

- **Data and information** — privacy violation, unfair (data-advantaged) competition, behavioral manipulation that exploits biases consumers cannot recognize.
- **Labor market** — excessive automation (firms don't internalize worker externalities), a distorted composition of technology (automation favored over new-task creation), loss of economies of scope in human judgment, and worker monitoring.
- **Communication and democracy** — echo chambers and polarization from AI-curated feeds, Big-Brother surveillance effects, and a political-economic channel: automation weakens workers' bargaining power by making them less indispensable.

A surprising implication: **greater competition can *exacerbate* these harms** rather than resolve them. Regulation and research redirection are part of the picture. Acemoglu's framework is the scaffolding under the empirical readings that follow — Teutloff documents displacement, Massenkoff documents who's exposed, Ranjit documents meaning loss, Agarwal documents upstream exploitation. Acemoglu names the *mechanisms* that connect them.

## 2. How do we *measure* AI's economic impact?

The field has iterated quickly through three measurement families in about two years:

- **Pure capability / feasibility** — "what *could* an LLM do" (Eloundou et al. 2023, GPTs are GPTs). Strong upper bound, weak prediction of what actually happens.
- **Provider telemetry** — what people *actually do* with the model, from anonymized conversation logs (Anthropic Economic Index v3, v4, India Brief). Large, real, recent — but one provider and skewed toward early adopters.
- **Capability × observed usage** — Massenkoff & McCrory's *observed exposure* combines the two: weight Eloundou-style feasibility by how much of each task is actually automated, then aggregate to occupations. Sharpens the measure considerably — in practice 68% of usage concentrates on β=1 (fully feasible) tasks, only 3% on β=0 tasks.

A fourth family appears in the behavioral-economics/HCI literature: **worker surveys on meaning, agency, and preferences** (Ranjit et al.) — capturing what telemetry cannot.

## 3. Unequal distribution of benefits

- **Anthropic Economic Index v4 (Primitives)** — top 10 tasks account for 24% of Claude.ai use; augmentation patterns now >50% of Claude.ai conversations; *directive* automation grew from 27% → 39% in 8 months.
- Claude's task portfolio skews toward *higher-skill, higher-education* work than the broader economy. Occupation-level effects are mixed: property managers would upskill (routine bookkeeping gives way to negotiations); travel agents would deskill (complex planning gives way to ticket purchasing).
- Success falls with complexity — Claude's success rate drops on longer-horizon tasks, echoing METR-style evaluations.

## 4. Labor market effects

- **Teutloff et al. 2025** — cleanest causal-style evidence to date. BERTopic clustering of a major freelance platform into 116 skill clusters, DiD around the ChatGPT launch.
  - **Substitutable skills fall 20–50%**; writing (–52%) and translation (–59%) worst hit.
  - **Complementary skills +7% on average, but highly heterogeneous**: ML programming +24%, AI chatbot development nearly tripled (+179%).
  - Sharpest decline for short-term (1–3 week) jobs.
  - **Novice workers lose out.** The "LLMs help novices" finding from lab studies (Brynjolfsson & McAfee, Noy & Zhang) does *not* generalize to freelance markets.
- **Massenkoff & McCrory 2026** — observed-exposure measure applied to US occupations.
  - Higher-exposure occupations projected to **grow less** through 2034 (BLS).
  - Most-exposed workers are **older, more female, more educated, higher-paid** — flips the classic "low-skill automation" framing.
  - **No systematic unemployment increase** yet, but suggestive evidence that **hiring of younger workers has slowed** in exposed occupations. Both authors converge on the same demographic signal from different methods.

## 5. Meaning of work, not only wages

- **Ranjit et al. 2026 (CHI)** — worker-centered design study. 171 tasks × 202 workers × 197 developers, five dimensions of meaningful work (perceived bullsh*t, perceived value, well-being, status maintenance, human flourishing).
  - **AI exposure is negatively correlated with meaningfulness.** Tasks AI can do well tend to be emotionally thin, transactional, lacking in-person interaction.
  - **Developer–worker gap.** Builders prefer polite, strict, imaginative AI systems; workers prefer straightforward, tolerant, practical ones. A concrete, measured value mismatch between who designs AI and who lives with it.
- Brings a variable into the economic conversation that pure wage/employment studies do not capture: displacement of the *valued* parts of a job can happen without displacement of the job itself.

## 6. Global inequality and divergence

- **Anthropic Economic Index v3 (Geography)** — introduces the **Anthropic AI Usage Index (AUI)** = country share of Claude use / share of world working-age population.
  - **AUI correlates strongly with GDP per capita** (1% higher GDP/capita ≈ 0.7% higher AUI). Small tech-advanced countries (Israel, Singapore) lead.
  - Raises the **great divergence** concern: previous GPTs (electrification, combustion) both drove aggregate growth *and* widened international income gaps. AI may do the same.
  - **Lower-income countries automate more; higher-income countries augment more.**
- **Anthropic 2026 India Brief** — zooms in: India is #2 by absolute Claude use (5.8%) but **101st of 116 per capita**. Four states (Maharashtra, Tamil Nadu, Karnataka, Delhi) account for >50% of Indian use, mirroring the country's IT-sector geography. "Second-largest AI user" is compatible with very narrow adoption.
- **Anthropic 2026 Economic Index v4** — within the US, state-level use is *converging* and would equalize in 2–5 years if trend holds. International divergence persists.

## 7. The upstream labor market — who produces the training data?

- **Agarwal 2026 (The Guardian)** — long-form reporting on global gig AI-training marketplaces (Kled AI, Silencio, Neon Mobile, Luel AI, ElevenLabs).
  - Workers upload video, audio, private phone calls, and biometric data for a few dollars per session; irrevocable, worldwide, royalty-free licenses — often with rights to create "derivative works" forever.
  - **Data drought** as a driver: C4, RefinedWeb, Dolma restricting scraping; high-quality text projected to run out around 2026; synthetic data causes model collapse → demand for "human-grade" data surges.
  - Structural critique (Mark Graham, Oxford): "precarious, non-progressive, effectively a dead end." A race to the bottom on wages; concentrated in the Global South.
- Essential counterweight to the telemetry readings: the "AI economic impact" story usually stops at *users* of AI. This reading is about the *suppliers of the training data* — a new, global, precarious labor market on which the entire Anthropic-Economic-Index corpus implicitly depends.

## 8. Cross-cutting themes
- **Winners and losers are visible at the skill-cluster level, not the occupation level** (Teutloff). Aggregating to "writers" or "software engineers" hides the action.
- **Demographic signal is consistent across methods:** exposed workers are older/educated/higher-paid (Massenkoff); novice entry declines (Teutloff + Massenkoff hiring slowdown).
- **Exposure measurement is maturing:** feasibility → telemetry → capability×usage → worker preferences.
- **What "AI's economic impact" excludes by default:** meaning-of-work (Ranjit) and upstream labor (Agarwal). Both belong in the conversation.
- **Theory–measurement–narrative stack:** Acemoglu names the *mechanisms* of harm → Teutloff/Massenkoff/Anthropic Index *measure* current effects → Angelo/Fortune translates the measurements into public *narrative* ("Great Recession for white-collar workers"). Useful to track how each layer transforms the prior — sometimes faithfully, sometimes not.

---

## 📖 Readings for Presentations

### Conceptual framework
- [Harms of AI (2021)](https://economics.mit.edu/sites/default/files/publications/Harms%20of%20AI.pdf) — Daron Acemoglu, MIT.
  *Prepared for the Oxford Handbook of AI Governance. Names the mechanisms: data/information harms, four labor-market channels (excessive automation, distorted tech composition, loss of economies of scope in human judgment, worker monitoring), and communication/democracy harms. Argues competition alone won't fix these — regulation is needed.*

### Labor-market effects — causal and descriptive
- [Winners and Losers of Generative AI: Early Evidence of Shifts in Freelancer Demand (2025)](https://doi.org/10.1016/j.jebo.2024.106845) — Teutloff, Einsiedler, Kässi, Braesemann, Mishkin & del Rio-Chanona, *Journal of Economic Behavior and Organization* 235.
  *Difference-in-differences on 116 freelance skill clusters around ChatGPT launch. Substitutable skills –20–50%, AI chatbot dev +179%. Cleanest early causal evidence.*
- [Labor Market Impacts of AI: A New Measure and Early Evidence (2026)](https://www.anthropic.com/research/labor-market-impacts) — Massenkoff & McCrory (Anthropic).
  *Introduces observed exposure = capability × actual automated usage. Most-exposed workers are older, more female, more educated, higher-paid; hiring of younger workers slowing in exposed occupations.*

### Telemetry snapshots of AI use
- [The Anthropic Economic Index Report: Economic Primitives (2026)](https://www.anthropic.com/research/economic-index-economic-primitives) — Appel, Massenkoff, McCrory et al.
  *Most comprehensive report. Five new primitives (skills, task complexity, autonomy, success, purpose) on ~1M November-2025 Claude conversations. Re-examines job exposure weighted by success rate.*
- [Anthropic Economic Index: Tracking AI's Role in the US and Global Economy (2025)](https://www.anthropic.com/research/economic-index-geography) — Anthropic, Sept 2025.
  *Introduces the Anthropic AI Usage Index (AUI); documents strong GDP–adoption correlation and the "great divergence" framing for AI.*
- [India Country Brief: The Anthropic Economic Index (2026)](https://www.anthropic.com/research/india-brief-economic-index) — Anthropic, Feb 2026.
  *India is #2 by absolute use but 101st per capita; four states account for >50% of Indian use. Concrete illustration of narrow, IT-sector-concentrated adoption.*

### Meaning of work
- [Are We Automating the Joy Out of Work? Designing AI to Augment Work, Not Meaning (2026)](https://doi.org/10.1145/3772318.3791845) — Ranjit, Zhou, Swayamdipta & Quercia, *CHI 2026*.
  *171 tasks, 202 workers, 197 developers. AI exposure negatively correlated with meaningful-work dimensions. Developer-worker design gap documented and measured.*

### Upstream labor — who produces the training data
- [Thousands of People Are Selling Their Identities to Train AI — But at What Cost? (2026)](https://www.theguardian.com/technology/2026/mar/21/ai-trainers-identity-cost) — Shubham Agarwal, *The Guardian*.
  *Long-form journalism on global gig AI-training platforms. Irrevocable royalty-free licenses, race to the bottom, biometric-data downstream risks. Counterweight to telemetry-heavy economic readings.*

### Narrative and reception
- [Anthropic Just Mapped Out Which Jobs AI Could Potentially Replace (2026)](https://fortune.com/2026/03/06/ai-job-losses-report-anthropic-research-great-recession-for-white-collar-workers/) — Jake Angelo, *Fortune*.
  *Business-press explainer of Massenkoff & McCrory. Surfaces the headline capability-vs-observed gaps (Computer & Math 96%/32%, Office & Admin 94%/42%) and the "Great Recession for white-collar workers" framing. Useful for seeing how a neutral measurement becomes a policy/public narrative.*

### Optional / further viewing
- [Productivity Gains and Labor Pains: What Will AI Do to Jobs? — Hoover Institution panel](https://www.hoover.org/events/productivity-gains-and-labor-pains-what-will-ai-do-jobs)
- [Mapped: Which Countries Use Claude AI the Most (Visual Capitalist)](https://www.visualcapitalist.com/mapped-which-countries-use-claude-ai-the-most/)

---

## 📊 Project Ideas & Datasets

### 1. Who captures the complementarity premium?
Teutloff shows aggregate +7% for complementary skills but +179% for AI chatbot development. At the freelancer level, are these gains concentrated in a small number of high-earning specialists, or broadly distributed? Combine the Teutloff skill-cluster classification with earnings data from a freelance platform to test whether the complementary-skills premium is *inclusive growth* or a new winner-take-most market.

### 2. Meaningful-work audit of a deployed AI tool
Take one organization's deployed AI workflow (customer support, legal drafting, HR screening). Apply Ranjit's five-dimension meaningful-work framework before/after deployment. Triangulate worker survey responses against task-level telemetry. Does AI deployment disproportionately automate the *valued* parts of the job?

### 3. Divergence accounting for AI
Build a small replication of the Anthropic AUI using an alternative data source (OpenRouter, open-weights provider logs, or Stack Overflow developer survey). Does the GDP–adoption correlation hold with non-Anthropic data? Decompose: how much of international divergence is driven by (a) internet/infrastructure, (b) language coverage, (c) sectoral composition?

### 4. Gig AI-trainer labor conditions — structured evidence
Agarwal's Guardian piece is journalism. A useful follow-up is a structured survey or scrape of 5–10 gig AI-training marketplaces: posted rates, license terms (transferability, perpetuity, derivative rights), geographic distribution of workers. Compare to conventional crowdwork platforms (MTurk, Prolific) on the same dimensions. Produce a transparency index.
