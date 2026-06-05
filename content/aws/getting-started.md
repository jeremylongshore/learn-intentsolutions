---
title: "Getting started — the AWS mental model"
date: 2026-06-05
description: "The shape of AWS before any individual service makes sense."
weight: 10
---

Before any service makes sense, the shape of AWS itself has to make sense. Three concepts unlock the rest.

## 1. Region → AZ → resource

Almost every AWS resource lives inside a **region** (e.g. `us-east-1`), and most live inside an **availability zone** (`us-east-1a`). A region is a geographic area; AZs are isolated data centers inside that area connected by low-latency fiber.

Why this matters: pricing, latency, and blast radius all change with the region. A bad day in `us-east-1` does not touch `eu-west-2`. A resource in `us-east-1a` going dark does not touch `us-east-1b`.

A handful of services are **global** (IAM, Route 53, CloudFront, S3 bucket names). The rest are regional.

## 2. IAM is the front door

Nothing happens without an IAM identity (user, role, or service) being allowed to do the action. Every API call is `(principal, action, resource, condition)` evaluated against IAM policies.

Default-deny. If no policy explicitly allows it, it's denied. If any policy explicitly denies it, it's denied no matter what.

The mental model that saves time later: **roles, not users**. A role is an identity that anything can temporarily assume; a user is a permanent identity with credentials. Production patterns use roles for everything; users are mostly for humans logging into the console.

## 3. Resources reference other resources by ARN

Every resource has an Amazon Resource Name: `arn:aws:<service>:<region>:<account-id>:<resource-id>`. IAM policies, event rules, cross-account access — everything routes through ARNs.

If you remember the ARN shape, you can navigate the console quickly: the bits in the URL match the bits in the ARN.

## What to read next

- Compute starts at **EC2** — but the modern shape is usually **Lambda** for events and **ECS/Fargate** or **EKS** for long-running services.
- Storage starts at **S3** for blobs, **EBS** for block storage attached to EC2, **RDS** for managed Postgres/MySQL.
- Networking is **VPC** — and **VPC** is the rabbit hole, learn it in a dedicated session.
- Identity is **IAM** plus **AWS Organizations** for multi-account. Most non-trivial AWS work is multi-account.

## Gotchas

- **`us-east-1` is special.** It hosts global service control planes (IAM, Route 53, CloudFront, billing). When `us-east-1` is degraded, even non-`us-east-1` workloads can break in surprising ways.
- **The free tier is a trap if you forget about it.** Set a Billing Alert in CloudWatch the moment you open the account. Set it low.
- **The console hides region behind a dropdown.** A resource you created "yesterday" but can't find today is almost always in a different region.
