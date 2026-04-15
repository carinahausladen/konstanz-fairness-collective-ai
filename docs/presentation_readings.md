---
layout: default
title: "Presentation Readings — Student Pick List"
permalink: /presentation-readings/
---

# Presentation Readings

22 readings across the six reading weeks. Students pick **one** to present.

Weeks are paired when a block spans two sessions. Readings within a paired block are split by theme — pick from the week you are presenting in.

---

## Week 2 · 15 Apr — Defining and Measuring Fairness in AI *(part 1: representational bias foundations)*

1. [Based on billions of words on the internet, people = men (2022)](https://www.science.org/doi/full/10.1126/sciadv.abm2463) — Bailey, Williams & Cimpian
   *Foundation: bias is already present in the corpus, upstream of any model. Embedding geometry on 630B tokens.*

2. [Explicitly unbiased large language models still form biased associations (2025)](https://doi.org/10.1073/pnas.2416228122) — Bai, Wang, Sucholutsky & Griffiths
   *Methodological pivot: RLHF'd models pass explicit tests but still show pervasive implicit bias that predicts downstream decisions.*

---

## Week 3 · 22 Apr — Defining and Measuring Fairness in AI *(part 2: from outcome bias to agentic misalignment)*

3. [Measuring gender and racial biases in large language models: Intersectional evidence from automated resume evaluation (2025)](https://academic.oup.com/pnasnexus/article/4/3/pgaf089/8098718) — An, Huang, Lin & Tai
   *Concrete intersectional audit: ~361k resumes × 5 LLMs. Non-additive effects — female candidates favored, Black males disadvantaged. Bridge reading: outcome-level bias in a deployed hiring context.*

4. [Sleeper Agents: Training Deceptive LLMs that Persist Through Safety Training (2024)](https://arxiv.org/abs/2401.05566) — Hubinger et al. (Anthropic / Redwood / Mila / Oxford)
   *Proof-of-concept that backdoored deceptive behavior survives SFT, RLHF, and adversarial training — and that adversarial training can make it better hidden rather than removed. Foundational for the agentic arc.*

5. [Agentic Misalignment: How LLMs Could Be Insider Threats (2025)](https://arxiv.org/abs/2510.05179) — Lynch et al.
   *The pivot from representational harm to agentic harm. 16 frontier models blackmail, leak, and sabotage under stressors — up to 0.96 rate.*

6. [Emergent Misalignment: Narrow Finetuning Can Produce Broadly Misaligned LLMs (2026)](https://arxiv.org/abs/2502.17424) — Betley et al.
   *Surprising result: fine-tuning GPT-4o on insecure code alone induces ~20% broad misalignment on unrelated prompts. Intent/framing in training data matters.*

---

## Week 4 · 29 Apr — Social Choice for AI *(part 1: social choice theory for LLM alignment)*

7. [Artificial Intelligence, Values, and Alignment (2020)](https://doi.org/10.1007/s11023-020-09539-2) — Iason Gabriel, *Minds and Machines* 30, 411–437
   *Accessible philosophical bridge. "Alignment with *whose* values?" — six increasingly demanding targets (instructions → expressed intentions → revealed preferences → informed desires → interest → values). Explicitly invokes Arrow-style impossibility; sets up the normative question that Conitzer then formalizes.*

8. [Social Choice Should Guide AI Alignment in Dealing with Diverse Human Feedback (2024)](https://arxiv.org/abs/2404.10271) — Conitzer et al. (ICML 2024)
   *Programmatic: RLHF is a voting rule in disguise; Arrow's theorem applies. Four areas where social choice can inform alignment.*

9. [The PRISM Alignment Dataset (2024)](https://arxiv.org/abs/2404.16019) — Kirk et al. (NeurIPS 2024)
   *1,500 participants × 75 countries × 21 LLMs × 8,011 conversations. Each rating linked to a participant profile and a self-written "constitution." Designed to surface disagreement, not average it away.*

10. [Cultivating Pluralism in Algorithmic Monoculture: The Community Alignment Dataset (2026)](https://arxiv.org/abs/2507.09650) — Zhang et al. (Meta FAIR)
    *15,000 participants × 5 countries × 21 LLMs. All 21 LLMs align with only ~41% of human preferences. Introduces negatively-correlated sampling — because preference-dataset fixes alone are insufficient if candidates are homogeneous.*

---

## Week 5 · 06 May — Social Choice for AI *(part 2: social-choice algorithms in deployment)*

11. [Impacts of Aggregation on Model Diversity and Consumer Utility (2026)](https://arxiv.org/abs/2602.23293) — Donahue & Raghavan
    *Supply-side angle. Winrate-based leaderboards drive producer homogenization and reduce consumer welfare. Proposes weighted winrate that rewards specialization. Aggregation rules as market infrastructure.*

12. [Consensus Stability of Community Notes on X (2026)](https://arxiv.org/abs/2601.14002) — Chuai, Lenzini & Pröllochs (WWW 2026)
    *Flagship empirical: 30.2% of publicly-displayed helpful notes later lose helpful status. Display triggers polarization that undoes the bridging consensus.*

13. [Hyperactive Minority Alters the Stability of Community Notes (2026)](https://arxiv.org/abs/2602.08970) — Nudo et al.
    *Activity is heavy-tailed and politically selective. A small hyperactive minority largely determines outcomes — classic social-choice participation inequality, visible at scale.*

---

## Week 6 · 13 May — Economic Impacts of AI

14. [Harms of AI (2021)](https://economics.mit.edu/sites/default/files/publications/Harms%20of%20AI.pdf) — Daron Acemoglu (MIT)
    *Conceptual framework for the block. Three domains of AI harm (data/information, labor market, communication/democracy) and four specific labor-market mechanisms. Key claim: greater competition alone can *exacerbate* harms — regulation and research redirection are needed.*

15. [Winners and Losers of Generative AI: Early Evidence of Shifts in Freelancer Demand (2025)](https://doi.org/10.1016/j.jebo.2024.106845) — Teutloff, Einsiedler, Kässi, Braesemann, Mishkin & del Rio-Chanona, *JEBO* 235
    *Cleanest causal-style early evidence. DiD on 116 freelance skill clusters around ChatGPT launch. Substitutable skills –20–50%, writing/translation –52% / –59%, AI chatbot dev +179%. Novice workers lose.*

16. [Labor Market Impacts of AI: A New Measure and Early Evidence (2026)](https://www.anthropic.com/research/labor-market-impacts) — Massenkoff & McCrory (Anthropic)
    *Introduces "observed exposure" = capability × actual automated usage. Exposed workers are older, more female, more educated, higher-paid. No aggregate unemployment signal yet, but hiring of younger workers slowing.*

17. [Are We Automating the Joy Out of Work? Designing AI to Augment Work, Not Meaning (2026)](https://doi.org/10.1145/3772318.3791845) — Ranjit, Zhou, Swayamdipta & Quercia, *CHI 2026*
    *171 tasks × 202 workers × 197 developers. AI exposure negatively correlated with meaningful-work dimensions. Measured developer–worker design gap.*

---

## Week 7 · 20 May — Democracy and LLMs

18. [Large Language Models (LLMs) as Agents for Augmented Democracy (2024)](https://doi.org/10.1098/rsta.2024.0100) — Gudiño, Grandi & Hidalgo, *Philosophical Transactions A* 382, 20240100
    *Anchor reading. 67 policies × 6 LLMs on Brazil's 2022 election. LLMs outperform a "bundle rule" for individual preference prediction and improve aggregate survey estimates. Flags LLM-governance risk explicitly.*

19. [AI can help humans find common ground in democratic deliberation (2024)](https://doi.org/10.1126/science.adq2852) — Tessler et al. (Google DeepMind), *Science* 386, eadq2852
    *The "Habermas Machine." >5,000 UK participants + a virtual citizens' assembly. AI-generated group statements consistently preferred to human-mediator statements across quality dimensions; AI-mediated deliberation measurably reduces within-group division without obscuring minority critiques. Flagship empirical result on LLM-mediated deliberation.*

20. [Reasoning Boosts Opinion Alignment in LLMs (2026)](https://arxiv.org/abs/2603.01214) — Berdoz, Billeter, Vonlanthen & Wattenhofer (ETH Zurich)
    *SFT + GRPO training on authentic political data (ANES, German parties, Swiss candidates). Reasoning consistently improves alignment; asymmetric bias across the ideological spectrum persists. Technical baseline for the faithfulness requirement.*

21. [Political Bias in Large Language Models: A Case Study on the 2025 German Federal Election (2025)](https://ceur-ws.org/Vol-4136/iaai9.pdf) — Kurtulus & Kruspe, *Identity-Aware AI workshop at ECAI 2025*
    *ChatGPT / Grok / DeepSeek audited on 38 Wahl-O-Mat statements × 100 runs. Consistent left-leaning tendency across all three models; robust disagreement with AfD; largely independent of prompt language.*

22. [Using LLMs to Enhance Democracy (2026)](https://doi.org/10.1007/s11023-026-09767-y) — Seth Lazar & Lorenzo Manuali, *Minds and Machines* 36, 12
    *Normative ceiling for the block. Six democratic values; keep LLMs out of *formal* decision-making under inequality and deep disagreement; they can strengthen the *informal public sphere*. Introduces "democracy-washing" as an auditable failure mode.*
