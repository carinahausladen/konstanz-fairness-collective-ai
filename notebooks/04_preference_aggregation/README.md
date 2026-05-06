# Preference Aggregation Tutorial

Hands-on companion to Week 4 (`docs/04.md` §2). Takes a small toy dataset of seven raters ranking three LLM responses, and runs four classical aggregation rules — **Plurality, Borda, Condorcet, Bradley–Terry–Luce** — to show that the same ratings produce different winners under different rules.

## What's here

```
04_preference_aggregation/
├── aggregation_tutorial.ipynb   main notebook — open this
├── README.md                    this file
└── data/                        downloaded datasets (gitignored)
```

§§1–10 are pure Python (numpy + scipy + matplotlib) on a toy 7-rater dataset. §§12–13 download two real preference datasets from HuggingFace and re-run the same aggregation logic at scale.

```bash
pip install numpy matplotlib scipy datasets huggingface_hub
jupyter notebook aggregation_tutorial.ipynb
```

**Disk usage.** First run of §§12–13 caches the datasets to `data/` (~65 MB for PRISM, ~1.8 GB for Community Alignment). The directory is gitignored.

## Pedagogical arc

1. §1 — RLHF as a voting rule (recap from Week 4 lecture).
2. §2 — A 7-rater × 3-response toy dataset, deliberately constructed so that rules disagree.
3. §3–§6 — Implement Plurality, Borda, Condorcet, BTL from scratch. ~20 lines each.
4. §7–§8 — Side-by-side comparison: same data, different winners.
5. §9 — Condorcet cycle: when pairwise majority breaks down (Arrow in miniature).
6. §10 — Why BTL specifically matters for RLHF.
7. §11 — Dataset overviews (PRISM, Community Alignment) — schema, design, links.
8. §12 — **Live demo on PRISM.** Download utterances, build pairwise wins from cardinal scores, run all four rules, rank the 21 evaluated LLMs. Subgroup analysis by `conversation_type` shows the leaderboard shifts between unguided / values-guided / controversy-guided prompts.
9. §13 — Community Alignment, briefly. Schema is anonymous (response_a/b/c/d), so we demo the country × preferred-position breakdown rather than full model-level aggregation.
10. §14 — Suggested next steps.

## Headline result of the toy example

| Rule          | Winner |
|---------------|--------|
| Plurality     | B (clinical/practical) — 3 first-place votes |
| Borda         | A (warm/emotional)     |
| Condorcet     | A (beats both pairwise) |
| Bradley–Terry | A (highest fitted log-score) |

Plurality picks B because three raters love it; the other four put it dead last. Borda/Condorcet/BTL all reward broad acceptance over peak intensity, and pick A.

The point isn't which rule is "right" — it's that **the choice of rule is normative, not technical**, and standard RLHF silently picks one (BTL).
