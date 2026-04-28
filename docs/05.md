---
layout: default
title: "Social Choice for AI: From Alignment to Community Fact-Checking"
permalink: /social-choice/
---

# Social Choice for AI

*Fairness — but for whom, and chosen how?*

Wherever an AI system combines inputs from many people into a single outcome, it is doing **social choice**. This week we look at two very different places this happens:

- **LLM alignment** — where RLHF, DPO, and Constitutional AI aggregate human preferences into a single model. Usually framed as a technical pipeline, but at its core a voting rule.
- **Community fact-checking on X** — where a bridging algorithm aggregates contributor ratings into a "Currently Rated Helpful" label. Here the aggregation rule is open-source, deployed at scale, and studied empirically across five papers this week.

The two halves are parallel: both take heterogeneous human judgments, both face polarization and participation inequality, both are shaped by how the aggregation rule is designed and who gets to participate. What varies is the visibility — in LLMs the voting rule is hidden inside a loss function; in Community Notes it is on GitHub.

---

## Part A — Social Choice for LLM Alignment

### A1. Motivation — why preference aggregation matters for LLMs
- LLMs are trained and evaluated on *aggregated* human judgments. The aggregation step is where majority preferences dominate and minority voices disappear.
- Two symptoms traced through the week: **algorithmic monoculture** (21 state-of-the-art LLMs align with only ~41% of human preferences; Zhang et al.) and **cross-cultural misalignment** (LLM responses cluster far tighter than human annotators across the Inglehart–Welzel cultural map).
- Mishra (2023): Arrow's impossibility theorem applies to RLHF. There is no perfectly fair aggregation rule — only choices among trade-offs.

### A2. Preference elicitation
- What counts as a preference? Revealed vs. stated, individual vs. contextual, value-alignment vs. helpfulness vs. safety.
- **Ordinal vs. cardinal** preferences, and what each enables downstream (Bradley–Terry needs pairs; Kemeny–Young works on rankings; rating scales enable welfare arithmetic at the cost of interpersonal comparability).
- Methods: rankings, pairwise comparisons, approvals, ratings, free-text justifications.
- **Self-written "constitutions"** as preference elicitation — PRISM asks each participant to write their own system prompt before interaction.

### A3. Preference aggregation
- From individual to collective choice — the classic voting rules: **majority, Borda, Condorcet, Approval, STV, Kemeny–Young**.
- Key properties: **monotonicity, Pareto efficiency, independence of irrelevant alternatives (IIA), proportionality, strategy-proofness**.
- How standard RLHF implicitly picks a rule: pairwise preferences → Bradley–Terry–Luce → scalar reward. Implicit choices hidden inside `preference_loss`.
- Conitzer et al.'s agenda: make the aggregation rule explicit; compare BTL to Kemeny–Young, Borda, Condorcet; evaluate via social-choice axioms rather than only downstream accuracy.

### A4. Committee elections and participatory budgeting
- Committee elections as a natural model for **selecting a *set* of models or principles** rather than a single best one.
- Proportional representation rules (PAV, Method of Equal Shares).
- **Participatory budgeting (PB)** as a generalization: aggregating preferences over bundles of items with costs. Proportional and cost-aware aggregation methods.
- Why this matters for AI: platforms increasingly expose *menus* of models (routers, model marketplaces). The aggregation question is "which set should be available?" — not only "which single model wins?".

### A5. Aggregation on the supply side — incentives and monoculture
- Donahue & Raghavan: leaderboards and routers are themselves aggregation rules, and they shape what models get built. **Winrate maximization** pushes producers toward *homogenization*. Their proposed **weighted winrate** rewards specialization and provably improves consumer welfare.
- Algorithmic monoculture as a supply-side phenomenon, not only a demand-side one.

### A6. Human-centered LLMs
- **RLHF** as the dominant aligned-from-preferences pipeline; **DPO / KTO** as alternative preference-based fine-tuning objectives.
- **Constitutional AI** as aggregation over *principles* rather than outputs — but: who writes the constitution? How are principles aggregated when they conflict? (See also Klaassen & Schroeder, Week 2, for the governance critique.)
- **Pluralistic alignment**: personalization, localization, distributional matching. Each strategy is one point in the design space Conitzer et al. map.

### A7. Procedures and participation — the normative ceiling
- Tasioulas: preference-based utilitarianism is necessary but insufficient. Humanistic ethics adds (a) plurality of values, (b) the intrinsic importance of procedures, (c) individual and collective participation in defining the good.
- González Barman et al.: pluralism in RLHF feedback groups has both ethical and *epistemic* payoffs (Scott–Page "Diversity Trumps Ability"). Balanced outputs can emerge from multiple committed perspectives — they do not require each annotator to be internally balanced.
- Implication: even a perfectly-designed social-choice aggregator still leaves open the question of who participates and with what legitimacy.

---

## Part B — Community Notes on X: A Live Case Study

X's Community Notes is the most **transparent deployed social-choice system** we have. The bridging algorithm is open-source; the full rating data is public; the pipeline from raw ratings to displayed labels can be independently scrutinized. Four papers this week study it from different angles, and together they stress-test the assumptions of the wisdom-of-crowds / bridging approach.

### B1. How the bridging algorithm works
- Core model: matrix factorization. Each rating $r_{ij} = \mu + \alpha_i + \beta_j + \gamma_i \delta_j + \epsilon_{ij}$ decomposes into a baseline, a rater tendency, a note-quality term, and a bilinear *ideology–alignment* term.
- **"Bridging" means** a note is surfaced as helpful only when it receives support from raters with very different $\gamma_i$ values — i.e., across the ideological axis.
- Key design choice: after ideology is accounted for, *all raters get equal weight* on the quality estimate. Condorcet's jury theorem framing applied to a noisy, politically-charged setting.

### B2. Stability under display — the polarization problem
- **Chuai et al. (Consensus Stability)**: 30.2% of notes that are displayed as helpful later lose their status. Display itself triggers a sharp increase in rating volume and a *shift* in rating leaning. Similar-viewpoint contributors add positive ratings; dissimilar ones add systematically negative ones → post-display polarization can undo the bridging consensus.
- The aggregation rule is only as stable as the process that feeds it samples.

### B3. Who gets to contribute — the input channel
- **Chuai et al. (Request a Note)**: X introduced a "Request Community Note" feature letting users flag posts for context. Requested posts with higher misleadingness and from higher-exposure authors are more likely to receive notes — but the contributors who respond are *more ideologically selective* than unsolicited note-writers. Partisan asymmetries: posts from Republicans receive requested notes more often than from Democrats.
- The input channel is a second lever beyond the voting rule — it shapes *who* is aggregated.

### B4. Participation inequality
- **Nudo et al.**: activity follows a heavy-tailed distribution. A small hyperactive minority generates a disproportionate share of ratings and is highly politically selective. Small perturbations to this minority produce markedly different outcomes.
- Classic social-choice concern (inequality of influence) appears empirically at scale in a deployed system. The "community" is effectively a minority.

### B5. Mechanism design — endogenous rater weighting
- **Goyal, Arora & Goel (QS-MF)**: add a per-rater **quality-sensitivity parameter** $\rho_i$ to the matrix factorization, estimated jointly with all other parameters. Grounded in peer-prediction theory (Miller–Resnick–Zeckhauser): without ground truth, influence should track demonstrated quality.
- Empirically: 26–40% fewer ratings needed to match baseline accuracy; substantial robustness against coordinated adversarial attacks; separates good from bad raters with AUC > 0.94.
- Constructive answer to the problems Chuai and Nudo document — and a concrete social-choice design decision (weighted vs. equal-weight aggregation) with measurable welfare consequences.

### B6. What the Community Notes case teaches us about social choice for AI
- Transparency + deployment at scale makes CN a **testbed for social-choice axioms in the wild**: stability, robustness to strategic behavior, representation of minorities.
- The same four levers appear as in LLM alignment: (1) who participates, (2) how their input is elicited, (3) what aggregation rule combines it, (4) what happens dynamically after outputs are exposed. Each lever is a locus for design and for critique.

---

## 📖 Readings for Presentations

### Week 4 · 29 Apr — Social choice theory for LLM alignment
- [Artificial Intelligence, Values, and Alignment (2020)](https://doi.org/10.1007/s11023-020-09539-2) — Iason Gabriel, *Minds and Machines* 30, 411–437.
  *Accessible philosophical bridge. "Alignment with *whose* values?" — six targets from instructions to values. Explicitly invokes Arrow-style impossibility; sets up the normative question that Conitzer then formalizes. Written for a non-technical audience.*
- [Social Choice Should Guide AI Alignment in Dealing with Diverse Human Feedback (2024)](https://arxiv.org/abs/2404.10271) — Conitzer et al. (ICML 2024). 🎧 ~29:32
  *Programmatic paper. Four areas where social choice can inform RLHF: pairwise aggregation, Constitutional AI, preference-based fine-tuning, collective modeling. Arrow applies to RLHF.*
- [The PRISM Alignment Dataset (2024)](https://arxiv.org/abs/2404.16019) — Kirk et al. (NeurIPS 2024 D&B). 🎧 ~15:40
  *1,500 participants × 75 countries × 21 LLMs. Each rating linked to participant profile and a self-written "constitution." Designed to surface disagreement, not average it away.*
- [Cultivating Pluralism in Algorithmic Monoculture: The Community Alignment Dataset (2026)](https://arxiv.org/abs/2507.09650) — Zhang et al. (Meta FAIR).
  *15,000 participants × 5 countries × 21 LLMs. All 21 LLMs align with only ~41% of human preferences. Introduces **negatively-correlated sampling** to diversify candidate responses.*

### Week 5 · 06 May — Social-choice algorithms in deployment
- [Impacts of Aggregation on Model Diversity and Consumer Utility (2026)](https://arxiv.org/abs/2602.23293) — Donahue & Raghavan.
  *Game-theoretic marketplace model. Winrate-based aggregation → homogenization → reduced consumer welfare. Proposes a weighted-winrate rule. Supply-side counterpart to the Community Notes case studies.*
- [Consensus Stability of Community Notes on X (2026)](https://arxiv.org/abs/2601.14002) — Chuai, Lenzini & Pröllochs (WWW 2026).
  *437k notes, 35M ratings. 30.2% of displayed helpful notes later disappear; display triggers polarization that undoes the bridging consensus.*
- [Hyperactive Minority Alters the Stability of Community Notes (2026)](https://arxiv.org/abs/2602.08970) — Nudo et al.
  *Activity is heavy-tailed and politically selective. A small hyperactive minority's behavior largely determines system outcomes. Classic social-choice participation inequality, visible at scale.*

### Background / further reading
- [Reinforcement Learning from Human Feedback: Whose Culture, Whose Values, Whose Perspectives? (2025)](https://doi.org/10.48550/arXiv.2407.17482) — González Barman, Lohse & de Regt, *Philosophy & Technology* 38, 35.
  *Epistemic/ethical case for pluralism in RLHF feedback groups.*
- [Artificial Intelligence, Humanistic Ethics (2022)](https://direct.mit.edu/daed/article/151/2/232/110615/Artificial-Intelligence-Humanistic-Ethics) — John Tasioulas, *Daedalus* 151(2).
  *Philosophical counterweight: preference-utilitarianism is insufficient. (Also in Week 5/Democracy block.)*
- [Request a Note: How the Request Function Shapes X's Community Notes System (2026)](https://arxiv.org/abs/2509.09956) — Chuai et al. (CHI 2026).
  *Input-channel analysis of the "Request Community Note" feature. Complements Consensus Stability on the same corpus.*
- [Quality-Sensitive Matrix Factorization for Community Notes (2026)](https://arxiv.org/abs/2604.11224) — Goyal, Arora & Goel.
  *Technical mechanism-design paper; adds per-rater quality-sensitivity to the CN matrix factorization.*
- [Representative Social Choice: From Learning Theory to AI Alignment (2024)](https://arxiv.org/abs/2410.23953) — Qiu. 🎧 ~28:26
- [Yang et al. (2024)](https://dl.acm.org/doi/full/10.1145/3665332)

### Technical Background
- [Probabilistic Artificial Intelligence — Chapter 12.7: Learning from Preferences (2025)](https://arxiv.org/pdf/2502.05244) — Krause & Hübotter, ETH Zürich lecture notes.
  *Technical machinery behind RLHF and DPO. Where the philosophical readings ask *whose* values RLHF encodes, this chapter shows *how* individual preferences are turned into model behavior — making precise where the social-choice critique bites: in the aggregation step that produces the scalar reward.*

---

## 📊 Project Ideas & Datasets

### 1. End-to-end welfare in multi-model ecosystems
Develop an integrated view of welfare in AI ecosystems by connecting the supply and demand sides.
- *Supply side:* which incentives encourage firms to build differentiated models rather than converging on a homogeneous set? (Donahue & Raghavan as a starting point.)
- *Demand side:* how should a platform, provider, or society select a menu of models so that overall welfare is high while minority preferences are not ignored? (Committee-election and PB aggregation rules as candidates.)
- *Contribution:* study how producer incentives and menu-selection rules interact; whether combining diversity-inducing supply incentives with proportional or welfare-aware selection leads to better outcomes for heterogeneous users.

### 2. Re-aggregating an existing preference dataset
Take PRISM or Community Alignment and swap the aggregation rule. Compare a Bradley–Terry baseline against Kemeny–Young, Borda, or a proportional rule. Measure downstream effects on (a) minority-group alignment, (b) cross-cultural variance, (c) judge-agreement with the model's final answer. The framing contribution is showing empirically what Conitzer et al. argue analytically — that the choice of aggregation rule is load-bearing.

### 3. Community Notes as a social-choice lab
CN's open-source algorithm and public data enable counterfactual experiments that are impossible inside LLM pipelines.
- Re-run the bridging algorithm with (i) Goyal-style quality weighting, (ii) caps on hyperactive raters (Nudo), (iii) different input-channel designs (with/without request feature, Chuai).
- Evaluate against: sample efficiency, time-to-consensus, minority representation, resilience to coordinated manipulation.
- Broader contribution: a menu of social-choice design choices with measurable welfare trade-offs in a *real* deployed system — directly transferable as design principles for future alignment systems.
