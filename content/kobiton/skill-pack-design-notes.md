---
title: "Mapping what a Kobiton skill pack would look like"
date: 2026-06-10
description: "Notes on applying my saas-packs template (24 skills × 3 tiers; same pattern as the Databricks / LangChain / crypto / pentesting packs) to the Kobiton MCP plugin surface."
weight: 60
---

## What I'm mapping

I run an open-source repo called `claude-code-plugins`. Inside it there's a `saas-packs/` directory of reusable packs that wrap a vendor's surface — `databricks-pack` is the live reference implementation (v1.0.0, 24 skills across three tiers), with sibling packs for LangChain, crypto tooling, and pentesting. The template is stable enough that I can hold it up against a new vendor surface and see what would and wouldn't fit before writing any code.

The Kobiton review work I've been doing for six weeks gave me a good empirical look at a different surface — real-device mobile testing, MCP-mediated, with a pain catalog I documented across three review cycles. So this page is me asking: *if I applied my own pack template to Kobiton, what would the resulting `kobiton-pack` look like?* Study exercise, not build plan.

## Why a skill pack instead of more tools in the upstream plugin

A *tool* (in the MCP sense) is an executable capability inside the MCP plugin — `reserveDevice`, `confirmAppUpload`, `getSessionArtifacts`. The vendor ships those; they're load-bearing. A *skill* (in the Claude Code sense) is reading-comprehension knowledge that activates when the agent needs it — a markdown file with imperative instructions about *how to use* the underlying surface well. Skills don't expand capability; they expand operational judgment.

Packs sit in the skill layer. A vendor pack is much easier to land than a tool change: no API surface to argue about, no upstream review of behavior, no compatibility break. It can be authored independently — complementing the plugin without coordinating on every release. For an audit-shaped engagement like the one I just finished, the pack is the natural follow-on: the review surfaced operational pain points; a pack converts them into reading-comprehension knowledge anyone installing the plugin can pick up.

## The 3-tier shape my template uses

The `databricks-pack` template is 24 skills split 12 / 6 / 6 across three tiers:

| Tier | Slots | What lives here |
|---|---|---|
| **Standard** | 12 | Install, auth, hello-world, local dev loop, SDK patterns, two most-common workflows, common errors, debug bundle, rate limits, security basics, pre-launch checklist. Day-1 onboarding. |
| **Pro** | 6 | CI recipes, workflow conversions, artifact decoding, runtime deltas, cost tuning, advisory skills for stacks the vendor doesn't first-class. Production integration. |
| **Flagship** | 6 | Multi-env setup, observability, incident runbook, triage, picker strategy, reference architecture. Operational excellence. |

Tier logic is progression of urgency and depth, not difficulty. Standard is everyone's first read. Flagship is what you reach for when something is on fire or you're designing the whole SDLC around the vendor.

## Where Kobiton's surface differs from Databricks

The template fits cleanly, with three honest content-shape adjustments rather than structural deviation.

**Three-surface coverage maps directly.** Databricks-pack covers REST + Python SDK + Spark SQL. Kobiton has the same three-surface shape — Kobiton REST API, Appium / WebDriver W3C driver protocol, and the Kobiton MCP server (JSON-RPC over HTTPS).

**Multi-host install is real here.** Databricks-pack assumes Claude Code is the host. The Kobiton MCP plugin already ships install paths for five agentic CLIs — Claude Code, Cursor, Codex CLI, Gemini CLI, Copilot CLI — each with subtly different `mcp.json` semantics. The install-auth skill has to cover all five. Content widening, not structural change.

**Driver-protocol parity adds a wrinkle.** Kobiton runs an Appium-compatible runtime plus a Kobiton-extended runtime, with a capability flag (`kobiton:runtime`) toggling between them. Practitioners coming from upstream Appium hit subtle deltas — most notably a W3C-strict log endpoint rejection that makes `driver.getLogs('logcat')` silently fail. Databricks has no analog. A dedicated Pro-tier skill is where this content lives.

None of those deviations break the template — they shift content allocation between tiers.

## Where the novel content would live

The skills with the most public-research-headroom are the ones where public docs are sparse — where writing a `SKILL.md` would teach the agent something the official documentation doesn't cover. Three pockets stand out:

1. **App-upload resilience.** The async-parser race after `confirmAppUpload` returns 200 OK, the missing diagnostic body when parsing fails, the version-expiry contradiction between two adjacent endpoints. Highest-impact pain across the review cycles. No consolidated public guide.

2. **Session-artifacts decoding.** Sessions emit a rich artifact surface — video, session-recording logs in a proprietary format, logcat / NSLog, screenshots, page source, network trace, crash logs. The shape of each is partially documented; the operational read — what each field means, how to pull them into a debug bundle, what to look for first — is not.

3. **Observability.** Which signals fire on the current server vs which don't, the OpenTelemetry signal taxonomy (log events vs trace spans), the gating env vars controlling instrumentation. Once-and-done Flagship-tier reference. No vendor publishes it.

Framing these as "most public-research-headroom" rather than "highest-value sells" — the point isn't what converts best, it's where a reading-comprehension artifact would meaningfully improve agent behavior versus duplicating what the vendor already ships.

## The build economics

Rough sizing against the existing template:

- **v0.1 MVP** — 10 skills, the highest-leverage subset (install-auth, hello-world, common errors, two most-novel Standard, two most-novel Pro, three Flagship anchors). ~**95 hours**.
- **v1.0.0 full pack** — 24 skills + companion docs + scaffolding + pre-release pressure-testing. ~**243 hours**.

Solo-capacity estimates against my own template, not a quote. At 25 hr/wk the full build is ~10 weeks; at half-time, 12–14. The v0.1 subset is plausibly a 2–3 week focused build.

## Risks I'd watch for

Three honest failure modes if I shipped this:

1. **Skills duplicate the vendor's own docs and become churn.** Mitigation: strict scoping — pack documents *operational* knowledge (what to do when X breaks), not *reference* knowledge (what the tool returns). Quarterly review pass to prune anything the vendor has since covered.

2. **Pack ships and nobody finds it.** Mitigation: cross-link from `tonsofskills.com` (the marketplace surface I maintain) plus a launch post tying it back to the broader pack template. The hardest part of a new vendor pack isn't writing the skills — it's the distribution moment.

3. **Pack accidentally exposes engagement-private content.** Mitigation: a `grep` scrub against partner-private terms before every commit, plus a documented scrub policy in the pack's `000-docs/`. Reading-comprehension content leaks names and commercial terms more easily than code does; the template doesn't enforce against that by default.

## What I'm watching next

- Whether the three-surface model (REST + driver protocol + JSON-RPC over MCP) generalizes enough that the *next* vendor pack I scope falls out of the template even faster. Three packs is a pattern; four is a methodology.
- Whether a vertical with this much undocumented operational pain needs 14 Standard-tier slots instead of 12 — i.e., whether the template needs a per-vertical flex range rather than a hard 12-cap.
- Whether novel-content skills get more traction as standalone reading versus bundled into a tiered pack. Bundling helps agents find the right depth; standalone gets more installs when novel content isn't gated behind a pack browse. No empirical data on this yet from my own packs.
