# live-docs-lookup

A skill that fetches current AI SDK/API documentation before answering any question about Anthropic, OpenAI, or Google APIs. Prevents stale training data from producing wrong model IDs, deprecated parameters, or missed APIs.

## The problem it solves

AI coding assistants have a training cutoff. Documentation changes faster than models retrain:

- Model IDs get renamed or deprecated (`gemini-1.5-flash` → `gemini-2.0-flash`)
- Parameters get removed (`budget_tokens` deprecated on Claude Opus 4.6)
- New APIs replace old ones (OpenAI Responses API replaces Chat Completions for agents)
- Built-in tools go unnoticed (Anthropic's native `web_search` and `web_fetch` tools)

A 30-second doc fetch before answering catches all of these. See [CREATION-LOG.md](./CREATION-LOG.md) for the real-world failure that motivated this skill.

## What it covers

| Provider | What gets fetched |
|----------|------------------|
| Anthropic | Models, tool use, streaming, prompt caching, batch API, extended thinking |
| OpenAI | Models, Responses API vs Chat Completions, function calling, streaming, batch |
| Google | Gemini models, Gemini API vs Vertex AI, function calling, structured output |

Detection is automatic — the skill infers which provider is in scope from imports, environment variable names, and model name patterns in your code or question.

## Install

### Claude Code

```bash
cp -r live-docs-lookup ~/.claude/skills/
```

### Other tools (Cursor, Codex, OpenCode)

Copy the `live-docs-lookup/` directory into your tool's skills/plugins folder. Check your tool's documentation for the exact path.

## How it triggers

The skill activates automatically when you ask about:

- Which model to use
- Tool use / function calling / structured output
- Streaming responses
- Prompt caching, batch processing, rate limits
- SDK setup, debugging, or planning for any AI API integration
- Anything that involves Anthropic, OpenAI, or Gemini

## Also available via superpowers

This skill is submitted to [obra/superpowers](https://github.com/obra/superpowers). If you use the superpowers plugin system, you can install it from there.

## Evals

The `evals/` directory contains 9 test prompts (5 Anthropic, 2 OpenAI, 2 Google) used during development. Pass rate with skill: 100%. Without skill: 45%. See [CREATION-LOG.md](./CREATION-LOG.md) for details.
