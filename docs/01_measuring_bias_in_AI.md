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

### 3. Bias evaluation datasets

We will examine commonly used datasets and evaluation setups for measuring bias:

- counterfactual inputs
- masked tokens (WinoBias)
- unmasked sentence pairs (CrowS-Pairs)
- prompts
- sentence completions (BOLD)
- question answering (BBQ)

### 4. Fairness, causality, and data limitations

We will also discuss the relationship between fairness and causality, including:

- limitations of observational data
- Simpson’s paradox

# Auditing a real world AI system 
https://www.eticas.ai/case-studies/auditing-ai-enabled-career-advisory-platform

## 📖 Readings

- Gallegos, I. O., Rossi, R. A., Barrow, J., Tanjim, M. M., Kim, S., Dernoncourt, F., Yu, T., Zhang, R., & Ahmed, N. K. (2024).  
*Bias and fairness in large language models: A survey.*  
Computational Linguistics, 50(3), 1097–1179.  
[Link](https://doi.org/10.1162/coli_a_00524) 🎧 ~1:12:48 min (1.5× estimated listening time)
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

### Technical Background

- Krause, A., & Hübotter, J. (2025).
  *Probabilistic Artificial Intelligence* (ETH Zürich lecture notes), **Chapter 7.4: Calibration** and **Chapter 2.2: Aleatoric and Epistemic Uncertainty**.
  [arXiv:2502.05244](https://arxiv.org/pdf/2502.05244)

  Two sections are worth reading alongside this week's material. **Calibration** (Ch. 7.4) is the technical foundation for probability-based fairness metrics: a model is calibrated if its confidence scores reflect true outcome probabilities. When calibration holds overall but breaks down for specific demographic groups, that gap *is* a bias — and a measurable one. **Aleatoric vs. epistemic uncertainty** (Ch. 2.2) offers a useful diagnostic framing: aleatoric uncertainty is irreducible noise, while epistemic uncertainty reflects lack of data. Models tend to be more epistemically uncertain for underrepresented groups — not by accident, but because they appear less in training data. This reframes poor performance on minority groups as a data representation problem, not just a model flaw.

