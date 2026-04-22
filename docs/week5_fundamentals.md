---
layout: default
title: "Week 5 — Fundamentals"
permalink: /week5-fundamentals/
---

**Paper tags.**

| Tag | Paper |
|---|---|
| 🟦 | **Donahue & Raghavan 2026** — *Aggregation, Model Diversity, Consumer Utility* |
| 🟩 | **Chuai, Lenzini & Pröllochs 2026** — *Consensus Stability of Community Notes* |
| 🟧 | **Nudo et al. 2026** — *Hyperactive Minority Alters Community Notes* |
| ⚪ | context only, not presented this week |

---

The thread this week: Week 4 was about aggregation *in principle*. This week it is about aggregation *in markets and on platforms* — where the aggregation rule itself creates incentives that feed back into the preferences it aggregates. The social-science backbone here is political economy and the sociology of collective action.

---

## 1. When aggregation shapes the supply of options — political economy &nbsp;🟦

Classical aggregation theory treats the set of alternatives as **fixed**. In a market or on a platform, the alternatives are **produced by strategic actors**, and those actors respond to the aggregation rule.

**Classical sources:**

- **Hotelling (1929)**, *Stability in Competition.* Two ice-cream sellers on a beach converge to the middle. First formal argument that competition under majority aggregation **homogenises** supply.
- **Downs (1957)**, *An Economic Theory of Democracy.* Lifts Hotelling to politics → **median-voter theorem** in two-party systems. The aggregation rule (plurality) drives candidates toward the median, not the ends.
- **Dixit & Stiglitz (1977)** — monopolistic competition with differentiated products. The rival intuition: in large markets, differentiation can be more profitable than sameness.
- **Salop (1979)** — circular-city model with variety. Variety exists when the aggregation rule *rewards* niches.

**Why this matters for AI.** Leaderboards, A/B tests, and winrate-based benchmarks are aggregation rules over producers (model developers). The rule they implement determines whether the model population converges or diversifies.

**The CS extension** — Donahue & Raghavan 2026. Winrate-based model leaderboards implement Hotelling's logic: the payoff is highest for a single modal answer, so producers converge. Welfare of users with niche preferences falls. Their proposed fix — **weighted winrate** rewarding specialisation — is explicitly a Dixit-Stiglitz move within the benchmark.

---

## 2. Platform-level aggregation — bridging-based ranking &nbsp;🟩 🟧

Both Community Notes papers presume understanding of the **bridging algorithm** that ranks notes. Teach it before the papers.

**Classical antecedent:**
- **Ideal-point estimation** in political science (Poole & Rosenthal, NOMINATE, 1985 onward). Legislators' positions are latent; votes reveal a low-dimensional ideology space via matrix factorisation.
- Same mathematics as the Community Notes algorithm.

**The algorithm in one paragraph.**
Each rater $u$ and each note $n$ gets two latent scalars:
- **polarity** $f_u, f_n$ — the left-right-style axis, and
- **helpfulness intercept** $i_u, i_n$ — axis-orthogonal baseline.

A note is displayed only if its $i_n$ exceeds a threshold. $i_n$ is high only when raters *from both poles of the polarity axis* have called it helpful — i.e. the note "bridges" the partisan divide.

**Why this is interesting as a social-choice rule.** Classical majority voting picks whatever the majority wants. Bridging ranking picks whatever clears the **cross-partisan intercept**, deliberately *under-valuing* notes that are approved only by one pole. It is a non-majoritarian aggregation rule that encodes a procedural value (bridging) rather than an outcome value.

---

## 3. Stability and feedback — a deployed rule perturbs its own inputs &nbsp;🟩

In classical social choice, preferences are assumed **exogenous**. On a live platform, they are not — display changes who rates.

**Classical sources:**
- **Sen (1993)**, *Internal Consistency of Choice* — choices from a pair may flip when the menu changes.
- **Agenda-setting** literature in political science (Riker 1982) — the order in which options are considered changes the winner.
- **Reflexivity** (Soros 1987; Merton 1948 on self-fulfilling prophecy) — the observer changes what is observed.

**For the lecture.** *Every* deployed aggregation rule has this problem. It is not a Community-Notes bug.

**The CS extension** — Chuai et al. 2026. **30.2 %** of helpful notes lose their status after being displayed. Mechanism: the early rater pool is bridging-oriented; once the note is displayed to *everyone*, the new rater distribution is more polarised, which drags the intercept below threshold.

---

## 4. Collective action and participation inequality &nbsp;🟧

Community Notes is a volunteer collective-action problem. The voluntariness is the point — and the classical literature predicts exactly what Nudo et al. find.

**Classical sources:**

- **Olson (1965)**, *The Logic of Collective Action.* Why small, intensely-motivated groups out-participate large, diffusely-motivated ones. Counters the naive "one person one vote → collective rationality" intuition.
- **Verba, Schlozman & Brady (1995)**, *Voice and Equality.* Participation is systematically skewed — by resources, motivation, identity.
- **Michels (1911)**, *Political Parties.* "Iron law of oligarchy" — every large voluntary organisation tends toward rule by a committed few.
- **Arrow's assumption of universal participation.** Classical voting theorems assume everyone votes. Reality is power-law participation; every theorem's conclusion needs to be re-read under that assumption.

**The CS extension** — Nudo et al. 2026. Community Notes rating activity is heavy-tailed (expected from Olson/Michels) *and politically selective* (expected from Verba). The bridging algorithm implicitly assumes the rater pool spans the polarity axis; skewed participation degrades the bridging property.

---

## 5. Polarisation and bridging — from political science

One more conceptual thread students should have:

- **Converse (1964)**, *The Nature of Belief Systems in Mass Publics.* The public is less ideologically coherent than we imagine; measured "polarisation" partly tracks media frames.
- **Iyengar et al. (2012)**, *Affective Polarisation.* Polarisation is increasingly about *how much we dislike the other side*, not policy distance. Changes what "bridging" means: if affect is the source of polarisation, aligning on an issue does not close the gap.
- **Mason (2015, 2018)** on social-identity polarisation.

**Why this matters for the three papers.** Community Notes as a bridging mechanism must overcome **affective** polarisation — not just issue-position polarisation. Week 5 papers implicitly operationalise bridging as issue-level convergence; the political-science literature suggests that is not enough.

---

## 6. The three-paper arc in one sentence

> The aggregation rule shapes the supply of models (Donahue) → deployment perturbs the aggregation signal (Chuai) → skewed participation further perturbs it (Nudo). Each paper identifies a failure mode that classical social-choice theory *predicts* if you take political economy and collective-action sociology seriously — but that Week-4's idealised aggregation theory does not.

---

## Key vocabulary

| Term | Classical home | Contemporary usage |
|---|---|---|
| **Hotelling homogenisation** | Hotelling 1929, Downs 1957 | Why winrate leaderboards converge |
| **Median-voter theorem** | Black 1948, Downs 1957 | Single-peaked preferences → median wins |
| **Ideal-point estimation** | Poole & Rosenthal | Matrix factorisation on rating data (= Community Notes) |
| **Bridging-based ranking** | Contemporary (Wojcik et al. 2022) | Non-majoritarian rule that rewards cross-partisan agreement |
| **Collective-action problem** | Olson 1965 | Why volunteer platforms see heavy-tailed participation |
| **Iron law of oligarchy** | Michels 1911 | Large organisations → rule by committed minority |
| **Affective polarisation** | Iyengar 2012, Mason 2015 | Group-identity dislike; distinct from issue distance |

---

## Conceptual spine for the lecture

1. **Aggregation rules create supply-side incentives.** Hotelling saw this in 1929.
2. **Bridging-based ranking is a recognisable variant of ideal-point estimation** — political scientists have used the same math since the 1980s.
3. **Display changes the rater distribution** — classical internal-consistency failures are alive on live platforms.
4. **Participation inequality is not a bug, it is the baseline** — predicted by Olson and Verba long before Community Notes existed.
5. **Affective polarisation may be the deeper enemy of bridging** — an open empirical question the papers don't fully address.

---

## Further reading

- Olson, *The Logic of Collective Action* (1965) — foundational for understanding volunteer platforms.
- Verba, Schlozman & Brady, *Voice and Equality* (1995) — empirical participation inequality.
- Wojcik, Hughes & colleagues — original Birdwatch (Community Notes) algorithm paper, 2022.
- Hong & Page 2004 — diversity as epistemic asset; counterweight to consensus-maximisation.

Local:
- [`03_social_choice`](./03_social_choice.html) — full block notes (Part B on Community Notes).
- `papers/social choice/` — PDFs.
