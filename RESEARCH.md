# Research annex

## B9. Computational efficiency and research questions

The central question is whether the additional processing required by these mechanisms is justified by the resulting improvement in work continuity, quality and overall resource efficiency.

Potential overhead includes semantic classification, tag maintenance, Mini Handoff generation, persistent storage, retrieval, dependency resolution and synchronization.

Potential benefits include reduced active context, reduced repeated retrieval, fewer user reminders, faster task resumption and fewer errors caused by lost decisions.

Neither savings nor quality improvements are assumed. Short, simple conversations may not benefit from the same mechanisms as long, multi-topic or collaborative projects.

### Proposed comparative evaluation

Compare equivalent tasks under four conditions:

1. Full conversation history, subject to model context limits.
2. Conventional conversation summaries.
3. Structured handoffs.
4. Tag-based Mini Handoffs and composed or incremental handoffs.

Use the same model, task requirements and acceptance criteria where possible. Include the full lifecycle cost of creating, maintaining, transferring and using state, not just the final prompt length.

| Metric | Evaluation target |
| --- | --- |
| Total processing tokens | All maintenance and execution stages |
| Latency | State creation, retrieval and task resumption |
| Storage and synchronization cost | Total additional state overhead |
| Decision recall | Correct retrieval of currently applicable decisions |
| Historical fidelity | Preservation of source and superseded information |
| User reminders | Number of repeated requirements or corrections |
| Task quality | Predefined acceptance criteria |
| Conflict detection | Identification of incompatible contributions |
| Transfer fidelity | Information loss or drift across successive handoffs |

Evaluate single-topic, multi-topic, cross-provider and collaborative tasks. Repeated transfer chains can test whether decisions, uncertainty and constraints survive successive handoffs without semantic drift.

Record regressions and negative results. Investigate whether adaptive activation of the proposed mechanisms offers better cost-effectiveness than universal activation.

### Proposed pilot and acceptance criteria

Start with Part A against conventional summaries and full history before implementing advanced automation. Use two or three representative projects, including short and multi-topic tasks. A candidate pilot of 10–20 repeated-transfer chains can expose failure modes but is not sufficient for broad statistical claims. Prepare a human-reviewed reference state containing approved decisions, exact critical constraints, rejected options, corrections and pending issues. Freeze inputs, task instructions, evaluation rubric and model versions where available; repeat runs and record variability, access failures and incomplete outputs.

Measure correct applicable decision recall against the reference, false approval rate, critical-constraint preservation, history accuracy, user review/correction time, time to a valid resumed action, and all processing/storage/transfer costs. Record user reminders as a practical proxy, not a replacement for ground truth. Evaluate manual versus automatic tagging separately and then test the combined system to expose interaction costs. Include cross-provider transfer and conflicting contributors; do not assume their errors are independent.

Candidate pilot gates (proposed, not validated): no false approval or lost critical constraint in the observed test cases; no unauthorized action; no silent unresolved conflict; no degradation of task acceptance relative to the chosen baseline. Pre-register quantitative recall and cost targets appropriate to the project before running comparative trials. Report failures and trade-offs even when average token use decreases. A minimal local Markdown generator/validator is a possible reference implementation; it need not include semantic tagging or any companion architecture. No such implementation or benchmark result is claimed here.

## Pilot execution refinements

Pre-register exact tasks, model identifiers, input ordering, repetitions, scoring rubric, cost accounting and stop conditions. Record unavailable version or sampling controls. Report per-condition distributions and failed runs, not only averages. Include missing-context cases and score correct uncertainty, unsupported reconstruction, unnecessary clarification and recovery cost. Include deliberately ambiguous approval and conflicts. Compare human review time and repeated approval burden; distinguish new decisions from transfer checks. A critical gate violation blocks the affected trial action and is recorded as a failure; quarantine unsafe artifacts where appropriate. Zero observed failures in a small pilot does not establish a zero failure rate. No sample size or acceptance threshold is claimed validated.

A minimal implementation may generate Markdown and validate required content and references; semantic correctness remains a separate evaluation. Once the manual pilot provides evidence, test manual, automatic and hybrid tagging, protected-core fidelity, and synchronization separately, then measure combined lifecycle costs. No pilot has yet been completed in this draft.
