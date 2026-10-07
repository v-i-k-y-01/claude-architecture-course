# Claude Certified Architect — Foundations (CCAR-F)
## Complete Study Guide

> **Unofficial study guide.** Anthropic's Claude Certified Architect — Foundations exam (code **CCAR-F**) is a scenario-based architecture exam. This guide is organized the same way the AWS material was: a Read Me, self-contained modules, worked examples, and a quiz with an answer key at every checkpoint. Always confirm exam logistics (price, validity, registration) against the current Exam Guide in the Anthropic Partner Academy, since those details change.

---

## Table of Contents

- [Read Me — How to Use This Guide](#read-me--how-to-use-this-guide)
- [Module 0 — Exam Overview & Strategy](#module-0--exam-overview--strategy)
- [Module 1 — Agentic Architecture & Orchestration (27%)](#module-1--agentic-architecture--orchestration-27)
- [Module 2 — Tool Design & MCP Integration (18%)](#module-2--tool-design--mcp-integration-18)
- [Module 3 — Claude Code Configuration & Workflows (20%)](#module-3--claude-code-configuration--workflows-20)
- [Module 4 — Prompt Engineering & Structured Output (20%)](#module-4--prompt-engineering--structured-output-20)
- [Module 5 — Context Management & Reliability (15%)](#module-5--context-management--reliability-15)
- [Module 6 — The Six Exam Scenarios, Walked Through](#module-6--the-six-exam-scenarios-walked-through)
- [Module 7 — Anti-Patterns & Decision Frameworks (Final Review)](#module-7--anti-patterns--decision-frameworks-final-review)
- [Appendix A — 4-Week Study Plan](#appendix-a--4-week-study-plan)
- [Appendix B — Glossary](#appendix-b--glossary)
- [Appendix C — Official Resources](#appendix-c--official-resources)

---

## Read Me — How to Use This Guide

### What this guide is

The CCAR-F exam does not test whether you can recite API parameters. Every question is a short business or engineering scenario followed by four design choices, and you pick the one a seasoned architect would make. This guide is built to train that judgment. Each module:

1. **Explains the concept** in plain language, with the "why" behind the recommended design.
2. **Shows a concrete example** — code, config, or a mini-scenario — so the concept is anchored to something real.
3. **Flags the anti-pattern** the exam uses as a distractor.
4. **Ends with a checkpoint quiz** (8–10 scenario questions) and an answer key that explains *why* each wrong option is wrong.

### Who it's for

Solution architects, senior engineers, and technical leads with roughly six months of hands-on experience using the Claude API, the Claude Agent SDK, Claude Code, and the Model Context Protocol (MCP). If you have less than that, pair this guide with the hands-on labs in Appendix C — reading alone is rarely enough for a scenario exam.

### How to study with it

| Step | What to do | Why |
|------|-----------|-----|
| 1 | Read Module 0 first. | It sets expectations for format, scoring, and how questions are phrased. |
| 2 | Work the modules in order (1 → 5). | They're arranged from highest to roughly lowest exam weight, and later modules build on earlier ones. |
| 3 | Take each quiz **closed-book** before reading the key. | The exam is closed-book and proctored. Practice retrieval, not recognition. |
| 4 | For every question you miss, re-read the section and write a one-sentence rule in your own words. | Converting a mistake into a rule is what makes it stick. |
| 5 | Do Module 6 (scenarios) and Module 7 (anti-patterns) in your final week. | These are the highest-yield review material — the exam's wrong answers are drawn almost entirely from the anti-pattern list. |
| 6 | Build at least one small project per domain. | The exam assumes production experience. There's no substitute for having hit the bugs yourself. |

### Conventions used

- **Bold** marks the term or rule you should be able to state from memory.
- `Monospace` marks API fields, file names, CLI flags, or config keys.
- 🚫 **Anti-pattern** callouts show what the exam wants you to *reject*.
- ✅ **Architect's rule** callouts give the one-line takeaway.

### Scoring your quizzes

| Score | Meaning |
|-------|---------|
| 90%+ | Exam-ready on that domain. Move on. |
| 70–89% | Review the items you missed, retake in 2–3 days. |
| Under 70% | Re-read the module fully and do the hands-on exercise before retaking. |

---

## Module 0 — Exam Overview & Strategy

### 0.1 Exam at a glance

| Attribute | Detail |
|-----------|--------|
| Exam name | Claude Certified Architect — Foundations |
| Exam code | CCAR-F |
| Format | 60 multiple-choice, scenario-based questions |
| Duration | 120 minutes |
| Delivery | Proctored, closed-book (Pearson VUE — online or test center) |
| Passing score | 720 / 1000 (scaled) |
| Guessing penalty | None — never leave a question blank |
| Scenario structure | 4 of 6 scenarios randomly selected per sitting |
| Target candidate | Architect with 6+ months on Claude API, Agent SDK, Claude Code, MCP |
| Registration | Through the Anthropic Partner Academy (currently gated to the Claude Partner Network) |
| Credential family | Associate — Foundations (CCAO-F), **Architect — Foundations (CCAR-F)**, Architect — Professional (CCAR-P), Developer — Foundations (CCDV-F) |

### 0.2 Domain weights

| # | Domain | Weight | ≈ Questions |
|---|--------|--------|-------------|
| 1 | Agentic Architecture & Orchestration | 27% | ~16 |
| 2 | Tool Design & MCP Integration | 18% | ~11 |
| 3 | Claude Code Configuration & Workflows | 20% | ~12 |
| 4 | Prompt Engineering & Structured Output | 20% | ~12 |
| 5 | Context Management & Reliability | 15% | ~9 |

Domain 1 alone is worth more than a quarter of the exam. If you're short on time, over-invest there.

### 0.3 How questions are written

A typical item looks like this:

> *A customer-support agent built on the Agent SDK sometimes keeps calling tools after the customer's issue is resolved, running up cost. The team proposes capping every conversation at 8 iterations. What should the architect recommend instead?*

Notice the pattern: a **real symptom**, a **tempting but naive fix** proposed by "the team," and a request for the **architecturally correct alternative**. The correct answer is almost always the option that is:

- **Deterministic over probabilistic** for anything critical (hooks, not prompts).
- **Explicit over implicit** (pass context, don't assume inheritance).
- **Signal-driven over heuristic** (check `stop_reason`, don't parse prose).
- **Diagnostic over silent** (structured errors, not empty results).

### 0.4 Time management

120 minutes for 60 questions is two minutes each. Scenario questions are wordy, so read the **last sentence first** (the actual ask), then read the scenario. Flag anything that takes more than three minutes and come back.

### Checkpoint Quiz — Module 0

1. What is the passing score for CCAR-F?
   - A. 650/1000
   - B. 700/1000
   - C. 720/1000
   - D. 750/1000

2. How many of the six exam scenarios appear in a single sitting?
   - A. All six
   - B. Five
   - C. Four
   - D. Three

3. Which domain carries the greatest weight?
   - A. Tool Design & MCP Integration
   - B. Agentic Architecture & Orchestration
   - C. Prompt Engineering & Structured Output
   - D. Context Management & Reliability

4. You are unsure of an answer with 90 seconds left. The best action is:
   - A. Leave it blank to avoid a penalty
   - B. Pick the most plausible option — there's no guessing penalty
   - C. Pick the longest option
   - D. Pick option A by default

5. The exam is best described as:
   - A. A model-training and fine-tuning exam
   - B. An API-syntax recall exam
   - C. An applied architecture exam built on real-world scenarios
   - D. A data-science statistics exam

#### Answer Key — Module 0

| # | Answer | Explanation |
|---|--------|-------------|
| 1 | **C** | 720/1000 scaled. |
| 2 | **C** | Four of six scenarios are selected at random. |
| 3 | **B** | Agentic Architecture & Orchestration is 27%. |
| 4 | **B** | There is no penalty for wrong answers; never leave blanks. |
| 5 | **C** | Every question is a design-choice scenario; no training or statistics content. |

---

## Module 1 — Agentic Architecture & Orchestration (27%)

This is the heaviest domain. It covers how an agent loop actually runs, when it should stop, how multiple agents coordinate, and how you enforce rules an LLM cannot be trusted to follow on its own.

### 1.1 The agentic loop and `stop_reason`

An **agent** is a model running in a loop: it reasons, calls a tool, receives the result, and decides whether to continue. The loop has to know when to stop, and the API tells you *explicitly* through the `stop_reason` field on every response.

| `stop_reason` | Meaning | What your loop should do |
|---------------|---------|--------------------------|
| `end_turn` | Model finished its turn naturally | Exit the loop; return the answer |
| `tool_use` | Model wants to call one or more tools | Execute tools, append results, call the API again |
| `max_tokens` | Output hit the `max_tokens` ceiling | Treat as incomplete; continue or raise the limit |
| `stop_sequence` | A custom stop sequence was hit | Handle per your design |
| `pause_turn` | A long-running server-side operation paused | Resume by sending the response back |
| `refusal` | Model declined for safety reasons | Surface to the user / fall back; do not retry blindly |

**Example — a correct minimal loop (Python):**

```python
import anthropic
client = anthropic.Anthropic()

messages = [{"role": "user", "content": "Look up order 4471 and summarize its status."}]

while True:
    resp = client.messages.create(
        model="claude-opus-5",
        max_tokens=4096,
        tools=TOOLS,
        messages=messages,
    )
    messages.append({"role": "assistant", "content": resp.content})

    if resp.stop_reason == "tool_use":
        results = []
        for block in resp.content:
            if block.type == "tool_use":
                output = run_tool(block.name, block.input)       # your code
                results.append({
                    "type": "tool_result",
                    "tool_use_id": block.id,
                    "content": output,
                })
        messages.append({"role": "user", "content": results})
        continue

    if resp.stop_reason == "max_tokens":
        # Incomplete — decide whether to continue with a larger budget
        ...
    break   # end_turn, refusal, etc.
```

🚫 **Anti-pattern #1:** Scanning the assistant's text for phrases like "I'm done" or "Task complete" to decide whether to exit. Natural language is not a control signal.

🚫 **Anti-pattern #2:** Using a hard iteration cap (e.g., "stop after 8 turns") as the *primary* stopping mechanism. A cap is fine as a **safety net** against runaway cost, but the loop should end because `stop_reason == "end_turn"`, not because a counter ran out.

✅ **Architect's rule:** *Drive the loop with `stop_reason`; use iteration caps and token budgets only as a backstop.*

### 1.2 Choosing a harness: Tool Runner vs Agent SDK vs Managed Agents

You have three ways to run an agent loop, and the exam expects you to match them to the scenario.

| Option | Who hosts the loop | Best when |
|--------|-------------------|-----------|
| **Manual loop / Tool Runner** (`client.beta.messages.tool_runner`) | You, in your own process | You need full control over each step, custom tools in your language, tight integration with existing code |
| **Claude Agent SDK** (`claude-agent-sdk`) | You, but the SDK provides the harness: built-in tools, file/bash access, subagents, hooks, session management | Building coding agents, developer tooling, or anything that benefits from the same harness Claude Code uses |
| **Managed Agents** | Anthropic hosts the loop and a sandbox | You want to offload infrastructure: no servers to run, sandboxed execution managed for you, latency-tolerant workloads |

**Example decision:** A fintech team wants an agent that reads internal PDFs and files Jira tickets, and their security team requires all compute to stay inside their VPC. → *Agent SDK or Tool Runner* (self-hosted). The same team prototyping a research assistant with no data-residency constraint → *Managed Agents* is the fastest path.

### 1.3 Multi-agent orchestration: coordinator and subagents

When a task is too large or too varied for one context window, split it. The standard pattern is a **coordinator (orchestrator)** that decomposes the task and dispatches **subagents**, each with a narrow role and its own clean context.

Key design principles:

- **Pass context explicitly.** A subagent does *not* automatically inherit the coordinator's conversation. Every fact it needs — the user's goal, constraints, prior findings — must be written into its prompt.
- **Give each subagent a small toolset.** A subagent with 4–5 tools performs far more reliably than one with 18. (See Module 2 for how tool search relaxes this at scale.)
- **Return structured results.** Subagents should hand back a defined shape (JSON, a fixed section layout), not free prose, so the coordinator can merge deterministically.
- **Handle partial failure.** If one of five research subagents fails, the coordinator should know *which* one, *why*, and whether the others' results are still usable.
- **Match effort to role.** Coordinators and complex coding tasks run at high effort; mechanical subagents (summarize this file, extract these fields) run at low effort to save cost and latency.

**Example — a research coordinator (pseudocode):**

```
coordinator prompt:
  "You are coordinating a competitive-analysis report on <topic>.
   Split the work into at most 5 independent research questions.
   For each, spawn a subagent with: the question, the date range,
   the output schema {source, claim, confidence, url}, and a 2,000-token limit.
   When all return, merge into a single report, citing sources.
   If a subagent returns an error, record it in a 'gaps' section — never silently omit it."
```

🚫 **Anti-pattern #9 (same-session self-review):** Asking the same agent, in the same context, to review its own work. It still "remembers" its reasoning and will rationalize its own mistakes. Spawn a **fresh reviewer** with a clean context.

✅ **Architect's rule:** *Subagents are blank slates — if it isn't in their prompt, they don't know it.*

### 1.4 Enforcement: hooks vs prompts

An LLM following a prompt is **best-effort**. A **hook** — code that runs deterministically before or after a tool call — is **guaranteed**. The exam constantly tests whether you know which to reach for.

| Use a prompt instruction when… | Use a hook when… |
|-------------------------------|------------------|
| The rule is stylistic or soft ("prefer concise answers") | The rule is financial, legal, safety, or compliance |
| Occasional violations are tolerable | A single violation is unacceptable |
| The rule needs judgment to apply | The rule can be expressed as code |

**Example:** A procurement agent must never approve a purchase order over $10,000 without a human.

- 🚫 *Prompt-only:* "Do not approve POs over $10,000." The model will comply 99% of the time. 1% of $10k+ orders is a real liability.
- ✅ *Hook:* A `PreToolUse` hook on `approve_purchase_order` inspects `amount`; if `> 10000` it blocks the call and returns an error instructing the agent to escalate. Now the rule is enforced in code, every time.

Claude Code and the Agent SDK expose hook events such as `PreToolUse`, `PostToolUse`, `Stop`, and `SessionStart`. A hook can **allow**, **block (with a message the model sees)**, or **modify** the action.

✅ **Architect's rule:** *If it would be a headline when it fails, enforce it in a hook, not a prompt.*

### 1.5 Escalation logic (support-agent scenario)

Support agents must decide when to hand off to a human. The exam has strong opinions here.

- **Escalate immediately** when the customer **explicitly asks** for a human. Don't try to "resolve first" — that erodes trust.
- **Resolve first** when the issue is **within the agent's capability** and the customer has not asked for a human.
- Escalation triggers should be **deterministic and observable**: failed tool calls, policy boundaries (refund > threshold), repeated identical questions, explicit request.

🚫 **Anti-pattern #4:** Asking the model to self-report a "confidence score" and escalating when it's below 0.7. Self-reported confidence is poorly calibrated and easily gamed by phrasing.

🚫 **Anti-pattern #5:** Escalating on negative **sentiment**. An angry customer with a simple password reset does not need a human; a calm customer with a multi-account billing dispute might. **Sentiment ≠ complexity.**

### 1.6 Session and state management

- **Sessions** let you resume an agent's conversation later. In the Agent SDK and Claude Code, sessions have IDs you can `--resume` or `--continue`.
- **State that must survive** — a running to-do list, extracted facts, a progress checkpoint — should live in **files or the memory tool**, never only in the conversation. Conversations get compacted and context gets cleared (Module 5).

### Checkpoint Quiz — Module 1

1. An agent loop sometimes exits while the model is still mid-task. On inspection, the exit happens whenever the model's text includes the word "complete." What is the root cause?
   - A. `max_tokens` is set too low
   - B. The loop is parsing natural language instead of checking `stop_reason`
   - C. The tool definitions are missing descriptions
   - D. The model is being run at `effort: low`

2. A team caps every agent run at 6 iterations to prevent runaway cost. Users report truncated results on complex tasks. The best fix is to:
   - A. Raise the cap to 12
   - B. Drive termination with `stop_reason == "end_turn"` and keep the cap only as a safety net
   - C. Remove the cap entirely
   - D. Switch to the Batch API

3. A loan-servicing agent must never disclose a full account number. Which approach guarantees this?
   - A. A system-prompt instruction in all caps
   - B. Few-shot examples of redacted output
   - C. A `PostToolUse`/output hook that redacts the pattern programmatically before the response is returned
   - D. Running at `effort: xhigh` so the model is more careful

4. A coordinator spawns five subagents for a research task. Three return results; two return nothing. The coordinator produces a polished report using the three. What is wrong?
   - A. Nothing — partial results are acceptable
   - B. The coordinator silently suppressed the failures; it should surface what's missing and why
   - C. It should have used fewer subagents
   - D. Subagents should never be used for research

5. Which `stop_reason` indicates the model wants you to execute something and send results back?
   - A. `end_turn`
   - B. `max_tokens`
   - C. `tool_use`
   - D. `refusal`

6. A support agent escalates whenever the customer's message is angry. Customers with trivial issues are being sent to humans, while calm customers with complex billing disputes are not. Which anti-pattern is this?
   - A. Self-reported confidence
   - B. Sentiment-based escalation
   - C. Prompt-based enforcement
   - D. Same-session self-review

7. A subagent repeatedly asks "what is the user's goal?" even though the coordinator knows it. The fix is to:
   - A. Enable context inheritance in the SDK
   - B. Include the goal explicitly in the subagent's prompt
   - C. Increase the subagent's `max_tokens`
   - D. Use a larger model for the subagent

8. A customer writes, "Just get me a person, please." The agent believes it can solve the issue. It should:
   - A. Attempt resolution first, then escalate if it fails
   - B. Ask the customer to describe the problem in more detail
   - C. Escalate immediately — explicit requests override capability
   - D. Run a sentiment check first

9. A team wants to deploy a coding agent but has no appetite to run servers or sandboxes. There are no data-residency constraints. The most appropriate harness is:
   - A. Managed Agents
   - B. A hand-written loop in a Lambda function
   - C. The Tool Runner inside a Kubernetes cluster
   - D. A cron job calling the Batch API

10. After generating a 400-line migration, an agent is asked, in the same conversation, to review it for bugs. It finds none. Later a bug is found. The architectural mistake was:
    - A. Not using plan mode
    - B. Same-session self-review — a fresh reviewer context should have been used
    - C. Not using the Batch API
    - D. Too few tools

#### Answer Key — Module 1

| # | Answer | Explanation |
|---|--------|-------------|
| 1 | **B** | Exiting on the string "complete" is Anti-pattern #1. Use `stop_reason`. |
| 2 | **B** | Caps are a backstop; `stop_reason` is the primary control. A and C just move the problem. |
| 3 | **C** | Only code guarantees enforcement. Prompts (A, B) are best-effort; effort level (D) is unrelated. |
| 4 | **B** | Anti-pattern #7: silent suppression. Surface gaps explicitly. |
| 5 | **C** | `tool_use` is the signal to execute tools and continue. |
| 6 | **B** | Sentiment ≠ complexity (Anti-pattern #5). |
| 7 | **B** | Subagents don't inherit context; pass it explicitly. There is no "inheritance toggle." |
| 8 | **C** | An explicit request for a human is an immediate-escalation trigger. |
| 9 | **A** | Managed Agents offloads hosting and sandboxing; the others still require you to run infra. |
| 10 | **B** | Anti-pattern #9. The reviewer must not share the author's reasoning context. |

---

## Module 2 — Tool Design & MCP Integration (18%)

Tools are how an agent acts on the world. This domain covers writing tools the model can use reliably, controlling *whether* and *which* tools get called, scaling to many tools, and connecting external systems through MCP.

### 2.1 Anatomy of a good tool definition

A tool is a JSON schema plus a description. The **description is the most important field** — it's the only thing the model reads to decide when to call it.

```json
{
  "name": "get_order_status",
  "description": "Look up the current fulfillment status of a single customer order by its 10-digit order ID. Returns status, carrier, tracking number, and estimated delivery. Use this when a customer asks where their order is. Do NOT use for returns or refunds — use process_return instead.",
  "input_schema": {
    "type": "object",
    "properties": {
      "order_id": {
        "type": "string",
        "pattern": "^[0-9]{10}$",
        "description": "The 10-digit order identifier, e.g. 4471029384"
      }
    },
    "required": ["order_id"]
  }
}
```

What makes this good:

- **Says what it does, when to use it, and when *not* to.** Disambiguation between sibling tools is the single biggest reliability win.
- **Describes return shape** so the model knows what to expect.
- **Constrains inputs** with `pattern`, `enum`, and `required` so malformed calls fail at the schema, not in your code.
- **Uses a verb_noun name** that reads naturally.

🚫 **Anti-pattern:** `"description": "Gets order."` The model has to guess.

### 2.2 Controlling tool invocation with `tool_choice`

| `tool_choice` | Effect | Use when |
|---------------|--------|----------|
| `{"type": "auto"}` (default) | Model decides whether to call a tool | Normal conversation |
| `{"type": "any"}` | Model **must** call *some* tool | You need a guaranteed tool call but don't care which (e.g., routing) |
| `{"type": "tool", "name": "extract_invoice"}` | Model **must** call *this* tool | Forcing structured extraction into a known schema |
| `{"type": "none"}` | No tool calls | You want a plain text answer this turn |

**Example:** A classification step must always produce one of three categories. Define `classify_ticket` with an `enum` and set `tool_choice: {"type": "tool", "name": "classify_ticket"}`. The output is now guaranteed to be schema-valid JSON.

### 2.3 Scaling to many tools: tool search and deferred loading

Historically the guidance was "keep it to 4–5 tools per agent." That remains true for **reasoning quality** — but modern APIs let you *have* many tools without *loading* them all into context.

- **Under ~10 tools:** load them all upfront.
- **10+ tools, or multiple MCP servers:** use the **tool search tool** with `defer_loading: true` on most tools. The model is given a lightweight searchable index and only pulls in a tool's full schema when it needs it. This keeps the prompt small (saving tokens and cache) while keeping capability broad.

**Programmatic tool calling** is a related capability: the model writes a small program that calls several tools in sequence inside a sandbox, returning only the final result — ideal for chaining five lookups without five round-trips through context.

✅ **Architect's rule:** *Many tools is a context problem, not a capability problem. Solve it with deferred loading, not by deleting tools you need.*

### 2.4 Tool results and error handling

How you return errors determines whether the agent can recover.

```json
// ✅ Structured error the model can act on
{
  "type": "tool_result",
  "tool_use_id": "toolu_01…",
  "is_error": true,
  "content": "{\"error_category\": \"NOT_FOUND\", \"retryable\": false, \"message\": \"Order 4471029384 does not exist. Verify the ID with the customer.\", \"partial_data\": null}"
}
```

🚫 **Anti-pattern #6:** `"content": "An error occurred."` The model can't tell whether to retry, ask the user, or escalate.

🚫 **Anti-pattern #7:** Catching the exception and returning `[]` as if the lookup succeeded with no results. The agent now confidently tells the customer they have no orders.

✅ **Architect's rule:** *Every tool error carries a category, a retryable flag, a human-readable message, and any partial data.*

### 2.5 Model Context Protocol (MCP)

**MCP** is an open standard for connecting models to external tools and data. An **MCP server** exposes *tools*, *resources*, and *prompts*; an **MCP client** (Claude Code, the Agent SDK, the API's MCP connector) consumes them.

| Transport | How it runs | Typical use |
|-----------|-------------|-------------|
| `stdio` | Server is a local subprocess | Local dev tools, filesystem, git |
| HTTP (streamable) | Server is a remote endpoint | Shared enterprise services (Jira, Slack, databases), multi-user |

**Example — Claude Code `.mcp.json` (project-scoped, checked into the repo):**

```json
{
  "mcpServers": {
    "jira": {
      "type": "http",
      "url": "https://mcp.example.com/jira",
      "headers": { "Authorization": "Bearer ${JIRA_TOKEN}" }
    },
    "local-db": {
      "command": "npx",
      "args": ["-y", "@example/db-mcp", "--readonly"],
      "env": { "DB_URL": "${DB_URL}" }
    }
  }
}
```

Design guidance:

- **Scope servers deliberately.** Project-scope (`.mcp.json`) for team-shared servers; user-scope for personal ones.
- **Never hardcode secrets.** Use environment-variable expansion.
- **Prefer read-only servers for exploration agents**, and gate writes behind hooks or human approval.
- **Each MCP server's tools count toward the tool budget** — this is where tool search / deferred loading matters most.
- **The API MCP connector** lets you attach remote MCP servers directly to a Messages API call without running a client yourself.

### Checkpoint Quiz — Module 2

1. An agent frequently calls `search_customers` when it should call `get_customer_by_id`. The most effective fix is:
   - A. Remove `search_customers`
   - B. Rewrite both descriptions to state when to use each and when not to
   - C. Set `tool_choice: any`
   - D. Increase `max_tokens`

2. You need every response in a pipeline step to be a call to `extract_fields`, never free text. Use:
   - A. `tool_choice: {"type": "auto"}`
   - B. `tool_choice: {"type": "any"}`
   - C. `tool_choice: {"type": "tool", "name": "extract_fields"}`
   - D. A system prompt saying "always use the tool"

3. An agent connects to three MCP servers exposing 42 tools total. Accuracy has dropped and prompt costs are up. The best remedy is:
   - A. Delete tools until there are 5
   - B. Use the tool search tool with `defer_loading` so only needed schemas enter context
   - C. Split into 42 separate agents
   - D. Switch to a smaller model

4. A tool's database call times out. The tool returns `""` with `is_error: false`. What will likely happen?
   - A. The model retries automatically
   - B. The model treats the empty result as a valid "no data" answer and proceeds incorrectly
   - C. The API raises an exception
   - D. The loop terminates with `refusal`

5. Which fields should a well-designed tool error include?
   - A. Only a stack trace
   - B. A generic "error occurred" string
   - C. Error category, retryable flag, actionable message, and any partial data
   - D. The full request payload

6. A team wants a shared Jira integration that every engineer's Claude Code picks up automatically when they clone the repo. Configure it in:
   - A. Each developer's user-scope settings
   - B. The project's `.mcp.json`
   - C. A system prompt
   - D. The `CLAUDE.md` file as prose

7. An MCP server for local git operations is best run over:
   - A. HTTP from a public endpoint
   - B. `stdio` as a local subprocess
   - C. WebSockets
   - D. The Batch API

8. `tool_choice: {"type": "any"}` guarantees that:
   - A. A specific named tool is called
   - B. Some tool is called, but the model picks which
   - C. No tool is called
   - D. All tools are called in sequence

9. Which is the best tool description?
   - A. "Refunds."
   - B. "Processes a refund."
   - C. "Issue a refund to the original payment method for a delivered order, up to $500. Requires order_id and reason. Do not use for orders not yet delivered — use cancel_order."
   - D. "Use this tool to do refund things for the customer when needed."

10. An exploration agent should be able to read a production database schema but never modify data. The cleanest design is:
    - A. Tell the model in the prompt not to write
    - B. Connect a read-only MCP server (or a read-only DB role) and gate any write tool behind a hook
    - C. Use `tool_choice: none`
    - D. Give it full access but monitor logs

#### Answer Key — Module 2

| # | Answer | Explanation |
|---|--------|-------------|
| 1 | **B** | Descriptions drive tool selection; disambiguate explicitly. |
| 2 | **C** | A forced named tool guarantees that specific call. `any` (B) could pick another tool. |
| 3 | **B** | Tool search + deferred loading solves the context problem without losing capability. |
| 4 | **B** | Anti-pattern #7: silent failure masquerading as success. |
| 5 | **C** | Structured, actionable error context. |
| 6 | **B** | `.mcp.json` is project-scoped and version-controlled. |
| 7 | **B** | Local tools → `stdio`. |
| 8 | **B** | `any` forces a tool call but leaves the choice to the model. |
| 9 | **C** | States purpose, limits, inputs, and when *not* to use it. |
| 10 | **B** | Deterministic access control beats prompt-based restraint. |

---

## Module 3 — Claude Code Configuration & Workflows (20%)

Claude Code is Anthropic's agentic coding tool for the terminal. This domain tests whether you can configure it for a team, shape its behavior with memory files and hooks, and choose the right workflow mode for a task.

### 3.1 The `CLAUDE.md` memory hierarchy

`CLAUDE.md` files are persistent instructions Claude Code loads at session start. They are layered, and **more specific scopes layer on top of broader ones**.

| Scope | Location | Checked in? | Use for |
|-------|----------|-------------|---------|
| Enterprise / managed | System-level policy path (managed by IT) | Yes (centrally) | Org-wide rules: security policies, banned libraries |
| Project | `./CLAUDE.md` (repo root) | **Yes** | Build commands, architecture notes, coding standards, test instructions |
| Project (local) | `./CLAUDE.local.md` | **No** (gitignored) | Your personal overrides for this repo |
| User | `~/.claude/CLAUDE.md` | No | Your preferences across all projects |
| Subdirectory | `./packages/api/CLAUDE.md` | Yes | Module-specific context, loaded when working in that path |

A `CLAUDE.md` can `@import` other files (`@docs/architecture.md`) so you don't duplicate content.

**Example — a good project `CLAUDE.md`:**

```markdown
# Payments Service

## Commands
- Build: `pnpm build`   Test: `pnpm test --filter payments`   Lint: `pnpm lint`
- Always run lint + tests before declaring a task done.

## Architecture
- Hexagonal: `domain/` has no imports from `infra/`.
- All money is `bigint` cents. Never use floating point for currency.

## Conventions
- Use `Result<T, E>` — never throw from domain code.
- New DB changes require a migration in `migrations/` AND a rollback script.

@docs/adr/README.md
```

Good `CLAUDE.md` content is **specific, verifiable, and short**. "Write clean code" is useless; "run `pnpm lint` before finishing" is actionable.

🚫 **Anti-pattern:** Putting a critical security rule *only* in `CLAUDE.md`. Memory files are instructions (best-effort). Critical rules go in **hooks** (Module 1.4) — `CLAUDE.md` can additionally *explain* the rule.

### 3.2 Settings and permissions

`settings.json` (user: `~/.claude/settings.json`; project: `.claude/settings.json`; local: `.claude/settings.local.json`) controls permissions, hooks, environment, and model defaults.

```json
{
  "permissions": {
    "allow": ["Bash(pnpm test*)", "Bash(pnpm lint*)", "Read", "Edit"],
    "deny":  ["Bash(rm -rf*)", "Bash(git push --force*)", "Read(./.env*)"]
  },
  "hooks": {
    "PreToolUse": [{
      "matcher": "Edit|Write",
      "hooks": [{ "type": "command", "command": "./scripts/block-prod-config.sh" }]
    }]
  }
}
```

- **`deny` rules win** over `allow`.
- Permission modes range from prompting on every action to auto-accepting edits; **`--dangerously-skip-permissions`** exists for sandboxed CI only — never on a developer laptop with production credentials.

### 3.3 Plan mode vs direct execution

| Choose **plan mode** when… | Choose **direct execution** when… |
|----------------------------|-----------------------------------|
| The change spans multiple files or modules | The change is a single file with an obvious fix |
| There are architectural decisions to make | The task is mechanical (rename, add a log line) |
| You want to review the approach before any edits | The blast radius is tiny and reversible |
| The task is ambiguous and needs exploration first | Requirements are crystal clear |

In plan mode Claude Code reads and reasons but **does not edit** until you approve the plan. This is where you catch "it's going to refactor the wrong module" before it happens.

### 3.4 Slash commands, skills, subagents, and plugins

| Mechanism | What it is | When to use |
|-----------|-----------|-------------|
| **Built-in slash commands** (`/compact`, `/clear`, `/review`, `/init`, `/memory`) | Session controls | Managing context and sessions |
| **Custom slash commands** (`.claude/commands/*.md`) | A reusable prompt template invoked with `/name` | Repeatable team workflows: `/release-notes`, `/fix-issue 123` |
| **Skills** (`SKILL.md` in a skills directory) | Packaged instructions + scripts Claude loads on demand when relevant | Domain know-how: "how we write migrations," "our API-docs format" |
| **Subagents** (`.claude/agents/*.md`) | Named agents with their own system prompt, tool allowlist, and model | Delegating specialized work (test-writer, security-reviewer) with a clean context |
| **Plugins** | A bundle of commands, skills, agents, hooks, and MCP servers distributed via a marketplace | Sharing a complete workflow across teams or the org |

**Example — a custom command `.claude/commands/fix-issue.md`:**

```markdown
Fix GitHub issue $ARGUMENTS.
1. Read the issue with `gh issue view $ARGUMENTS`.
2. Enter plan mode and propose a fix; wait for approval.
3. Implement, run `pnpm test`, and open a PR referencing the issue.
```

### 3.5 Built-in tools and codebase exploration

Claude Code ships with `Read`, `Edit`, `Write`, `Bash`, `Glob`, `Grep`, `WebFetch`, and an **Agent/Task** tool for spawning subagents. For large codebases, the recommended pattern is:

1. **Explore broadly with a subagent** ("find every place we construct a `PaymentIntent`") so the file dumps stay out of your main context.
2. **Pull only the conclusion** back into the primary session.
3. **Edit in the primary session** with a focused context.

### 3.6 Claude Code in CI/CD (headless mode)

`claude -p "<prompt>"` runs non-interactively. Combine with `--output-format json` for machine-readable results and `--allowedTools` to scope what it can do.

```yaml
# GitHub Actions step
- name: AI review
  run: |
    claude -p "Review the diff in this PR for security issues. Output JSON matching schema in .claude/review-schema.json." \
      --output-format json \
      --allowedTools "Read,Grep,Glob,Bash(git diff*)" > review.json
```

Design rules for CI:

- **Structured output** (JSON schema) so downstream steps can parse it.
- **Multi-pass review for large PRs:** one pass for security, one for performance, one for correctness — each with a fresh context — then merge. A single pass over a 2,000-line diff degrades.
- **Batch API** (Module 4) for latency-tolerant bulk jobs like nightly re-review of all open PRs.
- **Scope permissions tightly**; CI is the one place `--dangerously-skip-permissions` is sometimes acceptable *because the sandbox is disposable*.

### Checkpoint Quiz — Module 3

1. Build and test commands that every engineer should use belong in:
   - A. `~/.claude/CLAUDE.md`
   - B. `./CLAUDE.md` checked into the repo
   - C. `./CLAUDE.local.md`
   - D. A Slack pinned message

2. A developer wants Claude Code to prefer their personal editor conventions in every repo, without affecting teammates. Use:
   - A. Project `CLAUDE.md`
   - B. `~/.claude/CLAUDE.md`
   - C. `.mcp.json`
   - D. Enterprise policy

3. A task requires refactoring the authentication flow across 14 files. The best starting mode is:
   - A. Direct execution with auto-accept
   - B. Plan mode
   - C. `claude -p` in CI
   - D. Batch API

4. Both an `allow` and a `deny` rule match `Bash(git push --force origin main)`. The result is:
   - A. Allowed — allow wins
   - B. Denied — deny wins
   - C. Prompted
   - D. Undefined

5. A team repeatedly runs the same 5-step release-notes workflow. Package it as:
   - A. A long `CLAUDE.md` paragraph
   - B. A custom slash command in `.claude/commands/`
   - C. A `.env` variable
   - D. A comment in the README

6. An AI review step in CI needs its output consumed by a later script. Configure:
   - A. `--output-format json` with a defined schema
   - B. Interactive mode
   - C. Plain text output parsed with regex
   - D. `--verbose`

7. A 3,000-line PR gets a single-pass AI review that misses obvious issues. The recommended fix is:
   - A. Increase `max_tokens`
   - B. Multi-pass review, each pass focused and in a fresh context
   - C. Review only the first 500 lines
   - D. Skip AI review for large PRs

8. Where is `--dangerously-skip-permissions` reasonably acceptable?
   - A. A developer laptop with prod credentials
   - B. A disposable, sandboxed CI container
   - C. Production servers
   - D. Never

9. A critical rule — "never commit directly to `main`" — is in `CLAUDE.md`, yet it occasionally happens. The right remediation is:
   - A. Make the `CLAUDE.md` text bold
   - B. Add a `PreToolUse` hook that blocks `git commit`/`git push` on `main`
   - C. Repeat the rule three times
   - D. Switch models

10. You want a "security-reviewer" that always runs with a restricted toolset and its own system prompt, invoked by name. Create a:
    - A. Custom slash command
    - B. Subagent definition in `.claude/agents/`
    - C. `CLAUDE.local.md`
    - D. MCP server

#### Answer Key — Module 3

| # | Answer | Explanation |
|---|--------|-------------|
| 1 | **B** | Team-shared, version-controlled project memory. |
| 2 | **B** | User-scope memory applies across all projects for that user only. |
| 3 | **B** | Multi-file + architectural → plan mode. |
| 4 | **B** | Deny rules take precedence. |
| 5 | **B** | Custom slash commands are reusable prompt templates. |
| 6 | **A** | Structured JSON output for downstream parsing. |
| 7 | **B** | Multi-pass with fresh contexts for large PRs. |
| 8 | **B** | Only where the environment is disposable and credential-free. |
| 9 | **B** | Critical rules → hooks. `CLAUDE.md` is best-effort. |
| 10 | **B** | Subagents carry their own prompt, tools, and model. |

---

## Module 4 — Prompt Engineering & Structured Output (20%)

This domain covers getting reliable, parseable output from Claude — the backbone of the structured-extraction and CI/CD scenarios.

### 4.1 Prompt structure fundamentals

- **System prompt = role, rules, and context that never change.** User turn = the task at hand.
- **Be explicit about success criteria.** "Summarize this" is vague; "Summarize in ≤3 bullets, each ≤20 words, for a CFO audience" is checkable.
- **Use XML tags** to delimit inputs and desired output sections (`<document>…</document>`, `<answer>…</answer>`). They're unambiguous and easy to parse.
- **Few-shot examples** teach format and edge-case handling better than paragraphs of rules. Use 2–5 diverse examples; include a tricky one.
- **Give Claude room to think** for hard tasks (adaptive thinking, or an explicit `<scratchpad>` before the answer when not using thinking).
- **Prefer positive instructions** ("respond in JSON") over long lists of negatives.

**Example — explicit criteria beat adjectives:**

| Vague | Explicit |
|-------|----------|
| "Write a good commit message." | "Write a commit message: imperative mood, ≤72-char subject, blank line, then a body explaining *why*, referencing the issue number." |
| "Flag risky transactions." | "Flag a transaction if amount > $5,000 **or** country ≠ billing country **or** >3 transactions in 10 minutes. Output `{flagged: bool, reasons: string[]}`." |

### 4.2 Structured output: the three approaches

| Approach | How | Guarantee level | Best for |
|----------|-----|-----------------|----------|
| **Prompting for JSON** | "Respond only with JSON matching…" | Best-effort; needs validation | Quick prototypes |
| **Tool use as output schema** | Define a tool whose `input_schema` is your output shape; force it with `tool_choice` | Schema-valid JSON structure guaranteed | Extraction pipelines; works on all models |
| **Structured Outputs** (`output_format` with JSON schema) | API constrains generation to the schema | Strongest: schema-conformant output | Production extraction where exactness matters |

**Example — extraction via forced tool:**

```python
INVOICE_TOOL = {
  "name": "record_invoice",
  "description": "Record the extracted fields of an invoice.",
  "input_schema": {
    "type": "object",
    "properties": {
      "invoice_number": {"type": "string"},
      "vendor": {"type": "string"},
      "total_cents": {"type": "integer", "description": "Total in cents, no decimals"},
      "currency": {"type": "string", "enum": ["USD", "EUR", "GBP"]},
      "line_items": {"type": "array", "items": {
        "type": "object",
        "properties": {"description": {"type": "string"}, "amount_cents": {"type": "integer"}},
        "required": ["description", "amount_cents"]}},
      "confidence_notes": {"type": "string", "description": "Any fields that were ambiguous and why"}
    },
    "required": ["invoice_number", "vendor", "total_cents", "currency", "line_items"]
  }
}

resp = client.messages.create(
    model="claude-sonnet-5",
    max_tokens=2048,
    tools=[INVOICE_TOOL],
    tool_choice={"type": "tool", "name": "record_invoice"},
    messages=[{"role": "user", "content": [
        {"type": "document", "source": {"type": "base64", "media_type": "application/pdf", "data": pdf_b64}},
        {"type": "text", "text": "Extract this invoice."}
    ]}],
)
invoice = next(b.input for b in resp.content if b.type == "tool_use")
```

### 4.3 Validation-retry loops

Schema validity is not the same as **correctness**. `total_cents` can be a valid integer and still not equal the sum of line items. Add a **validation layer** and feed failures back.

```
1. Call model → get structured output
2. Validate: schema ✔, business rules ✔ (totals match, dates parse, enum in allowed set)
3. If invalid → re-prompt WITH the specific validation error:
   "Your previous output failed validation: total_cents (12500) ≠ sum(line_items) (12050). Correct it."
4. Retry at most N times; after N, route to human review with the error attached
```

🚫 **Anti-pattern:** Retrying with the identical prompt and hoping. Always include *what* failed.

🚫 **Anti-pattern #10:** Reporting "97% extraction accuracy" overall while one document type (handwritten receipts) sits at 40%. **Measure per document type / per field** and set thresholds on each.

### 4.4 Thinking and effort

- **Adaptive thinking** (`thinking: {"type": "adaptive"}`) lets the model decide how much to reason per request. It is the recommended setting on current models; the older `budget_tokens` style is only still used on Haiku 4.5 and is rejected by newer models.
- **Effort** (`low` / `medium` / `high` / `xhigh`) trades latency and cost against depth. Use **`xhigh`** for coding and complex agentic reasoning; **`low`** for mechanical subagents and classification.
- **Task budgets** let you cap total spend across a multi-step task.

### 4.5 Synchronous vs Batch API

| Messages API (sync) | Message Batches API |
|---------------------|---------------------|
| Response in seconds | Results within hours (often much faster) |
| Full price | ~50% discount |
| Blocking, interactive, agent loops | Latency-tolerant bulk jobs: nightly document extraction, re-scoring a backlog, bulk evaluations |

✅ **Architect's rule:** *If no human is waiting on the answer, it probably belongs in a batch.*

### 4.6 Prompt caching

Long, stable prefixes (system prompt, tool definitions, reference documents) can be **cached** with `cache_control` breakpoints. Cached tokens are much cheaper to read. Put stable content **first**, variable content **last**, and keep the stable prefix byte-identical between calls.

### Checkpoint Quiz — Module 4

1. An extraction pipeline must produce JSON that always matches a fixed schema. The strongest guarantee comes from:
   - A. Asking politely in the system prompt
   - B. Structured Outputs (`output_format` with a JSON schema) or a forced tool call
   - C. Setting temperature to 0
   - D. Adding "IMPORTANT" in caps

2. The invoice extractor returns schema-valid JSON, but totals don't match line items 8% of the time. Add:
   - A. More `max_tokens`
   - B. A business-rule validation step that re-prompts with the specific error
   - C. A larger model
   - D. A retry with the identical prompt

3. Your extraction dashboard shows 96% overall accuracy, but customers complain about receipts. The metric problem is:
   - A. The threshold is too high
   - B. Aggregate accuracy masks per-document-type failures
   - C. Accuracy should be measured weekly
   - D. There is no problem

4. A nightly job re-extracts 50,000 archived PDFs. No one is waiting. Use:
   - A. Synchronous Messages API with 50 threads
   - B. The Message Batches API
   - C. Streaming
   - D. Managed Agents

5. On a current model (e.g., Opus 5), which thinking configuration is correct?
   - A. `{"type": "enabled", "budget_tokens": 8000}`
   - B. `{"type": "adaptive"}`
   - C. `{"type": "always"}`
   - D. Thinking cannot be configured

6. For a subagent that only renames variables, the most cost-effective effort level is:
   - A. `xhigh`
   - B. `high`
   - C. `low`
   - D. Effort doesn't apply to subagents

7. Which prompt will produce the most consistent result?
   - A. "Make the summary good."
   - B. "Summarize concisely."
   - C. "Summarize in exactly 3 bullets, each under 20 words, for an executive audience, in `<summary>` tags."
   - D. "Summarize however you think is best."

8. You send the same 40-page policy document with every request plus a short, varying question. To cut cost:
   - A. Put the question first and the document last with a cache breakpoint
   - B. Put the document first with a `cache_control` breakpoint, then the varying question
   - C. Compress the document into a single paragraph
   - D. Use the Batch API

9. Few-shot examples are most valuable for:
   - A. Replacing the system prompt entirely
   - B. Teaching output format and edge-case handling
   - C. Increasing `max_tokens`
   - D. Enabling tool use

10. After three failed validation retries, the pipeline should:
    - A. Retry indefinitely
    - B. Accept the last output anyway
    - C. Route the item to human review with the validation errors attached
    - D. Drop the item silently

#### Answer Key — Module 4

| # | Answer | Explanation |
|---|--------|-------------|
| 1 | **B** | Schema-constrained generation or forced tool use; prompts alone are best-effort. |
| 2 | **B** | Validation-retry with the specific error. |
| 3 | **B** | Anti-pattern #10. Measure per type/field. |
| 4 | **B** | Latency-tolerant bulk → Batch API, ~50% cheaper. |
| 5 | **B** | Adaptive thinking; `budget_tokens` is rejected on current models (except Haiku 4.5). |
| 6 | **C** | Mechanical work → `low`. |
| 7 | **C** | Explicit, checkable criteria. |
| 8 | **B** | Stable prefix first, cached; variable content last. |
| 9 | **B** | Examples teach format and edge cases efficiently. |
| 10 | **C** | Bounded retries, then human-in-the-loop with diagnostics. |

---

## Module 5 — Context Management & Reliability (15%)

Context windows are large (up to 1M tokens on current models) but not infinite, and quality degrades well before the hard limit when the context is cluttered. This domain covers keeping context clean, persisting what matters, and making errors propagate usefully.

### 5.1 Why context management matters

Every token in context costs money, adds latency, and competes for the model's attention. Verbose tool results (a 30,000-token log dump), stale exploration output, and long back-and-forth all degrade reasoning. The architect's job is to keep the **signal-to-noise ratio** high.

### 5.2 Clear vs compact

| Technique | What it does | Use when |
|-----------|-------------|----------|
| **Context editing / clearing** (API `context_management`, Claude Code `/clear`) | Removes old tool results or wipes the session | Tool results were verbose and are no longer needed; starting an unrelated task |
| **Compaction** (API compaction, Claude Code `/compact`) | Summarizes the conversation so far into a shorter form, preserving the narrative | Long conversations where the *story* (decisions made, constraints discovered) must survive |

**Example:** An agent runs 40 `grep` calls while exploring a codebase. → **Clear** the tool results (they've served their purpose). A two-hour pairing session that has made six design decisions → **Compact** so the decisions survive but the chatter doesn't.

✅ **Architect's rule:** *Clear noise; compact narrative.*

### 5.3 Persist what must survive

Anything compaction might lose — a task list, extracted facts, a progress checkpoint, user preferences — must live **outside** the conversation:

- **Memory tool** — a model-driven file store the model can read/write across turns and sessions.
- **Files on disk** (e.g., `NOTES.md`, `progress.json`) in Claude Code / Agent SDK.
- **Your own database** keyed by session or user.

🚫 **Anti-pattern:** "The model will remember — it's in the conversation." After compaction it may not be.

### 5.4 Managing subagent context

Spawning a subagent is itself a context-management technique: the subagent does the noisy work (reading 50 files) in **its own** context and returns only a conclusion to the coordinator. This is why "delegate the search, keep the conclusion" is the recommended pattern in Claude Code.

### 5.5 Error propagation and provenance

Reliability in agent systems depends on errors carrying enough context to act on **at every hop**.

| Layer | What to propagate |
|-------|-------------------|
| Tool → model | Category, retryable, message, partial data (Module 2.4) |
| Subagent → coordinator | Which step failed, the error, what *did* succeed |
| Agent → user / operator | A clear statement of what could not be completed and why — never a confident answer built on missing data |

**Provenance** means every claim in an output can be traced to a source: a tool result ID, a document page, a URL. In research and extraction scenarios, require subagents to return `{claim, source, confidence}` triples rather than prose, so the final report can cite and so failures are visible.

### 5.6 Reliability patterns checklist

- **Idempotent tools** — retries must be safe (use idempotency keys for writes).
- **Timeouts and bounded retries** with exponential backoff on `429`/`529`/`overloaded_error`.
- **Graceful `refusal` handling** — surface to the user, don't loop.
- **Handle `max_tokens`** as incomplete, never as done.
- **Observability** — log `stop_reason`, token usage, tool calls, and latency per turn.
- **Evaluation** — per-category metrics (Anti-pattern #10), regression suites on real failure cases.

### Checkpoint Quiz — Module 5

1. An agent's context is full of 35 verbose `Bash` outputs from earlier exploration; it has started making mistakes. The best action is:
   - A. Compact the conversation
   - B. Clear the old tool results
   - C. Switch to a 1M-context model
   - D. Restart from scratch and lose the decisions

2. A long design session has produced important decisions, and context is getting large. To preserve the decisions while reducing size:
   - A. Clear everything
   - B. Compact the conversation
   - C. Delete the system prompt
   - D. Reduce `max_tokens`

3. A multi-hour agent task tracks progress only in the conversation. After compaction it repeats completed steps. Fix:
   - A. Disable compaction
   - B. Persist progress to a file or the memory tool
   - C. Increase the context window
   - D. Tell the model to "remember harder"

4. A subagent reports "task failed" with no detail; the coordinator proceeds and ships a report with gaps. Which principle is violated?
   - A. Prompt caching
   - B. Structured error propagation
   - C. Plan mode
   - D. Tool search

5. "Delegate the search, keep the conclusion" is primarily a technique for:
   - A. Cost accounting
   - B. Keeping the primary agent's context clean
   - C. Enforcing security rules
   - D. Batch processing

6. A research report must allow readers to verify every claim. Subagents should return:
   - A. Free-form prose
   - B. `{claim, source, confidence}` structured records
   - C. Only a summary
   - D. Sentiment scores

7. A response returns `stop_reason: "max_tokens"`. The correct interpretation is:
   - A. The task is complete
   - B. The output is incomplete
   - C. The model refused
   - D. A tool must be executed

8. The API returns `529 overloaded_error`. Your client should:
   - A. Fail immediately
   - B. Retry with exponential backoff, up to a bound
   - C. Retry in a tight loop
   - D. Switch to prompt caching

9. A write tool may be retried after a network blip. To keep retries safe:
   - A. Disable retries
   - B. Make the tool idempotent (e.g., idempotency keys)
   - C. Add a sleep
   - D. Use `tool_choice: none`

10. Which metric design best supports reliability in an extraction pipeline?
    - A. One overall accuracy number
    - B. Per-document-type and per-field accuracy with thresholds on each
    - C. Average latency only
    - D. Number of retries

#### Answer Key — Module 5

| # | Answer | Explanation |
|---|--------|-------------|
| 1 | **B** | Verbose, obsolete tool results → clear. |
| 2 | **B** | Narrative that must survive → compact. |
| 3 | **B** | Durable state lives outside the conversation. |
| 4 | **B** | Errors must carry actionable context at every hop. |
| 5 | **B** | Subagents absorb noisy context; the primary keeps the conclusion. |
| 6 | **B** | Structured, sourced claims enable provenance. |
| 7 | **B** | `max_tokens` = truncated. |
| 8 | **B** | Bounded backoff. |
| 9 | **B** | Idempotency makes retries safe. |
| 10 | **B** | Avoids Anti-pattern #10. |

---

## Module 6 — The Six Exam Scenarios, Walked Through

Four of these six scenarios will appear on your exam. For each, here is the setting, the concepts it draws from, the traps, and the design an architect would choose.

### Scenario 1 — Customer Support Resolution Agent

**Setting:** An Agent SDK-based agent handles tier-1 support with MCP tools for orders, refunds, and account lookup.

**Draws on:** Modules 1.1, 1.4, 1.5, 2.1, 2.4.

**Traps:** confidence-score escalation; sentiment-based escalation; prompt-only refund limits; generic tool errors.

**Architect's design:** `stop_reason`-driven loop; 4–6 well-described tools; `PreToolUse` hook enforcing the refund ceiling; deterministic escalation triggers (explicit request → immediate; policy boundary; repeated tool failure); structured tool errors so the agent can tell the customer *what* it couldn't do.

### Scenario 2 — Code Generation with Claude Code

**Setting:** A team adopts Claude Code for feature work in a monorepo.

**Draws on:** Module 3.1–3.4.

**Traps:** putting critical rules only in `CLAUDE.md`; direct execution for large refactors; one giant `CLAUDE.md` with no imports.

**Architect's design:** Project `CLAUDE.md` with commands/architecture/conventions and `@imports`; hooks for must-never-happen rules; plan mode for multi-file work; custom slash commands for repeated workflows; subagents for exploration.

### Scenario 3 — Multi-Agent Research System

**Setting:** A coordinator dispatches subagents to research topics and compiles a report.

**Draws on:** Modules 1.3, 5.4, 5.5.

**Traps:** assuming subagents inherit context; silently dropping failed subagents; same-session self-review; free-prose returns.

**Architect's design:** Explicit context in every subagent prompt; small toolsets; structured `{claim, source, confidence}` returns; a `gaps` section for failures; a fresh-context reviewer; low effort for mechanical subagents.

### Scenario 4 — Developer Productivity with Claude

**Setting:** Engineers use Claude Code's built-in tools and MCP servers to navigate and modify a large codebase.

**Draws on:** Modules 2.3, 2.5, 3.5.

**Traps:** loading 40 MCP tools upfront; exploring in the primary context; hardcoded secrets in `.mcp.json`.

**Architect's design:** Project-scoped `.mcp.json` with env-var secrets; tool search / deferred loading when tool count is high; delegate exploration to subagents; read-only servers for browsing with gated writes.

### Scenario 5 — Claude Code for CI/CD

**Setting:** Automated PR review and code-quality checks in a pipeline.

**Draws on:** Modules 3.6, 4.2, 4.5.

**Traps:** single-pass review of huge diffs; parsing free text; running sync API for nightly bulk jobs; skipping permission scoping.

**Architect's design:** `claude -p` with `--output-format json` and a schema; `--allowedTools` scoping; multi-pass review for large PRs with fresh contexts; Batch API for backlog/bulk; disposable sandbox if permissions are relaxed.

### Scenario 6 — Structured Data Extraction

**Setting:** Extracting fields from invoices, contracts, or forms at scale.

**Draws on:** Modules 4.2–4.3, 4.5, 5.6.

**Traps:** prompt-only JSON; retrying without the error; aggregate accuracy; unbounded retries.

**Architect's design:** Structured Outputs or forced tool; business-rule validation with error-informed retries; bounded retries then human review; Batch API for bulk; per-type/per-field metrics.

### Checkpoint Quiz — Module 6 (Mixed Scenarios)

1. *(Support)* The refund tool accepts any amount; the system prompt says "never refund over $200." A $900 refund went through. Fix:
   - A. Rewrite the prompt more firmly
   - B. Add a `PreToolUse` hook that blocks refunds > $200 and instructs escalation
   - C. Lower the model temperature
   - D. Remove the refund tool

2. *(Research)* The final report cites no sources and two topics are missing with no explanation. Two design changes fix this:
   - A. Bigger model; more tokens
   - B. Structured `{claim, source}` returns; explicit `gaps` reporting for failed subagents
   - C. Sentiment analysis; confidence scores
   - D. Batch API; prompt caching

3. *(Code gen)* An engineer asks Claude Code to "migrate the ORM across the service." It immediately starts editing files. What should have happened?
   - A. Nothing — that's correct
   - B. Plan mode should have been used to review the approach first
   - C. It should have asked for a confidence score
   - D. It should have used the Batch API

4. *(Dev productivity)* After adding four MCP servers, Claude Code's responses slowed and tool selection got worse. Best fix:
   - A. Remove three servers
   - B. Enable tool search with deferred loading
   - C. Use a smaller model
   - D. Increase `max_tokens`

5. *(CI/CD)* The review step prints prose that a shell script tries to parse with `grep`. It breaks weekly. Fix:
   - A. Better regex
   - B. `--output-format json` with a defined schema
   - C. Run it twice
   - D. Switch to interactive mode

6. *(Extraction)* Contracts extract at 99%, handwritten forms at 55%, overall 94%. The dashboard shows only 94%. The problem is:
   - A. The model
   - B. Aggregate metrics hiding a per-type failure
   - C. The threshold
   - D. The Batch API

7. *(Support)* A customer calmly describes a multi-account billing discrepancy spanning three months. The agent's tools only cover single-order lookups. It should:
   - A. Attempt resolution anyway
   - B. Escalate — the issue exceeds tool capability (a deterministic trigger)
   - C. Ask the customer to be more concise
   - D. Return a generic apology

8. *(Research)* To review the compiled report, the coordinator should:
   - A. Ask itself to review in the same session
   - B. Spawn a fresh reviewer subagent with only the report and the criteria
   - C. Skip review
   - D. Have each subagent review its own section

9. *(CI/CD)* A nightly job must re-review 400 open PRs. Use:
   - A. Sync API in a loop
   - B. Batch API
   - C. Interactive Claude Code
   - D. Managed Agents only

10. *(Extraction)* After validation fails three times on one document, the pipeline should:
    - A. Accept the output
    - B. Retry until success
    - C. Route to a human queue with the validation errors
    - D. Discard the document

#### Answer Key — Module 6

| # | Answer | Explanation |
|---|--------|-------------|
| 1 | **B** | Financial rule → hook. |
| 2 | **B** | Provenance + explicit failure reporting. |
| 3 | **B** | Multi-file architectural change → plan mode. |
| 4 | **B** | Tool search solves tool sprawl. |
| 5 | **B** | Structured output for machine consumption. |
| 6 | **B** | Anti-pattern #10. |
| 7 | **B** | Capability boundary is a deterministic escalation trigger; calm sentiment is irrelevant. |
| 8 | **B** | Avoid same-session self-review. |
| 9 | **B** | Latency-tolerant bulk → Batch. |
| 10 | **C** | Bounded retries, then human-in-the-loop. |

---

## Module 7 — Anti-Patterns & Decision Frameworks (Final Review)

### 7.1 The 10 critical anti-patterns

These appear as **wrong answers**. If an option matches one, eliminate it.

| # | Anti-pattern | Correct alternative |
|---|-------------|---------------------|
| 1 | Parsing natural language to decide loop termination | Check `stop_reason` |
| 2 | Iteration caps as the *primary* stopping mechanism | `stop_reason`-driven; cap only as a backstop |
| 3 | Prompt-based enforcement of critical business rules | Programmatic hooks |
| 4 | Self-reported confidence scores for escalation | Deterministic, observable triggers |
| 5 | Sentiment-based escalation | Complexity/capability-based triggers; explicit request → immediate |
| 6 | Generic error messages | Category + retryable + message + partial data |
| 7 | Silently suppressing errors (empty result as success) | Mark `is_error`; surface failures |
| 8 | Too many tools loaded per agent | 4–5 for small agents; tool search + `defer_loading` at scale |
| 9 | Same-session self-review | Fresh-context reviewer |
| 10 | Aggregate accuracy masking per-type failures | Per-type / per-field metrics with thresholds |

### 7.2 Decision frameworks

| Decision | Choose this… | …or this |
|----------|-------------|----------|
| Enforcement | **Hooks** — financial, safety, compliance | **Prompt** — stylistic, best-effort |
| Execution mode | **Plan mode** — multi-file, architectural | **Direct** — single-file, obvious |
| `tool_choice` | **`any`** — guarantee *a* tool call | **Named tool** — force a specific one |
| API type | **Sync** — someone is waiting | **Batch** — latency-tolerant, bulk |
| Error handling | **Structured** context | Never generic or silent |
| Escalation | **Immediate** — explicit request / capability boundary | **Resolve first** — within capability, no request |
| Code review | **Multi-pass** — large PRs | **Single-pass** — small, focused |
| Subagent context | **Always explicit** | Never assume inheritance |
| Thinking | **Adaptive** on current models | `budget_tokens` only on Haiku 4.5 |
| Effort | **`xhigh`** — coding, complex agentic | **`low`** — mechanical subagents |
| Tool exposure | **Load upfront** — <~10 tools | **Tool search + defer** — 10+ or multi-MCP |
| Context reduction | **Clear** — verbose tool results | **Compact** — long narrative |
| Durable state | **Memory tool / files** | Never conversation-only |
| Harness | **Tool Runner / Agent SDK** — you host | **Managed Agents** — Anthropic hosts |

### 7.3 Quick-fire self-test (one-liners)

Cover the right column and answer from memory.

| Prompt | Answer |
|--------|--------|
| The field that tells you why the model stopped | `stop_reason` |
| Deterministic enforcement mechanism in Claude Code / Agent SDK | Hooks (`PreToolUse`, `PostToolUse`, …) |
| Project-scoped, version-controlled MCP config file | `.mcp.json` |
| Personal, gitignored project memory file | `CLAUDE.local.md` |
| Mode that reads and plans but doesn't edit | Plan mode |
| Scales to dozens of tools without bloating context | Tool search + `defer_loading` |
| ~50% cheaper API for latency-tolerant bulk work | Message Batches API |
| Strongest schema guarantee for output | Structured Outputs / forced tool |
| Removes stale tool results | Context editing / `/clear` |
| Summarizes while preserving narrative | Compaction / `/compact` |
| Where durable agent state belongs | Memory tool / files |
| Thinking mode on current models | Adaptive |
| Who should review generated code | A fresh-context reviewer |
| Sentiment vs. what, for escalation? | Complexity (and explicit request) |

### Checkpoint Quiz — Module 7 (Comprehensive)

1. Which option is **not** an anti-pattern?
   - A. Using `stop_reason` to end the loop
   - B. Parsing "I'm finished" from text
   - C. Returning `[]` on a timed-out lookup
   - D. One accuracy number for all document types

2. The single best indicator a rule belongs in a hook rather than a prompt:
   - A. It's long
   - B. A single violation is unacceptable
   - C. It's about formatting
   - D. It's hard to explain

3. "Clear vs compact" — which pairing is right?
   - A. Clear = verbose tool results; Compact = long narrative
   - B. Clear = long narrative; Compact = verbose tool results
   - C. Both remove everything
   - D. Both are identical

4. An agent has 7 tools total. Tool exposure strategy:
   - A. Tool search mandatory
   - B. Load them all upfront
   - C. Split into 7 agents
   - D. Remove 3

5. A pipeline processes documents while a user watches a progress bar expecting results in seconds. API choice:
   - A. Batch API
   - B. Synchronous Messages API
   - C. Managed Agents
   - D. Email

6. Which `tool_choice` makes the model call *exactly* `classify`?
   - A. `auto`
   - B. `any`
   - C. `{"type": "tool", "name": "classify"}`
   - D. `none`

7. A subagent's output must be verifiable later. Require:
   - A. Prose summary
   - B. `{claim, source, confidence}` records
   - C. Sentiment
   - D. Token count

8. On Opus 5, sending `budget_tokens` will:
   - A. Work normally
   - B. Be ignored
   - C. Return a 400 error — use adaptive thinking
   - D. Enable extended output

9. What is the recommended effort for a complex multi-file coding task?
   - A. `low`
   - B. `medium`
   - C. `xhigh`
   - D. Effort is not configurable

10. A team wants to share a complete workflow — commands, a skill, a subagent, hooks, and an MCP server — across the whole org. Package it as a:
    - A. `CLAUDE.md`
    - B. Plugin
    - C. Slash command
    - D. `.env` file

#### Answer Key — Module 7

| # | Answer | Explanation |
|---|--------|-------------|
| 1 | **A** | The others are Anti-patterns #1, #7, #10. |
| 2 | **B** | Zero-tolerance rules need deterministic enforcement. |
| 3 | **A** | Clear noise; compact narrative. |
| 4 | **B** | Under ~10 tools → load upfront. |
| 5 | **B** | Someone is waiting → sync. |
| 6 | **C** | Forced named tool. |
| 7 | **B** | Provenance. |
| 8 | **C** | `budget_tokens` is rejected on current models; use `{"type": "adaptive"}`. |
| 9 | **C** | `xhigh` for coding and complex agentic work. |
| 10 | **B** | Plugins bundle all of these for distribution. |

---

## Appendix A — 4-Week Study Plan

Assumes 1.5–2 hours per day.

| Week | Focus | Modules | Daily goal | Hands-on |
|------|-------|---------|-----------|----------|
| 1 | Core architecture | 0, 1, 2 | One section + its quiz | Build a `stop_reason`-driven loop with 3 tools and one `PreToolUse` hook |
| 2 | Applied skills | 3, 4 | One section + quiz | Set up a project `CLAUDE.md`, a custom slash command, and a `claude -p` JSON step; build an extraction pipeline with validation-retry |
| 3 | Reliability + end-to-end | 5, 6 | Review weak areas | Build a coordinator + 3 subagents that return structured results and report gaps; add compaction and file-based progress |
| 4 | Exam prep | 7 + all quizzes | One timed 60-question set per day (re-mix the module quizzes) | Anti-pattern drills; re-read every explanation for questions you missed |

---

## Appendix B — Glossary

| Term | Definition |
|------|-----------|
| **Agent loop** | Repeated cycle of model call → tool execution → model call until `end_turn`. |
| **Agent SDK** | Anthropic's SDK providing the Claude Code harness (tools, hooks, subagents, sessions) for your own agents. Formerly "Claude Code SDK." |
| **Batch API** | Asynchronous bulk processing endpoint at a ~50% discount. |
| **`CLAUDE.md`** | Persistent instruction/memory file for Claude Code, layered by scope. |
| **Compaction** | Summarizing a conversation to shrink context while preserving narrative. |
| **Context editing** | Removing specific content (e.g., old tool results) from context. |
| **Coordinator / orchestrator** | The agent that decomposes a task and dispatches subagents. |
| **`defer_loading`** | Tool flag that keeps the full schema out of context until tool search pulls it in. |
| **Effort** | Parameter (`low`→`xhigh`) trading depth for latency/cost. |
| **Hook** | Deterministic code run on lifecycle events (`PreToolUse`, `PostToolUse`, `Stop`, …). |
| **Managed Agents** | Anthropic-hosted agent loop and sandbox. |
| **MCP** | Model Context Protocol — open standard for exposing tools/resources to models. |
| **Memory tool** | Model-driven persistent file store across turns and sessions. |
| **Plan mode** | Claude Code mode that explores and proposes but doesn't edit until approved. |
| **Plugin** | Distributable bundle of commands, skills, agents, hooks, and MCP servers. |
| **Prompt caching** | Reusing a stable prompt prefix at reduced cost via `cache_control`. |
| **Provenance** | Traceability of every claim to a source. |
| **Skill** | `SKILL.md` package of instructions/scripts loaded on demand. |
| **`stop_reason`** | Field indicating why generation ended (`end_turn`, `tool_use`, `max_tokens`, …). |
| **Structured Outputs** | API feature constraining generation to a JSON schema. |
| **Subagent** | A delegated agent with its own clean context, prompt, and toolset. |
| **`tool_choice`** | Controls whether/which tool the model must call. |
| **Tool search** | Built-in tool letting the model discover deferred tools by searching. |
| **Validation-retry** | Checking output against schema + business rules and re-prompting with the specific error. |

---

## Appendix C — Official Resources

**Program**

- Anthropic Partner Academy (registration; current Exam Guide) and Pearson VUE's Anthropic program page
- Anthropic Skilljar — *Building with the Claude API*
- *Building Effective Agents* (Anthropic research)

**API (platform.claude.com/docs)**

- Tool use overview · Tool search tool · Programmatic tool calling · Memory tool · MCP connector
- Thinking · Effort · Task budgets · Context editing · Compaction · Prompt caching
- Structured outputs · Handling stop reasons · Refusals and fallback
- Managed Agents overview · Models overview

**Claude Code (code.claude.com/docs)**

- Overview · CLI reference · Subagents · Skills · Plugins · Hooks · MCP · Memory and `CLAUDE.md` · Agent SDK overview

**Background**

- MCP Introduction (modelcontextprotocol.io)
- *Advanced tool use* and *Effective context engineering for AI agents* (Anthropic Engineering blog)

---

*This is an unofficial, community-style study guide. "Claude Certified Architect" is a certification program by Anthropic. Model names, prices, and exam logistics change — verify against the official Exam Guide before your test date.*
