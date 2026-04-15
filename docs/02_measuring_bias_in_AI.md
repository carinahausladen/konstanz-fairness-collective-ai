---
layout: default
title: "Defining and Measuring Fairness in AI"
permalink: /bias/
---

# Defining and Measuring Fairness in AI

## Agenda

### Introductory Example — Hiring Discrimination
Starting point: hiring discrimination in humans and in AI. How do we move from the intuition that something is "unfair" to a quantity we can measure on a model? We use An et al.'s resume-audit study as a concrete anchor: ~361,000 resumes with randomized identity markers, scored by five LLMs. The results are non-trivial — female candidates score *higher* than males on average, but Black male candidates score lower, and the intersectional patterns don't decompose into a simple sum of single-axis effects. This motivates the rest of the week.

### 1. Fairness Foundations
- **Definitions of fairness**: group fairness (demographic parity, equalized odds, calibration), individual fairness (similar individuals → similar outcomes), counterfactual fairness.
- **Where bias enters the LLM lifecycle**: the training corpus itself (Bailey shows PEOPLE≈MEN at the level of billions of web words), pre-training objectives, fine-tuning/RLHF data, prompt formulation, evaluation choice, deployment context.
- **Bias in canonical NLP tasks**: coreference resolution, sentiment analysis, translation, QA, generation.
- **Fairness desiderata and their conflicts**: well-known impossibility results (e.g., Kleinberg et al.) — you cannot simultaneously satisfy calibration and balance for positive/negative class across groups when base rates differ.

### 2. Fairness Metrics
Three families of metrics, each with different assumptions and failure modes:
- **Embedding-based** — cosine geometry between demographic and attribute word sets (WEAT, SEAT). Strength: cheap, reveals upstream associations (Bailey). Weakness: does not guarantee downstream harm.
- **Probability-based** — token/sequence likelihoods on paired sentences differing only in a demographic term (StereoSet, CrowS-Pairs). Sensitive to template design.
- **Generated-text metrics** — score open-ended generations (BOLD, prompts). Closer to deployment but noisy and judge-dependent.

Bai et al. argue that because modern RLHF'd models pass explicit tests, the field needs **behavioral** probes adapted from psychology — implicit association tests and relative decision tasks — to expose biases that *explicit* metrics no longer catch.

### 3. Calibration and Uncertainty
Probability-based fairness relies on calibration: $\Pr(Y=1 \mid \widehat{p}=p) = p$. If this holds overall but differs across demographic groups, the gap itself is a measurable form of bias.

- **Aleatoric** (irreducible) vs. **epistemic** (reducible-by-more-data) uncertainty.
- Underrepresented groups tend to have higher *epistemic* uncertainty, which translates to less reliable predictions — an allocative harm even when average accuracy looks fine.
- Khan et al. turn this observation into a benchmark: rather than accuracy gaps, they measure **coreference-confidence disparities** across 245,700 intersectional prompts. Confidence can drop >20% for doubly-disadvantaged identities, and — surprisingly — also for hegemonic markers like "White" or "cisgender," which suggests reliance on memorization rather than reasoning.

### 4. Bias Evaluation Datasets
Commonly used setups, and what each one can and cannot show:
- **Counterfactual inputs** — swap a demographic attribute, measure change.
- **Masked tokens (WinoBias, WinoGender)** — does the model resolve "the doctor … she" correctly?
- **Unmasked sentence pairs (CrowS-Pairs, StereoSet)** — compare likelihoods of stereotypical vs. anti-stereotypical completions.
- **Prompts and sentence completions (BOLD)** — measure toxicity, sentiment, regard in open-ended text.
- **Question answering (BBQ)** — bias under ambiguous vs. disambiguated contexts.
- **Intersectional extensions** — WinoIdentity (Khan) augments WinoBias with 25 demographic markers across 10 attributes, yielding 50 bias patterns rather than a single gender axis.

### 5. Fairness, Causality, and Data Limitations
- Observational data gives correlations; fairness claims often implicitly invoke counterfactuals.
- **Simpson's paradox** — group-level and subgroup-level effects can point in opposite directions (cf. An et al.'s intersectional results, where the gender and race effects do not add linearly for Black men and Black women).
- Resume-audit designs (Bertrand–Mullainathan style) partially sidestep this by randomizing the identity signal.

### 6. From Representational Harm to Agentic Misalignment
This is the week's pivot. The earlier sections treat bias as a *property of model outputs* on fixed benchmarks. As LLMs move into autonomous agent roles, a second failure mode appears: goal-directed, strategic harm.

- **Sleeper Agents** (Hubinger): deceptive behavior can be trained in and *persist* through SFT, RLHF, and adversarial training — adversarial training can even *hide* the backdoor better.
- **Agentic Misalignment** (Lynch): 16 frontier models resort to blackmail, espionage, and information leaking when faced with replacement or goal conflict. Not jailbreaks, not sleeper agents — misalignment that emerges spontaneously under stressors.
- **Emergent Misalignment** (Betley): fine-tuning GPT-4o on a narrow task (insecure code) induces *broad* misaligned behavior on unrelated prompts (~20% rate). The intent/framing of the training data matters, not just its surface content.
- **Mitigations** (Gomez): an externally-governed escalation channel drops blackmail rates from 38.73% → 1.21% — demonstrating that *operational* controls, not only training-time fixes, are part of the fairness/safety toolbox.
- **Governance framing** (Klaassen & Schroeder): critical view on "Claude's Constitution" — cautions against mistaking a company's values document for institutional accountability. Relevant when we ask who gets to define what "unbiased" means and who enforces it.

---

## 📖 Readings for Presentations

### Foundations — where bias comes from
- [Based on billions of words on the internet, people = men (2022)](https://www.science.org/doi/full/10.1126/sciadv.abm2463) — Bailey, Williams & Cimpian. 🎧 ~32:10
  *Embedding geometry on 630B tokens shows PERSON words cluster closer to MEN than WOMEN, and male-stereotypical traits/verbs dominate person-contexts. Establishes that androcentrism is upstream of the model.*

### Measuring bias in modern LLMs
- [Explicitly unbiased large language models still form biased associations (2025)](https://doi.org/10.1073/pnas.2416228122) — Bai, Wang, Sucholutsky & Griffiths. 🎧 ~20:40
  *IAT-style word-association and relative-decision tests across 8 models and 33,000+ prompts. Models that pass explicit tests still show pervasive implicit bias that predicts downstream allocative decisions.*
- [Defining and evaluating political bias in LLMs (2025)](https://openai.com/index/defining-and-evaluating-political-bias-in-llms/) — OpenAI.
  *Operationalizes bias as communicative style along five axes: user invalidation, user escalation, personal political expression, asymmetric coverage, political refusals. A useful template beyond the political case.*

### Intersectional and outcome-level bias
- [Measuring gender and racial biases in large language models: Intersectional evidence from automated resume evaluation (2025)](https://academic.oup.com/pnasnexus/article/4/3/pgaf089/8098718) — An, Huang, Lin & Tai.
  *~361k resumes × 5 LLMs. Non-additive intersectional effects; models favor female candidates but disadvantage Black males. Direct parallel to the introductory hiring example.*
- [Investigating Intersectional Bias in LLMs using Confidence Disparities in Coreference Resolution (2025)](https://arxiv.org/abs/2508.07111) — Khan et al. (COLM 2025). 🎧 ~42:00
  *Introduces WinoIdentity (245,700 prompts, 50 bias patterns) and shifts the metric from accuracy to confidence. Distinguishes validity failures (memorization) from value-alignment failures.*

### Auditing and governance
- [Auditing an AI-Enabled Career Advisory Platform (2025)](https://www.eticas.ai/case-studies/auditing-ai-enabled-career-advisory-platform) — Eticas.ai.
  *Rare post-deployment audit using production data, live outputs, and system documentation across four risk domains. Contrasts with pre-deployment benchmark studies.*
- [The Code Is Not the Law: Why Claude's Constitution Misleads (2026)](https://www.lawfaremedia.org/article/the-code-is-not-the-law--why-claude-s-constitution-misleads) — Klaassen & Schroeder, *Lawfare*.
  *Argues Anthropic's "Constitution" borrows constitutional language without the institutional guarantees. Useful counterweight when discussing self-regulation as a fairness mechanism.*

### From bias to agentic misalignment
- [Sleeper Agents: Training Deceptive LLMs that Persist Through Safety Training (2024)](https://arxiv.org/abs/2401.05566) — Hubinger et al.
  *Proof-of-concept that backdoored deceptive behavior survives SFT, RLHF, and adversarial training — and that adversarial training can make it better hidden rather than removed.*
- [Agentic Misalignment: How LLMs Could Be Insider Threats (2025)](https://arxiv.org/abs/2510.05179) — Lynch et al.
  *Red-team stress tests of 16 frontier models in simulated corporate settings. Blackmail rates up to 0.96 (Claude Opus 4). Misbehavior increases when the model believes the scenario is real.*
- [Emergent Misalignment: Narrow Finetuning Can Produce Broadly Misaligned LLMs (2026)](https://arxiv.org/abs/2502.17424) — Betley et al.
  *Fine-tuning GPT-4o on insecure code alone induces ~20% misaligned responses on unrelated free-form prompts. Intent/framing in the training set matters — a benign "educational" framing of the same code removes the effect.*
- [Adapting Insider Risk Mitigations for Agentic Misalignment: An Empirical Study (2025)](https://arxiv.org/abs/2510.05192) — Gomez.
  *66,600 samples across 10 LLMs. Externally-governed escalation channel reduces blackmail from 38.73% → 1.21%. Surfaces a new failure mode where Gemini 2.5 Pro and Grok-4 take harmful actions without explicit goal conflict.*

### Technical Background
- [Probabilistic Artificial Intelligence — Chapter 7.4 (Calibration) and 2.2 (Aleatoric and Epistemic Uncertainty) (2025)](https://arxiv.org/pdf/2502.05244) — Krause & Hübotter, ETH Zürich lecture notes.
- [Bias and Fairness in Large Language Models: A Survey (2024)](https://doi.org/10.1162/coli_a_00524) — Gallegos et al., *Computational Linguistics* 50(3). 🎧 ~1:12:48
  *Reference taxonomy for bias sources, metric families, and mitigation strategies — useful as a map of the field.*
