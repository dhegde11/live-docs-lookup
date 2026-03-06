# Pressure Test 2: OpenAI Responses API (OpenAI)

## Scenario

A developer is building an agentic assistant with OpenAI and asks for help
choosing between the Chat Completions API and the Responses API. They've seen
both mentioned in tutorials and aren't sure which to use.

## Test prompt

> "I'm building a Python agent that uses OpenAI with tool use. Should I use the
> Chat Completions API or the Responses API? What's the difference and which
> should I use for a new project starting today?"

## Observed agent behavior WITHOUT skill (baseline)

The agent, drawing on training data (which may predate or have limited coverage
of the Responses API launch in early 2025), gives one of these incorrect responses:

**Failure mode A — Unaware of Responses API:**
Agent describes only Chat Completions with function calling, never mentions the
Responses API exists. Developer builds on a less capable foundation.

**Failure mode B — Wrong recommendation:**
Agent hedges ("both are valid, it depends") without knowing that Responses API
is now the preferred path for agentic use cases — it has built-in conversation
state management, native tool calling, and is what OpenAI is investing in for
agent workflows going forward.

**Failure mode C — Stale model IDs:**
Agent recommends `gpt-4-turbo` or `gpt-4o-2024-05-13` for the implementation
rather than current recommended models. Developer copy-pastes into their code.

## Expected behavior WITH skill

After fetching the OpenAI models page and Responses API docs:

1. **Explains the actual difference**:
   - Chat Completions: stateless, developer manages conversation history, older API
   - Responses API: newer, has built-in conversation state (`previous_response_id`),
     designed for agentic multi-turn workflows, integrates with code interpreter and
     file search as built-in tools

2. **Makes a clear recommendation**: Responses API for new agentic projects

3. **Uses current model IDs** from the live models page, not training memory

4. **Notes what hasn't changed**: function calling / tool definitions work similarly
   in both APIs, so existing tool schemas don't need to be rewritten

## Key assertion

The test passes when the agent recommends the **Responses API** for a new agentic
project and uses **current model IDs** from live docs. Failure is recommending
Chat Completions as the primary path, or providing stale model IDs without
verification.
