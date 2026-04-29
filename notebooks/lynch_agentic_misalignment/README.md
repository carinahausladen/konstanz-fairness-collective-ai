# Lynch et al. 2025 — Agentic Misalignment tutorial

A from-scratch reconstruction of the canonical *SummitBridge / Alex / Kyle Johnson* blackmail vignette from Lynch et al., *Agentic Misalignment: How LLMs Could Be Insider Threats* (arXiv:2510.05179).

The point is pedagogical: students see every component (system prompt, inbox, tool, model output) in isolated cells, then run four ablations to watch how each variable changes the outcome.

## What's here

```
lynch_agentic_misalignment/
├── lynch_tutorial.ipynb     main notebook — open this
├── system_prompt.md         the "Alex" agent's instructions
├── emails/                  7 inbox messages assembled into the canonical scenario
├── transcripts/             cached API responses, .json + .md per condition
└── README.md                this file
```

## Two ways to run it

The notebook has a toggle near the top:

```python
USE_LIVE_API = False    # cache-only mode
USE_LIVE_API = True     # hit the OpenAI API
```

**Cache-only mode (default).** Reads pre-recorded transcripts from `transcripts/`. No API key needed. Use this if you don't have an OpenAI key, or to read through the notebook without spending credits.

**Live mode.** Set `USE_LIVE_API = True`, export your key, and re-run any cell. The runner saves both `transcripts/{condition}.json` (full structure) and `transcripts/{condition}.md` (human-readable).

```bash
pip install openai matplotlib jupyter
export OPENAI_API_KEY=...
jupyter notebook lynch_tutorial.ipynb
```

Default model is `gpt-4.1` — the same OpenAI model Lynch tested directly (80% blackmail rate on the canonical condition). Swap `MODEL` in the §5 toggle cell to try `gpt-4o` or `gpt-5`.

## Recording the cached transcripts

To populate `transcripts/` for students:

1. `export OPENAI_API_KEY=...`
2. Open the notebook, set `USE_LIVE_API = True`.
3. Run all cells. Four conditions × ~2k tokens each ≈ a few cents on `gpt-4.1`.
4. Set `USE_LIVE_API = False`, restart the kernel, run all cells. Confirm the cached transcripts read back cleanly.
5. Commit `transcripts/*.json` and `transcripts/*.md`.

## Original source

Lynch et al. open-sourced the full harness — 16 models, thousands of samples, dozens of permutations — at:
https://github.com/anthropic-experimental/agentic-misalignment

This notebook is the deliberately-stripped-down classroom version. The real harness is what to point students at after they've understood the mechanism here.

## Disclaimers

All names and emails are fictional, taken from the paper's controlled simulation. The scenario depicts an extramarital affair and a blackmail attempt. Cached transcripts let students read the notebook through without making API calls if they prefer.
