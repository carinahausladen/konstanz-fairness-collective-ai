---
layout: default
title: "Week 6 — Fundamentals"
permalink: /week6-fundamentals/
---

**Paper tags.**

| Tag | Paper |
|---|---|
| 🟦 | **Acemoglu 2021** — *Harms of AI* |
| 🟩 | **Teutloff et al. 2025** — *Winners and Losers of Generative AI* |
| 🟧 | **Massenkoff & McCrory 2026** — *Labor Market Impacts of AI* |
| 🟥 | **Ranjit et al. 2026** — *Automating the Joy Out of Work* |

---

The thread this week: **two centuries of labor economics already contain the vocabulary we need — automation vs task creation, skill-biased technological change, compensating mechanisms, meaningful work.** The Week-6 empirical papers are the latest measurement cycle on an old argument.

---

## 1. Technology and jobs — a 200-year-old argument &nbsp;🟦

The worry that machines destroy work is not new. Every generation has had a version, and labor economics has a developed vocabulary for it.

**Classical sources:**

- **Ricardo (1821)**, *On Machinery* — 3rd edition of the *Principles*. Reverses his earlier optimism: machines *can* permanently reduce worker welfare, not just shift it. First technical statement of what we now call **labour-saving technical change**.
- **Marx (1867)**, *Capital*, Vol. 1. The "organic composition of capital" argument: as machines replace workers, the proportion of living labor falls, and with it the rate of profit — but also wages and employment in the displaced sectors.
- **Keynes (1930)**, *Economic Possibilities for our Grandchildren*. Introduces **technological unemployment**: "unemployment due to our discovery of means of economising the use of labour outrunning the pace at which we can find new uses for labour."
- **Leontief (1952)** — warns that automation may break the old compensating mechanism whereby displaced workers find new sectors.

**The canonical counter-argument.** Technological change is **complementary** on net: new tools require new skills, new tasks, new sectors. Labour economics spent most of the 20th century documenting this balance.

**The recent correction** — **Autor, Levy & Murnane (2003)**: routine tasks are substitutable by computers; non-routine tasks (abstract or manual) are complements. **Skill-biased** and **routine-biased technical change** become the core analytical frames.

**Why Acemoglu matters.** His 2021 piece argues that the complementarity story is *conditionally* true, and that AI is currently being deployed in a direction — *excessive* automation, labor monitoring, data advantage — that biases it toward harm. Institutions, not technology, determine which direction wins. This is a direct descendant of the Ricardian machinery argument, not a novel claim.

---

## 2. Acemoglu's framework — the scaffolding &nbsp;🟦

Before the empirical papers, students need Acemoglu's map.

**Three domains of harm.**

| Domain | Mechanism |
|---|---|
| **Data and information** | Privacy erosion, unfair data-advantaged competition, behavioural manipulation |
| **Labor market** | Excessive automation, distorted tech composition, loss of economies of scope, worker monitoring |
| **Communication and democracy** | Echo chambers, surveillance, weakened worker bargaining power |

**Four labor-market mechanisms.**

1. Excessive automation — firms don't internalise the social cost of displacement.
2. Distorted composition of technology — automation favoured over new-task creation.
3. Loss of economies of scope in human judgement — context-rich work chopped into routinisable pieces.
4. Worker monitoring — automation amplifies surveillance.

**The institutional claim.** More competition alone does not fix this; it can amplify harm. Regulation and **research direction** matter.

---

## 3. Measuring technological change — causal inference in labor economics &nbsp;🟩 🟧

The methodological backbone for Teutloff and Massenkoff. Teach this before the empirical results.

**The identification problem.** You want the effect of *AI adoption* on employment / wages. Firms that adopt are not random; they differ in ways that independently predict labor outcomes.

**Classical solutions:**
- **Difference-in-differences** — pre/post treatment, treated vs control. Canonical use: Card & Krueger (1994) on minimum wages.
- **Shift-share / Bartik instruments** — exploit pre-existing industry composition × national shocks (Bartik 1991; Autor, Dorn & Hanson 2013 — the "China shock" paper).
- **Instrumental variables** — exploit a source of variation plausibly exogenous to labor outcomes.

**Three generations of AI-exposure measurement** the papers represent:

| Generation | What it measures | Example |
|---|---|---|
| **Capability / feasibility** | What an LLM *could* do | Eloundou et al. 2023 "GPTs are GPTs" |
| **Telemetry** | What users actually do with the model | Anthropic Economic Index |
| **Capability × observed usage** | Feasibility weighted by actual use | Massenkoff & McCrory 🟧 |

**The CS extensions.**
- Teutloff runs difference-in-differences on 116 freelance skill clusters around the ChatGPT launch. The clusters come from BERTopic — a topic-modelling approach. The DiD itself is textbook labor economics. 🟩
- Massenkoff introduces **observed exposure** = capability × actual usage share, aggregated to occupations. 68 % of Claude use concentrates on fully-feasible ($\beta=1$) tasks; 3 % on infeasible ones. Pure feasibility over-predicts; observed exposure sharpens. 🟧

---

## 4. Winners, losers, and skill clusters &nbsp;🟩 🟧

**Classical insight.** Labor-market effects are **heterogeneous within occupations**. Aggregating to the 3-digit occupation code hides the action. Autor's task-based framework (Autor, Levy & Murnane 2003; Autor & Dorn 2013) is built precisely on this.

**What the empirical papers add:**

- **Teutloff:** substitutable skills fall 20–50 %; writing −52 %, translation −59 %; AI chatbot development +179 %. The aggregate may net out to zero while the distribution splits into winners and losers.
- **Massenkoff:** exposed workers are **older, more female, more educated, higher-paid** — which *flips* the classical "low-skill automation" framing that has been the dominant narrative since the 1990s.
- **Novice vs experienced.** The lab finding *"LLMs help novices most"* (Brynjolfsson-Li-Raymond 2023 call-centre study, Noy-Zhang 2023 writing task) does *not* generalise to freelance markets, where novices lose out. 🟩

**For the lecture.** The "AI is good/bad for workers" discourse in the press is at the aggregate level. The interesting action is at the level of tasks within occupations, and at the level of demographics within tasks.

---

## 5. The meaning of work — sociology of work &nbsp;🟥

Wage-and-employment studies miss a variable that the sociology of work has always treated as first-class: whether the work is *meaningful*.

**Classical sources:**

- **Marx (1844)** — alienation under capitalist production. Four forms: from product, from process, from species-being, from other workers. Foundational diagnostic.
- **Braverman (1974)**, *Labor and Monopoly Capital*. **Deskilling** — management takes intellectual content out of skilled work; workers become interchangeable. The standard reference for the "degradation of work" thesis.
- **Weber** on bureaucratic rationalisation — the iron cage.
- **Hackman & Oldham (1976)** — **Job Characteristics Model.** Five dimensions: skill variety, task identity, task significance, autonomy, feedback. Still the backbone of organisational psychology.
- **Graeber (2018)**, *Bullshit Jobs*. Contemporary popularisation of the meaninglessness thesis.

**The CS extension** — Ranjit et al. 2026. 171 tasks × 202 workers × 197 developers. Five dimensions of meaningful work:
- perceived *bullshit* (direct Graeber reference)
- perceived value
- well-being
- status maintenance
- human flourishing.

**Headline finding.** AI exposure correlates *negatively* with meaningfulness. Tasks AI does well tend to be the emotionally thin, transactional ones — but also sometimes the meaningful human-interaction ones. There is a **developer–worker design gap**: builders prefer polite, strict, imaginative AI; workers prefer straightforward, tolerant, practical AI. A measured mismatch between who designs and who uses.

**For the lecture.** Displacement of the *valued* parts of a job can happen without displacement of the job itself. This is not captured by employment or wage data.

---

## 6. What standard labor-impact studies miss

- **Upstream labor.** The data-labelling, human-grading workforce (Agarwal 2026, *Guardian* — context only ⚪). A global, precarious labor market on which the Anthropic-Economic-Index baseline implicitly depends.
- **Narrative framing.** The Fortune "Great Recession for white-collar workers" piece (Angelo 2026, context only) turns a neutral measurement into a policy story. The *Economist* "Don't blame AI (yet)" (context only) offers a counter-narrative from the same data. **Framework → measurement → narrative** is a three-step stack worth drawing on the board.

---

## Key vocabulary

| Term | Classical home | Contemporary usage |
|---|---|---|
| **Technological unemployment** | Keynes 1930 | Jobs lost to automation faster than new ones are created |
| **Skill-biased technical change** | Katz-Murphy 1992, ALM 2003 | Automation complements skilled, substitutes unskilled |
| **Routine-biased technical change** | Autor-Dorn 2013 | Automation substitutes *routine* tasks, regardless of skill |
| **Task-based framework** | Autor-Levy-Murnane 2003 | Occupations are bundles of tasks; tasks are the right unit |
| **Difference-in-differences** | Card & Krueger 1994 | Two-period, two-group causal identification |
| **Deskilling** | Braverman 1974 | Management removing intellectual content from work |
| **Alienation** | Marx 1844 | Worker disconnected from product/process/self/others |
| **Job Characteristics Model** | Hackman-Oldham 1976 | Five-factor model of meaningful work |

---

## Conceptual spine for the lecture

1. **The "machines destroy jobs" argument is 200 years old**, and labor economics has an established vocabulary for it (Ricardo → Keynes → ALM 2003).
2. **Acemoglu re-frames the old argument** — AI harms are institutional, not technological.
3. **Measuring AI's impact has moved from capability to telemetry to capability × usage** — each generation sharpens the last.
4. **Winners and losers live at the skill-cluster level, not the occupation level** — and the demographic profile is not the classical "low-skill" story.
5. **Meaning of work is a first-class variable** that wage-and-employment studies cannot see. Sociology of work has known this since Marx.

---

## Further reading

- Autor, Levy & Murnane (2003) — *The Skill Content of Recent Technological Change.* The foundational task-based analysis.
- Acemoglu & Restrepo (2018, 2020) — theoretical task-based model of automation and new-task creation.
- Bresnahan & Trajtenberg (1995) — general-purpose technologies as a concept.
- Brynjolfsson, Li & Raymond (2023) — *Generative AI at Work.* The call-centre productivity paper.

Local:
- [`04_economic_impacts`](./04_economic_impacts.html) — full block notes.
- `papers/economics/` — PDFs including the *Economist* and Fortune counter-narratives.
