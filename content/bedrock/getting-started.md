---
title: "Getting started — what Bedrock actually does"
date: 2026-06-06
description: "Bedrock is IAM-gated, region-pinned access to many foundation models behind one API. The three things you'll actually do, and the gotchas that bite."
weight: 10
---

Bedrock is the answer to "I want to call Claude (or Llama, or Mistral) from inside my AWS account, billed to that account, with the request never leaving AWS."

## 1. The one-sentence model

Bedrock is a managed proxy: an AWS service that fronts many foundation models behind one IAM-gated, region-pinned API. You don't manage GPUs. You don't manage scaling. You pay per token (or reserve capacity).

The three resources that matter:

- **Models** — what you invoke. Each has a `modelId` like `anthropic.claude-sonnet-4-6-20260520-v1:0`. Availability varies by region.
- **Model access** — opt-in per account per region. New AWS account → you must request access before any `InvokeModel` call works, even though the model "exists."
- **Quotas** — TPM (tokens/min) and RPM (requests/min) per model per region, in **Service Quotas**. Default quotas are low. Raise them before you go to prod.

## 2. Three things you'll actually do

**Invoke a model.** `bedrock-runtime:InvokeModel` (raw, per-vendor schema) or `bedrock-runtime:Converse` (unified messages-API shape across all vendors — use this). The Converse API is the right default unless you need a vendor-specific feature.

**Run a Knowledge Base.** Bedrock's managed RAG. You point it at an S3 prefix (or OpenSearch, or Pinecone), it chunks + embeds + indexes; you query with `RetrieveAndGenerate`. The model assembles a grounded answer with citations. Use this before you build your own vector store from scratch.

**Run an Agent.** Bedrock Agents take a task, plan steps, invoke tools (via OpenAPI schemas), and loop until done. Useful when you need orchestration without rolling your own. The trap: debugging an Agent's reasoning is harder than debugging your own loop.

## 3. The IAM shape you'll need

Minimum to call Claude on Bedrock:

```json
{
  "Effect": "Allow",
  "Action": [
    "bedrock:InvokeModel",
    "bedrock:InvokeModelWithResponseStream",
    "bedrock:Converse",
    "bedrock:ConverseStream"
  ],
  "Resource": "arn:aws:bedrock:us-east-1::foundation-model/anthropic.claude-sonnet-4-6-*"
}
```

Pin the model ARN, not `*`. Future-you will thank you when a finance person asks "who's invoking what."

## What to read next

- [Bedrock User Guide](https://docs.aws.amazon.com/bedrock/latest/userguide/what-is-bedrock.html) — start at "What is Amazon Bedrock?" and follow the linked sections.
- [Converse API](https://docs.aws.amazon.com/bedrock/latest/userguide/conversation-inference.html) — the unified call shape.
- [Anthropic models on Bedrock](https://aws.amazon.com/bedrock/anthropic/) — current Claude model IDs and regions.
- [Cross-region inference](https://docs.aws.amazon.com/bedrock/latest/userguide/cross-region-inference.html) — let Bedrock route to whichever region has capacity. Reduces 429s.

## Gotchas

- **Model access opt-in is per account per region.** A working dev account in `us-east-1` does not mean prod in `us-west-2` works. Each combination is its own approval.
- **Default quotas are too low for real workloads.** Bedrock returns `ThrottlingException` long before you think you're at scale. Open a Service Quota increase before you ship — it can take a day or two for some models.
- **Cross-region inference IS the answer for Claude throughput.** If you're hitting limits in one region, the `us.anthropic.claude-sonnet-4-6...` inference profile lets Bedrock route across `us-east-1`, `us-east-2`, `us-west-2` transparently.
- **Guardrails are evaluated as a separate API call.** They sit on top of inference; budget the extra latency. They're worth it for any user-facing surface.
- **Knowledge Base ingestion is the cost surprise.** Embedding 50 GB of documents costs real money before you've answered the first question. Estimate it.
- **`Converse` returns a different response shape than `InvokeModel`.** Don't write code that branches on both in the same app — pick one (Converse) and stay there.
