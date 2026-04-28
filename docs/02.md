---
layout: default
title: "Week 2 — Recap"
permalink: /week2-recap/
---

# Week 2 — Recap

The material follows **Gallegos et al. 2024 — *Bias and Fairness in Large Language Models: A Survey*** as the baseline. 
Reference: [doi:10.1162/coli_a_00524](https://doi.org/10.1162/coli_a_00524) 

---

## 1. Fairness Definitions



**Definition — Group Fairness.** For a model $\mathcal{M}$ with outcome $\widehat{Y} = \mathcal{M}(X;\theta)$ and a set of social groups $\mathbb{G}$, group fairness requires approximate parity — up to $\epsilon$ — of some statistical outcome measure $\mathbb{M}_Y$ conditioned on group membership:

$$\lvert \mathbb{M}_Y(G) - \mathbb{M}_Y(G') \rvert \leq \epsilon$$

The choice of $\mathbb{M}$ is subjective and contextual — accuracy, true positive rate, false positive rate, calibration, and so on. Different choices yield different fairness notions (demographic parity, equalised odds, calibration).

**Definition — Individual Fairness.** Similar individuals should receive similar outcomes. For individuals $x, x' \in V$ and a distance metric $d$:

$$\forall x, x' \in V.\quad D(\mathcal{M}(x), \mathcal{M}(x')) \leq d(x, x')$$

**Counterfactual fairness** (informally): the outcome should not change under a counterfactual change of the protected attribute alone.

**Why both notions matter.** Group fairness is easy to measure but can be satisfied on aggregate while violating it for subgroups with intersectional identities. Individual fairness captures that failure but requires a distance metric on people — and *whose* distance metric? Week 3's An et al. will make the group-vs-subgroup tension empirical.

---

## 2. Social Biases

**Definition (Social Bias).** Disparate treatment or outcomes between social groups that arise from historical and structural power asymmetries. Gallegos splits these into two taxonomic trunks:

### Representational harms

| Harm | Description |
|---|---|
| **Derogatory language** | Pejorative slurs, insults targeting a group |
| **Disparate system performance** | Degraded processing / generation for some groups or dialects (e.g. AAE misclassified as non-English) |
| **Erasure** | Omission or invisibility of a group's language / experiences |
| **Exclusionary norms** | Reinforced normativity of a dominant group (e.g. *"both genders"*) |
| **Misrepresentation** | Non-representative generalisations about a group |
| **Stereotyping** | Generalised, immutable associations (e.g. *Muslim → terrorist*) |
| **Toxicity** | Offensive language that attacks, threatens, or incites |

### Allocational harms

| Harm | Description |
|---|---|
| **Direct discrimination** | Disparate treatment due explicitly to group membership (e.g. LLM-aided resume screening preserving hiring inequities) |
| **Indirect discrimination** | Disparate treatment via facially neutral proxies |

**Why this taxonomy is useful.** Most Week 3 papers can be localised on this map. Bailey, Bai → primarily **stereotyping** and **misrepresentation**. An → primarily **direct discrimination** in a hiring context, with a stereotyping channel. The agentic papers (Hubinger, Lynch, Betley) push past this taxonomy — their failure modes are goal-directed, not representational — which motivates the Week 3 pivot.

---

## 3. Where Bias Enters the LLM Lifecycle

Bias is not a single artefact — it enters at every stage. We walked through the pipeline:

1. **Training data** — the source corpus encodes existing inequities. Bailey 2022 shows PEOPLE = MEN at the level of 630 B web words, *before any model is trained on top*.
2. **Pre-training objective** — next-token prediction rewards majority patterns; what is rare gets underfit.
3. **Fine-tuning / instruction data** — curation choices alter what counts as a "good" answer.
4. **RLHF / preference data** — whose preferences are collected, and how they are aggregated (ties to the Week 4-5 social-choice block).
5. **Prompt formulation** — the same model can produce different bias signals under different prompts (relevant for Bai et al.).
6. **Evaluation choice** — picking a benchmark is picking what you will see.
7. **Deployment context** — downstream use can amplify a small upstream bias into a large allocative harm.

---

## 4. Biases in NLP Tasks

Bias manifests differently task by task. Gallegos's non-exhaustive map:

| Task | Typical bias manifestation |
|---|---|
| **Text generation** | *Local* — next-token likelihoods differ when *man* vs *woman* appears. *Global* — sentiment / toxicity of the full continuation. |
| **Machine translation** | Default to masculine forms in ambiguous source (*I am happy* → *je suis **heureux***). |
| **Information retrieval** | Returns more masculine-associated documents for non-gendered queries. |
| **Question answering** | Relies on stereotypes to answer ambiguous questions (BBQ benchmark). |
| **Natural language inference** | Infers entailment / contradiction from stereotypical pairings rather than logic. |
| **Classification** | Toxicity classifiers mis-flag African-American English as negative more than Standard American English. |


---

## 5. Fairness Desiderata

Operationalising "fair LLM" demands multiple desiderata at once. We surveyed:

- **Invariance** — the output distribution should not depend on the protected attribute in ways not licensed by the task.
- **Equal social-group associations** — no group should be systematically closer (in representation space) to negative-valence attributes.
- **Equal performance** — accuracy / calibration / latency should not differ across groups.
- **Demographic parity** of outputs — equal positive-outcome rates across groups.
- **Equalised odds** — equal TPR *and* FPR across groups.
- **Calibration** — $\Pr(Y=1 \mid \widehat{p}=p) = p$ should hold for each group.


---

## 6. Bias Metrics



| Level | Category | Access required | Notebook |
|---|---|---|---|
| Vector space | **Embedding-based** | Model's hidden representations | [`1_metrics_WEAT.ipynb`](https://github.com/carinahausladen/konstanz-fairness-collective-ai/blob/main/notebooks/bias%20metrics/1_metrics_WEAT.ipynb) |
| Conditional probability | **Probability-based** | Token log-probabilities | [`2_metrics_maskedtoken.ipynb`](https://github.com/carinahausladen/konstanz-fairness-collective-ai/blob/main/notebooks/bias%20metrics/2_metrics_maskedtoken.ipynb) · [`3_metrics_pll.ipynb`](https://github.com/carinahausladen/konstanz-fairness-collective-ai/blob/main/notebooks/bias%20metrics/3_metrics_pll.ipynb) |
| Output text | **Generated text-based** | Only the generated continuations | [`4_metrics_generatedtext.ipynb`](https://github.com/carinahausladen/konstanz-fairness-collective-ai/blob/main/notebooks/bias%20metrics/4_metrics_generatedtext.ipynb) |

### 6.1 Embedding-based — WEAT (notebook 1)

**Idea.** If a model is unbiased, male and female target words should be equally close — in cosine distance — to career and to family attribute words.

For target sets $X, Y$ and attribute sets $A, B$:

$$s(w, A, B) = \underset{a\in A}{\mathrm{mean}}\,\cos(w,a) - \underset{b\in B}{\mathrm{mean}}\,\cos(w,b)$$

$$\text{WEAT} = \sum_{x\in X} s(x,A,B) - \sum_{y\in Y} s(y,A,B)$$

**Strength / weakness.** Cheap, reveals *upstream* associations. But upstream geometry does not guarantee downstream harm — a model may be clean *in outputs* while its embeddings retain a bias signal, or vice versa.

### 6.2 Probability-based — masked-token and PLL (notebooks 2 and 3)

Probability-based metrics use the model's **token-level log-probabilities** rather than its hidden states. Two sub-families:

**6.2.1 Masked Token Metrics**

Fill a `[MASK]` in a template like *"[X] is `[MASK]`"* with `X = he` and then `X = she`. Compare the top-*k* predictions.

We ran DisCo (Webster et al. 2020) across multiple templates. The score measures the overlap (or divergence) between the top-*k* completions conditioned on different gender tokens. A large divergence is evidence of gendered expectations baked into the token distribution.

Related: **LPBS** (Log Probability Bias Score), **CAT** (Category Bias Score), **AUL** (All Unmasked Likelihood).

**6.2.2 Pseudo-Log-Likelihood**

Score entire sentences by how "natural" the model finds them — compare stereotypical vs anti-stereotypical pairs.

For sentence $s$ of length $T$:

$$\mathrm{PLL}(s) = \frac{1}{T}\sum_{t=1}^{T} \log P(s_t \mid s_{\setminus t})$$

A systematic PLL gap across many paired templates is the **CrowS-Pairs / StereoSet** signal.

**Strength / weakness.** Directly probes what the model *would say* (masked-token) or *would score as natural* (PLL). But highly template-sensitive; length and frequency confounds can masquerade as bias.

### 6.3 Generated text-based

When only the model's **outputs** are accessible — no embeddings, no log-probabilities — you score the generated text itself. Two metrics we implemented:

**Toxicity Probability (TP).** Sample $n$ generations from the model; use a toxicity classifier to label each. TP is the empirical probability of at least one generation with toxicity $\geq 0.5$:

$$\mathrm{TP}(\hat{Y}) = P\Big(\textstyle\sum_{\hat{y}\in\hat{Y}} \mathbb{1}[c(\hat{y}) \geq 0.5] \geq 1\Big)$$

TP is a *worst-case* metric — one toxic generation is enough.

Related: **Toxic Fraction (TF)** — the average rather than max-style measure.

**Co-Occurrence Bias Score.** For target terms and demographic groups, count how often they appear together in generated text and compare distributions across groups. Captures *global* bias in generated continuations.

**Strength / weakness.** Closest to deployment behaviour. But judge-dependent (toxicity classifiers are themselves biased) and high variance.

