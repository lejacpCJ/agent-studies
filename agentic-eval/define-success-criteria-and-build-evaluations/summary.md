# Define success criteria and build evaluations — Summary

**TL;DR:** Effective LLM apps require explicit, measurable success criteria and systematic evaluations — without them, prompt engineering is guesswork.

## Key points

- **SMART criteria:** Success criteria should be Specific, Measurable, Achievable, and Relevant — even fuzzy goals like "safe outputs" must be quantified (e.g., <0.1% toxicity rate across 10k trials).
- **Multidimensional:** Most apps need to evaluate across several axes: task fidelity, consistency, tone, latency, cost, privacy, context utilization.
- **Eval design:** Mirror real task distribution, include edge cases, and favor automated grading (code or LLM-based) over human grading for scale.
- **Volume beats perfection:** Many slightly-noisier automated test cases outperform few hand-graded ones.
- **Grading hierarchy:** Code-based (fastest/rigid) → LLM-based (flexible/scalable) → human (highest quality/slowest). Default to code; use LLM grading for nuanced judgements after validating reliability.
- **LLM grading tips:** Use detailed rubrics, enforce structured outputs (binary/ordinal), and prompt the LLM to reason before scoring — then discard the reasoning.
- **Leverage Claude to scale:** Use Claude to generate additional test cases from a small baseline set.

## Why it matters

Without explicit evals, prompt changes can regress silently and improvements can't be measured. This framework turns LLM development from intuition-driven iteration into a repeatable engineering process.
