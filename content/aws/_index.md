---
title: "AWS"
date: 2026-06-05
description: "Personal notes on AWS plus the canonical reference links worth bookmarking."
---

Working through AWS services as I need them. Each note is a focused page on one thing: what it is, how it works, the gotchas, the way I'll remember it next time.

## Official AWS reference

The canonical first-stop links. Most other "tutorials" you find online lag behind these by months.

- [AWS Documentation home](https://docs.aws.amazon.com/) — every service, every API.
- [AWS Free Tier](https://aws.amazon.com/free/) — what stays free, what flips to billed, expiration windows.
- [Well-Architected Framework](https://aws.amazon.com/architecture/well-architected/) — the six pillars (operational excellence, security, reliability, performance, cost, sustainability). Read it once even if you skim.
- [AWS Architecture Center](https://aws.amazon.com/architecture/) — reference architectures by use case.
- [AWS Builder's Library](https://aws.amazon.com/builders-library/) — how Amazon itself builds and operates distributed systems. Best free reading on AWS.
- [AWS Solutions Library](https://aws.amazon.com/solutions/) — vetted reference implementations.

## Training and certification

- [AWS Skill Builder](https://skillbuilder.aws/) — official free + paid training. The Cloud Practitioner Essentials course is free and a sane on-ramp.
- [AWS Training and Certification](https://aws.amazon.com/training/) — cert paths (Cloud Practitioner → Associate → Professional → Specialty).
- [AWS Workshops](https://workshops.aws/) — hands-on labs by service, free, runnable in your own account.
- [AWS Cloud Quest](https://aws.amazon.com/training/digital/aws-cloud-quest/) — gamified hands-on labs. Useful for muscle memory.

## Community and news

- [Last Week in AWS (Corey Quinn)](https://www.lastweekinaws.com/) — weekly newsletter, no-nonsense commentary on AWS announcements. The shortcut to knowing what changed.
- [AWS What's New](https://aws.amazon.com/new/) — official release feed.
- [AWS Blogs](https://aws.amazon.com/blogs/) — by service / role. The Compute and Architecture blogs are the high-signal ones.
- [re:Post](https://repost.aws/) — official community Q&A (the new AWS forums).
- [aws-samples on GitHub](https://github.com/aws-samples) — runnable sample apps. Search before you write.

## CLI and SDK reference

- [AWS CLI v2 reference](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/index.html) — searchable command index.
- [boto3 (Python SDK)](https://boto3.amazonaws.com/v1/documentation/api/latest/index.html) — most-used SDK; docs are excellent.
- [AWS CDK](https://docs.aws.amazon.com/cdk/v2/guide/home.html) — infrastructure as code in Python/TypeScript/Go.
- [Terraform AWS provider](https://registry.terraform.io/providers/hashicorp/aws/latest/docs) — the other dominant IaC path.

## Service deep-dives (start here for any service)

- [EC2 User Guide](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/) — compute, AMIs, instance types, security groups.
- [S3 User Guide](https://docs.aws.amazon.com/AmazonS3/latest/userguide/) — object storage, versioning, lifecycle, replication.
- [IAM User Guide](https://docs.aws.amazon.com/IAM/latest/UserGuide/) — identity, policies, roles, STS. Read the [policy evaluation logic page](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_evaluation-logic.html) twice.
- [VPC User Guide](https://docs.aws.amazon.com/vpc/latest/userguide/) — networking. The largest learning curve in AWS.
- [Lambda Developer Guide](https://docs.aws.amazon.com/lambda/latest/dg/) — serverless functions, event sources, runtimes.
- [RDS User Guide](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/) — managed relational DBs (Postgres, MySQL, etc.).
- [DynamoDB Developer Guide](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/) — managed NoSQL. The [data modeling guide](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/best-practices.html) is essential.
- [Route 53 Developer Guide](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/) — DNS, health checks, routing policies.
- [CloudWatch User Guide](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/) — metrics, logs, alarms.

## My notes
