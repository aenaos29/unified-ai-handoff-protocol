# Worked examples

## A9. Worked example — Educational application

The following fictional example illustrates the format; it is not evidence of a completed Aenaos test. Source identifiers refer to hypothetical messages and logs, not actual documents.

```markdown
# HANDOFF — Example educational application / Local AI
Project ID: example-edu
Topic ID: local-ai
Revision: 3; baseline: 2
Objective: Generate a grounded question from a textbook paragraph.

## Confirmed requirements
- D002: Operate offline. [User message U12, explicit approval]
- D004: Evaluate models up to 3B parameters. [U18, explicit approval]
- C001: “Do not introduce facts absent from the source paragraph.” [U12]

## Current work and observed results
- T001: Model A returned a question but introduced an unsupported fact.
  Status: failed grounding test. [Hypothetical log L01]

## Proposals and assumptions
- P001: Try Model B next. [AI proposal; not approved]
- H001: Smaller models may reduce latency. [Untested hypothesis]

## History
- D001: Evaluate models up to 1B. Superseded by D004. [U09]
- R001: Earlier record claimed cloud use was approved; recording error.
- R002: Corrects R001; no cloud-use approval exists. [U12]

## Open issues and dependencies
- O001: Model B availability and device memory not verified.
- Required source: textbook paragraph; not included in this export.

## Next action
- Retrieve authorized source and verify device resources.
- Obtain approval for P001 before changing the test plan.

## Verification limits
- Illustrative records only; no actual execution or device test claimed.
```

The receiver can distinguish a failed test from a proposed experiment, and a genuine decision change from a false historical recording. The missing source prevents a grounded test until it is supplied.

---

## A second example — conflicting branches (fictional)

Project `example-edu`, baseline revision 3. D004 permits evaluation of models up to 3B. C002 is an approved offline-only constraint. Contributor A proposes a cloud fallback (P010); contributor B reports that a local test passed (R010), but supplies no log. A third handoff claims the cloud fallback was approved (D010), citing an ambiguous message: “try it if needed.” The source is unavailable.

- C002 remains applicable; P010 is not approved. D010 is pending confirmation, not a replacement for C002.
- R010 is a reported result, not independently verified. Request its log and test conditions.
- Conflict X001 links C002 and D010; it remains open pending authorized clarification. No cloud operation is authorized.
- A candidate correction to D010 is pending until the source is recovered. Preserve the original claim; if erroneous, invalidate it through a linked correction, not a fictional change of user decision.
- Continue unaffected local verification if resources and permissions permit. Otherwise report the blocker. Integration remains untested.

This example illustrates intended behavior, not evidence that a system reliably performs it.
