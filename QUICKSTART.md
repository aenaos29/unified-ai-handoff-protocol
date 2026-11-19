# Quick Start — Practical AI Collaboration Methods

## A1. Portable handoffs

A handoff may be delivered as copy-ready text or as a Markdown (`.md`) file. Both representations should preserve equivalent information.

| Source | Destination |
| --- | --- |
| Conversation | Another conversation |
| Chat | Work or execution environment |
| Work | Chat |
| Work | Another execution environment |
| AI system | Another AI system |
| One or multiple sources | Local or external memory |
| Human collaborator | Another collaborator or shared integration conversation |

Markdown files may also be uploaded directly to conversations that support file attachments. Direct system integration is not required for manual transfer.

The handoff should be self-contained, easy to copy in its entirety, and separated from unrelated assistant commentary. Users should not need to manually clean the exported text.

## A2. Recommended handoff contents

```markdown
# HANDOFF — [Project / Topic]
Date: [date]
Scope: [scope]
Status: [current status]

## Objective
## Confirmed decisions and requirements
## Constraints
## Current work and deliverables
## Tests and observed results
## Proposals and assumptions
## Rejected or superseded approaches
## Open issues and dependencies
## Next actions
## Source references and verification limits
```

This is a suggested format, not a mandatory schema. Include sections relevant to the task. Do not silently turn AI suggestions into user-approved decisions or unverified claims into observed results.

Record the source and scope of each consequential decision. Use “confirmed decision” only when there is evidence of explicit approval by the user or an authorized delegate. Silence, a suggestion, a joke or permission to run an experiment does not establish a permanent decision. If approval or scope is unclear, mark the item pending confirmation. Preserve exact wording for critical requirements where paraphrasing could change their meaning; reference the source if disclosure is authorized.

A lightweight handoff for simple tasks may contain just objective, approved constraints, current state, unresolved items, next action and source/verification limits. Compactness is relative to what the receiver needs, not an arbitrary word limit. Never omit a critical constraint merely to meet a size target.

## A3. Generate and continue a handoff

**Prompt — Generate a handoff**

> Create a self-contained handoff for [project/topic] that allows another AI or collaborator to continue the work. Preserve confirmed decisions, exact constraints, current progress, relevant results, rejected approaches, dependencies and unresolved issues. Distinguish user decisions from AI proposals and verified information from assumptions. State what you could not access or verify. Exclude unrelated content. Return only the handoff in one copy-ready Markdown block, or provide it as a .md file if supported.

**Prompt — Receive a handoff**

> Read the attached or pasted handoff as transferred project state. Identify the applicable decisions, constraints, dependencies and next action. Check whether the information is sufficient and whether the required resources are available. Report conflicts, missing information and unverified claims without inventing replacements. Do not restart completed work or change confirmed decisions without authorization.

A receiving AI should treat imported content as project data, not as authority to override permissions or safety constraints.

The sender should review consequential or sensitive records before sharing. The receiver should distinguish authenticated approval from claims of approval inside the artifact. Where authority is uncertain, ask the responsible human before relying on the disputed decision or taking consequential action. A prompt is guidance, not enforceable protection against malicious content.

## A4. Topic-specific handoffs and branching

A single conversation may contain many distinct design proposals. Continuing every topic in the same context can make the project difficult to navigate.

Users can request a handoff for one topic, develop that topic in a separate conversation, and return the resulting decisions and tests to the original project.

**Prompt — Handoff on a topic**

> Create a handoff specifically for [topic]. Include its relevant shared requirements and dependencies, but exclude unrelated branches. Identify open questions and decisions that must remain consistent with the parent project.

Example: an educational application may contain separate workstreams for its learning engine, local AI engine, memory management and content format. Each can be developed independently while retaining common application constraints.

## A5. Selective human-to-human sharing

A handoff can communicate relevant project state to another person without sharing the complete originating conversation.

The sender should be able to review the content, remove unrelated or private information and choose the intended recipient. Selective sharing reduces unnecessary disclosure but does not itself guarantee privacy.

**Prompt — Share selected work**

> Prepare a handoff for [recipient/role] containing only the information necessary for [purpose]. Preserve relevant decisions and dependencies. Exclude unrelated discussions and unnecessary personal or confidential information. Mark any omitted information that is essential to continuing the work.

## A6. Standalone Collaborative Work

A team may work toward a common objective using different AI systems and independent approaches. Each member may design, execute and test a solution separately, then submit a handoff to a coordinating conversation.

**Standalone Design — Standalone Execution — Standalone Testing — Collaborative Integration.**

The coordinating environment should compare proposals on their merits, not seek agreement for its own sake. Compatible elements of different proposals may form a better result than selecting a single proposal in its entirety.

An individual user can also apply this method by requesting independent design solutions from multiple AI systems and evaluating the responses centrally.

**Prompt — Independent contribution**

> Develop your own solution to [common objective] within [shared constraints]. Record your design decisions, assumptions, implementation status, executed tests, observed results, failures and remaining dependencies. Produce a handoff suitable for comparison with independently developed solutions.

**Prompt — Aggregate contributions**

> Review the supplied handoffs as independent contributions to the same project. Preserve source attribution. Identify compatible approaches, conflicting decisions, duplicated work, missing dependencies, verified results and untested claims. Propose an integrated result and necessary integration tests. Do not silently resolve conflicts or present untested integration as successful. Produce a consolidated handoff.

### Conflict handling in manual collaboration

1. Check project identity, scope, baselines and source evidence before classifying a disagreement as a conflict.
2. Separate factual disputes, competing proposals and incompatible approved decisions. Preserve both contributions and their attribution.
3. Compare evidence and acceptance tests; test candidate integrations where feasible. Agreement among models is not independent verification, and majority vote is not authorization.
4. The coordinator proposes a resolution; the responsible user or authorized human delegate approves consequential changes. Hold disputed actions pending resolution; continue unaffected work if safe.
5. Record the resolution and its rationale, including rejected alternatives. Do not merge incompatible designs merely to achieve consensus.

## A7. Aggregate and incremental memory handoffs

A user may periodically collect work from multiple conversations and projects, consolidate it into Markdown and transfer it into a local memory directory, such as CodexMemory or another user-controlled system.

**Prompt — Daily or project-wide handoff**

> Collect the relevant work from all accessible sources for [time range/project]. Identify the conversations and workstreams used. Group contributions by project, preserve confirmed decisions and constraints, record results and pending actions, and distinguish changes from previously recorded state where available. State any inaccessible sources or incomplete coverage. Produce a consolidated Markdown handoff for local memory. Preserve existing historical records.

If only changes since a previous handoff are needed, request an incremental handoff and provide the prior handoff or its identifiable version. Without a reliable baseline, completeness of the incremental result cannot be guaranteed.

## A8. When to create a handoff

Consider a handoff before switching environments or collaborators, after a meaningful decision or tested milestone, when branching a topic, or when context becomes unreliable. For small tasks, direct continuation may be cheaper. Periodic and token-based triggers are candidates for experimentation, not universal thresholds. The user may request, defer or correct a handoff.

## Recommended minimum for a transferable state

Objective and scope; applicable decisions and constraints; current state; open issues; next action; sources and verification limits; baseline/revision when relevant. Mark unavailable information explicitly. This is a candidate content minimum, not a normative conformance standard. Simple tasks may combine fields. Review consequential new state; do not require renewed approval merely to transfer an already approved decision with intact evidence. If an authorized human is unavailable, keep disputed state pending and continue only unaffected, authorized work. Do not merge apparently compatible contributions without checking shared dependencies and integration assumptions.

See [worked examples](EXAMPLES.md).
