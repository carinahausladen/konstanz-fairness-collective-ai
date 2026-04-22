---
layout: default
title: "Week 7 — Fundamentals"
permalink: /week7-fundamentals/
---

**Paper tags.**

| Tag | Paper |
|---|---|
| 🟦 | **Gudiño, Grandi & Hidalgo 2024** — *LLMs as Agents for Augmented Democracy* |
| 🟩 | **Tessler et al. 2024** — *AI can help humans find common ground* |
| 🟧 | **Kurtulus & Kruspe 2025** — *Political Bias in LLMs, 2025 German Election* |
| ⚪ | context only, not presented this week |

---

The thread this week: **democratic theory has spent two centuries arguing about representation, deliberation, and legitimacy.** Every LLM-democracy paper we read is re-parameterising one of those debates. The job of the lecture is to make the classical framing visible before students read the empirical CS on top.

---

## 1. Two competing visions of democracy

Students need this dyad before anything else — the Week-7 papers each sit on one side or straddle it.

**Aggregative democracy.** Legitimacy comes from fairly aggregating *pre-existing preferences*. Voting is the paradigm mechanism. Social choice theory (Week 4) is the formal backbone.

- **Schumpeter (1942)**, *Capitalism, Socialism and Democracy.* Minimalist / competitive theory: democracy is just a procedure for choosing elites via vote. Preferences are exogenous; aggregation is everything.
- **Downs (1957)** — voting as rational choice. We saw him in Week 5.
- **Dahl (1971)**, *Polyarchy.* Operationalises "democracy" as a set of institutional conditions.

**Deliberative democracy.** Legitimacy comes from *the process* of reasoned discussion that *shapes* preferences. Aggregation comes at the end, if at all.

- **Habermas (1984, 1987)**, *Theory of Communicative Action.* The ideal speech situation — undistorted, power-free discourse.
- **Habermas (1996)**, *Between Facts and Norms.* Discourse theory of law and democracy. Legitimacy = procedural, rooted in discursive justification.
- **Cohen (1989)** — deliberative conception of legitimacy.
- **Gutmann & Thompson (1996)** — *Democracy and Disagreement.* Applied deliberation.
- **Fishkin (1991, 2018)** — **deliberative polling** as an empirical operationalisation. Assembles a representative mini-public; they deliberate; outcomes compared to surveys. Tessler's experimental design is deliberative polling scaled up with an AI mediator. 🟩

**For the lecture.** Draw the dyad on the board. Gudiño sits mostly in the aggregative frame (higher-bandwidth representation). Tessler tests deliberative claims empirically. Kurtulus audits the model itself, a prerequisite for either.

---

## 2. Representation — who speaks for whom &nbsp;🟦

If an LLM is going to *represent* a citizen, we need the classical theory of representation.

**Classical sources:**

- **Hobbes**, *Leviathan* (1651). Representation as *authorisation* — the representative speaks *as* the represented.
- **Burke (1774)**, Speech to the Electors of Bristol. **Trustee vs delegate.** Trustee: the representative exercises their own judgement for the common good. Delegate: the representative transmits the constituents' preferences faithfully. Every representation scheme picks one.
- **Pitkin (1967)**, *The Concept of Representation.* The canonical synthesis: *formal, descriptive, symbolic, substantive* representation — four distinct senses. Most debates conflate them.
- **Mansbridge (2003)** — four varieties of representation (promissory, anticipatory, gyroscopic, surrogate). Contemporary extension.

**Why this matters for LLM-agents.**

- An LLM-representative aligned to *expressed instructions* is a **delegate** — it transmits.
- An LLM-representative aligned to *informed desires* or *interests* is a **trustee** — it judges.
- Pitkin's *substantive* representation asks whether the represented are actually better off under the representation. Gudiño's "faithfulness" metric is a thin operationalisation of substantive representation.

**Gabriel's ladder from Week 4 is the Burkean spectrum, re-expressed.**

**The CS extension** — Gudiño 2024. 67 policies × 6 LLMs on Brazil's 2022 election. LLMs predict individual preferences better than a bundle rule (assume party-line). Representation becomes higher-bandwidth. Legitimacy concern is that "higher-bandwidth" is not the same as "better": a well-predicted citizen is not a well-represented one.

---

## 3. Deliberation at scale — the Habermas problem &nbsp;🟩

The oldest objection to deliberative democracy is scale. Habermas's ideal speech situation is plausible for a New England town meeting, implausible for a continental democracy.

**Classical responses:**

- **Fishkin's deliberative polling** — sample a representative mini-public of 200-500; they deliberate for days; their post-deliberation views are treated as a signal. Empirically effective at moving views; expensive.
- **Citizens' assemblies** — Ireland's constitutional assemblies, the Convention Citoyenne pour le Climat. Institutionalised deliberative mini-publics.
- **Mansbridge, Bohman & colleagues** — *Deliberative Systems* approach: stop demanding that one institution meet all deliberative criteria; evaluate the ecosystem.

**Empirical work on deliberation quality** — pre-LLM:
- **Steiner et al. (2004)**, *Deliberative Quality Index.* Measures parliamentary speeches on respect, reasoning, constructive politics.
- **Mutz (2006)** — *Hearing the Other Side.* Exposure to cross-cutting political discussion reduces participation.

**The CS extension** — Tessler et al. 2024, the "Habermas Machine". >5,000 UK participants, virtual citizens' assembly. AI-generated group statements *consistently preferred* to human-mediator statements on quality dimensions (accuracy, fairness, informativeness, clarity). AI-mediated deliberation measurably *reduces within-group division* without obscuring minority critiques.

**Critical move to make in class.** The paper shows AI-mediated statements are *preferred* — which is not the same as showing they produce *better decisions*. The Habermas label stakes a strong claim; ask whether it is earned.

---

## 4. Political bias of the representative &nbsp;🟧

Whether a representative is a delegate or a trustee, its own biases contaminate the representation it provides.

**Classical sources:**

- **Converse (1964)**, *The Nature of Belief Systems in Mass Publics.* Ideological coherence is weaker than observers assume; measured "opinion" depends heavily on how it is elicited.
- **Poole & Rosenthal** — NOMINATE. Measures legislators' ideological position from roll-call votes using latent-variable methods. The technical backbone of the entire measurement tradition we are in. (Same mathematics as Week 5's bridging algorithm.)
- **Gerring (1997)** — *Ideology: A Definitional Analysis.* What does it mean for an agent to "have" an ideology? Survey of the conceptual confusion.

**Why this matters in 2026.** If LLMs sit at Layer 1 (representation) or Layer 2 (mediation), their own political leanings contaminate everything downstream. Layer 3 is infrastructure-critical: monoculture across frontier models means no competitive marketplace of political stances.

**The CS extension** — Kurtulus & Kruspe 2025. 38 Wahl-O-Mat statements × 100 runs × three models (ChatGPT, Grok, DeepSeek). Consistent **left-leaning** tendency across all three. Robust *disagreement with AfD*. Largely independent of prompt language.

**Audit methodology.** The Wahl-O-Mat is a voter-advice-application (VAA). VAAs (SmartVote, StemWijzer, Kieskompas) have been used by political scientists since the early 2000s for ideal-point estimation. Kurtulus is applying a *political-science instrument* to LLMs — ideal-point estimation for the model itself.

---

## 5. Procedural legitimacy and democracy-washing &nbsp;⚪

The normative ceiling for the block.

**Classical sources:**

- **Habermas (1996)** on discursive legitimacy — again.
- **Rawls (1993)**, *Political Liberalism* — public reason as the ground of legitimacy.
- **Estlund (2008)**, *Democratic Authority.* Epistemic vs procedural legitimacy.

**The contemporary warning.** Lazar & Manuali 2026 (open issue #23, unpresented) introduce **democracy-washing** — using democratic vocabulary ("inclusive", "deliberative", "representative") to launder a decision made elsewhere. An auditable failure mode.

**For the lecture.** An empirical win on *preferred statements* (Tessler) or *prediction accuracy* (Gudiño) does not settle the political question. Procedural legitimacy concerns *who sets the terms*, not *how good the output is*.

---

## 6. The three layers of democratic infrastructure — a quick map

| Layer | Role | Paper | Classical frame |
|---|---|---|---|
| **Representation** | LLM as agent of a citizen | Gudiño 🟦 | Burke, Pitkin |
| **Mediation** | LLM as facilitator | Tessler 🟩 | Habermas, Fishkin |
| **Model itself** | LLM as political object | Kurtulus 🟧 | Converse, Poole-Rosenthal |

All three are being built *simultaneously*. Keep them separated analytically or the discussion collapses.

---

## Key vocabulary

| Term | Classical home | Contemporary usage |
|---|---|---|
| **Trustee vs delegate** | Burke 1774 | Two models of what a representative does |
| **Aggregative vs deliberative democracy** | Schumpeter / Habermas | Two families of democratic theory |
| **Ideal speech situation** | Habermas 1984 | Undistorted, power-free discourse; baseline for legitimate deliberation |
| **Deliberative polling** | Fishkin 1991 | Sample mini-public deliberates; post-views are the signal |
| **Ideal-point estimation** | Poole & Rosenthal | Matrix factorisation on voting data — used in Community Notes & Kurtulus |
| **Democracy-washing** | Lazar 2026 | Procedural vocabulary laundering non-procedural decisions |
| **Digital twin** | Contemporary | LLM imitating a specific individual's preferences |

---

## Conceptual spine for the lecture

1. **Aggregative vs deliberative democracy is the master dyad** — place each paper on the map.
2. **Representation is Burkean at heart** — the LLM-agent is either delegate or trustee; every "faithfulness" metric picks one.
3. **Fishkin's deliberative polling is the pre-LLM ancestor** of Tessler's experimental design.
4. **Kurtulus is ideal-point estimation applied to the model** — not a new methodology, a new target.
5. **Democracy-washing is the normative ceiling** — empirical wins do not settle legitimacy.

---

## Further reading

- Pitkin, *The Concept of Representation* (1967) — still the best single book on representation.
- Fishkin, *Democracy When the People Are Thinking* (2018) — accessible account of deliberative polling.
- Habermas, *Between Facts and Norms* (1996) — discourse theory of legitimacy.
- Estlund, *Democratic Authority* (2008) — on epistemic and procedural legitimacy.
- Dryzek, *Foundations and Frontiers of Deliberative Governance* (2010).

Local:
- [`05_LLMs_democracy`](./05_LLMs_democracy.html) — full block notes.
- `papers/democracy/` — PDFs for all readings in the block.
