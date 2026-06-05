---
title: "Learn"
date: 2026-06-05
---

Personal study notes plus the link directory I actually use. Topics I'm working through now: **AWS**, **Anthropic / Claude**, **Amazon Bedrock**, and the **enterprise AI** patterns that tie them together. Public because someone else might find them useful, but the audience is me later.

> Read this page top-to-bottom once to see the lay of the land. After that it's a directory — jump straight to the section you need.

## Anthropic & Claude

### Official documentation
- [Anthropic Docs](https://docs.anthropic.com/) — root of everything Anthropic ships.
- [Claude API reference](https://docs.anthropic.com/en/api) — endpoints, parameters, errors.
- [Claude Code docs](https://code.claude.com/docs) — the CLI, hooks, skills, agents, MCP integration.
- [Model overview](https://docs.anthropic.com/en/docs/about-claude/models) — Opus / Sonnet / Haiku, context windows, pricing per token.
- [Anthropic API status](https://status.anthropic.com/) — live incident page; bookmark for outage triage.

### Building with Claude
- [Anthropic Cookbook](https://github.com/anthropics/anthropic-cookbook) — runnable example notebooks (tool use, RAG, agents, vision, etc.).
- [Anthropic Courses](https://github.com/anthropics/courses) — structured curricula on prompt engineering, tool use, real-world prompting.
- [Prompt engineering overview](https://docs.anthropic.com/en/docs/build-with-claude/prompt-engineering/overview) — the canonical patterns.
- [Tool use](https://docs.anthropic.com/en/docs/build-with-claude/tool-use) — function calling, parallel tools, response shaping.
- [Vision](https://docs.anthropic.com/en/docs/build-with-claude/vision) — image inputs, mixed modalities.
- [Prompt caching](https://docs.anthropic.com/en/docs/build-with-claude/prompt-caching) — the cost / latency lever for any serious app.
- [Extended thinking](https://docs.anthropic.com/en/docs/build-with-claude/extended-thinking) — visible reasoning for harder problems.

### Agents and protocols
- [Model Context Protocol (MCP)](https://modelcontextprotocol.io/) — the open standard for tool / resource servers that Claude (and others) call.
- [MCP specification](https://spec.modelcontextprotocol.io/) — the wire-level spec.
- [Claude Agent SDK](https://docs.anthropic.com/en/api/agent-sdk) — building agents on top of the Claude API.

### Enterprise & governance
- [Claude for Enterprise](https://www.anthropic.com/enterprise) — SSO, audit logs, custom retention, enterprise SLAs.
- [Anthropic Trust Center](https://trust.anthropic.com/) — SOC 2, ISO, GDPR, sub-processor list. The one page to bookmark for compliance questions.
- [Anthropic Privacy Policy](https://www.anthropic.com/legal/privacy) — what data is collected, how it's used, retention.
- [Commercial Terms](https://www.anthropic.com/legal/commercial-terms) — API customer agreement (includes the DPA-by-reference).
- [Anthropic Acceptable Use Policy](https://www.anthropic.com/legal/aup) — what models can / can't be used for.
- [Anthropic Usage Policies](https://www.anthropic.com/legal/usage-policy) — service-tier rules.
- [Console](https://console.anthropic.com/) — billing, API keys, usage dashboards.
- [Pricing](https://www.anthropic.com/pricing) — per-token and Claude.ai plan pricing.

## Amazon Bedrock

### Service docs
- [Bedrock landing](https://aws.amazon.com/bedrock/) — high-level overview.
- [Bedrock User Guide](https://docs.aws.amazon.com/bedrock/latest/userguide/what-is-bedrock.html) — the canonical deep-dive.
- [Bedrock API Reference](https://docs.aws.amazon.com/bedrock/latest/APIReference/) — control plane.
- [Bedrock Runtime API](https://docs.aws.amazon.com/bedrock/latest/APIReference/API_Operations_Amazon_Bedrock_Runtime.html) — data plane (`InvokeModel`, `Converse`).
- [Supported models](https://docs.aws.amazon.com/bedrock/latest/userguide/models-supported.html) — model IDs by region.
- [Bedrock pricing](https://aws.amazon.com/bedrock/pricing/) — per-model on-demand + provisioned throughput.

### Claude on Bedrock
- [Anthropic models on Bedrock](https://aws.amazon.com/bedrock/anthropic/) — overview + region availability.
- [Cross-region inference](https://docs.aws.amazon.com/bedrock/latest/userguide/cross-region-inference.html) — for higher throughput / failover.
- [Converse API](https://docs.aws.amazon.com/bedrock/latest/userguide/conversation-inference.html) — unified messages-API shape across providers.

### Bedrock building blocks
- [Knowledge Bases](https://aws.amazon.com/bedrock/knowledge-bases/) — managed RAG over your data.
- [Agents](https://aws.amazon.com/bedrock/agents/) — multi-step task orchestration with tool calling.
- [Guardrails](https://aws.amazon.com/bedrock/guardrails/) — content filtering, denied topics, PII redaction.
- [Prompt Management](https://docs.aws.amazon.com/bedrock/latest/userguide/prompt-management.html) — versioned prompts you reference by ARN.
- [Bedrock Studio](https://aws.amazon.com/bedrock/studio/) — collaborative dev environment for prompts + agents.
- [Model customization (fine-tuning)](https://docs.aws.amazon.com/bedrock/latest/userguide/custom-models.html) — fine-tune supported models on your data.
- [Provisioned Throughput](https://docs.aws.amazon.com/bedrock/latest/userguide/prov-throughput.html) — guaranteed capacity, reserved pricing.

### Samples and workshops
- [Bedrock workshop catalog](https://workshops.aws/?tag=Amazon%20Bedrock) — hands-on labs, free.
- [Bedrock samples on GitHub](https://github.com/aws-samples?q=bedrock) — runnable reference implementations.
- [Anthropic on Bedrock cookbook](https://github.com/anthropics/anthropic-cookbook/tree/main/third_party/Bedrock) — the Anthropic-published version.

## AWS — general

### Official reference
- [AWS Documentation home](https://docs.aws.amazon.com/) — every service, every API.
- [AWS Free Tier](https://aws.amazon.com/free/) — what stays free, what flips to billed.
- [Well-Architected Framework](https://aws.amazon.com/architecture/well-architected/) — the six pillars.
- [AWS Architecture Center](https://aws.amazon.com/architecture/) — reference architectures by use case.
- [AWS Builder's Library](https://aws.amazon.com/builders-library/) — how Amazon itself builds distributed systems. Free, high-signal.
- [AWS Solutions Library](https://aws.amazon.com/solutions/) — vetted reference implementations.

### Training and certification
- [AWS Skill Builder](https://skillbuilder.aws/) — official free + paid training.
- [AWS Training and Certification](https://aws.amazon.com/training/) — the cert ladder (Cloud Practitioner → Associate → Professional → Specialty).
- [AWS Workshops](https://workshops.aws/) — hands-on labs by service.
- [AWS Cloud Quest](https://aws.amazon.com/training/digital/aws-cloud-quest/) — gamified hands-on.

### Community and news
- [Last Week in AWS (Corey Quinn)](https://www.lastweekinaws.com/) — weekly digest, no-nonsense.
- [AWS What's New](https://aws.amazon.com/new/) — official release feed.
- [AWS Blogs](https://aws.amazon.com/blogs/) — by service / role. Compute and Architecture are high-signal.
- [re:Post](https://repost.aws/) — official community Q&A.
- [aws-samples on GitHub](https://github.com/aws-samples) — runnable sample apps.

### CLI and SDKs
- [AWS CLI v2 reference](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/index.html) — searchable command index.
- [boto3 (Python SDK)](https://boto3.amazonaws.com/v1/documentation/api/latest/index.html) — most-used SDK.
- [AWS CDK](https://docs.aws.amazon.com/cdk/v2/guide/home.html) — IaC in Python/TypeScript/Go.
- [Terraform AWS provider](https://registry.terraform.io/providers/hashicorp/aws/latest/docs) — the other dominant IaC path.

### Service deep-dives (start here for any service)
- [EC2 User Guide](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/) — compute, AMIs, instance types, security groups.
- [S3 User Guide](https://docs.aws.amazon.com/AmazonS3/latest/userguide/) — object storage, versioning, lifecycle, replication.
- [IAM User Guide](https://docs.aws.amazon.com/IAM/latest/UserGuide/) — identity, policies, roles, STS.
- [VPC User Guide](https://docs.aws.amazon.com/vpc/latest/userguide/) — networking. Largest learning curve in AWS.
- [Lambda Developer Guide](https://docs.aws.amazon.com/lambda/latest/dg/) — serverless functions.
- [RDS User Guide](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/) — managed relational DBs.
- [DynamoDB Developer Guide](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/) — managed NoSQL.
- [Route 53 Developer Guide](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/) — DNS, health checks.
- [CloudWatch User Guide](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/) — metrics, logs, alarms.

## Enterprise AI — security, identity, cost, scale

### AWS GenAI platform
- [AWS Generative AI](https://aws.amazon.com/ai/generative-ai/) — the umbrella product page.
- [Generative AI Innovation Center](https://aws.amazon.com/ai/generative-ai/innovation-center/) — AWS-led GenAI engagements.
- [Amazon SageMaker](https://aws.amazon.com/sagemaker/) — the broader ML platform (training, hosting, MLOps).
- [SageMaker JumpStart](https://aws.amazon.com/sagemaker/jumpstart/) — pre-built foundation-model deployments.

### Security and data isolation
- [Bedrock data protection](https://docs.aws.amazon.com/bedrock/latest/userguide/data-protection.html) — what AWS does / doesn't do with your prompts.
- [PrivateLink / VPC interface endpoints for Bedrock](https://docs.aws.amazon.com/bedrock/latest/userguide/usingVPC.html) — no public-internet egress.
- [Bedrock Guardrails](https://docs.aws.amazon.com/bedrock/latest/userguide/guardrails.html) — content filtering, denied topics, PII.
- [HIPAA Eligible Services](https://aws.amazon.com/compliance/hipaa-eligible-services-reference/) — what you can put PHI through.
- [AWS Artifact](https://aws.amazon.com/artifact/) — SOC, ISO, PCI reports for audits.
- [Shared Responsibility Model](https://aws.amazon.com/compliance/shared-responsibility-model/) — read this once before any security argument.

### GDPR and EU data protection
The horizontal compliance layer that touches both Amazon and Anthropic — DPAs, lawful-basis questions, sub-processor lists, regional data residency.

**Amazon / AWS / Bedrock:**
- [AWS GDPR Center](https://aws.amazon.com/compliance/gdpr-center/) — the consolidated GDPR landing page (DPA download, Standard Contractual Clauses, customer guidance).
- [AWS Data Processing Addendum (DPA)](https://aws.amazon.com/compliance/gdpr-center/) — downloadable from the GDPR Center; covers AWS services as data processor.
- [AWS Privacy Notice](https://aws.amazon.com/privacy/) — what AWS does as a controller vs. processor.
- [AWS Compliance Programs](https://aws.amazon.com/compliance/programs/) — full list (ISO 27001/27017/27018, SOC, C5, etc.).
- [AWS European Sovereign Cloud](https://aws.amazon.com/blogs/security/aws-european-sovereign-cloud/) — for the strictest EU residency / sovereignty requirements.
- [Data residency: where your data lives](https://aws.amazon.com/compliance/data-protection/) — region selection, control-plane vs data-plane location.
- [Bedrock and data privacy FAQs](https://aws.amazon.com/bedrock/faqs/) — see "Security and privacy" section: prompts/outputs not used to train base models, region-pinned.
- [Bedrock model invocation logging](https://docs.aws.amazon.com/bedrock/latest/userguide/model-invocation-logging.html) — opt-in; if you enable, those logs are *your* data under GDPR.

**Anthropic / Claude:**
- [Anthropic Trust Center](https://trust.anthropic.com/) — the GDPR / sub-processor / DPA hub.
- [Anthropic Privacy Policy](https://www.anthropic.com/legal/privacy) — controller-level disclosures.
- [Anthropic DPA](https://www.anthropic.com/legal/data-processing-addendum) — Anthropic-as-processor terms for API and Claude for Work / Enterprise.
- [Sub-processors list](https://trust.anthropic.com/) — under the Trust Center; review before signing the DPA.
- [Anthropic API data usage](https://privacy.anthropic.com/en/articles/7996868-is-my-data-used-for-model-training) — API inputs/outputs are not used to train models (commercial paid tier).
- [Privacy Help Center](https://privacy.anthropic.com/) — request data export / deletion (GDPR Articles 15 / 17 rights).

**Cross-cutting:**
- When the API customer is in the EU and Anthropic is the processor, AWS Bedrock as the intermediate path adds an extra processor — you sign DPAs with both. The Trust Center sub-processor list does not automatically capture Bedrock as a sub-processor; that relationship lives in your AWS contract.

### Identity and multi-account
- [IAM Identity Center (SSO)](https://aws.amazon.com/iam/identity-center/) — federated workforce identity.
- [AWS Organizations](https://aws.amazon.com/organizations/) — multi-account topology + SCPs.
- [Service Control Policies (SCPs)](https://docs.aws.amazon.com/organizations/latest/userguide/orgs_manage_policies_scps.html) — guardrails across all accounts.
- [Control Tower](https://aws.amazon.com/controltower/) — opinionated multi-account landing zone.
- [IAM policy evaluation logic](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_evaluation-logic.html) — the canonical "why was this denied" page. Read twice.

### Cost and governance
- [AWS Cost Explorer](https://aws.amazon.com/aws-cost-management/aws-cost-explorer/) — the dashboard everyone forgets to open.
- [Cost Allocation Tags](https://docs.aws.amazon.com/awsaccountbilling/latest/aboutv2/cost-alloc-tags.html) — how you actually split a bill across teams / workloads.
- [AWS Budgets](https://aws.amazon.com/aws-cost-management/aws-budgets/) — alerts before you regret it.
- [Service Quotas](https://aws.amazon.com/servicequotas/) — request limit increases (Bedrock TPM/RPM lives here).

### Amazon Q (AWS-native AI assistants)
- [Amazon Q Developer](https://aws.amazon.com/q/developer/) — IDE / chat for AWS-aware coding.
- [Amazon Q Business](https://aws.amazon.com/q/business/) — connect to your data sources for org-internal Q&A.
- [Amazon Q in QuickSight](https://aws.amazon.com/quicksight/q/) — natural-language BI.

### Observability for AI workloads
- [Amazon CloudWatch Logs Insights](https://docs.aws.amazon.com/AmazonCloudWatch/latest/logs/AnalyzingLogData.html) — query Bedrock invocation logs.
- [Bedrock model invocation logging](https://docs.aws.amazon.com/bedrock/latest/userguide/model-invocation-logging.html) — turn on per-account.
- [AWS X-Ray](https://aws.amazon.com/xray/) — distributed tracing including Bedrock calls.

## Topics — my running notes
