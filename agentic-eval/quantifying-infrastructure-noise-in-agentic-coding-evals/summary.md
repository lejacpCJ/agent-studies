# Summary: Quantifying Infrastructure Noise in Agentic Coding Evals

**Source:** https://www.anthropic.com/engineering/infrastructure-noise

## Core Finding

Infrastructure config alone can swing agentic coding benchmark scores by up to **6 percentage points** — often larger than leaderboard gaps between top models.

## Why Agentic Evals Are Different

Static benchmarks score output only; runtime doesn't matter. Agentic evals give models a live environment (write code, run tests, install deps, iterate). The runtime is now part of the test. Two agents with different resource budgets are not taking the same test.

## The Kubernetes Discovery

Anthropic ran Terminal-Bench 2.0 on GKE. Scores didn't match the official leaderboard. Root cause: their setup set container resource guaranteed allocation = hard kill ceiling. Zero headroom → transient memory spikes OOM-killed containers that would have succeeded. The leaderboard's sandboxing provider allows temporary overallocation, avoiding spurious kills.

## Resource Experiment Results

Ran 6 resource configs from strict 1x to uncapped:

| Range | Effect |
|-------|--------|
| 1x → 3x | Infra errors drop 5.8% → 2.1% (p<0.001). Score lift within noise (p=0.40). Fixes reliability, not capability. |
| 3x → uncapped | Infra errors drop additional 1.6pp, but scores jump ~4pp. Resources now enable new solution strategies. |
| 1x vs uncapped | +6pp total (p<0.01) |

## What This Means for Measurement

- **Below ~3x:** extra resources fix infra reliability. Eval gets more stable, not easier.
- **Above ~3x:** extra resources change what's being measured. Tight limits reward lean/fast code; generous limits reward brute-force heavy-dependency approaches. Both valid tests — but conflating them in one score is misleading.

Example: `bn-fit-modify` (Bayesian network fitting) — some models install full data science stack (fails under tight limits due to OOM during install); others implement math from scratch with stdlib (succeeds either way). Resource config determines which strategy wins.

## Other Variance Sources

- Time of day → API latency fluctuates with traffic
- Cluster health, hardware specs, concurrency, egress bandwidth all confound
- "Model capability" vs "infrastructure behavior" boundary is blurry

## Recommendations

1. Specify **two** resource parameters per task: guaranteed allocation + hard kill ceiling (not a single pinned value)
2. Calibrate the band so scores at floor vs ceiling fall within noise
3. Terminal-Bench example: 3x ceiling over per-task specs → good tradeoff (errors cut by ~2/3, score lift within noise)
4. Report the multiplier used
5. Run evals at multiple times/days to average out noise

## Practical Takeaway

Leaderboard differences **below 3pp** deserve skepticism without documented, matched infrastructure config. Naive binomial CIs already span 1–2pp; infrastructure confounders stack on top. A few-point lead might be a bigger VM, not a better model.
