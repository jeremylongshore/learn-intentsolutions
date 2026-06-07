---
title: "Getting started — the enterprise AI mental model"
date: 2026-06-06
description: "Three layers of constraint (data, identity, cost) and the architecture decision tree: Anthropic API vs Bedrock for enterprise workloads."
weight: 10
---

Enterprise AI is not a different technology stack. It's the same Claude / Bedrock / LLM stack with **three layers of constraint** that consumer / hobbyist projects ignore.

## 1. Three layers of constraint

**Data isolation — where prompts and outputs live.**
The question every CISO asks first. Two patterns:

- **Anthropic API direct**: Your prompts go to Anthropic-controlled infrastructure. Anthropic is the processor under your DPA. Outputs are not used to train models (commercial paid tier). Audit lives in Anthropic's logs.
- **Anthropic via Bedrock**: Your prompts go through your AWS account boundary first. AWS is *also* a processor. Outputs are not used to train base models. Audit lives in CloudTrail + Bedrock model-invocation logs. Optional PrivateLink endpoints keep the call off the public internet entirely.

Pick **Bedrock** when the workload needs to stay inside an AWS account boundary, when the customer's contract specifies AWS regions for data residency, or when PrivateLink is a hard requirement. Pick **Anthropic API direct** when you want the freshest model availability (Bedrock lags by a few weeks on new model releases) or when the customer relationship is with Anthropic Enterprise directly.

**Identity — who can call the model.**
Three controls stack:

1. **IAM at the call site** — which roles / users can `bedrock:InvokeModel` against which model ARN.
2. **Service Control Policies (SCPs)** — org-wide guardrails. "No account in this OU can call Bedrock outside `eu-central-1`."
3. **SSO / Identity Center** — federated workforce identity so individual humans aren't long-lived API keys.

If you skip any of the three, the auditor finds it on day one.

**Cost — who pays.**
LLM bills surprise people because token costs are tiny per call but the call count explodes. Three things to wire from day one:

- **Cost Allocation Tags** on every Bedrock-invoking resource (Lambda, ECS service, etc.) — without this you can't split the bill across teams.
- **AWS Budgets** with alerts at 50% / 80% / 100% of expected monthly spend.
- **Service Quotas as a backstop** — a runaway loop can burn $10k/hour at Opus pricing. The quota is your circuit breaker.

## 2. The architecture decision tree

```
Does the workload have hard residency / sovereignty rules?
  Yes → Bedrock in the right region. PrivateLink endpoint. Period.
  No ↓

Is the customer already deep in AWS (IAM, billing, audit centralized)?
  Yes → Bedrock. The procurement path is shorter; the DPA is already signed.
  No ↓

Do you need a feature Bedrock hasn't shipped yet (newest model, extended context, vision modes)?
  Yes → Anthropic API direct.
  No → Bedrock by default.
```

The default is Bedrock for enterprise; Anthropic API direct is the override when you have a specific reason.

## 3. The pieces that are easy to forget

- **Sub-processor lists are dual.** Anthropic's Trust Center lists Anthropic's sub-processors. AWS's GDPR Center lists AWS's. Bedrock-as-intermediary doesn't appear in Anthropic's list because Bedrock isn't Anthropic's sub-processor — it's *yours*. Two contracts, two lists.
- **Model invocation logging is opt-in.** Bedrock will happily run forever without logging a single prompt or response. If you need the audit trail (and for any regulated workload, you do), turn it on per account per region.
- **Guardrails ≠ prompt-side validation.** Bedrock Guardrails catch some content-policy violations on the model side. They do not replace your own input sanitization, output filtering, or PII redaction. Treat them as one layer, not the layer.
- **The "free" Bedrock services aren't free.** Knowledge Base storage in OpenSearch Serverless, Agent action group invocations, Guardrails evaluations — each has its own price. Read the pricing page before you architect.

## What to read next

- [Well-Architected Framework: Generative AI Lens](https://docs.aws.amazon.com/wellarchitected/latest/generative-ai-lens/) — the canonical AWS framing for GenAI workloads.
- [AWS GDPR Center](https://aws.amazon.com/compliance/gdpr-center/) — the DPA, SCCs, and the customer guidance doc.
- [Anthropic Trust Center](https://trust.anthropic.com/) — the matching Anthropic-side compliance hub.
- [Service Control Policies](https://docs.aws.amazon.com/organizations/latest/userguide/orgs_manage_policies_scps.html) — the org-wide guardrail layer.

## Gotchas

- **"AWS handles the GDPR for us" is wrong.** AWS is a processor; you are the controller for your end-users' data. The DPA assigns specific obligations to each side. Read it once.
- **SCPs deny, IAM allows.** The mental model trap is thinking SCPs grant access. They never do. They only prune the set of actions that IAM can then allow.
- **Region selection drives more than latency.** It drives data residency, which drives compliance, which drives whether your contract is even signable. Decide region before architecture.
- **Bedrock's `Converse` is the same shape as Anthropic's Messages API by design.** Switching between Bedrock and direct Anthropic should be hours of work, not weeks. Build that flexibility from day one — it's free and the day you need it, you'll be glad.
