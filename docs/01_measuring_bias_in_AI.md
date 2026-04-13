---

## layout: default
title: "Defining and Measuring Fairness in AI"
permalink: /week-01/week-02/

## Agenda

### Introductory Example

Hiring Discirmination in humans and AI and how to measure it.

### 1. Fairness foundations

- fairness definitions
- where bias enters the LLM lifecycle
- biases in NLP tasks
- fairness desiderata

### 2. Fairness metrics

We will review fairness metrics across three categories:

- embedding-based metrics
- probability-based metrics
- generated-text metrics

### 3. Calibration and Uncertainty

Probability-based fairness metrics rely on calibrated predictions: $\Pr(Y = 1 \mid \widehat{p} = p) = p$
If calibration holds overall but differs across demographic groups, this gap is a measurable form of bias.
We distinguish between Aleatoric (irreducible noise) vs. epistemic (uncertainty due to limited data) uncertainty
Underrepresented groups tend to have higher epistemic uncertainty, leading to less reliable predictions. 

### 4. Bias evaluation datasets

We will examine commonly used datasets and evaluation setups for measuring bias:

- counterfactual inputs
- masked tokens (WinoBias)
- unmasked sentence pairs (CrowS-Pairs)
- prompts
- sentence completions (BOLD)
- question answering (BBQ)

### 5. Fairness, causality, and data limitations

We will also discuss the relationship between fairness and causality, including:

- limitations of observational data
- Simpson’s paradox


## 📖 Readings for Presentations
- Bailey, A. H. (2022).  
*Based on billions of words on the internet, people = men.*  
Science Advances.  
[Link](https://www.science.org/doi/full/10.1126/sciadv.abm2463) 🎧 ~32:10 min (1.5× estimated listening time)
- Bai, X., Wang, A., Sucholutsky, I., & Griffiths, T. L. (2025).  
*Explicitly unbiased large language models still form biased associations.*  
Proceedings of the National Academy of Sciences.  
[Link](https://doi.org/10.1073/pnas.2416228122) 🎧 ~20:40 min (1.5× estimated listening time)
- Khan, F. A., Sivakumar, N., Wang, Y. O., Metcalf, K., Camacho, C., & Theobald, B.-J. (2025).
*Investigating intersectional bias in large language models using confidence disparities in coreference resolution.*
Proceedings of COLM 2025.
[Link](https://arxiv.org/abs/2508.07111) 🎧 ~42:00 min (1.5× estimated listening time)
- Eticas.ai (2026)  
  *Auditing an AI-enabled career advisory platform*  
  https://www.eticas.ai/case-studies/auditing-ai-enabled-career-advisory-platform

- [Agentic Misalignment: How LLMs Could Be Insider Threats](https://arxiv.org/abs/2510.05179)

### Technical Background Readings

- Krause, A., & Hübotter, J. (2025).
  *Probabilistic Artificial Intelligence* (ETH Zürich lecture notes), **Chapter 7.4: Calibration** and **Chapter 2.2: Aleatoric and Epistemic Uncertainty**.
  [arXiv:2502.05244](https://arxiv.org/pdf/2502.05244)
  - Gallegos, I. O., Rossi, R. A., Barrow, J., Tanjim, M. M., Kim, S., Dernoncourt, F., Yu, T., Zhang, R., & Ahmed, N. K. (2024).  
  *Bias and fairness in large language models: A survey.*  
  Computational Linguistics, 50(3), 1097–1179.  
  [Link](https://doi.org/10.1162/coli_a_00524) 🎧 ~1:12:48 min (1.5× estimated listening time)
