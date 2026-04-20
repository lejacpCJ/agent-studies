# Summary: Demystifying evals for AI agents

> Source: [src.md](src.md) — Anthropic Engineering, Jan 2026

## Core argument

Evals compound in value over an agent's lifecycle. Teams without them react to production failures blind. Teams with them ship faster, adopt new models in days not weeks, and turn failures directly into test cases.

## Key definitions

| Term | Meaning |
| --- | --- |
| **Task** | Single test with defined inputs + success criteria |
| **Trial** | One attempt at a task (run multiple for consistency) |
| **Grader** | Logic that scores agent output — code, model, or human |
| **Transcript** | Full record of a trial (all API calls + responses) |
| **Outcome** | Final environment state, not what the agent said |
| **Eval harness** | Infrastructure running evals end-to-end |
| **Agent harness** | System enabling model to act as agent (scaffold) |

## Three grader types

- **Code-based** — fast, cheap, deterministic; brittle to valid variations
- **Model-based** — flexible, handles nuance; needs calibration against humans
- **Human** — gold standard; slow and expensive, use for calibration

Grade what the agent *produced*, not the path it took. Build partial credit for multi-component tasks.

## Agent type eval strategies

| Agent type | Primary grader | Key challenge |
| --- | --- | --- |
| Coding | Unit tests (pass/fail) | Deterministic but grade transcript too |
| Conversational | LLM rubric + state check | Quality of interaction is part of the eval; needs user simulator |
| Research | Combined (groundedness + coverage + source quality) | Subjective; calibrate LLM graders to experts frequently |
| Computer use | Environment state (URL, DB, filesystem) | Balance DOM vs screenshot for token efficiency |

## Capability vs. regression evals

- **Capability evals** — start low, hill-climb; measure what agent *can't* do yet
- **Regression evals** — near 100% pass rate; catch backsliding
- Saturated capability evals graduate → regression suites

## Non-determinism: pass@k vs pass^k

- **pass@k** — probability of ≥1 success in k tries. Rises with k. Use when one success is enough.
- **pass^k** — probability all k trials succeed. Falls with k. Use for consistent customer-facing agents.

## 8-step roadmap

0. **Start early** — 20-50 tasks from real failures is enough to begin
1. **Start with manual tests** — convert existing checks + bug reports to tasks
2. **Write unambiguous tasks** — two domain experts should independently agree on pass/fail; create reference solutions
3. **Balance problem sets** — test both "should trigger" and "should not trigger"
4. **Stable eval harness** — isolate each trial; shared state = correlated failures
5. **Design graders thoughtfully** — prefer deterministic; grade output not steps; partial credit
6. **Read the transcripts** — failures should feel fair; verify graders aren't rejecting valid solutions
7. **Monitor saturation** — 100% eval → regression only, no improvement signal; build harder tasks
8. **Maintain as living artifact** — dedicated infra team + domain experts contributing tasks

## Evaluation methods comparison

| Method | When useful | Weakness |
| --- | --- | --- |
| Automated evals | Pre-launch, CI/CD | False confidence if tasks don't match real usage |
| Production monitoring | Post-launch drift | Reactive; users hit problems first |
| A/B testing | Validating significant changes | Slow; needs traffic |
| User feedback | Surfacing surprises | Sparse, self-selected |
| Transcript review | Ongoing calibration | Doesn't scale |
| Human studies | Calibrating LLM graders | Expensive, slow |

## Key pitfalls

- Grading the path (tool call order) instead of the outcome → brittle tests
- Class-imbalanced eval (only positive cases) → over-triggered agent
- Shared state between trials → correlated failures mask real performance
- Eval harness diverging from production → misleading scores
- 0% pass rate on many trials → broken task spec, not incapable agent
- Eval saturation → scores stop reflecting capability gains
