---
title: "What the research says about community formation around developer tools"
date: 2026-06-09
description: "Notes on the OSS-community-formation literature — Steinmacher cluster on social barriers, Casalnuovo et al. on pre-existing social ties, Bao et al. on follower-count as the strongest retention predictor."
weight: 20
---

## The question I was actually asking

When somebody asks "how do we build a vibrant community around our tool" — what does the academic literature actually say is happening when one forms? Not the LinkedIn-thread version. The empirical version. I went looking because "vibrant community" was about to become a deliverable and I didn't want to design against vibes.

Short answer: a lot, surprisingly consistent, and almost none of it routes through marketing.

## The Steinmacher cluster — what they actually found

The canonical line is Steinmacher and colleagues, mostly through CSCW between 2015 and 2019 (Steinmacher et al. 2015, *CSCW*, 300 citations; Steinmacher, Treude & Gerosa 2019, *IEEE Software*; plus the 2018 CSCW Journal extension). What surprised me reading their work back-to-back is how flatly they reject the technical-barriers explanation. The reason newcomers drop out before landing their first contribution is almost never the build system or the test suite. It's social: nobody answered the issue, contribution norms weren't visible, the review came back terse and they couldn't tell if they were welcome.

That reframes the on-ramp problem. If dropoff is social, making the README more comprehensive doesn't help. What helps is making the human surface visible.

## The Bao quantitative ratifier

The paper I keep coming back to is Bao et al. 2021 (*IEEE TSE*) — 917 projects, 75,046 contributors, predicting long-time-contributor status at AUC > 0.75 across 1/2/3-year intervals. The load-bearing finding: **follower count is the single most important predictor**. Not commits, not language familiarity, not company affiliation. The visible social tie.

That's a hard claim at first — it sounds like the popularity-contest version of OSS. But lined up against the Steinmacher "social barriers" finding it locked into place. Follower count is a proxy for pre-existing community embedding. People with visible ties show up *as people*, not as anonymous PR-openers; the on-ramp is socially easier because there's pre-context.

Casalnuovo et al. 2015 (*ESEC/FSE*) showed the upstream version: developers preferentially join GitHub projects where they have prior relationships, and pre-existing ties combined with language overlap predict higher productivity both initially and cumulatively. Casalnuovo: social ties drive joining. Bao: they drive staying.

## Geiger reframes maintainership

The piece that pulled it together is Geiger, Howard & Irani 2021 (*CSCW*): OSS maintainers don't just maintain code — they "perform complex and often-invisible interpersonal and organizational work to keep their projects operating as active communities of users and contributors." That sentence sat with me. The labor that holds the community together is the interpersonal labor, done by a small number of identifiable people doing the part nobody puts in the job description.

## Why marketing-driven community formation doesn't show up

This is the part worth internalizing. I went looking for counter-evidence — papers arguing that marketing campaigns, paid promotion, or content-driven funnels successfully build sustained developer communities — and couldn't find any. The literature is consistent that communities form when (a) the tool solves a real practitioner pain, (b) the on-ramp is socially welcoming, and (c) a small number of identifiable maintainers do the interpersonal work. None of those are marketing tasks. Marketing can amplify a community that exists; the empirical record doesn't show it as the formation mechanism.

Useful prior to hold when designing community engineering work: lower the social barrier to first contribution, make contributor identity visible (Bao operationalized), resource the interpersonal-labor side of maintainership. Not a campaign.

## What I'm watching next

Two open threads. First — what does the Bao finding look like inside corporate-OSS where follower count is less a free-floating reputation signal and more shaped by employer brand? I suspect it still holds but the mechanism shifts. Second — is there rigorous work on the *transition* from "vendor-curated repo with a handful of named contributors" to "self-sustaining community where the maintainer stops being the bottleneck"? That phase change is what every developer-tool engagement is trying to engineer, and I haven't seen a clean academic study of it.
