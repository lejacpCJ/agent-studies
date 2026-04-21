Start simple, add complexity only when it demonstrably improves outcomes — that is the core thesis of Anthropic's guide to building effective agents.

**Key points:**

- **Workflows vs. agents**: Workflows use predefined code paths; agents let LLMs dynamically direct their own tool use. Both are "agentic systems" but warrant different design approaches.
- **Five workflow patterns**: prompt chaining, routing, parallelization, orchestrator-workers, and evaluator-optimizer — each suited to distinct task structures.
- **Agents for open-ended tasks**: Use agents when steps can't be predicted upfront and you need model-driven decision-making. Accept the tradeoff: higher cost, compounding error risk.
- **Frameworks help but obscure**: Start with raw LLM API calls; frameworks add abstraction that hides prompts and makes debugging harder.
- **Tool design = prompt engineering**: The agent-computer interface (ACI) deserves as much attention as the system prompt — clear parameter names, good docstrings, absolute paths over relative, poka-yoke constraints.
- **Three principles**: simplicity in design, transparency in planning steps, rigorous tool documentation and testing.

**Why it matters:** Most agentic failures stem from over-engineering, not under-powering. This guide gives a concrete vocabulary (the five patterns) and a decision framework for when to escalate complexity, grounded in production deployments across dozens of teams.
