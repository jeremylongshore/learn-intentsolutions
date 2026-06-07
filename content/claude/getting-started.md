---
title: "Getting started — the Claude mental model"
date: 2026-06-06
description: "The three concepts that make every other Claude doc make sense: model selection, the Messages API, and tool use → MCP."
weight: 10
---

Before the cookbook, before MCP, before any specific feature — three concepts unlock the rest.

## 1. There is a family, not a model

"Claude" is a family. The current shape is **Opus** (largest, smartest, most expensive), **Sonnet** (mid-tier, balanced, the workhorse for production), and **Haiku** (smallest, fastest, cheapest). Versions tick: Claude 4.6, 4.7, etc.

The model-selection question is almost always cost / latency / quality, in that order:

- **Throughput-heavy with bounded difficulty** → Haiku. The cost delta vs Sonnet is real.
- **Default for application code** → Sonnet. Quality is usually indistinguishable from Opus on practical tasks; cost is 5× lower.
- **Hard reasoning, agent loops, complex tool use** → Opus.

Don't pick by gut. Run both Sonnet and Opus on a small eval set and look at the spread.

## 2. Everything is the Messages API

The wire-level interface is `POST /v1/messages`. You send:

- `system` — the system prompt (free, doesn't count toward conversation context).
- `messages` — alternating `user` / `assistant` turns, each with content blocks (text, image, tool_use, tool_result, etc.).
- `tools` — optional schema list the model can call into.

Everything else is dressing on this shape. The SDKs wrap it. Claude Code wraps it. Bedrock's Converse API wraps it. Knowing the bare shape means you can debug at any layer.

## 3. Tool use is the door; MCP is the open standard

A "tool" in the Claude API is a JSON schema the model can choose to invoke. The model returns a `tool_use` content block; your code executes the tool; you send back a `tool_result`; the model continues.

**MCP (Model Context Protocol)** generalizes this: tools, resources, and prompts that live in *servers* rather than baked into each app. Claude Code, Cursor, Codex, and others all speak MCP — write a tool once, every host can call it. This is the part that makes Claude composable.

## What to read next

- [Prompt engineering overview](https://docs.anthropic.com/en/docs/build-with-claude/prompt-engineering/overview) — patterns first, examples second.
- [Prompt caching](https://docs.anthropic.com/en/docs/build-with-claude/prompt-caching) — the cost lever. Any non-trivial app should use it.
- [Tool use](https://docs.anthropic.com/en/docs/build-with-claude/tool-use) — function calling, parallel tools.
- [MCP intro](https://modelcontextprotocol.io/) — the protocol behind composable agents.

## Gotchas

- **Claude API ≠ Claude.ai ≠ Claude Code.** Three different surfaces, three different billing models, three different data-handling defaults. The API customer agreement says inputs/outputs are not used for training. The Claude.ai consumer plans are different. Read the relevant terms before assuming.
- **Context windows are not free.** A 200k-token context window costs ~200k tokens to use even if the answer is short. The pricing scales with input length. Prompt caching is how you blunt this.
- **Model deprecation cycle is real.** Old models get retired with notice. Pin a specific model version in production code, and budget time for upgrades on every major release.
- **"System prompt" and "system message in `messages`" are not the same.** The top-level `system` field is the canonical one; passing a `system`-role message inside `messages` is a different and lesser-used pattern.
