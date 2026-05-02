# Composite Multi-Component Reward Functions for Tool-Using LLM Orchestrators: A 16-Trace Characterisation

A four-component composite reward function for tool-using LLM orchestrators (correctness 0.40, efficiency 0.20, cost 0.20, quality 0.20), characterised on a 16-trace held-out evaluation log over four production tools (octra, falcon, prisma, firecrawl_search) and designed as a turn-key `reward_funcs` argument for GRPO training of a Qwen2.5 orchestrator policy.

## Paper

- PDF: [tex/main.pdf](tex/main.pdf)
- Source: [tex/main.tex](tex/main.tex), bibliography [tex/references.bib](tex/references.bib).
- Compile with `tectonic -X compile tex/main.tex` (or `pdflatex` 3 times + `bibtex`).

## Primary result

Mean composite reward 7.64/10 (range 6.50 to 8.86) across 16 traces. Reward is monotone in tool-call count: 8.75/10 at the two-call budget, declining to 6.53/10 at five calls. Three named failure modes (repeated falcon, failed prisma chart, empty result sets) leave distinct fingerprints across the four reward components.

## Figures

| Figure | Description |
| --- | --- |
| fig-architecture.png | End-to-end orchestrator-reward pipeline. |
| fig-reward-formula.png | 40/20/20/20 weighting and the four sub-reward definitions. |
| fig-reward-components.png | Per-component mean scores across the 16-trace evaluation. |
| fig-score-by-calls.png | Composite reward by tool-call count (peaks at the 2-call budget). |
| fig-cost-vs-score.png | Per-trace composite score vs realised dollar cost, coloured by tool-call count. |
| fig-failure-modes.png | Per-component point drop attributable to each of the three failure modes. |

## How to reproduce

The evaluation pool is the 16-trace `conversation-sample.json` log distributed alongside the orchestrator-reward Python package. The package itself is at https://github.com/rushitparmar-lab/eval and the orchestrator policy at https://github.com/rushitparmar-lab/rl-tool-router. Reproducing every number in the paper amounts to running `python run_tests.py` followed by `python example_usage.py` against the frozen evaluation log; SHA-256-keyed SQLite caching makes the run bit-for-bit deterministic.

## Recommended venues

- NeurIPS Workshop on Foundation Models for Decision Making (FM4DM) - strong stylistic fit for reward-design papers on tool-using LLM agents.
- ICLR Workshop on Agentic AI - workshop track values careful instrument papers.
- COLM 2026/2027 - mid-tier conference accepting RL/RLHF and evaluation-harness papers.
- TMLR - rolling submission, technical-correctness-first review.
- JAIR - archival journal with a strong agent-evaluation tradition.

See `state.delivery.recommended_venues` for the full rationale.

## Authors

Rushit Parmar.

## Provenance

Session id: `20260502-023040-6b22`. Audit trail in [log.md](log.md), full state snapshot in [state.json](state.json), peer review of the sealed PDF in [review.md](review.md).
