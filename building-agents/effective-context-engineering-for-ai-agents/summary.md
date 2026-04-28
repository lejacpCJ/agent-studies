Context engineering—curating the optimal token set at each inference step—is the critical evolution beyond prompt engineering for building capable agents.

**Key points**

- **Context rot is real**: as context window fills, LLM recall degrades due to n² attention relationships stretching thin; treat context as a finite resource with diminishing returns.
- **System prompt altitude**: avoid both brittle if-else hardcoding and vague high-level guidance; target the Goldilocks zone—specific enough to guide, flexible enough to generalize.
- **Tool design matters for context**: bloated, overlapping tool sets waste attention budget and cause ambiguous decisions; minimal, self-contained tools with clear contracts are essential.
- **Just-in-time retrieval over pre-loading**: agents that hold lightweight references (file paths, links) and dynamically fetch data outperform those that dump everything up front; mirrors human working memory.
- **Compaction for long-horizon tasks**: summarize + reinitiate context window near limit; tune compaction prompts for maximum recall first, then prune superfluous content (tool result clearing is the lowest-risk first step).
- **Structured note-taking**: agents writing persistent notes outside context (e.g., NOTES.md, todo lists) maintain coherence across resets without inflating the window.
- **Sub-agent architectures**: specialized agents handle focused tasks in clean windows, returning 1–2K token summaries to a coordinator—separates deep search context from high-level synthesis.

**Why it matters**

Context is the primary lever for agent reliability; getting it wrong produces unfocused, incoherent, or hallucinating agents regardless of model capability. These techniques directly translate to longer-horizon task success, lower cost, and more predictable behavior in production agentic systems.
