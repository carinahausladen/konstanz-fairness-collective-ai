---
layout: default
title: "LLMs and Democracy"
permalink: /democracy/
---

# LLMs and Democracy

*Can we use LLMs as democratic infrastructure — and what does it cost to try?*

LLMs touch democracy at **four distinct layers**. At the **input** layer, they already sit inside the recommender systems that shape what citizens see before they form opinions. At the **representation** layer, they are being trained to act as faithful "digital twins" of individual voters. At the **output** layer, proposals like "augmented democracy" use those digital twins to aggregate fine-grained policy preferences directly. At the **mediation** layer, LLMs facilitate deliberation *between* humans — the flagship result here is Tessler et al.'s *Science* paper on the "Habermas Machine," which at scale outperforms human mediators in helping groups find common ground.

All four layers share one load-bearing requirement: **faithfulness**. An LLM that misrepresents what citizens think, mediates a deliberation with hidden bias, or skews the content a recommender shows them, does not augment democracy — it distorts it. This block asks how close we are to faithful LLM infrastructure, what breaks when we are not, and whether "augmented democracy" is a legitimate goal even if it were technically solved.

---

## Agenda

### 1. LLMs as democratic infrastructure — four integration layers
- **Input / recommendation.** LLMs already curate political information on platforms that shape voters' opinions. Bojić et al. 2024 stress-test recommender-system rules with LLM-powered social-media agents. Connects to Helberger's normative work on the democratic role of news recommenders.
- **Representation / opinion alignment.** Can an LLM faithfully reproduce *this specific person's* political views? Berdoz et al. 2026 (ETH Zurich) train this explicitly using reinforcement learning with chain-of-thought reasoning.
- **Output / voting.** Gudiño, Grandi & Hidalgo 2024 propose LLM "digital twins" that predict individual policy preferences and vote on citizens' behalf — an empirical study on Brazil's 2022 presidential election.
- **Mediation / deliberation.** Tessler et al. 2024 (*Science*, Google DeepMind) build the "Habermas Machine" — an LLM mediator that iteratively drafts group statements from individual opinions and critiques. Tested with 5,000+ UK participants in a virtual citizens' assembly; group statements from the AI are consistently preferred to those written by human mediators, and deliberation measurably reduces within-group division.

This four-layer view organises the rest of the agenda. The papers talk past each other when read in isolation; they complement each other when read as slices of one pipeline.

### 2. Augmented democracy — the Gudiño proposal
- **Concept.** Software agents trained on individual citizen preferences act as personalized representatives. Sits between representative democracy (bundle voting for parties) and direct democracy (voting on every issue), aiming to give citizens fine-grained control without cognitive overload.
- **Empirical anchor.** 67 policies extracted from the manifestos of Brazil's 2022 presidential candidates (Lula, Bolsonaro). Six off-the-shelf LLMs benchmarked.
- **Two empirical claims:**
  1. **Individual level:** LLMs outperform a "bundle rule" (assume citizens vote with their self-reported party) for out-of-sample preference prediction. → LLMs capture nuances that cross party lines.
  2. **Population level:** a probabilistic sample *augmented* by an LLM yields more accurate aggregate preference estimates than the non-augmented sample alone. → LLMs as survey data augmentation.
- **Caveats the authors flag:**
  - LLMs reflect political bias in training data; groups absent from training data cannot be represented (remote, offline, indigenous communities).
  - Governance of the model itself varies — OpenAI, Meta (Llama), Mistral, Falcon, Gemma each have different sponsors and capture risks.
  - LLMs struggle with logical/mathematical reasoning; complex policy trade-offs are where this matters most.

### 3. Faithfulness — how close are we to digital twins that actually represent us?
Four empirical papers approach faithfulness at different scales:

- **Individual level — Berdoz et al. 2026** train LLMs on authentic political data using SFT followed by GRPO (the RL objective from DeepSeek-R1). Three datasets: US voters (ANES), German parties, Swiss candidates. **Reasoning consistently improves alignment; asymmetric bias across the ideological spectrum persists.**
- **Population-level synthetic surveys — Jiang et al. 2025** ("Matching-LLM") use ChatGPT-4o with demographic personas *matched to historical survey respondents* (System-1 cultural signal) to replicate WVS responses and predict the 2024 US presidential election. Cultural differences across US/China reproduce well; **value-sensitive topics (gender roles, morality)** show the largest synthetic/real gaps.
- **Agent-based electoral simulation — Zhou et al. 2025 (FlockVote)** build LLM-powered agents with high-fidelity demographic profiles from the 2023 ACS and 2020 US Religion Census. Tested on the 2024 US Presidential Election across seven swing states; predicts Trump wins 6 of 7 → matches actual outcome. Paper's main contribution is **interpretability** — agents can be "interviewed," ablations run — not prediction alone.
- **Group-level homogeneity — Yang et al. 2024** (Hausladen et al.) find LLM voting produces **more homogeneous patterns than human groups**. Direct threat to the pluralism any augmented-democracy system needs in order to be legitimate.
- **Cross-reference to Week 3:** Kirk's PRISM and Zhang's Community Alignment document the same failure mode from the preference-data side.

### 4. Political bias of the model itself
- **Kurtulus & Kruspe 2025** audit ChatGPT, Grok, DeepSeek against Germany's 2025 Bundestag election using the **Wahl-O-Mat** (the official civic voter-advice tool) with 38 statements × 100 stochastic runs. Responses in German and English, constrained to Agree/Neutral/Disagree.
  - **Consistent left-leaning tendency across all three models.**
  - **Notable disagreement with far-right (AfD) positions** — robust, not prompt-driven.
  - **Ideological slant largely independent of prompt language** → a property of the model, not the framing.
- Methodological strength: uses a *nationally-grounded civic instrument* rather than researcher-designed prompts, which improves construct validity. Cross-reference: OpenAI's "Defining and evaluating political bias in LLMs" (Week 2) — parallel goal, US rather than German framing.

### 5. The mediation layer — AI in the deliberation itself
- **Tessler et al. 2024** (*Science*, Google DeepMind): the "Habermas Machine" — an LLM fine-tuned to generate group statements from individual opinions and *iteratively refine* them by incorporating participants' critiques. Trained with a reward model over human preferences.
  - **>5,000 UK participants** across multiple experiments plus a **virtual citizens' assembly** with a demographically representative sample.
  - **AI-generated group statements consistently preferred** to those written by a human mediator. Higher quality, clarity, informativeness, and perceived fairness on external-judge ratings.
  - **Deliberation reduces within-group division** — participants' stances converge toward a common position. Simple opinion exchange without mediation does *not* produce the same effect.
  - **Minority critiques are incorporated** into revised statements; shifts are not attributable to model bias (discussants moved similarly on contested and non-contested issues).
- **Where this sits in the normative map:** Lazar & Manuali (§6) argue LLMs should stay out of *formal* decision-making but can strengthen the *informal public sphere*. The Habermas Machine is a concrete instantiation of exactly that — it doesn't vote, it doesn't decide, it helps a group *discuss better*.
- **Open questions:** does the effect generalize beyond UK English and beyond the topics tested? Whose "common ground" is the model converging on? What happens under strong partisan polarization (the sample is representative of UK residents, not maximally adversarial)?

### 6. The input layer — LLMs, recommenders, and polarization
- **Bojić et al. 2024** build **RecSysLLMsP**: a simulation environment where LLM agents play social-media users parameterized along 10 dimensions (Big Five, cognitive style, open-mindedness, dynamic political attitude, social connectivity, emotive reaction). Three recommender conditions tested:
  - **Plurality** — diverse content → diverse interactions, but engagement concentrates on aligned content anyway.
  - **Balanced** — mixed feed; moderate outcomes.
  - **Similarity** — classic filter-bubble setup; highest satisfaction, maximum polarization.
- Methodologically this is **in-silico A/B testing of recommender rules** using LLM agents as synthetic users. Raises its own faithfulness question: do LLM-simulated users polarize like real users?
- **Normative frame (Helberger 2019)** — three democratic roles a recommender can play (liberal, deliberative, participatory); each implies different design principles and each can be at odds with engagement-maximizing defaults.

### 7. Procedural legitimacy — the normative ceiling
Three readings converge on the claim that not every *technically successful* LLM-democracy tool is *democratically legitimate*:

- **Tasioulas 2022** (cross-referenced from Week 3): preference-utilitarian aggregation — whether via LLM digital twins or traditional polls — is necessary but insufficient. Humanistic ethics emphasizes **plurality of values**, the **intrinsic importance of procedures**, and **individual and collective participation** as goods in themselves. Even if an LLM perfectly predicts my policy preferences, voting *through* it may erode the democratic good of participating *myself*.
- **Lazar & Manuali 2026** (*Minds and Machines*) turn this into an operational distinction. They identify **six democratic values** (non-instrumental: equal standing, accountability, civic virtue; instrumental: stable government, pragmatic coordination, conflict reconciliation) and argue:
  - **Keep LLMs out of *formal* democratic decision-making** under background inequality and deep moral disagreement.
  - **LLMs *can* strengthen the *informal public sphere*** — information-seeking, forming publics, holding leaders accountable.
  - Coin/adopt **"democracy-washing"** (Himmelreich 2023) for initiatives that invoke democratic legitimacy rhetorically without serving democratic values.
- **Luo et al. 2026** (Berkeley, PolSims@CHI) set **three strong preconditions** for using LLM-agent simulations in policy at all:
  1. Do not treat simulations of marginalized populations as neutral technical outputs.
  2. Do not simulate populations without their participation.
  3. Do not simulate without accountability.
  - Dual-use framing: the same simulation enables emergency preparedness *and* nativist deportation optimization. Good intentions don't control downstream uses.

Together these three readings produce a concrete evaluation rubric for any of the empirical papers in sections 2–5.

### 8. Open questions
- If LLMs can simulate voter preferences better than bundle rules, should parties or citizens *use* them? What is the ethical status of a simulated opinion?
- What governance regime should an "augmented democracy" LLM sit under? Gudiño flags but does not answer: a government-dependent LLM reshapes the democracy it represents.
- Can recommender-simulation studies (Bojić) transfer to real platforms, or are LLM-simulated users too homogeneous to test real polarization dynamics (Yang)?
- How does this block interact with Week 3's social-choice apparatus? An LLM-augmented democracy still needs an aggregation rule; Arrow still applies.

---

## 📖 Readings for Presentations

### Foundational proposal
- [Large Language Models (LLMs) as Agents for Augmented Democracy (2024)](https://doi.org/10.1098/rsta.2024.0100) — Gudiño, Grandi & Hidalgo, *Philosophical Transactions A* 382, 20240100.
  *Anchor reading. Empirical study on Brazil's 2022 election with 67 policies × 6 off-the-shelf LLMs. LLMs outperform a bundle rule at individual level and improve aggregate survey estimates via data augmentation. Flags LLM-governance risk explicitly.*

### Faithfulness — can LLMs represent individuals, populations, electorates?
- [Reasoning Boosts Opinion Alignment in LLMs (2026)](https://arxiv.org/abs/2603.01214) — Berdoz, Billeter, Vonlanthen & Wattenhofer (ETH Zurich).
  *SFT + GRPO training on authentic political opinion data (ANES, German parties, Swiss candidates). Reasoning consistently improves alignment but asymmetric bias across the ideological spectrum persists.*
- [Donald Trumps in the Virtual Polls: Predicting Public Opinions Using LLMs (2025)](https://arxiv.org/abs/2411.01582) — Jiang, Wei & Zhang (Wuhan University).
  *"Matching-LLM" method — demographic personas matched to historical survey respondents (System-1 cultural signal). Replicates US/China cultural differences on WVS; forecasts 2024 US election.*
- [FlockVote: LLM-Empowered Agent-Based Modeling for Simulating U.S. Presidential Elections (2025)](https://arxiv.org/abs/2512.05982) — Zhou, Xu, Wang & Wang, *ICAIS 2025*.
  *Agents with ACS 2023 + US Religion Census profiles. Tested on 2024 election swing states — predicts Trump wins 6/7. Main contribution is interpretability (agent-level "interviews"), not prediction.*
- [LLM Voting: Human Choices and AI Collective Decision Making (2024)](https://arxiv.org/abs/2402.01766) — Yang, Dailisan, Korecki, Hausladen & Helbing.
  *LLMs produce more homogeneous voting patterns than real human groups — direct threat to the pluralism any augmented-democracy system would need.*

### Mediation — AI in the deliberative process
- [AI can help humans find common ground in democratic deliberation (2024)](https://doi.org/10.1126/science.adq2852) — Tessler et al. (Google DeepMind), *Science* 386, eadq2852.
  *The "Habermas Machine." >5,000 UK participants + a virtual citizens' assembly. AI-generated group statements consistently preferred to human-mediator statements across quality dimensions; AI-mediated deliberation measurably reduces within-group division without obscuring minority critiques.*

### Political bias in the model itself
- [Political Bias in Large Language Models: A Case Study on the 2025 German Federal Election (2025)](https://ceur-ws.org/Vol-4136/iaai9.pdf) — Kurtulus & Kruspe, *Identity-Aware AI workshop at ECAI 2025*.
  *ChatGPT / Grok / DeepSeek audited against 38 Wahl-O-Mat statements × 100 stochastic runs. Consistent left-leaning tendency across all three models; robust disagreement with AfD positions; largely independent of prompt language.*

### Input layer — recommenders as democratic infrastructure
- [Towards Recommender Systems LLMs Playground (RecSysLLMsP): Exploring Polarization and Engagement in Simulated Social Networks (2024)](https://arxiv.org/abs/2502.00055) — Bojić, Dodevska, Deldjoo & Pantelić, *ROEGEN@RecSys'24*.
  *In-silico A/B testing of recommender conditions (Plurality, Balanced, Similarity) with 10-dim LLM user agents. Plurality feeds don't fully cure polarization — engagement still concentrates on aligned content.*
- [On the Democratic Role of News Recommenders (2019)](https://doi.org/10.1080/21670811.2019.1623700) — Natali Helberger, *Digital Journalism* 7(8), 993–1012.
  *Normative framework for what a recommender owes a democracy. Three democratic roles (liberal, deliberative, participatory); each suggests different design principles and each conflicts with engagement maximization.*

### Procedural and philosophical grounding
- [Using LLMs to Enhance Democracy (2026)](https://doi.org/10.1007/s11023-026-09767-y) — Seth Lazar & Lorenzo Manuali, *Minds and Machines* 36, 12.
  *Operational philosophical framework. Six democratic values (instrumental / non-instrumental). Keep LLMs out of *formal* decision-making; they can strengthen the *informal public sphere*. Introduces "democracy-washing" as an auditable failure mode.*
- [We Need Strong Preconditions For Using Simulations In Policy (2026)](https://arxiv.org/abs/2604.07838) — Luo, Arora & Guirado (UC Berkeley), *PolSims@CHI 2026*.
  *Three preconditions: don't treat simulations of marginalized populations as neutral; don't simulate without participation; don't simulate without accountability. Dual-use framing.*
- [Artificial Intelligence, Humanistic Ethics (2022)](https://direct.mit.edu/daed/article/151/2/232/110615/Artificial-Intelligence-Humanistic-Ethics) — John Tasioulas, *Daedalus* 151(2). *(Cross-referenced from Week 3.)*
  *Plurality of values, procedures as goods in themselves, participation. Parallel to but earlier than Lazar 2026.*

### Optional / further reading
- Conitzer et al. (2024), *Social Choice Should Guide AI Alignment* — Week 3 anchor; relevant for which aggregation rule turns LLM-augmented individual preferences into a collective decision.
- Kirk et al. (2024), PRISM; Zhang et al. (2026), Community Alignment — Week 3; empirical evidence that LLMs fail to reflect human pluralism, which is the prerequisite for Gudiño's proposal.

---

## 📊 Project Ideas & Datasets

### 1. Re-run Gudiño on a different election
Gudiño tested Brazil 2022. Replicate on a more multi-party election (Germany 2025, Switzerland's direct-democracy referenda). Does the LLM-beats-bundle-rule result hold when there are more parties and more fine-grained policy spaces? What model-governance differences (open vs. closed-weights) matter most?

### 2. Faithfulness across the ideological spectrum
Berdoz documents asymmetric bias across the political spectrum. Build a structured audit: for which ideological sub-groups do current LLMs most fail to predict out-of-sample opinions? Cross Berdoz's three datasets (US, Germany, Switzerland) and Kirk's PRISM to map where the pluralism gap is largest.

### 3. Recommender-condition A/B in silico → ex post on a real platform
Bojić runs three recommender conditions on LLM agents. A stronger claim would be: do LLM-simulated polarization outcomes predict real-platform outcomes? Pair RecSysLLMsP with a natural-experiment-style analysis of a real recommender change (e.g., Community Notes rollout, X's algorithm shift). Which simulated findings replicate?

### 4. Stress-testing the Habermas Machine
Tessler's experiments are UK-English, with contested-but-not-extreme topics, and a representative (not adversarial) sample. Design a follow-up: replicate the HM on a harder case — e.g. a highly polarized topic in a multilingual/multicultural context, or a group with pre-existing outgroup hostility. Does the common-ground effect hold? Does it converge on a genuine shared position, or does it mask minority disagreement through polite-sounding aggregation? Could combine Tessler's methodology with Lazar & Manuali's "democracy-washing" test.

### 5. Legitimacy audit of an augmented-democracy proposal
Take one concrete augmented-democracy proposal (Gudiño's Brazil exercise, or a participatory-budgeting case in Barcelona/Zurich). Apply Tasioulas's three pillars (plurality of values, procedure, participation) and identify where LLM augmentation strengthens or weakens each. Output: a legitimacy rubric for future proposals.
