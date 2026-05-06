# Bridging-Based Ranking and its Failure Modes

Companion lab to Week 5 (`docs/05.md` §3 and §4 — Chuai et al. and Nudo et al.). Build a small synthetic Community Notes simulation, implement the bridging matrix factorisation from scratch, and run two experiments that expose what classical aggregation theory assumes silently and is empirically false.

## What's here

```
05b_community_notes/
├── community_notes_tutorial.ipynb   main notebook — open this
└── README.md                        this file
```

Pure-Python (numpy + scipy + matplotlib), no API key, no internet. Runs in under a minute.

```bash
pip install numpy scipy matplotlib
jupyter notebook community_notes_tutorial.ipynb
```

## Pedagogical arc

1. §1 — The bridging algorithm in one paragraph.
2. §2 — Synthetic Community Notes setup (200 raters × 60 notes with hidden polarity + quality).
3. §3 — Implement bridging matrix factorisation by L-BFGS in ~20 lines.
4. §4 — Initial display: which notes pass the threshold? (Visualise β vs δ.)
5. §5 — **Experiment A (Chuai)**: simulate display by adding polarised raters, refit, watch helpful-status erode.
6. §6 — **Experiment B (Nudo)**: heavy-tailed activity that's politically asymmetric — empirical characterisation.
7. §7 — Takeaway: the two assumptions of classical voting theory that deployment violates.

## What the toy reproduces — and what it doesn't

- **Chuai's 30 % loss-of-helpful-status** is reproduced *in direction* (≈ 10 %) but not in magnitude. Bridging is robust by design — the polarity term $\gamma_u \cdot \delta_n$ absorbs partisan disagreement. The real-data magnitude requires factors the toy doesn't model: time dynamics, fixed calibrated thresholds, multidimensional polarity, partisan asymmetry in which notes attract post-display attention.
- **Nudo's heavy-tailed + politically-asymmetric activity** is reproduced cleanly: the top 5 % of raters by activity account for ~35 % of all ratings *and* sit visibly to one side of the polarity distribution. The lesson — that the *effective* rater pool is non-representative — is the right one even at toy scale.

## What students see

| | Toy result | Real-data finding |
|---|---|---|
| Chuai — helpful notes lose status post-display | 8 % | 30.2 % |
| Nudo — activity concentration | top 5 % → 35 % of ratings | heavy-tailed |
| Nudo — top-5 % polarity asymmetry | mean +0.5 vs +0.0 in full pool | politically selective |

The honest framing in the notebook: bridging is an excellent algorithm; *deployment* is what breaks it. Both papers expose generic deployment conditions that any algorithmic aggregator faces.
