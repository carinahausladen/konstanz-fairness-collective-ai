# AI Marketplaces and Aggregation Rules

Companion lab to Week 5 (`docs/05.md` §2 — Donahue & Raghavan). Build a toy AI marketplace where two producers compete for 200 consumers spread across a 1-D taste axis, and run best-response dynamics under two scoring rules:

- **Plain winrate** — producers cluster on one side, abandon the other consumer cluster (Hotelling-on-a-beach).
- **Weighted winrate** — producers split cleanly, one per consumer cluster (Donahue & Raghavan's proposed alternative).

## What's here

```
05a_markets_aggregation/
├── markets_tutorial.ipynb   main notebook — open this
└── README.md                this file
```

Pure-Python, no API key, no internet. Runs in under a minute.

```bash
pip install numpy matplotlib
jupyter notebook markets_tutorial.ipynb
```

## Pedagogical arc

1. §1 — Aggregation rules over producers (recap from Week 5 lecture).
2. §2 — A toy 1-D AI marketplace with bimodal consumer distribution.
3. §3 — Two scoring rules: plain winrate vs. weighted winrate.
4. §4 — Best-response dynamics: each producer grid-searches its position to maximize its score.
5. §5 — Where producers end up: side-by-side trajectory plot.
6. §6 — Consumer welfare CDF: niche consumers under each equilibrium.
7. §7 — Takeaway: a leaderboard is an aggregation rule over producers.
8. §8 — Knobs to turn: more producers, different consumer distributions, custom rules.

## Headline result

| Rule              | Final producer positions | Worst-10% consumer welfare |
|-------------------|--------------------------|----------------------------|
| Plain winrate     | both at ~0.29 (left cluster) | 0.524 |
| Weighted winrate  | 0.29 + 0.71 (one per cluster) | 0.906 |

Same consumers, same starting producers, ten iterations of best response — only the scoring rule changes.
