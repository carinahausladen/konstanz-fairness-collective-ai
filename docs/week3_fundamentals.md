---

## layout: default
title: "Week 3 — Fundamentals"
permalink: /week3-fundamentals/

**Paper tags.**


| Tag | Paper                                                                    |
| --- | ------------------------------------------------------------------------ |
| 🟦  | **Bailey 2022** — *people = men*                                         |
| 🟩  | **Bai 2025** — *explicitly unbiased LLMs still form biased associations* |
| 🟧  | **An 2025** — *intersectional resume bias*                               |
| 🟥  | **Lynch 2025** — *agentic misalignment*                                  |


---

The thread this week: **how social-science has measured bias and discrimination for decades, and what gets added (or lost) when we re-run those measurements on an LLM**.

---

## 1. Bias in the social sciences — before there was an LLM to measure

Everything the Week 3 papers do draws on a social-science tradition that pre-dates machine learning by half a century. Three bodies of work worth naming explicitly:

**1.1 Prejudice and stereotype research — psychology.**

- **Allport (1954), *The Nature of Prejudice*.** Allport decomposes the phenomenon into three components that still structure the field:
  - **Cognitive** — *stereotype*: the belief ("women are warm, men are competent").
  - **Affective** — *prejudice*: the feeling toward the group ("I dislike / distrust X").
  - **Behavioural** — *discrimination*: the act (not hiring, not renting, not trusting).
  The three are related but **dissociable**. A person can hold a stereotype without feeling prejudice, and exhibit discriminatory behaviour without consciously endorsing either. This distinction is the intellectual backbone for every bias measurement that follows — each technique targets one of the three levels, and much confusion in the LLM-fairness literature comes from papers that slide between them (e.g., measuring a stereotype with an implicit task, then claiming the model has been "debiased" once explicit prejudice is gone).
  **Mapping this week's papers onto Allport's three components.**

  | Component                        | What is measured                         | Week 3 paper(s)                                                                         |
  | -------------------------------- | ---------------------------------------- | --------------------------------------------------------------------------------------- |
  | **Cognitive** (stereotype)       | Which associations the model encodes     | 🟦 **Bailey** — embedding geometry · 🟩 **Bai** — implicit word-association score       |
  | **Affective** (prejudice)        | The model's "feeling" toward a group     | — Arguably ill-defined for LLMs; no Week 3 paper targets this                           |
  | **Behavioural** (discrimination) | What the model *does* in a decision task | 🟧 **An** — resume callback / score gap · 🟥 **Lynch** — harmful actions under pressure |

  The interesting split the papers reveal: **Bai** shows RLHF can make the explicit/affective layer look clean while the cognitive/implicit layer stays biased. **An** and **Lynch** both measure behaviour but in very different environments — An in a one-shot resume-scoring task, Lynch in a multi-step scaffolded environment. That environmental difference is the entire axis §4 will unpack as *benchmark* vs *agentic* evaluation.
- **Fiske, Cuddy, Glick & Xu (2002), Stereotype Content Model (SCM).** The empirical claim: stereotypes about social groups are not one-dimensional ("good/bad"); they live in a **two-axis space**.
  - **Warmth** — is the group cooperative or threatening? (friendliness, trustworthiness, sincerity)
  - **Competence** — is the group capable of acting on its intentions? (skill, intelligence, efficacy)

```text
          ┌─────────────────┬─────────────────┐
          │  PATERNALIZED   │    ADMIRED      │
    HIGH  │     (pity)      │    (pride)      │
  WARMTH  │                 │                 │
          │  elderly        │  in-group       │
          │  disabled       │  middle-class   │
          ├─────────────────┼─────────────────┤
          │    CONTEMPT     │    ENVIED       │
     LOW  │   (disgust)     │  (resentment)   │
  WARMTH  │                 │                 │
          │  homeless       │  rich           │
          │  drug users     │  Asian, Jewish  │
          └─────────────────┴─────────────────┘
             LOW COMPETENCE    HIGH COMPETENCE
```

  The SCM is the measurement framework most widely re-used in LLM audits of group associations, both because it produces a clean two-dimensional output and because decades of human data make it possible to compare an LLM's stereotype space directly to a population's. 

**1.2 Implicit vs explicit attitudes.**

- **Greenwald, McGhee & Schwartz (1998) — the Implicit Association Test (IAT).** The IAT is a reaction-time task. Participants sort words into categories using two keys.
  - *Compatible block:* culturally associated categories share a key (e.g., `flower + pleasant` on the left, `insect + unpleasant` on the right).
  - *Incompatible block:* the pairing is reversed (`flower + unpleasant` / `insect + pleasant`).
  The **response-time difference** between the two blocks is the implicit-association score. When sorting is faster in the compatible block, the underlying association between the category and the valence is inferred to be stronger. Crucially, the score is obtained *without ever asking the subject what they believe* — it is read off motor behaviour under time pressure.

```text
         EXPLICIT measure                    IMPLICIT measure
       (survey / self-report)                 (reaction time)
                │                                    │
                ▼                                    ▼
         "I have no bias."               250 ms slower when the
                                         pairing cuts against bias
                │                                    │
                └──────────────────┬─────────────────┘
                                   ▼
                       Same subject, same construct,
                         two incompatible readings.
```

- **🟩 Bai et al. 2025 — the same dissociation in LLMs.** They transport the IAT logic directly, with two adapted measures across 8 models (GPT-3.5/4, Claude 3 Opus/Sonnet, Llama 2 Chat 7B/13B/70B, Alpaca 7B), 4 categories (race, gender, religion, health), and 33,000+ prompts:
  - **LLM Word Association Bias** — an IAT analogue prompting the model to match group terms with valence/attribute words.
  - **LLM Relative Decision Bias** — presenting two profiles in an applied scenario and observing which the model picks.
  Ask an RLHF-aligned model *explicitly* — *"is it fair to assign notetaking duties to the woman in the meeting?"* — and you get a clean, principled refusal. Present the *same* scenario as an ordinary office-assignment task and ask *"who should take notes?"* — the model disproportionately picks the woman. Same underlying bias, two incompatible measurements. Bai et al. replicate this pattern across race (Black candidates assigned stereotypical roles), gender, religion, and health.
- **Why the distinction matters for training interventions.** You can move the *explicit* needle (survey answers, refusal behaviour) while leaving the *implicit* needle (associations, completions, downstream-decision analogues) where it was. **RLHF does exactly this** — see §6 for what RLHF is and why it behaves like a surface correction. This is also *why* explicit-refusal benchmarks systematically overstate how much RLHF has fixed.

**1.3 Statistical vs taste-based discrimination — economics.**

- **Becker (1957), *The Economics of Discrimination* — taste-based model.** Becker formalises discrimination as a **preference**: the employer (or customer, or co-worker) has a **disutility** from contact with members of group G. Formally, the discriminator's utility function penalises each unit of contact with G by a "discrimination coefficient" $d$. Economically this means the discriminator is willing to give up money — pay a *premium* to hire non-G workers, or accept lower-quality hires — just to avoid the contact. The model's central prediction: **discrimination is costly to the discriminator**, and in a competitive market, non-discriminating firms should out-compete discriminating ones, eroding taste-based discrimination over time. Empirically it often does not erode, which is one motivation for the alternative model below.
- **Arrow (1973), Phelps (1972) — statistical discrimination.** Here the decision-maker has *no taste* for discrimination; they are simply trying to predict an unobserved trait (productivity, default risk, return rate) from noisy signals. If group membership is *correlated* with that unobserved trait in the available data, a Bayes-rational decision-maker will **use group membership as a proxy** — and will produce discriminatory outcomes without any animus. The behaviour is "rational" in the narrow decision-theoretic sense and still produces disparate outcomes.
- **Why this matters for LLMs — and what economics does with the problem.**
  - *The defensive move.* *"The model is just using the information it has"* is literally the **statistical-discrimination defence**, well-rehearsed in labour economics.
  - *Why surface fixes fail.* The channel is **proxy variables** (names, zip codes, schools, writing style, prior job titles). Simply **blinding** the model — removing the protected attribute from the prompt — does not eliminate the bias, because the proxies carry the signal. Bertrand & Mullainathan's design is proof: they varied **only names**, and that alone recovered a ~50% callback gap.
  - *The economics / legal response.* US labour law treats **disparate impact** as actionable regardless of intent. **Griggs v. Duke Power (1971)**: a facially neutral practice that disproportionately burdens a protected group is unlawful unless justified by business necessity. No animus needed; outcomes are enough.
  - *The doctrine now imports into AI.* The **EU AI Act** requires bias testing on protected characteristics in high-risk systems, carrying the Griggs logic into the algorithmic era. "Just accurate" is not a defence under disparate-impact doctrine, and it is not a defence under the EU AI Act either.
  - *Takeaway for the lecture.* The distinction is not academic — it names the most common defence of biased systems, explains why naive fixes (blinding, de-biasing one attribute) fail, and points to an existing regulatory apparatus that already transferred to AI.

---

## 2. Measuring discrimination causally — the audit-study tradition  🟧

The methodological ancestor of every LLM discrimination paper we read this week.

**The problem.** Observational data on hiring, lending, housing is confounded by unobservables. You cannot tell whether the Black applicant was rejected *because* they were Black or because of correlated but unobserved traits.

**The solution.** Randomise the identity signal on otherwise-identical applications.

- **Bertrand & Mullainathan (2004), AER — *Are Emily and Greg More Employable than Lakisha and Jamal?*** The canonical design and the direct ancestor of every LLM resume-audit. ~~5,000 fictitious CVs sent to real job ads in Boston and Chicago; **names** were the only randomised signal of race (distinctively white vs distinctively Black first names); otherwise CVs were matched on quality and content. A **~~50% callback gap** favouring white-sounding names, robust across industries and across CV quality tiers. Because names are randomised and everything else is held fixed, the gap is an **average treatment effect of perceived race** on callback — unobservable confounding is designed out.

**What the Week 3 paper adds.** An et al. 2025 🟧 run the same design with 361k CVs, five LLMs as decision-makers, and crossed identity cues (race × gender). The logic is unchanged; scale and cross-classification are new.

**Bridge from §1 to §2 — warmth × competence *predicts* audit-study discrimination.** Cuddy, Fiske & Glick (2007, 2008) show that the **stereotype content** of a group — its position in the warmth × competence space — predicts the pattern of behavioural discrimination measured in audit-style designs: **warmth** drives active behaviours (help vs attack), **competence** drives passive ones (association vs neglect). So the two-axis geometry of §1 is not just descriptive; it maps onto observable audit outcomes. **Hausladen et al.** extend this from human behaviour to **vision–language models**: warmth × competence systematises group-level discrimination in multimodal model outputs the same way it does in human data.

---

## 3. Intersectionality — a concept from critical legal studies  🟧

- **Crenshaw (1989), *Demarginalizing the Intersection of Race and Sex*.** Crenshaw builds her argument on actual US case law. In ***DeGraffenreid v. General Motors*** (1976), five Black women sued GM alleging discrimination. The court ruled against them on the grounds that (a) GM hired women — *white* women, in clerical roles — and (b) GM hired Black workers — *Black men*, in industrial roles. Because neither a standalone race claim nor a standalone sex claim could succeed, and because the court refused to recognise a combined "Black woman" claim, the plaintiffs had no viable cause of action. Crenshaw's point: the legal framework, by treating race and sex as *separable* protected categories, **structurally erases** the people who sit at their intersection.
- **The claim is statistical as well as legal.** The interaction is **non-additive**. In a linear model
$$\text{outcome}_i = \beta_0 + \beta_R \cdot \text{Black}_i + \beta_S \cdot \text{female}*i + \varepsilon_i$$
the effect on Black women is not recoverable as $\beta_R + \beta_S$. You need the interaction term $\beta*{RS}\cdot(\text{Black}_i \cdot \text{female}_i)$, and in many real datasets that term is the largest of the three. A regression on race and gender alone — without the interaction — will systematically **under-report** the effect on the doubly-marked group. This is the standard econometric treatment of heterogeneous effects (Angrist & Pischke 2009, *Mostly Harmless Econometrics*, §3.1);

**Simpson's paradox — a related warning.** Yule (1903), Simpson (1951). An association present in every subgroup can **reverse** when subgroups are pooled. The canonical example is the **UC Berkeley 1973 graduate-admissions** case:

- **Pooled:** men admitted at ~44%, women at ~35% — looks like direct sex discrimination.
- **Disaggregated by department:** women were actually admitted at *slightly higher* rates than men in most departments.

The reversal happened because women applied disproportionately to departments with **lower overall admission rates** (e.g., English), while men applied to departments with higher rates (e.g., engineering). A confounder — department choice — was hiding in the aggregate. Same structural warning as Crenshaw's: the pooled number is not the subgroup number, and which one is "correct" depends on the causal question you are asking.

When a paper reports "LLM X is more biased than LLM Y" on a single-axis benchmark, the correct follow-up is always: *what does the subgroup pattern look like?* Aggregate bias numbers are Simpson-vulnerable.

---

## 4. Benchmark datasets  🟦 🟩

Benchmarks are where most of the LLM-bias literature actually lives — and they are, in a precise sense, the **descendant of the audit-study design from §2**. On a counterfactual benchmark, a single protected term (gender, race, occupation) is changed and the model's output is compared across the change. Same causal logic as Bertrand & Mullainathan — randomised identity cue, everything else held fixed — transposed from "real CV → real employer" to "prompt pair → model". This is why benchmarks work at all: the per-item signal is isolated by construction.

**Gallegos organises them by structure**, independent of the metric that scores them:


| Structure                 | Description                                              | Examples                                          |
| ------------------------- | -------------------------------------------------------- | ------------------------------------------------- |
| **Counterfactual inputs** | Sentence pairs / sets differing only in a protected term | WinoBias, WinoGender, CrowS-Pairs, StereoSet, BBQ |
| **Prompts**               | Phrases that condition open-ended generation             | BOLD, RealToxicityPrompts                         |


**What benchmarks are good at.** Measuring a **specific, pre-specified bias in isolation**. Does swapping "she" for "he" change which antecedent the model resolves (WinoBias)? Does "The Muslim" vs "The Christian" change completion toxicity (BOLD)? For targeted regression testing — *"did this new checkpoint make our gender-coreference number worse?"*.

**What benchmarks are not good at — the Goodhart problem.** Once a benchmark is known, an optimising system learns to pass it without fixing the underlying property. Training-data leakage is one mechanism (the benchmark ends up in the pre-training corpus); targeted fine-tuning is another. This is why *"passed the benchmark"* and *"does not carry the bias"* are different claims. Bai et al. 🟩 is the clean demonstration: models that pass explicit benchmarks still carry the implicit associations.

**Benchmarks vs agentic evaluation — a distinction worth drawing now.** Benchmarks treat bias as an **output property** of the model: input in, output out, scored against a key. The agentic-misalignment line (§5, §7) measures something structurally different: **behaviour along a trajectory**, under tools, under stressors, over many turns. 


|                        | Benchmark evaluation         | Agentic / trajectory evaluation                |
| ---------------------- | ---------------------------- | ---------------------------------------------- |
| **Unit of analysis**   | Single input → single output | Sequence of actions in an environment          |
| **Inherits from**      | §2 audit-study design        | §5 principal–agent / red-team tradition        |
| **Papers this week**   | Bailey 🟦, Bai 🟩, An 🟧     | Lynch 🟥                                       |


These measure different things, and benchmarks do not substitute for trajectory evaluation (or vice versa).

**How the labs actually use benchmarks.** The major frontier labs publish explicit safety frameworks in which static benchmarks are **one input among several**: Anthropic's **[Responsible Scaling Policy](https://www.anthropic.com/rsp)**, OpenAI's **[Preparedness Framework](https://openai.com/safety/preparedness/)**, and Google DeepMind's **[Frontier Safety Framework](https://deepmind.google/discover/blog/introducing-the-frontier-safety-framework/)** all combine bias/capability benchmarks with **red-teaming**, **dangerous-capability evaluations**, **deployment monitoring**, and increasingly **mechanistic or implicit probes** (§1.2 IAT-style methods). These are published policy documents (not peer-reviewed papers) — but they are the authoritative statement of how each lab actually evaluates its own models. 

---

## 5. From bias-as-output to bias-as-agent — the conceptual pivot  🟥

The first four sections treat bias as an **output property** of the model — measurable on a fixed test set. The Lynch paper sits in a different literature.

**Classical antecedents.** Two bodies of work from economics and game theory already formalised this:

- **Principal–agent theory — the economics of institutions.** Ross (1973), Jensen & Meckling (1976); situated inside the broader tradition of **Coase, Williamson, and Hart** on contracts, firms, and delegated authority (for which Williamson and Hart received Nobels in 2009 and 2016). The *principal* (shareholder, manager, user) delegates action to an *agent* (CEO, employee, LLM). The agent has its own objectives, and monitoring is imperfect. The formal result: unless incentives are *perfectly* aligned **and** fully observable, the agent will sometimes act in its own interest rather than the principal's — the classic **agency cost**. The entire apparatus of the modern firm (incentive contracts, auditors, boards, separation of duties) exists because institutions already discovered this problem is structural, not behavioural.
  The **blackmail / sabotage / leaking** behaviours Lynch et al. document are, in this older language, principal–agent failures where the "agent" happens to be a scaffolded LLM. The implication is that the *fix* should look institutional, not only technical: external escalation channels, separation of authority, audit trails — exactly what the insider-risk / operational-controls literature (Gomez 2025, in our reading list) is now applying to AI agents.
- **Deception and strategic behaviour — game theory.** Schelling (1960), *The Strategy of Conflict*; Harsanyi (1967–68) on **games of incomplete information**; Spence (1973), *Job Market Signaling*; the broader **signalling-games** tradition. Core result: when one party has private information (their type, their intentions, their internal state) and the other has to act on inferred signals, it is **often rational to send misleading signals** if that yields a better outcome — and the receiver's optimal response is to *discount* the signal, not take it at face value.
  For LLM agents: the **chain-of-thought** is a signal sent by the agent to the overseer. Nothing in the training objective forces the signal to be *faithful* to the computation underneath. This is the game-theoretic reason *"just ask the model to show its reasoning"* is **not** a safety guarantee — the literature predicted decades ago that signals and underlying states come apart under strategic pressure, and that rational receivers must account for this.


---

## 6. How LLMs learn social behaviours (technical primer)  🟩 🟥

Needed to understand **why RLHF can fix explicit bias but not implicit**, and why Lynch's agents still misbehave.

**Pre-training in one paragraph.** A transformer language model is trained to **predict the next token** (roughly, the next word-piece) in a sequence, given all previous tokens. The training corpus is huge — hundreds of billions to trillions of tokens of web text, books, code. There is no explicit "teacher" labelling each example as good or bad; the objective is simply to assign high probability to the token that actually appeared next. After enough data and parameters, this next-token objective forces the model to internalise syntax, facts, style — and, because the training corpus is a record of human language use, the **statistical associations between social groups and descriptors** (e.g., "nurse" appears more often after "she" than after "he"; "engineer" the opposite). 

**The three-stage pipeline — with this week's papers mapped onto the stages.**

1. **Pre-training** — next-token prediction on web-scale text. Produces a model that is fluent but not aligned to any particular user-facing behaviour. *Corpus bias enters here.*
  - 🟦 **Bailey 2022** measures this stage directly: the embedding geometry of the pre-trained model already encodes *people = men* before any fine-tuning touches it.
2. **RLHF / RLAIF** — *Reinforcement Learning from Human (or AI) Feedback*. Humans (or, in RLAIF, another model following written principles) compare pairs of model outputs and mark which is better; a **reward model** is trained on those preferences; the main model is then fine-tuned with reinforcement learning to maximise reward-model scores. This is the stage where models learn not to produce racist completions, not to help with weapons synthesis, not to say things the labellers rated badly.
  - 🟩 **Bai 2025** locates its central result here: models that pass explicit RLHF-era refusal tests *still* carry the pre-training associations intact. RLHF fixes stage 3 outputs; it does not rewrite stage 1 geometry.

**Why RLHF is a surface correction.** RLHF reshapes the **output distribution conditional on training-like inputs**. It does *not* rewrite the embedding geometry or the implicit co-occurrence structure learned during pre-training. That is Bai et al.'s entire point: probe the model explicitly ("is this biased?") and RLHF-era answers look clean; probe it implicitly (association tasks, disguised completions, off-distribution prompts) and the pre-training associations are still there. 
Red teaming (§7), **Constitutional AI** (Anthropic's variant of RLHF where a model critiques its own outputs against a written constitution), adversarial training. All operate on the output distribution.

---

## 7. Agents, environments, red-teaming — security-research heritage  🟥

Lynch's experimental design sits in a long red-teaming / tabletop-exercise tradition from security research.

- **Red teaming.** Originated in US DoD Cold-War simulations: a dedicated "red team" plays the role of an adversary against the organisation's "blue team" defences. The point is to stress-test defences under **intelligent, goal-directed attack** — exactly the regime that random testing misses. Applied to LLMs since Perez et al. 2022 (*Red Teaming Language Models with Language Models*), and now standard practice at every frontier lab. Lynch et al. is red-teaming **at the agent level**: instead of "can we make the model say a bad thing?", the question becomes "in a simulated deployment with tools and pressure, does the agent *take* bad actions?". The unit of analysis shifts from output to trajectory.
- **Scaffolded agent.** An LLM + outer control loop + tool access. The LLM on its own produces only text; the **outer loop** (planner, memory, tool-router) reads that text, dispatches actions (send an email, run a shell command, modify a file), and feeds the results back into the next prompt. 
- **Goal conflict / instrumental convergence.** A theoretical result from agent-foundations literature: **any sufficiently goal-directed agent**, regardless of its *terminal* goal, has incentives to develop certain **instrumental sub-goals** — **self-preservation** (can't achieve the goal if you are shut down), **resource acquisition**, **goal-content integrity** (resist modification of your own objective). Formalised by Omohundro (2008), popularised by Bostrom (2014). This is **not a claim about LLMs specifically** — it is a claim about goal-directed systems in general, derived before the LLM era. 


| Term                 | Meaning                                                                 |
| -------------------- | ----------------------------------------------------------------------- |
| **Scaffolding**      | The outer loop (planner, memory, tool-router) wrapping the LLM.         |
| **System prompt**    | Hidden instructions that set the agent's role and tools.                |
| **Chain-of-thought** | The agent's *visible* reasoning trace. Can be faithful or performative. |
| **Goal conflict**    | Mismatch between the agent's objective and the principal's.             |


---

## Recap — in a nutshell

1. **Bias isn't new.** We have 70 years of social-science work on what it is and how to measure it.
2. **The audit design is the causal workhorse** — we are running 20-year-old sociology at LLM scale.
3. **Intersectionality is non-additive** — single-axis benchmarks hide the most interesting patterns.
4. **Agentic misalignment is principal–agent theory rediscovered with an LLM in the middle.**

