---
title: "Why tools spread (or don't) inside enterprise teams"
date: 2026-06-09
description: "Notes on the TAM and user-innovation literatures — perceived usefulness and pain-driven adoption as the two convergent answers to why tooling diffuses."
weight: 30
---

## The question

I wanted to know what the literature actually says about why a developer tool catches on inside a team versus dying on the vine. Not the vendor-blog version. The version that survives a rigorous read.

Two academic lineages have been working this for decades — one from information systems, one from innovation management — and they end up at the same load-bearing claim from opposite directions.

## The TAM lineage

TAM citation counts feel surreal. Venkatesh & Bala 2008 (*Decision Sciences*) sits at **7,819 citations**; the original Davis line goes back to 1989. Legris, Ingham & Collerette 2003 (*Information & Management*, 4,280 citations) is the critical review.

The predictive chain TAM gives you: **perceived usefulness → perceived ease-of-use → intention → adoption.** Perceived usefulness does the heavy lifting; ease-of-use matters but is secondary. That's worth holding because the practitioner instinct is usually the opposite — polish the UX, then adoption follows. The literature says: if the tool isn't useful for the specific problem, frictionless onboarding doesn't save it.

Hu, Chau, Sheng & Tam 1999 (*JMIS*) on physicians adopting telemedicine showed that in professional-expert contexts, perceived usefulness *in the specific domain* dominates ease-of-use even more strongly. Hu et al. 2019 layered in trust as a separate construct beyond the original TAM variables. Legris et al. makes the honest point: TAM is robust but partial — environmental and organizational variables matter beyond user perceptions.

## The user-innovation lineage

This one starts with von Hippel 2001 (*MIT Sloan Management Review*, 725 citations) on lead users and innovation by user communities. His thesis: lead users are *systematically* the source of high-impact innovations in software, and user communities self-organize around solving shared pain that vendors fail to address. Füller, Jawecki & Mühlbacher 2007 (*J Business Research*) extended that finding to non-software domains.

The practitioner-canonical version of the same mechanism is Christensen, Dillon, Hall & Duncan 2016 — *Competing Against Luck* — where customers "hire" products to do specific jobs, and understanding the job predicts adoption better than understanding the customer demographic. Hankammer et al. 2019 (*J Cleaner Production*) operationalized this with structured importance-vs-satisfaction measurement; in their consumer-electronics study they found "11 of 30 needs [are] currently not well satisfied" — and those 11 are exactly where the next features should land.

## Where the two converge

Reading these side by side, the two lineages converge on the same claim from opposite ends. TAM says: adoption is predicted by perceived usefulness in the specific user's context. User-innovation says: the highest-impact innovations come from understanding the specific pain a practitioner is trying to resolve. Both land at **a tool spreads when it visibly closes a pain that practitioners articulate themselves**, and stalls when it ships features that solve problems the marketing team named.

That convergence is what gives the claim its weight — two schools that don't talk to each other reaching the same conclusion through different methods.

## The DevOps adoption ratifier

Khan et al. 2022 (*IEEE Access*, systematic review on DevOps adoption) grounds this in something a developer-tool engagement actually faces. Their top adoption-killer findings: *"lack of collaboration and communication, lack of skill and knowledge, complicated infrastructure, lack of management, lack of DevOps approach, and trust confidence problems."* Every item is social or organizational. None are "the tool doesn't have feature X." The marginal driver of adoption isn't technical capability — it's whether the tool fits the social, practice, and political environment of its host.

Pain-articulation work and social-fit work matter more than the feature checklist.

## What I'm watching next

Two things to dig into further. First — empirical work on the time delay between pain articulation and feature adoption? Anecdotally the gap feels like months or years, but I haven't seen a clean measurement. Second — the user-innovation literature is heavier on consumer products than developer tooling. I'd love to see a Hankammer-style importance-satisfaction study run against a real developer-tool catalog. The methodology is portable; nobody seems to have done it at scale.
