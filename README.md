# agent-studies

Personal knowledge base for AI/agentic systems research. Articles saved as markdown with local images, organized by topic.

## Structure

Each article lives in `<topic>/<slug>/src.md` with downloaded images alongside.

Topics:
- [`agentic-eval/`](#agentic-eval) — evaluating AI agents
- [`building-agents/`](#building-agents) — designing and building agentic systems

---

## agentic-eval

| Article | Description |
| --- | --- |
| [Demystifying evals for AI agents](agentic-eval/demystifying-evals-for-ai-agents/src.md) | Anthropic's field-tested guide: eval structure, grader types, coding/conversational/research/computer-use agent evals, pass@k vs pass^k, 8-step roadmap from zero to production evals |
| [Quantifying infrastructure noise in agentic coding evals](agentic-eval/quantifying-infrastructure-noise-in-agentic-coding-evals/src.md) | How infra error rates skew benchmark scores by several percentage points — sometimes more than the gap between top models |

---

## building-agents

| Article | Description |
| --- | --- |
| [Building effective agents](building-agents/building-effective-agents/src.md) | Anthropic's guide: workflows vs agents, five workflow patterns (chaining/routing/parallelization/orchestrator-workers/evaluator-optimizer), when to use autonomous agents, tool design as ACI, start simple |
