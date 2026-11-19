# Part B — Technical Architecture & Research Proposals

The following mechanisms are proposals for investigation and possible future implementation. They are not prerequisites for the manual methods in Part A.

## B1. Tagging and Tag Foldering

A system may automatically identify topics, subtopics, decisions and workstreams within conversations and organize them using semantic tags.

**Tag Foldering** is the logical organization of these tags into related topics and subtopics independently of chronological conversation order.

```text
Educational Application
├── Learning Engine
│   ├── Assessment
│   └── Prerequisites
├── Local AI Engine
│   ├── Model Selection
│   └── Memory Management
└── Content Packs
```

The structure acts as a logical filesystem for work context, not necessarily as a physical directory hierarchy. Cross-topic references and dependencies may be necessary. Whether hierarchical, graph-based or hybrid indexing is preferable remains an implementation question.

Users should not be required to manually maintain or select tags. Natural-language requests should be sufficient to identify relevant work, subject to clarification when necessary.

Stable project and tag identifiers should remain independent of display names. Renaming should not silently create a new identity; merging or splitting tags should preserve references and provenance. A topic may belong to multiple contexts. Compare manual tagging, automatic tagging and hybrid correction workflows before choosing an indexing structure. Automatic record references are a research requirement, not an assumption that tagging is already reliable.

## B2. Mini Handoff per Tag

Each tag may maintain a compact representation of its current work state:

- Objective and scope.
- Confirmed decisions and constraints.
- Proposals, assumptions and unresolved questions.
- Progress, results and verification status.
- Dependencies and references to original material.

The Mini Handoff is updated as relevant information changes. The original material remains available for verification or detailed retrieval.

An active-context manager, such as the separately proposed Adaptive Conversation Layer (ACL), could retrieve relevant Mini Handoffs instead of repeatedly loading complete historical responses.

This approach must be tested for information loss, stale state and retrieval errors. It is not assumed that a compact representation can replace all original context.

Investigate a protected core of critical constraints, approved decisions and their identifiers/source references. Preserve exact source wording when materially significant rather than recursively paraphrasing it. The core is protected against silent compression, not against authorized revision or deletion. Mini Handoffs may be manually organized and retrieved without ACL or automatic tagging.

## B3. Semantic Handoff Retrieval and Composition

When a user requests a handoff for a topic, the system should identify relevant tags semantically, retrieve their Mini Handoffs and investigate necessary dependencies.

Handoff by Composition assembles the selected work state into one portable handoff. The user does not need to know the internal tag structure.

```text
Natural-language request
        ↓
Semantic tag retrieval
        ↓
Mini Handoffs + necessary dependencies
        ↓
Source and conflict checks
        ↓
Composed handoff
```

The system should consult original sources when compact state is insufficient, ambiguous or inconsistent. Missing sources and unresolved conflicts should remain explicit.

Candidate escalation conditions include a missing required field, conflicting records, uncertain topic identity, stale revision, missing dependency or inability to trace a critical decision. Retrieve additional authorized sources, request clarification or abstain from the affected action. Semantic similarity alone does not establish relevance or completeness; measure retrieval precision, recall and missed critical dependencies against annotated tasks.

## B4. Information status and decision history

A proposed state representation should distinguish confirmed facts, user decisions, AI proposals, hypotheses, observed results, rejected approaches, superseded decisions and pending items.

A change in project state should not erase historical knowledge. An earlier decision may be superseded by a later authorized decision while remaining available in the history.

Suggested record metadata includes a stable identifier, timestamp, source, topic, information status and explicit references to records being revised.

The implementation must distinguish a genuine decision update from discussion of a possible change. Conflicting decisions from independent contributors must not be silently resolved by recency alone.

Separate information type, approval, verification and lifecycle state where useful: an approved decision can later be superseded, and an observed result may be disputed. Record who asserted or approved it, source reference, and whether evidence is a quotation, paraphrase or inference. Confidence may help prioritize review but never substitutes for source evidence or authorization. Uncertain extractions remain pending.

A correction invalidates an erroneous recording; supersession replaces a previously valid decision. Both can be represented by new linked records without implying the user changed their mind. A current-state view must exclude invalidated records while preserving authorized historical access.

## B5. Creation Flags and Incremental Handoff

A tag starts without a handoff creation flag. When it is included in a generated handoff, its flag is set. When the tag receives new relevant information, its flag is cleared. Inclusion in a new handoff sets it again.

This mechanism can identify work state that has changed since handoff generation.

Generation does not prove successful transfer or storage. For automatic synchronization, destination-specific versions and separate delivery acknowledgements are suggested extensions to investigate.

| Event | Creation flag | Delivery status |
| --- | --- | --- |
| New tag or updated state | Unset | Not synchronized for current revision |
| Handoff generated | Set | Not implied |
| Destination confirms storage | Set | Acknowledged for that revision |
| New relevant information | Unset | Earlier acknowledgement retained in history |

Incremental transfers should contain sufficient revision and baseline information to be interpreted correctly. If the receiving baseline is missing or inconsistent, a full handoff may be required.

### Revision-aware synchronization sketch

A Creation Flag is a generation-dirty indicator only, not a synchronization or conflict-resolution protocol. For a candidate implementation, associate it with a captured tag revision. If a tag changes while its handoff is being generated, the earlier generation must not mark the newer revision clean. Track delivery independently for each destination and exact revision. A failed or incomplete transfer remains pending; an acknowledgement must identify what was actually stored. On recovery, reconcile durable records with destination acknowledgements rather than trust a volatile flag. Retrying an already committed transfer should not create another state change. Stable operation identifiers, content digests, transactional writes or logical clocks are possible mechanisms to evaluate; none is prescribed here.

## B6. Automated Handoff and Persistent Memory Service

A dedicated service may have authorized access to relevant conversations and a user-selected memory directory, such as the `Memory` folder of CodexMemory or another compatible memory system.

Its responsibilities would include:

1. Extract decisions and relevant work state from authorized conversations.
2. Retrieve related previous records from memory.
3. Identify new information, changes and dependencies.
4. Generate complete or incremental handoffs as appropriate.
5. Transfer and store the handoffs automatically.
6. Verify successful storage and update synchronization state.
7. Retrieve the currently applicable decisions for subsequent work.

Possible triggers include task completion, periodic synchronization, user requests and context-limit warnings where such signals are available. Trigger policy and destination permissions remain under user control.

A tag update could trigger local memory synchronization, subject to permissions, batching and failure recovery. Automatic extraction may store candidate records without approving them. The user must be able to inspect, correct and approve consequential state; routine transfer of already approved records may be automated within explicitly granted permissions. Evaluate the burden of review as well as processing cost.

Direct local-folder access requires an actual supported integration or local service. The ability to produce a Markdown file does not imply access to a user's filesystem.

### Append-Only History

The automated service must retain previous memory entries rather than deleting or overwriting them when a decision changes. A new record identifies the earlier record it supersedes.

Illustrative example:

| Record | Decision | Status |
| --- | --- | --- |
| D001 | Maximum model size: 1B | Superseded by D002 |
| D002 | Maximum model size: 3B | Current |

Both records remain available; a current-state index can point to D002 without requiring the system to reprocess the complete history.

Append-only operation is a rule for automated state updates, not a restriction on the authorized user's right to manage or delete their data. Retention and deletion mechanisms must respect applicable privacy requirements.

## B7. Validation, conflicts and failure recovery

A handoff receiver should validate the availability of its required sources, dependencies, resources and execution capabilities before continuing work.

Research and implementation should address:

- Conflicting contributions and concurrent revisions.
- Duplicate or partially delivered handoffs.
- Stale baselines and missing dependencies.
- Uncertain extraction of decisions.
- Recovery after interrupted generation or transfer.
- Integrity of the historical record and its source references.
- Idempotent processing of repeated transfers.

Stable identifiers, version tracking and integrity verification are suggested mechanisms, not prescribed implementation details.

### Candidate failure scenarios and expected behavior

| Scenario | Expected behavior to test |
| --- | --- |
| Two contributors revise the same baseline | Preserve both branches; flag conflict; obtain authorized resolution |
| AI suggestion or joke recorded as approved | Prevent promotion; if propagated, append correction and invalidate affected current views |
| Wrong topic or missing dependency retrieved | Escalate to source retrieval or clarification; report incomplete state |
| Critical constraint altered in repeated transfers | Detect discrepancy against source/core; do not silently accept |
| Truncated or linguistically corrupted handoff | Detect structural or semantic incompleteness where possible; request recovery or source verification |
| Duplicate, partial or interrupted delivery | Avoid duplicate effects; retain pending status and reconcile on retry |
| Sensitive data or malicious instructions imported | Restrict disclosure and execution; quarantine or review as appropriate |
| Unsupported schema or unavailable baseline | Preserve original artifact; reject unsafe incremental application or request full handoff |

These are proposed acceptance behaviors, not tested guarantees. A validator cannot establish semantic correctness merely by accepting a syntactically valid file.

## B8. Interoperability, privacy and authorization

The framework should support human-readable text and Markdown independently of any optional machine-readable representation or transport mechanism.

A future technical specification may define a structured schema, capability negotiation and transport conventions. No mandatory wire format or API is defined in this version.

Automatic retrieval and transfer should be limited to authorized sources and destinations. Exported handoffs should not contain credentials or unnecessary sensitive information. Users should retain control over what is exported and shared.

Imported handoffs can contain untrusted instructions or false claims. Receiving systems must not treat imported project content as privileged instructions or authorization to perform external actions.

The persistence layer should protect integrity, access permissions and recovery. Automatically preserving history does not by itself prevent malicious modification or unauthorized disclosure.

A candidate implementation should isolate imported data from privileged configuration, parse structured fields as data, validate allowed operations, enforce least-privilege permissions outside the language model, and require independent authorization for sensitive actions. Sandboxing and read-only access where appropriate reduce exposure but do not prove semantic safety. A content digest can detect changes relative to a trusted reference; it does not establish authorship or approval. Signatures or authenticated channels may be evaluated separately.

### Optional metadata sketch (illustrative, not normative)

```yaml
uahp_version: "0.3"
schema_version: "example-1"
handoff_id: H003
project_id: example-edu
tag_ids: [local-ai]
revision: 3
base_revision: 2
source: hypothetical-conversation
records:
  - id: D004
    type: user_decision
    lifecycle: current
    approval: explicit
    evidence: {kind: quote, ref: U18}
    supersedes: [D001]
    text: "Evaluate models up to 3B parameters."
```

A future schema may add timestamps, author identity, correction references, verification status, destination and content digest, with defined semantics and canonicalization rules. Schema version is distinct from document and state revision. Unknown fields should not be silently treated as approval; unsupported versions should be preserved and explicitly migrated or rejected. Migration should preserve identity, provenance and meaning and retain the original when authorized. Markdown-only exchange remains valid for Part A.
## B10. Relationship to other proposals

UAHP may complement the Collaborative Pre-Prompt Mode (CPPM) for task preparation and the Adaptive Conversation Layer (ACL) for selective context management. Tag Foldering, Mini Handoffs and persistent memory may also form part of a broader AI operating architecture.

None of these companion proposals is required to adopt the manual collaboration methods or investigate the handoff concept independently.

ACL and CPPM are companion concepts, not assumed available implementations or required interfaces. A manually selected Mini Handoff and a standalone local store are sufficient to investigate basic transfer; automated active-context selection can be evaluated separately. Aenaos AI OS is a prospective implementation environment, not a dependency or evidence of completed integration.

---

## Candidate refinements for implementation trials

The protected core should be selected from applicable, authorized decisions and critical requirements, with user review of consequential classification; uncertain candidates must not be silently promoted. Preserve exact wording where meaning depends on it. Routine transfer is distinct from approval.

Candidate conflict record (illustrative only):

```yaml
conflict_id: X001
type: incompatible_claims
records: [C001, D010]
status: pending
resolution_ref: null
```

Use globally scoped artifact identifiers and explicit parent revisions to represent forks; do not require a single monotonic identifier across independent contributors. Define canonicalization, approval evidence and compatibility rules before claiming machine interoperability. Preserve unsupported records without granting them authority. Test Markdown-to-structured conversion against human-reviewed meaning rather than assuming round-trip fidelity. Retention, access and deletion policies must be configured by the authorized owner.

### Candidate threat and detection matrix

| Threat or failure | Candidate detection/control | Limitation |
| --- | --- | --- |
| False approval or spoofed provenance | Compare authorized source and identity; escalate uncertainty | Syntax cannot establish authority |
| Malicious imported instructions | Isolate data, restrict operations externally | No complete semantic detector assumed |
| Sensitive leakage | Scoped export, human review, access controls | Automated screening may miss information |
| Stale baseline or concurrent fork | Parent revision and conflict checks | Requires trusted state |
| Altered critical constraint | Compare protected source text or trusted digest | Digest does not prove authorship |
| Missing dependency or wrong topic | Reference checks and retrieval escalation | Semantic gaps may remain undetected |
| Partial or duplicate delivery | Revision-specific acknowledgments and idempotent retry | Requires durable destination support |
| Truncated or corrupted content | Parse and completeness checks; source recovery | Well-formed text can still be wrong |

When a consequential check fails, block affected automatic application, preserve evidence where authorized, and request resolution or recover a valid baseline. Mechanisms remain untested candidates.
