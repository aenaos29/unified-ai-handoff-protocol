# Unified AI Handoff Protocol (UAHP)

*A proposed framework for AI work-state transfer and context continuity*

**Version:** 0.3 — Public Research Draft  
**Date:** 2026-11-19  
**Author:** Aenaos  
**Origin:** Aenaos Suite / Aenaos Educational

## 1. Introduction

AI-assisted work increasingly spans conversations, execution environments, models, providers and human collaborators. Yet decisions, constraints, progress and unresolved questions often remain confined to the conversation in which they originated.

Users may have to repeat previous decisions, reconstruct project state, transfer entire conversations or manually assemble information from multiple sources. AI systems may repeatedly process large amounts of historical context to recover a small amount of relevant information.

A **handoff** is a portable representation of the relevant state of a task or project, intended to allow another conversation, AI system, execution environment or human collaborator to continue work without reconstructing its entire history.

This proposal has two audiences:

- Users who can improve their workflows today through structured handoffs and existing AI interfaces.
- Developers, researchers and AI providers who may investigate native support for handoff generation, context organization, persistence and synchronization.

UAHP is a proposed conceptual framework, not an implemented or standardized protocol. Its novelty, interoperability and performance are not assumed.

The contribution sought is the synthesis of portable work-state transfer, explicit information status, independent collaboration and lifecycle evaluation, rather than the invention of each underlying mechanism. Existing decision records, version control, retrieval systems and memory products may provide complementary capabilities. Their comparative merits remain to be studied.

A handoff is a **transfer artifact**; persistent memory is a **store**; context management selects information for active work. A handoff can feed memory, and memory can supply a later handoff, but these functions are distinct. UAHP prioritizes provider-independent transfer and does not require replacement of existing memory systems.

## 2. Objectives and scope

- Reduce repetitive reminders of previous decisions and constraints.
- Reduce repeated searches through the entire available context.
- Preserve continuity across conversations, environments and AI providers.
- Enable selective sharing without exposing an entire conversation.
- Support independent design, execution and testing followed by collaborative integration.
- Retain historical decisions while identifying the currently applicable state.
- Investigate total computational cost rather than assuming that additional processing is beneficial.

The framework is provider-independent and does not require a particular model, API, memory product or shared account.

## 3. Non-goals

UAHP is not a chat-history replication system, a replacement for version control, a security boundary, or a claim of formal standardization. It does not grant execution permissions, require universal adoption or prescribe a particular database, model or transport. The manual method can be evaluated independently of all proposed automation.

---

## Part A — Practical method

Use portable Markdown or text to transfer relevant work state, not an entire conversation. Preserve approved decisions, constraints, evidence, progress, uncertainty and next actions. Topic-specific branching, selective sharing, independent contributions and incremental memory handoffs are available without native integration. See [Quick Start](QUICKSTART.md) for the complete manual method.

## Part B — Research direction

Investigate tag foldering, per-tag Mini Handoffs, semantic retrieval and composition, protected constraints, decision history, incremental generation and authorized synchronization. These mechanisms are candidates, not implemented capabilities. See [Technical annex](TECHNICAL.md) and [Research annex](RESEARCH.md).

## Relationship to existing practice

| Practice | Complementary role | Question for UAHP |
| --- | --- | --- |
| Architecture decision records | Record decisions and rationale | Can a portable state include decisions plus tests and pending work? |
| Issue trackers | Track work and dependencies | Can selected state travel between tools without duplicating tracking? |
| Version control | Preserve revisions and branches | Can existing revision mechanisms be reused rather than rebuilt? |
| Retrieval and memory systems | Store and retrieve context | Can a portable handoff preserve status and authority across stores? |
| Structured summaries and agent state files | Compact or transfer context | Does explicit approval, provenance and lifecycle improve fidelity? |

This is a conceptual comparison, not a literature review or novelty finding. Manual transfer is provider-independent in design; automated access remains platform-dependent. Security-aware design does not itself provide a security guarantee.

## Roadmap

First evaluate manual handoffs against summaries and full history. Develop a minimal local generator/validator to support reproducible trials; assess cross-provider fidelity. Investigate advanced mechanisms separately before integrating them. Preserve negative results and revise the proposal accordingly.

## Documents

- [Quick Start](QUICKSTART.md)
- [Examples](EXAMPLES.md)
- [Technical annex](TECHNICAL.md)
- [Research annex](RESEARCH.md)
- [Review methodology and findings](REVIEW.md)
- [Acknowledgments](ACKNOWLEDGMENTS.md)
- [Change log](CHANGELOG.md)

No implementation, standardization, measured benefit or provider endorsement is claimed. Copyright © 2026 Aenaos. The documentation is licensed under [Creative Commons Attribution 4.0 International (CC BY 4.0)](LICENSE).

**From conversation continuity to persistent work continuity.**
