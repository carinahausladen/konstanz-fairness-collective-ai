---
layout: default
title: "Social Choice and AI Alignment"
permalink: /week-03/
---

# Social Choice for LLM Alignment

Fairness, for whom?

- Motivation: why study preference aggregation and fairness  
- Preference elicitation  
  - What are preferences?  
  - Ordinal vs cardinal preferences  
  - Methods of elicitation (rankings, approvals, ratings)  
- Preference aggregation  
  - From individual to collective choice  
  - Different voting methods (majority, Borda, Condorcet, Approval, STV)  
  - Fairness and proportionality principles  
  - Key properties: monotonicity, quota rules, representation  
- Committee elections  
  - Thiele and Phragmén rules  
  - Examples of proportional representation  
- Participatory budgeting (PB)  
  - PB as generalization of committee elections  
  - Aggregation methods for PB (proportional and cost-aware)  
  - Importance of proportional aggregation  
  - Preference elicitation for PB  
  - Negative voting and PB as a two-step process  
- Human-centered LLMs  
  - Learning from human preferences (RLHF)  
  - Constitutional AI and alignment by written principles  
- Pluralistic alignment

---
## 📖 Readings

- Impacts of Aggregation on Model Diversity and Consumer Utility; https://arxiv.org/abs/2602.23293

- Cultivating Pluralism In Algorithmic Monoculture: The Community Alignment Dataset; https://arxiv.org/abs/2507.09650

- Kirk, H. R., Whitefield, A., Röttger, P., Bean, A., Margatina, K., Mosquera, R., Bartolo, M., Williams, A., He, H., Vidgen, B., & Hale, S. A. (2024).  
  *The PRISM Alignment Dataset: What participatory, representative and individualised human feedback reveals about the subjective and multicultural alignment of large language models.*  
  arXiv preprint.  
  https://arxiv.org/abs/2404.16019 🎧 ~15:40 min (1.5× estimated listening time)

- Zhang, L. H., et al. (2025).  
  *Cultivating pluralism in algorithmic monoculture: The Community Alignment Dataset.*  
  arXiv preprint.  
  https://arxiv.org/abs/2507.09650

- Conitzer, V., Freedman, R., Heitzig, J., Holliday, W. H., Jacobs, B. M., Lambert, N., Mossé, M., Pacuit, E., Russell, S., Schoelkopf, H., & Tewolde, E. (2024).  
  *Social choice should guide AI alignment in dealing with diverse human feedback.*  
  arXiv preprint.  
  [Link](https://arxiv.org/pdf/2404.10271) 🎧 ~29:32 min (1.5× estimated listening time)

- Qiu, T. (2024).  
  *Representative social choice: From learning theory to AI alignment.*  
  arXiv preprint.  
  [Link](https://arxiv.org/abs/2410.23953) 🎧 ~28:26 min (1.5× estimated listening time)


- González Barman, K., Lohse, S., & de Regt, H. W. (2025).  
  *Reinforcement learning from human feedback in LLMs: Whose culture, whose values, whose perspectives?*  
  Philosophy & Technology, 38, 35.  
  [Link](https://doi.org/10.48550/arXiv.2407.17482) 🎧 ~27:17 min (1.5× estimated listening time)


### Optional 

- Yang et al. (2024) — [Link](https://dl.acm.org/doi/full/10.1145/3665332)
- Tasioulas (2022) — [Link](https://direct.mit.edu/daed/article/151/2/232/110615/Artificial-Intelligence-Humanistic-Ethics)



---
## 📊 Project Ideas & Datasets

1. End-to-End Welfare in Multi-Model Ecosystems

Develope an end-to-end view of welfare in AI ecosystems by connecting the supply side and the demand side.
On the supply side, the question is which incentives encourage firms to build differentiated models rather than converging on a homogeneous set of systems.
On the demand side, the question is how a platform, provider, or society should select a menu of models so that overall welfare is high while minority preferences are not ignored.
A possible contribution would be to study how producer incentives and menu-selection rules interact, and whether combining diversity-inducing supply incentives with proportional or welfare-aware selection leads to better outcomes for heterogeneous users.
