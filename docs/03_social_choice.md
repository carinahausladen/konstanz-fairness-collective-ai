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

1. Aggregation and alignment preferences (PRISM dataset, Community Alignment Dataset)
One direction would be to study alignment preferences using the PRISM dataset and compare different aggregation methods (e.g., majority voting, proportional or group-balanced aggregation). A key contribution would be to analyze how these aggregation choices affect outcomes across sociodemographic groups.

https://huggingface.co/datasets/HannahRoseKirk/prism-alignment

2. Aggregation under polarization (X Community Notes)
Another direction would be to study X’s Community Notes system, which is consensus-oriented: when ratings are polarized, notes tend to disappear. Using the publicly available Community Notes data, one could evaluate alternative aggregation methods and examine how they affect note visibility and stability under polarization.

https://github.com/twitter/communitynotes  
https://communitynotes.x.com/guide/en/under-the-hood/download-data

Related Paper: 
https://arxiv.org/abs/2510.12559
https://arxiv.org/abs/2509.09956
https://arxiv.org/abs/2502.13322

