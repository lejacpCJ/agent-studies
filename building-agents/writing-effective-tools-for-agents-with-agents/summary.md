Tools for agents require a fundamentally different design philosophy than APIs for deterministic software — and Claude Code can help you optimize them automatically.

**Key points**

- **Tools ≠ APIs.** Tools are contracts between deterministic systems and non-deterministic agents. Agents may hallucinate, misuse, or ignore tools — design with that in mind, not like you're writing functions for other developers.
- **Eval-driven iteration.** Build a prototype → generate real-world eval tasks (multi-step, not sandbox) → measure accuracy + tool call metrics → analyze transcripts → improve → repeat. Use Claude Code to automate the analysis and tool-rewriting loop.
- **Fewer, higher-signal tools win.** Avoid wrapping raw API endpoints. Consolidate multi-step workflows into single tools (e.g., `schedule_event` instead of `list_users` + `list_events` + `create_event`). Too many or overlapping tools distract agents.
- **Namespace deliberately.** Prefix or suffix tools by service/resource (e.g., `asana_projects_search`) to reduce ambiguity when agents have access to hundreds of tools across multiple MCP servers.
- **Return only what matters.** Strip UUIDs and low-level identifiers; prefer human-readable names. Expose a `response_format` enum (`concise` / `detailed`) so agents can control verbosity and token cost (~3x savings shown in Slack example).
- **Cap token output.** Add pagination, filtering, and truncation. Make truncated/error responses actionable — tell the agent what to do next, not just that something failed.
- **Prompt-engineer descriptions.** Tool descriptions are loaded into agent context and directly steer behavior. Treat them like onboarding docs for a new hire. Even small wording changes had measurable accuracy gains (e.g., SWE-bench Verified SOTA).

**Why it matters**

As MCP adoption grows and agents gain access to hundreds of tools, the quality of tool design becomes a primary lever for agent performance — often more impactful than model capability alone. The iterative, eval-driven workflow described here lets teams systematically extract gains that pure "expert" intuition misses.
