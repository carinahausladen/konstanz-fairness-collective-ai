---
layout: default
title: "Week 4 — Fundamentals"
permalink: /week4-fundamentals/
---

**Paper tags.**

| Tag | Paper |
|---|---|
| 🟦 | **Gabriel 2020** — *AI, Values, and Alignment* |
| 🟩 | **Kirk et al. 2024** — *The PRISM Alignment Dataset* |
| ⚪ | context only, not presented this week |

---

The thread this week: **how more than two centuries of social-choice and political-philosophy work on aggregating preferences resurface — renamed, re-parameterised — inside modern alignment pipelines**. RLHF is a social-choice problem. Recognising this puts the Week-4 papers into a deep tradition rather than into a CS vacuum.

---

## 1. The preference-aggregation problem — older than computer science

The question *"how do we combine individual preferences into a collective choice?"* is the defining problem of social choice theory. The fact that alignment pipelines now solve it *at scale* does not make the problem new.

**The canonical sources** — these should be in the lecture:

- **Condorcet (1785)** — first formal study of voting. Introduces the **Condorcet winner** (an option that beats every other in pairwise vote) and the **Condorcet paradox** (collective preferences can cycle even when all individuals are rational). The paradox is the foundational shadow of every aggregation scheme.
- **Borda (1784)** — alternative rule: score each option by its rank in each voter's ballot, sum across voters. Different winner than Condorcet in general. Two reasonable rules, two incompatible outputs.
- **Arrow (1951), *Social Choice and Individual Values***. **Impossibility theorem**: no aggregation rule satisfies all four of — unrestricted domain, non-dictatorship, Pareto efficiency, independence of irrelevant alternatives (IIA). Any aggregation rule we write down *must* violate at least one. 🟦
- **Gibbard (1973) / Satterthwaite (1975)**. Strategic manipulation is *always* possible in non-dictatorial rules. Every voting system admits insincere voting.
- **Sen (1970), *Collective Choice and Social Welfare***. Relaxes Arrow's axioms; shows a *Paretian liberal* is impossible. Opens the domain-restriction literature.
- **Black (1948) / Downs (1957)** — **median-voter theorem** for single-peaked preferences. Under a single ideological axis, the median voter's preference wins. Predicts homogenisation of competing platforms, a theme we will hit in Week 5.

**Why this matters for RLHF.** Any preference-aggregation system inherits every one of the impossibility and manipulation results above. You cannot engineer your way out. You can only pick *which* axiom to sacrifice, and that choice is normative.

**The CS bridge** — Conitzer et al. 2024 (unpresented this week, but the technical bridge): *RLHF is a voting rule in disguise.* Arrow applies.

---

## 2. What does "align with *whose* values" even mean? &nbsp;🟦

Gabriel's ladder — but before Gabriel, the same question ran through political philosophy for two centuries.

**The classical alternatives for "whose values":**

- **Utilitarianism** (Bentham, Mill). Sum individual utilities; maximise the total. Needs interpersonal utility comparison — contested from day one.
- **Kantian / deontological.** Align with principles that could be rational for any agent to will universally. Refuses aggregation.
- **Rawls (1971), *A Theory of Justice***. The **veil of ignorance** — choose the rule you would accept not knowing which social position you occupy. A meta-aggregation procedure.
- **Habermas (1984/1987)**, communicative action — legitimacy comes from *undistorted discourse*, not aggregation. Relevant when we pivot to deliberation in Week 7.
- **Sen (1999), *Development as Freedom***. Reject preference-satisfaction as the ground; aim at capabilities instead.

**Gabriel's contribution** (re-expressing the classical problem for ML):

Six rungs of increasing demandingness for "align with":

1. Instructions
2. Expressed intentions
3. Revealed preferences
4. Informed desires
5. Interest (objective good for the user)
6. Values (shared moral / political)

Each higher rung requires inference about something less observable.

**For the lecture.** Pick one rung and ask the room: *"Would you want your GP to align with your instructions, or your interest?"* The answer depends on the stake — which is Gabriel's entire point.

---

## 3. Preference elicitation — how you ask matters

Before aggregation comes **elicitation**. The choice of elicitation format is already a normative commitment.

- **Binary pairwise preferences** — used in most RLHF. Simple, cheap, but discards intensity.
- **Rank ordering** — Borda-compatible; captures preference structure.
- **Rating scales** — Likert-style. Cardinal information, but comparability across individuals is contested (Arrow already knew this).
- **Open-ended narrative** — captures reasons, not just preferences. The PRISM approach.

**Classical sources:**
- Fishburn (1973) on the mathematics of elicitation.
- Camerer (2003) on behavioural economics — people don't have stable preferences waiting to be elicited; elicitation constructs the preferences.

**For ML.** Every RLHF dataset is an elicitation choice, and most papers don't justify the choice.

---

## 4. Pluralism vs aggregation — a normative fork &nbsp;🟩

The deepest question in the block. Two families of answers:

**Aggregate everything into a single reward signal.** Classical RLHF. Produces one model that does *on average* what the labelled majority preferred. Pluralism is lost — by design.

**Preserve disagreement as data.** Refuse to average. Model the distribution of preferences; deploy context-specific subsets.

**Classical philosophy of pluralism:**
- **Berlin (1958)**, *Two Concepts of Liberty* — value-pluralism: multiple, incommensurable goods.
- **Rawls (1993)**, *Political Liberalism* — reasonable pluralism as the baseline condition of modern democracies.
- Agonistic democracy (Mouffe 2000) — conflict is productive, not a bug.

**The CS extension.** Kirk et al. (PRISM) build a dataset explicitly designed to surface disagreement, not average it away — 1,500 participants × 75 countries × per-participant self-written "constitution". The Community Alignment dataset (Zhang, unpresented) takes a complementary turn: not just register disagreement, but *sample* negatively-correlated preferences to combat model monoculture.

---

## 5. Procedural vs substantive legitimacy &nbsp;⚪

One more classical dyad students should recognise:

- **Substantive** — a decision is legitimate if its *content* is right.
- **Procedural** — a decision is legitimate if the *process* that produced it was fair (Habermas 1996, *Between Facts and Norms*).

RLHF, as usually deployed, implicitly claims procedural legitimacy (*"we collected many preferences, averaged them fairly"*). The **democracy-washing** failure mode (Lazar & Manuali, unpresented) is a warning: procedural vocabulary can launder a substantive decision made elsewhere. We return to this in Week 7.

---

## 6. Key vocabulary

| Term | Classical home | Contemporary usage |
|---|---|---|
| **Condorcet winner** | Condorcet 1785 | Would beat any alternative in pairwise majority |
| **Arrow's impossibility** | Arrow 1951 | No aggregation rule satisfies the four axioms jointly |
| **Single-peaked preferences** | Black 1948 | Condition under which the median-voter theorem works |
| **Strategic voting** | Gibbard-Satterthwaite 1973–75 | Any non-dictatorial rule is manipulable |
| **Preference aggregation** | Social choice | The core problem RLHF solves (implicitly) |
| **Reward model** | RLHF | The learned scalar that aggregates preference labels |
| **Pluralism** | Berlin, Rawls | The normative position that incompatible values coexist |
| **Constitution** (as in Kirk / Anthropic) | Contemporary | A written principle set the model should follow |

---

## Conceptual spine for the lecture

1. **RLHF is a voting rule.** Arrow applies. Pretending otherwise is a category error.
2. **Every preference-aggregation mechanism makes a normative choice.** There is no neutral default.
3. **Elicitation is already an aggregation commitment** — pairwise vs rank vs narrative gives different signals.
4. **Gabriel's ladder is the classical *"align with whose values"* question, re-expressed.**
5. **Pluralism is a live alternative to averaging**, and PRISM is its empirical instantiation.

---

## Further reading

- Sen, *Collective Choice and Social Welfare* (1970) — the single best book on the problem.
- List & Polak 2010 — *Introduction to Judgment Aggregation.* Covers the extension from preferences to beliefs.
- Christiano et al. 2017 — *Deep RL from Human Preferences.* Original RLHF reference.
- Conitzer et al. 2024 — *Social Choice Should Guide AI Alignment* ([arXiv:2404.10271](https://arxiv.org/abs/2404.10271)). The bridge paper; not being presented this week but worth citing.

Local:
- [`03_social_choice`](./03_social_choice.html) — full block notes.
- `papers/social choice/` — PDFs.
