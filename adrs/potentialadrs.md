# Potential ADRs

## Purpose and Review Basis

This is a review inventory of labelled architecture decision records, earlier versions, unnumbered design proposals and explicit ADR requests from the estate documents and Slack discussions. Inclusion does not establish that an item warrants an ADR or that the team has accepted it.

The working threshold is Edward’s: an ADR is warranted when changing a decision would be hard, time-consuming or expensive. Cross-system ownership, safety and contractual boundaries should also be assessed for their cost of change, including coordination, migration and operational consequences. A quick code change is not necessarily a cheap architectural change.

For each item, the next review should determine: whether it merits an ADR; whether it is decided or open; whether it duplicates another item; and whether it belongs instead in a domain design, implementation note, principle or requirement. Those classifications have not been imposed in this inventory.

## How to Read This Inventory

- H-01–H-11 identify Helen’s revised integrated ADRs; M-01–M-11 identify Matt’s earlier integrated ADRs. These inventory keys disambiguate reused source IDs and are not new ADR numbers.
- RO, AC, CS and VG retain Matt’s source namespaces for Rides, Animal Care, Crowd/Site Operations and Visitor Growth.
- C-01–C-08 identify Chris’s unnumbered enhancement proposals. R-01–R-04 identify Helen’s review requests. U-01 records the CRM decision confirmed in this conversation. S-01–S-06 collect additional decision-related source material.
- Labelled ADR fields are transcribed from the source tables, with formatting normalised. Missing context, alternatives, dates or approval information have not been invented. Summaries and review observations are explicitly labelled.
- Source assertions, especially about regulation, existing animal systems, tagging and statistical validation, are preserved for review rather than independently certified as facts.

## Confirmed Decision From This Conversation

### U-01 — Buy a CRM Rather Than Build One

Written in: Edward’s instruction in this Codex conversation, 16 September 2026. [Conversation](codex://threads/01a0a1a2-151f-7682-96dc-adbdc17dccc0). Earlier request: [Pete’s Slack message asking for a CRM buy-versus-build ADR](https://architecturek-iz73826.slack.com/archives/C0C0J2MSLTG/p1789488220033629).

| Field | Recorded Information |
|---|---|
| Decision Status | Decided: Edward confirms that the team has decided to buy a CRM. |
| Decision | Buy an existing CRM rather than develop a bespoke CRM. |
| Rationale Supplied | CRM is a standard capability; Edward sees no benefit in building it rather than buying it. |
| Integration Requirement | The chosen product must provide an API or another suitable mechanism, such as MCP or CLI, for integration with other estate systems. These are alternatives, not a requirement to support all three. |
| Alternative Rejected | Build a bespoke CRM. |
| Product Selection | Not specified. Salesforce was mentioned as an example in the catch-up discussion, not as the selected product. |
| Consequences / Further Evaluation | No detailed cost, licence, migration or exit assessment was supplied with this confirmation. Product fit and integration suitability remain to be evaluated. |
| ADR Qualification | Awaiting review against the agreed cost-of-change threshold. The buy decision is confirmed regardless of how it is ultimately documented. |

## Labelled ADR Inventory

There are 46 labelled source entries: 11 in Helen’s revision, 11 in Matt’s earlier integrated version, and six in each of four capability documents. This is a count of source entries, not unique architectural decisions.

| Inventory Key | Source ID | Source Title |
|---|---|---|
| H-01 | ADR-01 | Domain-owned systems of record |
| H-02 | ADR-02 | Event-driven estate integration |
| H-03 | ADR-03 | Edge-first MQTT ingestion |
| H-04 | ADR-04 | Deterministic control remains local |
| H-05 | ADR-05 | AI is advisory and evidence-backed |
| H-06 | ADR-06 | Provider-neutral AI boundary |
| H-07 | ADR-07 | Privacy-minimised sensing and consent |
| H-08 | ADR-08 | Curated analytics, not a second truth |
| H-09 | ADR-09 | APIs for commands; events for facts |
| H-10 | ADR-10 | Animal records are human-authored and reconciled to the accredited record |
| H-11 | ADR-11 | Welfare owns visibility; prediction is bounded-autonomous |
| M-01 | ADR-01 | Domain-owned systems of record |
| M-02 | ADR-02 | Event-driven estate integration |
| M-03 | ADR-03 | Edge-first MQTT ingestion |
| M-04 | ADR-04 | Deterministic control remains local |
| M-05 | ADR-05 | AI is advisory and evidence-backed |
| M-06 | ADR-06 | Provider-neutral AI boundary |
| M-07 | ADR-07 | Privacy-minimised sensing and consent |
| M-08 | ADR-08 | Curated analytics, not a second truth |
| M-09 | ADR-09 | APIs for commands; events for facts |
| M-10 | ADR-10 | Selective build versus buy |
| M-11 | ADR-11 | Zero-trust device and retrieval boundary |
| RO-01 | ADR-RO-01 | Ride Operations Platform as system of record |
| RO-02 | ADR-RO-02 | Safety controls remain local and deterministic |
| RO-03 | ADR-RO-03 | Edge-first telemetry resilience |
| RO-04 | ADR-RO-04 | Event-driven estate integration |
| RO-05 | ADR-RO-05 | AI is advisory for maintenance |
| RO-06 | ADR-RO-06 | Provider-neutral model boundary |
| AC-01 | ADR-AC-01 | Animal Care Platform as system of record |
| AC-02 | ADR-AC-02 | Edge-first resilience |
| AC-03 | ADR-AC-03 | Event-driven estate integration |
| AC-04 | ADR-AC-04 | AI is advisory only |
| AC-05 | ADR-AC-05 | Specialised AI by risk profile |
| AC-06 | ADR-AC-06 | Provider-neutral inference boundary |
| CS-01 | ADR-CS-01 | Anonymous counting by default |
| CS-02 | ADR-CS-02 | Queue estimates are derived state |
| CS-03 | ADR-CS-03 | Edge-first ingestion |
| CS-04 | ADR-CS-04 | Event-driven integration |
| CS-05 | ADR-CS-05 | AI is advisory |
| CS-06 | ADR-CS-06 | Separate operational and public views |
| VG-01 | ADR-VG-01 | Commerce is deterministic |
| VG-02 | ADR-VG-02 | Consent is first-class |
| VG-03 | ADR-VG-03 | Operational truth stays in domains |
| VG-04 | ADR-VG-04 | Controlled offline entry |
| VG-05 | ADR-VG-05 | AI recommendations are advisory |
| VG-06 | ADR-VG-06 | Growth uses experimentation |

## Helen’s Revised Integrated Architecture

### H-01 — Domain-owned systems of record

Original identifier: ADR-01.

Written in / source: [Helen’s Architecture Kata 2026.docx, shared 15 September 2026](https://architecturek-iz73826.slack.com/archives/C0C0J2MSLTG/p1789484308135269), §7 Architectural decision records; Word export of her Pages revision.

Version / status note: Helen’s revised integrated architecture. Source status is Proposed, not confirmed team acceptance.

Status: Proposed

Decision: Use four domain-aligned platforms, each authoritative for its records.

Consequences: Clear accountability; requires governed integration.

Rejected alternative: Central enterprise monolith.

Enforcement / review: Enforce ownership in APIs, schemas and access reviews.


### H-02 — Event-driven estate integration

Original identifier: ADR-02.

Written in / source: [Helen’s Architecture Kata 2026.docx, shared 15 September 2026](https://architecturek-iz73826.slack.com/archives/C0C0J2MSLTG/p1789484308135269), §7 Architectural decision records; Word export of her Pages revision.

Version / status note: Helen’s revised integrated architecture. Source status is Proposed, not confirmed team acceptance.

Status: Proposed

Decision: Exchange curated, versioned facts through the Estate Event Platform.

Consequences: Loose coupling and replay; eventual consistency.

Rejected alternative: Point-to-point database integration.

Enforcement / review: Contract and idempotency tests; controlled replay policy.


### H-03 — Edge-first MQTT ingestion

Original identifier: ADR-03.

Written in / source: [Helen’s Architecture Kata 2026.docx, shared 15 September 2026](https://architecturek-iz73826.slack.com/archives/C0C0J2MSLTG/p1789484308135269), §7 Architectural decision records; Word export of her Pages revision.

Version / status note: Helen’s revised integrated architecture. Source status is Proposed, not confirmed team acceptance.

Status: Proposed

Decision: Use zoned gateways with identity, validation, buffering, replay and local thresholds.

Consequences: Outage resilience; adds fleet management and reconciliation.

Rejected alternative: Every device publishes directly to cloud.

Enforcement / review: Quarterly outage tests and device-health SLO.


### H-04 — Deterministic control remains local

Original identifier: ADR-04.

Written in / source: [Helen’s Architecture Kata 2026.docx, shared 15 September 2026](https://architecturek-iz73826.slack.com/archives/C0C0J2MSLTG/p1789484308135269), §7 Architectural decision records; Word export of her Pages revision.

Version / status note: Helen’s revised integrated architecture. Source status is Proposed, not confirmed team acceptance.

Status: Proposed

Decision: Keep ride interlocks, life-support alarms and bounded entry validation local.

Consequences: Strong independence; limits remote automation.

Rejected alternative: Cloud-controlled operational protection.

Enforcement / review: Architecture test prohibits cloud or AI dependencies in critical paths.


### H-05 — AI is advisory and evidence-backed

Original identifier: ADR-05.

Written in / source: [Helen’s Architecture Kata 2026.docx, shared 15 September 2026](https://architecturek-iz73826.slack.com/archives/C0C0J2MSLTG/p1789484308135269), §7 Architectural decision records; Word export of her Pages revision.

Version / status note: Helen’s revised integrated architecture. Source status is Proposed, not confirmed team acceptance.

Status: Proposed

Decision: Require evidence, policy filtering and accountable approval for consequential outcomes.

Consequences: Lower autonomy; better safety and auditability.

Rejected alternative: Autonomous operational action.

Enforcement / review: Schema and workflow controls; risk acceptance required for any expansion.


### H-06 — Provider-neutral AI boundary

Original identifier: ADR-06.

Written in / source: [Helen’s Architecture Kata 2026.docx, shared 15 September 2026](https://architecturek-iz73826.slack.com/archives/C0C0J2MSLTG/p1789484308135269), §7 Architectural decision records; Word export of her Pages revision.

Version / status note: Helen’s revised integrated architecture. Source status is Proposed, not confirmed team acceptance.

Status: Proposed

Decision: Use versioned internal inference contracts and retain evaluation assets independently.

Consequences: Portability; compatibility effort.

Rejected alternative: Provider-specific logic embedded in domains.

Enforcement / review: Annual replacement and cost rehearsal.


### H-07 — Privacy-minimised sensing and consent

Original identifier: ADR-07.

Written in / source: [Helen’s Architecture Kata 2026.docx, shared 15 September 2026](https://architecturek-iz73826.slack.com/archives/C0C0J2MSLTG/p1789484308135269), §7 Architectural decision records; Word export of her Pages revision.

Version / status note: Helen’s revised integrated architecture. Source status is Proposed, not confirmed team acceptance.

Status: Proposed

Decision: Use anonymous counts by default and centralise consent decisions.

Consequences: Reduced privacy risk; less individual tracking.

Rejected alternative: Persistent individual location tracking.

Enforcement / review: Contract tests and recurring privacy review.


### H-08 — Curated analytics, not a second truth

Original identifier: ADR-08.

Written in / source: [Helen’s Architecture Kata 2026.docx, shared 15 September 2026](https://architecturek-iz73826.slack.com/archives/C0C0J2MSLTG/p1789484308135269), §7 Architectural decision records; Word export of her Pages revision.

Version / status note: Helen’s revised integrated architecture. Source status is Proposed, not confirmed team acceptance.

Status: Proposed

Decision: Build analytical projections from events; commands return to owning domains.

Consequences: Cross-estate insight; eventual consistency.

Rejected alternative: Shared operational database.

Enforcement / review: Freshness and reconciliation checks.


### H-09 — APIs for commands; events for facts

Original identifier: ADR-09.

Written in / source: [Helen’s Architecture Kata 2026.docx, shared 15 September 2026](https://architecturek-iz73826.slack.com/archives/C0C0J2MSLTG/p1789484308135269), §7 Architectural decision records; Word export of her Pages revision.

Version / status note: Helen’s revised integrated architecture. Source status is Proposed, not confirmed team acceptance.

Status: Proposed

Decision: Use authenticated APIs for immediate commands and events for completed business facts.

Consequences: Clear intent and consistency boundaries; two integration modes.

Rejected alternative: Everything as events or direct database calls.

Enforcement / review: API/event naming and architecture tests.


### H-10 — Animal records are human-authored and reconciled to the accredited record

Original identifier: ADR-10.

Written in / source: [Helen’s Architecture Kata 2026.docx, shared 15 September 2026](https://architecturek-iz73826.slack.com/archives/C0C0J2MSLTG/p1789484308135269), §7 Architectural decision records; Word export of her Pages revision.

Version / status note: Helen’s revised integrated architecture. Source status is Proposed, not confirmed team acceptance.

Status: Proposed

Decision: Publish population as a range with confidence, method and inputs for operational use. The recorded figure, and any regulatory or studbook return, is human-authored. Treat the accredited sector record (ZIMS) as authoritative for regulated animal data; the Animal Care Platform owns workflow, telemetry and evidence and reconciles to it.

Consequences: Honest uncertainty operationally and a defensible regulated record; adds reconciliation effort and a dependency on an external system.

Rejected alternative: A single integer produced by the vision model; or making the estate platform the authoritative regulated record.

Enforcement / review: Schema rejects population events lacking interval, method and inputs; contract test asserts no regulated field is model-written; reconciliation exception report at each stocktake.

Review note: This replaces the subject previously numbered ADR-10. Its external-system ownership differs from AC-01; ZIMS adoption and the estate’s licensing/accreditation position need evidence.


### H-11 — Welfare owns visibility; prediction is bounded-autonomous

Original identifier: ADR-11.

Written in / source: [Helen’s Architecture Kata 2026.docx, shared 15 September 2026](https://architecturek-iz73826.slack.com/archives/C0C0J2MSLTG/p1789484308135269), §7 Architectural decision records; Word export of her Pages revision.

Version / status note: Helen’s revised integrated architecture. Source status is Proposed, not confirmed team acceptance.

Status: Proposed

Decision: Animal Care owns visibility state and may suppress publication unilaterally. Visitor Journey consumes a sanitised, read-only projection. Predicted visible windows publish without per-instance approval, bounded by post-model policy filters.

Consequences: Commercial incentive cannot reach the welfare signal; demonstrates autonomy calibrated to consequence; requires reliable automatic suspension.

Rejected alternative: Visitor platform reads animal records directly; or human approval for every prediction.

Enforcement / review: Contract test asserts no clinical field crosses the boundary; an accuracy breach auto-suspends publication.

Review note: This replaces the subject previously numbered ADR-11. Reconcile its permitted automatic predictions with the advisory-only wording elsewhere.


## Matt’s Earlier Integrated Architecture

### M-01 — Domain-owned systems of record

Original identifier: ADR-01.

Written in / source: [Matt’s Von_Digitalis_Estates_Integrated_Architecture.docx, shared 12 September 2026](https://architecturek-iz73826.slack.com/archives/C0C0J2MSLTG/p1789227304285259), §7 Architectural decision records.

Version / status note: Earlier integrated architecture; retained for comparison with Helen’s revision, not as a second current decision set.

Status: Proposed

Decision: Use four domain-aligned platforms, each authoritative for its records.

Consequences: Clear accountability; requires governed integration.

Rejected alternative: Central enterprise monolith.

Enforcement / review: Enforce ownership in APIs, schemas and access reviews.


### M-02 — Event-driven estate integration

Original identifier: ADR-02.

Written in / source: [Matt’s Von_Digitalis_Estates_Integrated_Architecture.docx, shared 12 September 2026](https://architecturek-iz73826.slack.com/archives/C0C0J2MSLTG/p1789227304285259), §7 Architectural decision records.

Version / status note: Earlier integrated architecture; retained for comparison with Helen’s revision, not as a second current decision set.

Status: Proposed

Decision: Exchange curated, versioned facts through the Estate Event Platform.

Consequences: Loose coupling and replay; eventual consistency.

Rejected alternative: Point-to-point database integration.

Enforcement / review: Contract and idempotency tests; controlled replay policy.


### M-03 — Edge-first MQTT ingestion

Original identifier: ADR-03.

Written in / source: [Matt’s Von_Digitalis_Estates_Integrated_Architecture.docx, shared 12 September 2026](https://architecturek-iz73826.slack.com/archives/C0C0J2MSLTG/p1789227304285259), §7 Architectural decision records.

Version / status note: Earlier integrated architecture; retained for comparison with Helen’s revision, not as a second current decision set.

Status: Proposed

Decision: Use zoned gateways with identity, validation, buffering, replay and local thresholds.

Consequences: Outage resilience; adds fleet management and reconciliation.

Rejected alternative: Every device publishes directly to cloud.

Enforcement / review: Quarterly outage tests and device-health SLO.


### M-04 — Deterministic control remains local

Original identifier: ADR-04.

Written in / source: [Matt’s Von_Digitalis_Estates_Integrated_Architecture.docx, shared 12 September 2026](https://architecturek-iz73826.slack.com/archives/C0C0J2MSLTG/p1789227304285259), §7 Architectural decision records.

Version / status note: Earlier integrated architecture; retained for comparison with Helen’s revision, not as a second current decision set.

Status: Proposed

Decision: Keep ride interlocks, life-support alarms and bounded entry validation local.

Consequences: Strong independence; limits remote automation.

Rejected alternative: Cloud-controlled operational protection.

Enforcement / review: Architecture test prohibits cloud or AI dependencies in critical paths.


### M-05 — AI is advisory and evidence-backed

Original identifier: ADR-05.

Written in / source: [Matt’s Von_Digitalis_Estates_Integrated_Architecture.docx, shared 12 September 2026](https://architecturek-iz73826.slack.com/archives/C0C0J2MSLTG/p1789227304285259), §7 Architectural decision records.

Version / status note: Earlier integrated architecture; retained for comparison with Helen’s revision, not as a second current decision set.

Status: Proposed

Decision: Require evidence, policy filtering and accountable approval for consequential outcomes.

Consequences: Lower autonomy; better safety and auditability.

Rejected alternative: Autonomous operational action.

Enforcement / review: Schema and workflow controls; risk acceptance required for any expansion.


### M-06 — Provider-neutral AI boundary

Original identifier: ADR-06.

Written in / source: [Matt’s Von_Digitalis_Estates_Integrated_Architecture.docx, shared 12 September 2026](https://architecturek-iz73826.slack.com/archives/C0C0J2MSLTG/p1789227304285259), §7 Architectural decision records.

Version / status note: Earlier integrated architecture; retained for comparison with Helen’s revision, not as a second current decision set.

Status: Proposed

Decision: Use versioned internal inference contracts and retain evaluation assets independently.

Consequences: Portability; compatibility effort.

Rejected alternative: Provider-specific logic embedded in domains.

Enforcement / review: Annual replacement and cost rehearsal.


### M-07 — Privacy-minimised sensing and consent

Original identifier: ADR-07.

Written in / source: [Matt’s Von_Digitalis_Estates_Integrated_Architecture.docx, shared 12 September 2026](https://architecturek-iz73826.slack.com/archives/C0C0J2MSLTG/p1789227304285259), §7 Architectural decision records.

Version / status note: Earlier integrated architecture; retained for comparison with Helen’s revision, not as a second current decision set.

Status: Proposed

Decision: Use anonymous counts by default and centralise consent decisions.

Consequences: Reduced privacy risk; less individual tracking.

Rejected alternative: Persistent individual location tracking.

Enforcement / review: Contract tests and recurring privacy review.


### M-08 — Curated analytics, not a second truth

Original identifier: ADR-08.

Written in / source: [Matt’s Von_Digitalis_Estates_Integrated_Architecture.docx, shared 12 September 2026](https://architecturek-iz73826.slack.com/archives/C0C0J2MSLTG/p1789227304285259), §7 Architectural decision records.

Version / status note: Earlier integrated architecture; retained for comparison with Helen’s revision, not as a second current decision set.

Status: Proposed

Decision: Build analytical projections from events; commands return to owning domains.

Consequences: Cross-estate insight; eventual consistency.

Rejected alternative: Shared operational database.

Enforcement / review: Freshness and reconciliation checks.


### M-09 — APIs for commands; events for facts

Original identifier: ADR-09.

Written in / source: [Matt’s Von_Digitalis_Estates_Integrated_Architecture.docx, shared 12 September 2026](https://architecturek-iz73826.slack.com/archives/C0C0J2MSLTG/p1789227304285259), §7 Architectural decision records.

Version / status note: Earlier integrated architecture; retained for comparison with Helen’s revision, not as a second current decision set.

Status: Proposed

Decision: Use authenticated APIs for immediate commands and events for completed business facts.

Consequences: Clear intent and consistency boundaries; two integration modes.

Rejected alternative: Everything as events or direct database calls.

Enforcement / review: API/event naming and architecture tests.


### M-10 — Selective build versus buy

Original identifier: ADR-10.

Written in / source: [Matt’s Von_Digitalis_Estates_Integrated_Architecture.docx, shared 12 September 2026](https://architecturek-iz73826.slack.com/archives/C0C0J2MSLTG/p1789227304285259), §7 Architectural decision records.

Version / status note: Earlier integrated architecture; retained for comparison with Helen’s revision, not as a second current decision set.

Status: Proposed

Decision: Buy commodity capabilities where fit; build estate-specific workflow, policy and optimisation differentiators.

Consequences: Faster delivery; integration and vendor constraints.

Rejected alternative: Build everything or outsource all domain logic.

Enforcement / review: Capability assessment, exit criteria and total-cost review.

Version note: Helen explicitly removed this generic principle. U-01 records the later, concrete CRM buy decision.


### M-11 — Zero-trust device and retrieval boundary

Original identifier: ADR-11.

Written in / source: [Matt’s Von_Digitalis_Estates_Integrated_Architecture.docx, shared 12 September 2026](https://architecturek-iz73826.slack.com/archives/C0C0J2MSLTG/p1789227304285259), §7 Architectural decision records.

Version / status note: Earlier integrated architecture; retained for comparison with Helen’s revision, not as a second current decision set.

Status: Proposed

Decision: Authorize every device, user, workload and retrieval source explicitly.

Consequences: Lower compromise risk; additional operational controls.

Rejected alternative: Trusted internal network and unrestricted knowledge corpus.

Enforcement / review: Certificate, access and adversarial retrieval tests.

Version note: Helen explicitly moved this control into §6 rather than retaining a separate ADR.


## Ride Operations

### RO-01 — Ride Operations Platform as system of record

Original identifier: ADR-RO-01.

Written in / source: [Matt’s Ride_Operations_C4_Capability.docx, shared 12 September 2026](https://architecturek-iz73826.slack.com/archives/C0C0J2MSLTG/p1789215670905659), §7 Architectural decision records. [Repository Markdown copy](https://github.com/PeteH-GGB-UK/OReillyArchitectureKata-2026/blob/main/architecture/Ride_Operations_C4_Capability.md).

Version / status note: Capability draft. No individual status, approval date or decision owner is supplied in this ADR table.

Context: Data arrives from engineers, operations and devices.

Decision: Own status, inspections, defects and maintenance history in the Ride Operations Platform.

Consequence: Clear accountability and auditability; requires integration from telemetry and estate systems.


### RO-02 — Safety controls remain local and deterministic

Original identifier: ADR-RO-02.

Written in / source: [Matt’s Ride_Operations_C4_Capability.docx, shared 12 September 2026](https://architecturek-iz73826.slack.com/archives/C0C0J2MSLTG/p1789215670905659), §7 Architectural decision records. [Repository Markdown copy](https://github.com/PeteH-GGB-UK/OReillyArchitectureKata-2026/blob/main/architecture/Ride_Operations_C4_Capability.md).

Version / status note: Capability draft. No individual status, approval date or decision owner is supplied in this ADR table.

Context: Connectivity and AI cannot be trusted for immediate safety action.

Decision: Keep certified ride controls and interlocks outside the cloud and AI path.

Consequence: Preserves safety independence; limits remote automation.


### RO-03 — Edge-first telemetry resilience

Original identifier: ADR-RO-03.

Written in / source: [Matt’s Ride_Operations_C4_Capability.docx, shared 12 September 2026](https://architecturek-iz73826.slack.com/archives/C0C0J2MSLTG/p1789215670905659), §7 Architectural decision records. [Repository Markdown copy](https://github.com/PeteH-GGB-UK/OReillyArchitectureKata-2026/blob/main/architecture/Ride_Operations_C4_Capability.md).

Version / status note: Capability draft. No individual status, approval date or decision owner is supplied in this ADR table.

Context: Estate connectivity is patchy.

Decision: Use zoned gateways with buffering, health checks and replay.

Consequence: Retains operational data through outages; adds managed estate hardware.


### RO-04 — Event-driven estate integration

Original identifier: ADR-RO-04.

Written in / source: [Matt’s Ride_Operations_C4_Capability.docx, shared 12 September 2026](https://architecturek-iz73826.slack.com/archives/C0C0J2MSLTG/p1789215670905659), §7 Architectural decision records. [Repository Markdown copy](https://github.com/PeteH-GGB-UK/OReillyArchitectureKata-2026/blob/main/architecture/Ride_Operations_C4_Capability.md).

Version / status note: Capability draft. No individual status, approval date or decision owner is supplied in this ADR table.

Context: Queue, visitor, workforce and analytics services need ride status.

Decision: Publish curated ride domain events through the Estate Event Platform.

Consequence: Loose coupling; requires versioned event contracts and replay governance.


### RO-05 — AI is advisory for maintenance

Original identifier: ADR-RO-05.

Written in / source: [Matt’s Ride_Operations_C4_Capability.docx, shared 12 September 2026](https://architecturek-iz73826.slack.com/archives/C0C0J2MSLTG/p1789215670905659), §7 Architectural decision records. [Repository Markdown copy](https://github.com/PeteH-GGB-UK/OReillyArchitectureKata-2026/blob/main/architecture/Ride_Operations_C4_Capability.md).

Version / status note: Capability draft. No individual status, approval date or decision owner is supplied in this ADR table.

Context: Predictions are non-deterministic and safety consequences are material.

Decision: AI creates evidence-backed recommendations; engineers authorise action.

Consequence: Predictive value without delegating accountability; lower automation.


### RO-06 — Provider-neutral model boundary

Original identifier: ADR-RO-06.

Written in / source: [Matt’s Ride_Operations_C4_Capability.docx, shared 12 September 2026](https://architecturek-iz73826.slack.com/archives/C0C0J2MSLTG/p1789215670905659), §7 Architectural decision records. [Repository Markdown copy](https://github.com/PeteH-GGB-UK/OReillyArchitectureKata-2026/blob/main/architecture/Ride_Operations_C4_Capability.md).

Version / status note: Capability draft. No individual status, approval date or decision owner is supplied in this ADR table.

Context: Models, providers and economics will change.

Decision: Use internal versioned inference contracts and retain evaluation assets independently.

Consequence: Improves replaceability; adds abstraction and compatibility testing.


## Animal Care and Welfare

### AC-01 — Animal Care Platform as system of record

Original identifier: ADR-AC-01.

Written in / source: [Matt’s Animal_Management_C4_Capability.docx, shared 12 September 2026](https://architecturek-iz73826.slack.com/archives/C0C0J2MSLTG/p1789215670905659), §7 Architectural decision records. [Repository Markdown copy](https://github.com/PeteH-GGB-UK/OReillyArchitectureKata-2026/blob/main/architecture/Animal_Management_C4_Capability.md).

Version / status note: Capability draft. No individual status, approval date or decision owner is supplied in this ADR table.

Context: Welfare data originates from devices and people.

Decision: Own health, husbandry, feeding, population and incident records in the Animal Care Platform.

Consequence: Clear ownership and auditability; requires integration from telemetry and estate systems.


### AC-02 — Edge-first resilience

Original identifier: ADR-AC-02.

Written in / source: [Matt’s Animal_Management_C4_Capability.docx, shared 12 September 2026](https://architecturek-iz73826.slack.com/archives/C0C0J2MSLTG/p1789215670905659), §7 Architectural decision records. [Repository Markdown copy](https://github.com/PeteH-GGB-UK/OReillyArchitectureKata-2026/blob/main/architecture/Animal_Management_C4_Capability.md).

Version / status note: Capability draft. No individual status, approval date or decision owner is supplied in this ADR table.

Context: Connectivity is unreliable and welfare monitoring cannot depend on the cloud.

Decision: Use zoned gateways with local thresholds, alarms and encrypted store-and-forward.

Consequence: Continues protection during outages; adds managed estate hardware.


### AC-03 — Event-driven estate integration

Original identifier: ADR-AC-03.

Written in / source: [Matt’s Animal_Management_C4_Capability.docx, shared 12 September 2026](https://architecturek-iz73826.slack.com/archives/C0C0J2MSLTG/p1789215670905659), §7 Architectural decision records. [Repository Markdown copy](https://github.com/PeteH-GGB-UK/OReillyArchitectureKata-2026/blob/main/architecture/Animal_Management_C4_Capability.md).

Version / status note: Capability draft. No individual status, approval date or decision owner is supplied in this ADR table.

Context: Operations, maintenance and workforce services need animal-care impacts.

Decision: Publish curated domain events through the Estate Event Platform.

Consequence: Loose coupling and independent evolution; requires event-contract governance.


### AC-04 — AI is advisory only

Original identifier: ADR-AC-04.

Written in / source: [Matt’s Animal_Management_C4_Capability.docx, shared 12 September 2026](https://architecturek-iz73826.slack.com/archives/C0C0J2MSLTG/p1789215670905659), §7 Architectural decision records. [Repository Markdown copy](https://github.com/PeteH-GGB-UK/OReillyArchitectureKata-2026/blob/main/architecture/Animal_Management_C4_Capability.md).

Version / status note: Capability draft. No individual status, approval date or decision owner is supplied in this ADR table.

Context: Welfare decisions carry ethical, operational and reputational consequences.

Decision: AI can recommend investigation but cannot diagnose, prescribe or authorise action.

Consequence: Preserves accountability; deliberately limits automation.


### AC-05 — Specialised AI by risk profile

Original identifier: ADR-AC-05.

Written in / source: [Matt’s Animal_Management_C4_Capability.docx, shared 12 September 2026](https://architecturek-iz73826.slack.com/archives/C0C0J2MSLTG/p1789215670905659), §7 Architectural decision records. [Repository Markdown copy](https://github.com/PeteH-GGB-UK/OReillyArchitectureKata-2026/blob/main/architecture/Animal_Management_C4_Capability.md).

Version / status note: Capability draft. No individual status, approval date or decision owner is supplied in this ADR table.

Context: Detection and generative assistance have different failure modes.

Decision: Use conventional ML or vision for bounded detection; use GenAI only for cited retrieval and summarisation.

Consequence: Improves evaluability and reduces hallucination exposure; operates multiple model types.


### AC-06 — Provider-neutral inference boundary

Original identifier: ADR-AC-06.

Written in / source: [Matt’s Animal_Management_C4_Capability.docx, shared 12 September 2026](https://architecturek-iz73826.slack.com/archives/C0C0J2MSLTG/p1789215670905659), §7 Architectural decision records. [Repository Markdown copy](https://github.com/PeteH-GGB-UK/OReillyArchitectureKata-2026/blob/main/architecture/Animal_Management_C4_Capability.md).

Version / status note: Capability draft. No individual status, approval date or decision owner is supplied in this ADR table.

Context: AI models, providers and commercial terms will change.

Decision: Use versioned internal model contracts and retain evaluation assets independently.

Consequence: Improves replaceability; introduces an abstraction and compatibility-testing burden.


## Crowd and Site Operations

### CS-01 — Anonymous counting by default

Original identifier: ADR-CS-01.

Written in / source: [Matt’s Crowd_and_Site_Operations_C4_Capability.docx, shared 12 September 2026](https://architecturek-iz73826.slack.com/archives/C0C0J2MSLTG/p1789227268578989), §7 Architectural decision records. [Repository Markdown copy](https://github.com/PeteH-GGB-UK/OReillyArchitectureKata-2026/blob/main/architecture/Crowd_and_Site_Operations_C4_Capability.md).

Version / status note: Capability draft. No individual status, approval date or decision owner is supplied in this ADR table.

Context: Popularity insight does not require personal identity.

Decision: Use counts and throughput; prohibit biometric identity processing.

Consequence: Reduces privacy risk; limits individual-level analysis.


### CS-02 — Queue estimates are derived state

Original identifier: ADR-CS-02.

Written in / source: [Matt’s Crowd_and_Site_Operations_C4_Capability.docx, shared 12 September 2026](https://architecturek-iz73826.slack.com/archives/C0C0J2MSLTG/p1789227268578989), §7 Architectural decision records. [Repository Markdown copy](https://github.com/PeteH-GGB-UK/OReillyArchitectureKata-2026/blob/main/architecture/Crowd_and_Site_Operations_C4_Capability.md).

Version / status note: Capability draft. No individual status, approval date or decision owner is supplied in this ADR table.

Context: Sensors provide observations, not authoritative waiting time.

Decision: Calculate estimates with confidence and freshness metadata.

Consequence: Supports quality-aware guidance; requires calibration.


### CS-03 — Edge-first ingestion

Original identifier: ADR-CS-03.

Written in / source: [Matt’s Crowd_and_Site_Operations_C4_Capability.docx, shared 12 September 2026](https://architecturek-iz73826.slack.com/archives/C0C0J2MSLTG/p1789227268578989), §7 Architectural decision records. [Repository Markdown copy](https://github.com/PeteH-GGB-UK/OReillyArchitectureKata-2026/blob/main/architecture/Crowd_and_Site_Operations_C4_Capability.md).

Version / status note: Capability draft. No individual status, approval date or decision owner is supplied in this ADR table.

Context: Connectivity is patchy.

Decision: Use zoned gateways with buffer, replay and device health.

Consequence: Preserves observations; adds managed hardware.


### CS-04 — Event-driven integration

Original identifier: ADR-CS-04.

Written in / source: [Matt’s Crowd_and_Site_Operations_C4_Capability.docx, shared 12 September 2026](https://architecturek-iz73826.slack.com/archives/C0C0J2MSLTG/p1789227268578989), §7 Architectural decision records. [Repository Markdown copy](https://github.com/PeteH-GGB-UK/OReillyArchitectureKata-2026/blob/main/architecture/Crowd_and_Site_Operations_C4_Capability.md).

Version / status note: Capability draft. No individual status, approval date or decision owner is supplied in this ADR table.

Context: Ride and site status change independently.

Decision: Exchange curated events through the estate backbone.

Consequence: Loose coupling; requires contract governance.


### CS-05 — AI is advisory

Original identifier: ADR-CS-05.

Written in / source: [Matt’s Crowd_and_Site_Operations_C4_Capability.docx, shared 12 September 2026](https://architecturek-iz73826.slack.com/archives/C0C0J2MSLTG/p1789227268578989), §7 Architectural decision records. [Repository Markdown copy](https://github.com/PeteH-GGB-UK/OReillyArchitectureKata-2026/blob/main/architecture/Crowd_and_Site_Operations_C4_Capability.md).

Version / status note: Capability draft. No individual status, approval date or decision owner is supplied in this ADR table.

Context: Forecasts can be wrong during unusual conditions.

Decision: Require duty-manager approval for consequential actions.

Consequence: Maintains accountability; limits automation.


### CS-06 — Separate operational and public views

Original identifier: ADR-CS-06.

Written in / source: [Matt’s Crowd_and_Site_Operations_C4_Capability.docx, shared 12 September 2026](https://architecturek-iz73826.slack.com/archives/C0C0J2MSLTG/p1789227268578989), §7 Architectural decision records. [Repository Markdown copy](https://github.com/PeteH-GGB-UK/OReillyArchitectureKata-2026/blob/main/architecture/Crowd_and_Site_Operations_C4_Capability.md).

Version / status note: Capability draft. No individual status, approval date or decision owner is supplied in this ADR table.

Context: Internal incidents may contain sensitive detail.

Decision: Publish sanitised status and guidance projections.

Consequence: Protects data; requires projection logic.


## Visitor Journey and Growth

### VG-01 — Commerce is deterministic

Original identifier: ADR-VG-01.

Written in / source: [Matt’s Visitor_Journey_and_Growth_C4_Capability.docx, shared 12 September 2026](https://architecturek-iz73826.slack.com/archives/C0C0J2MSLTG/p1789227268578989), §7 Architectural decision records. [Repository Markdown copy](https://github.com/PeteH-GGB-UK/OReillyArchitectureKata-2026/blob/main/architecture/Visitor_Journey_and_Growth_C4_Capability.md).

Version / status note: Capability draft. No individual status, approval date or decision owner is supplied in this ADR table.

Context: Tickets and passes are contractual entitlements.

Decision: Keep order, payment and entitlement decisions outside generative AI.

Consequence: Strong auditability; less conversational automation.


### VG-02 — Consent is first-class

Original identifier: ADR-VG-02.

Written in / source: [Matt’s Visitor_Journey_and_Growth_C4_Capability.docx, shared 12 September 2026](https://architecturek-iz73826.slack.com/archives/C0C0J2MSLTG/p1789227268578989), §7 Architectural decision records. [Repository Markdown copy](https://github.com/PeteH-GGB-UK/OReillyArchitectureKata-2026/blob/main/architecture/Visitor_Journey_and_Growth_C4_Capability.md).

Version / status note: Capability draft. No individual status, approval date or decision owner is supplied in this ADR table.

Context: Growth activity depends on valid permission.

Decision: Centralise consent and enforce it at every outbound decision.

Consequence: Improves trust; adds policy integration.


### VG-03 — Operational truth stays in domains

Original identifier: ADR-VG-03.

Written in / source: [Matt’s Visitor_Journey_and_Growth_C4_Capability.docx, shared 12 September 2026](https://architecturek-iz73826.slack.com/archives/C0C0J2MSLTG/p1789227268578989), §7 Architectural decision records. [Repository Markdown copy](https://github.com/PeteH-GGB-UK/OReillyArchitectureKata-2026/blob/main/architecture/Visitor_Journey_and_Growth_C4_Capability.md).

Version / status note: Capability draft. No individual status, approval date or decision owner is supplied in this ADR table.

Context: Ride and site status changes independently.

Decision: Consume curated status events rather than copy operational ownership.

Consequence: Reduces inconsistency; requires freshness handling.


### VG-04 — Controlled offline entry

Original identifier: ADR-VG-04.

Written in / source: [Matt’s Visitor_Journey_and_Growth_C4_Capability.docx, shared 12 September 2026](https://architecturek-iz73826.slack.com/archives/C0C0J2MSLTG/p1789227268578989), §7 Architectural decision records. [Repository Markdown copy](https://github.com/PeteH-GGB-UK/OReillyArchitectureKata-2026/blob/main/architecture/Visitor_Journey_and_Growth_C4_Capability.md).

Version / status note: Capability draft. No individual status, approval date or decision owner is supplied in this ADR table.

Context: Entry cannot rely solely on live cloud access.

Decision: Validate signed, time-bounded entitlements from a local cache.

Consequence: Maintains entry; requires revocation and reconciliation design.


### VG-05 — AI recommendations are advisory

Original identifier: ADR-VG-05.

Written in / source: [Matt’s Visitor_Journey_and_Growth_C4_Capability.docx, shared 12 September 2026](https://architecturek-iz73826.slack.com/archives/C0C0J2MSLTG/p1789227268578989), §7 Architectural decision records. [Repository Markdown copy](https://github.com/PeteH-GGB-UK/OReillyArchitectureKata-2026/blob/main/architecture/Visitor_Journey_and_Growth_C4_Capability.md).

Version / status note: Capability draft. No individual status, approval date or decision owner is supplied in this ADR table.

Context: Ranking can be wrong or stale.

Decision: Apply consent, availability and safety policies after model output.

Consequence: Bounds risk; may reduce recommendation yield.


### VG-06 — Growth uses experimentation

Original identifier: ADR-VG-06.

Written in / source: [Matt’s Visitor_Journey_and_Growth_C4_Capability.docx, shared 12 September 2026](https://architecturek-iz73826.slack.com/archives/C0C0J2MSLTG/p1789227268578989), §7 Architectural decision records. [Repository Markdown copy](https://github.com/PeteH-GGB-UK/OReillyArchitectureKata-2026/blob/main/architecture/Visitor_Journey_and_Growth_C4_Capability.md).

Version / status note: Capability draft. No individual status, approval date or decision owner is supplied in this ADR table.

Context: Correlation alone cannot prove value.

Decision: Use controlled experiments with guardrail metrics and attribution.

Consequence: Improves evidence; adds analytical discipline.


## Chris’s Unnumbered AI Enhancement Proposals

Written in: Chris’s AI Innovation Assessment and Enhancements, shared 15 September 2026. [Slack announcement](https://architecturek-iz73826.slack.com/archives/C0C0J2MSLTG/p1789487903914399); [repository document](https://github.com/PeteH-GGB-UK/OReillyArchitectureKata-2026/blob/main/requirements/AI_Innovation_Assessment_and_Enhancements.md).

Source status: recommendations, not recorded decisions. The document does not select all of these for implementation. The following eight sections preserve the proposal text, including examples, controls and qualifications; illustrative figures are not measured results.


### C-01 — Estate digital twin and simulation

Source location: “Recommended AI enhancements”, item 1.

Create a living digital twin of:

- Rides and their operational state.
- Enclosures and animal populations.
- Visitor flows and queues.
- Weather and environmental conditions.
- Staff, maintenance and veterinary capacity.
- Ticket demand and attraction availability.

AI could use the twin to simulate questions such as:

- What happens to queue times if one major ride closes?
- What staffing pattern best handles a forecast 12,000-visitor day?
- Which ticket incentive increases attendance without overwhelming the site?
- What is the likely effect of moving an animal group or changing feeding times?
- Which maintenance work should be brought forward before a peak weekend?

This moves beyond forecasting into counterfactual decision support. The AI recommends scenarios; duty managers, engineers and animal-care specialists approve actions.

This directly supports the brief's suggested combination of IoT, digital twins and predictive analytics.


### C-02 — Bounded multi-agent operations assistant

Source location: “Recommended AI enhancements”, item 2.

Introduce specialised AI agents behind a controlled orchestration layer:

- **Visitor Experience Agent:** builds itineraries, explains queues and recommends alternatives.
- **Crowd Operations Agent:** identifies emerging pressure and proposes staffing or routing responses.
- **Ride Reliability Agent:** correlates telemetry, inspections and maintenance history.
- **Animal Welfare Agent:** summarises welfare signals and prioritises keeper or veterinary review.
- **Revenue Agent:** proposes campaigns, pricing experiments and repeat-visit interventions.

Agents should use typed tools and domain APIs with:

- Explicit permissions.
- Read-only versus write action separation.
- Policy checks.
- Human approval gates.
- Full audit trails.
- Maximum action scopes.
- Deterministic fallback behaviour.

For example, the Ride Reliability Agent may create a maintenance investigation task, but cannot close a ride or approve its return to service. The Animal Welfare Agent may assemble evidence for veterinary review, but cannot diagnose or prescribe treatment.

This uses the brief's agentic AI direction without compromising safety.


### C-03 — Multimodal animal welfare monitoring

Source location: “Recommended AI enhancements”, item 3.

Extend animal monitoring by combining:

- Camera-based activity and posture analysis.
- Feeding and drinking behaviour.
- Vocalisation or sound analysis where appropriate.
- Environmental telemetry.
- Historical veterinary records.
- Keeper observations.
- Population and movement data.

For example, a change in a jumping piranha group's movement pattern could be correlated with water temperature, oxygen, feeding behaviour and recent maintenance events. The system could produce an evidence bundle such as:

> Activity is 32% below the learned baseline, coinciding with a temperature deviation and reduced feeding. Confidence is moderate. Manual observation and water-quality inspection recommended.

Controls should include:

- AI produces an observation or welfare-risk indication, not a diagnosis.
- Video processing prefers enclosure-local analysis and short-lived derived features.
- Human-verified observations feed back into evaluation datasets.
- Population counts require confidence thresholds and manual confirmation before changing the authoritative record.

This gives the jumping piranha requirement a concrete, memorable AI use case.


### C-04 — AI-driven care and resource optimisation

Source location: “Recommended AI enhancements”, item 4.

Use constrained optimisation to propose improvements to:

- Feed quantities and preparation.
- Feeding schedules.
- Enclosure environmental conditions.
- Veterinary workload.
- Keeper rounds.
- Medication and consumables inventory.
- Supplier ordering.
- Energy consumption for aquatic and climate-controlled enclosures.

The optimiser must respect species and individual welfare requirements, veterinary-approved limits, minimum staffing levels, regulatory constraints, care schedules and enclosure capacity.

The output is a proposed plan with assumptions, expected savings and welfare constraints. A qualified person approves the plan. This connects AI directly to the brief's high animal-care cost problem.


### C-05 — Visitor co-pilot with real-time accessible planning

Source location: “Recommended AI enhancements”, item 5.

A consent-aware visitor co-pilot could:

- Build an itinerary based on family interests, mobility needs, available time and current queues.
- Re-plan when rides close or crowd conditions change.
- Offer accessible routes and quieter alternatives.
- Explain animal exhibits in age-appropriate language.
- Provide translation and voice interaction.
- Coordinate booking, food, retail and attraction availability.
- Adapt recommendations based on visit behaviour, subject to consent.

The co-pilot must consume authoritative, real-time operational data rather than invent park conditions. Responses should be grounded in current ride and site status, approved attraction content, accessibility metadata, ticket rules and visitor consent.

This makes the visitor-facing AI requirement visible and useful rather than limiting it to generic recommendations.


### C-06 — Causal revenue and investment intelligence

Source location: “Recommended AI enhancements”, item 6.

Use controlled experiments, causal analysis and scenario modelling to answer questions such as:

- Did a new ride actually increase repeat visits?
- Did queue reductions increase satisfaction or spending?
- Which attraction improvements are likely to produce the greatest return?
- Which visitor groups are most likely to return?
- Did a campaign attract new visitors or merely discount existing demand?
- Which site areas underperform because of poor visibility, access or queue friction?

This supports staffing and investment decisions more effectively than descriptive popularity reporting alone.


### C-07 — Edge AI for degraded connectivity

Source location: “Recommended AI enhancements”, item 7.

Specify which models run locally at the edge:

- Queue and occupancy estimation.
- Ride telemetry anomaly screening.
- Enclosure environmental anomaly detection.
- Basic animal activity or population estimation.
- Device fault classification.

The cloud handles model training, fleet-wide analysis, cross-domain correlation, scenario simulation and model evaluation. The lifecycle becomes:

1. Sensors produce local observations.
2. Edge models generate immediate, quality-rated signals.
3. Gateways buffer and synchronise evidence.
4. Cloud models perform richer analysis.
5. Human outcomes feed back into evaluation.
6. Approved model versions are redeployed to the edge.

The architecture should also specify model compatibility, rollback and handling of devices that are temporarily offline.


### C-08 — Synthetic data and privacy-preserving learning

Source location: “Recommended AI enhancements”, item 8.

Use synthetic or simulated data for:

- Visitor-flow testing.
- Ride telemetry and failure scenarios.
- Enclosure conditions.
- Rare animal-health incidents.
- Crowd surges.
- Extended backhaul outages.

Synthetic data is useful for testing, resilience exercises and pre-deployment evaluation, but must not be treated as proof of production performance. Real-world validation remains necessary before operational use.

### Chris’s Prioritisation and Scope Qualification

The submission should not add every possible AI feature. The strongest enhancement is one coherent story built around:

1. An estate digital twin for simulation and cross-domain reasoning.
2. Bounded domain agents that use the twin and approved domain tools.
3. Multimodal animal welfare monitoring, including the jumping piranha collection.
4. A grounded visitor co-pilot for adaptive, accessible visit planning.
5. A constrained optimisation service for staffing, care costs and maintenance planning.

This gives the submission a clear innovation narrative:

> The estate is not just collecting data or calling isolated AI models. It is building a governed intelligence layer that observes the physical estate, simulates possible decisions, coordinates specialist recommendations and keeps accountable people in control.

The existing safety, resilience and governance controls should remain unchanged. New AI capabilities should be added as bounded decision-support services with explicit tool permissions, evidence bundles, evaluation datasets, model and version lineage, human approval and deterministic fallbacks.

## Helen’s Review Requests for Decisions and Supporting Evidence

Written in: kata-review-and-suggestions.md, 14 September 2026, §4 Priority fixes. [Source message](https://architecturek-iz73826.slack.com/archives/C0C0J2MSLTG/p1789402000758639). These are review requests, not accepted ADRs. Some assertions in this earlier review were overtaken by later documents; preserve the request without treating its diagnosis as current fact.


### R-01 — Design the piranha count

Source location: §4, P1. Original review text follows.

Section 8's traceability table claims coverage of *"Animal health, feeding and **population**"*, but population counting appears nowhere in sections 2–5. The only trace is the phrase *"and selected vision"* in the AI value map. **This is an overclaim, not just a gap.**

It is also the single best opportunity in the kata, because **you cannot ground-truth a fish count**:

- What is the labelled test set when nobody knows the true number?
- Calibrate against a periodic manual count? Count at feed time when they surface? Mark-recapture?
- Report a **range with confidence**, not an integer
- What size of change in that range is *actionable* versus noise?

That reasoning is exactly criterion 6, and it is memorable in a way "multivariate anomaly detection" is not. **Worth its own dynamic diagram and its own ADR.**


### R-02 — Size the edge design

Source location: §4, P2. Original review text follows.

Section 3 asserts "zoned, mains-powered gateways" but never says how many zones, how many devices each, at what publish interval. FF-05 promises *"<0.1% loss during a simulated 24-hour backhaul outage"* — unprovable without knowing message rates and buffer capacity.

One page of arithmetic from the brief's own numbers (40 rides, 55 enclosures, 200+ animals, 5k→15k visitors) turns the strongest idea in the submission from an assertion into an engineering decision. Include: devices per zone, messages/second at peak, bytes per message, gateway buffer size for a 24-hour outage, backhaul bandwidth, annual storage growth, and peak checkout TPS at 15,000 visitors/day.


### R-03 — Answer all three uncertainty questions

Source location: §4, P3. Original review text follows.

The brief (slide 27) asks three things. We answer one.

| Question | Current state |
|---|---|
| Best model/provider changes | **Answered** — ADR-06 provider-neutral inference contracts, FF-10 replacement rehearsal |
| Provider changes prices on you | **Not answered** — no per-inference cost telemetry, no budget circuit-breaker |
| Provider suddenly shuts down | **Not answered** — no named alternative provider or self-host fallback |

Add a *trigger → designed response → rehearsal that proves it* table. Half a page, closes a named criterion most teams fumble.


### R-04 — Introduce a consequence-calibrated autonomy gradient

Source location: §4, P4. Original review text follows.

Every guardrail in all five documents is prohibitive. That is correct for welfare, safety, commerce and consent — **keep all of those**. But criterion 1 is *innovative use of AI*, and there is currently nowhere in the architecture that AI acts alone.

Name one or two genuinely low-consequence, reversible, monitored decisions where it does — digital signage copy, in-app alternative-attraction suggestions, cleaning or staff task ordering — each with an explicit "reversible within N minutes, monitored by X, auto-suspends on Y".

The position becomes **"autonomy calibrated to consequence"** rather than "we never automate". Stronger, more interesting, and the cheapest available lift on our weakest criterion. (Kata-na came 3rd with the prohibition; the gradient is the differentiator.)


### Additional Specific Decision Requests in Helen’s Review

Source location: §5 Specific edits to the integrated document. The following are extracted summaries, not new decisions:

| Subject | Request | Relationship |
|---|---|---|
| Offline Admission | Commit to an outage window, accepted fraud exposure and reconciliation behaviour. | H-04 / M-04 and VG-04. |
| Event Contracts | Select a schema-registry approach and CI enforcement for compatibility. | H-02 / M-02. |
| Provider Change | Specify price-change and shutdown triggers, responses, alternatives and rehearsals. | H-06 / M-06. |
| Edge Capacity | Quantify zones, device counts, rates, buffers, backhaul and storage. | H-03 / M-03; R-02. |
| Model Promotion | Replace deferred quality thresholds with measurable acceptance criteria. | H-05 / M-05; domain AI decisions. |

Review observation: sizing arithmetic and acceptance thresholds may be evidence attached to a decision rather than separate ADRs. Helen’s suggested five-to-ten ADR count is team guidance, not an official numeric requirement.

## Additional Decision-Related Source Material

### S-01 — Helen’s Revision and Renumbering Note

Written in: Helen’s Slack change summary, 15 September 2026. [Source](https://architecturek-iz73826.slack.com/archives/C0C0J2MSLTG/p1789481800949749). Status: author’s description of changes, not evidence of team approval. Preserved below to show the rationale for added, removed and merged ADRs.

> Ive come up with this, added the bit in about the piranhas. i also got claude to trim things down.
> 
> *Changes to the integrated architecture doc*
> *Added — animal identity, population and visibility (new subsection in §5)*
> • Designed the piranha population capability, which §8 previously claimed under "population" but nothing in the document actually covered
> • PIT / ISO 11784/11785 tag telemetry as the identity backbone — with the point that exotic collections are usually microchipped already, so this is mostly readers rather than tagging
> • Population published as a *range with confidence, never an integer*, from three sources: continuous tag detections, a daily vision count at feed, and a quarterly manual count
> • The validation story for AI you can't ground-truth: the manual count retrospectively labels every estimate, calibrated coverage is the metric instead of accuracy, and the two sensor sources cross-check each other between counts
> • A deterministic absence rule at the gateway — individual tag unseen beyond its window raises a keeper task with no cloud and no model
> • Extended the same tags to *visitor-facing visibility*: readers at den entrances resolve direction of travel, so the app and signage can show which animals are actually out
> • Visibility state table including `UNKNOWN` as a first-class state, so a broken reader never reads as "animal not out"
> • Guardrails: welfare owns the signal and can suppress publication; visitor channels get a sanitised projection and can't write back; publication is damped so it doesn't create the crowding it's meant to relieve
> • *Regulatory context* — licensing and accreditation, ZIMS as the authoritative animal record, and why a regulated return can't be a model output
> *Added — supporting changes*
> • *Figure 7* (population: three sources, one range) and *Figure 8* (visibility: welfare owns the signal), drawn to match the existing diagram style
> • *ADR-10* — animal records are human-authored and reconciled to the accredited record
> • *ADR-11* — welfare owns visibility; prediction is bounded-autonomous
> • New rows in: the AI value map (§4), threat scenarios (§6), traceability (§8), fitness functions FF-11/12/13 (§8), risks and data lifecycle (§10), and the glossary (PIT, ZIMS, EAZA/BIAZA)
> • Two constraints bullets in §1 covering licensing and the external animal record
> *Trimmed*
> • *ADRs 14 → 11.* Removed "Selective build versus buy" (stated a principle, not a decision) and "Zero-trust device and retrieval boundary" (already fully covered in §6 — the clause was folded in there). Merged two animal-record ADRs into one.
> • *All ADR references in the traceability matrix renumbered* to match
> • Deleted the *cost and benefit hypothesis table* in §9 — it listed categories of cost and benefit but no actual figures
> • *Value gates*: four bullets → one sentence, all four gates kept
> • *Accessibility*: four bullets → one sentence
> • §6 security controls table tightened
> • My own §5 prose cut back by about 160 words and both figures reduced in size
> *Net effect:* 3,144 → 4,259 words (about 6.3 → 8.5 pages), still *11 ADRs*, and the population requirement is now actually designed rather than just claimed.
> Files: Architecture Kata 2026.pages (ID: F0C1TLAU5EX, application/x-iwork-pages-sffpages, 2.3 MB)

### S-02 — Population Estimation, Identity and Animal Visibility Design

Written in: Helen’s revised integrated architecture, §5 Animal identity, population and visibility, including its Regulatory context subsection. [Word source](https://architecturek-iz73826.slack.com/archives/C0C0J2MSLTG/p1789484308135269). Related records: H-10 and H-11. This source text contains additional choices that may need their own record or supporting design rather than being hidden inside the broad ADRs.

Original text (table rows flattened with separators):

> Population and visibility are two business questions answered by one sensing investment. Exotic collections are routinely microchipped to ISO 11784/11785 for identification and licensing — the same standard as the PIT tags used in aquatic displays. Where those chips already exist the estate installs readers rather than tags, and the welfare cost approaches zero. Confirm during discovery.
> 
> The jumping piranha collection cannot be ground-truthed: no label exists, so a model reporting an exact count can be neither confirmed nor falsified. Three independent estimators are therefore combined — continuous PIT detections at a feed antenna, which identify marked fish; a daily vision count over the feed window, which sees all fish but is biased low by occlusion; and a quarterly manual count, the only exact observation. A mark-recapture estimator publishes a range with confidence, never an integer.
> 
> This is the estate's worked example of validating AI where no labels exist. Each manual count retrospectively scores every estimate published since the previous one, and the headline metric is calibrated coverage — whether a 95% interval contains the truth 95% of the time — rather than accuracy. Between counts the sources police each other: if vision sees fewer marked fish than the antennas read in the same window, vision is under-counting today. The deterministic baseline needs no AI — an individual tag unseen beyond its window raises a keeper task from a rule at the gateway.
> 
> Figure 7. Three independent sources produce one range with confidence. The manual count labels every estimate since the previous count; the deterministic absence rule runs at the gateway without cloud or model.
> 
> Sited at a den entrance rather than a feed station, two readers in sequence resolve direction of travel and yield an occupancy state machine. Published to visitors, this removes the most common disappointment in an animal collection, spreads crowds away from congestion, and separates “unpopular” from “empty when people arrived” — a distinction that changes where the estate invests. A tag reports presence, not consciousness: resting is inferred from keeper status, schedules and species activity pattern, and only the forecast of the next visible window requires a model.
> 
> State | Determined by | Treatment
> 
> ON_SHOW | Direction-resolved passage outward | High confidence
> 
> OFF_SHOW | Direction-resolved passage inward | High confidence
> 
> LIKELY_RESTING | Species activity pattern, time of day, no recent passage | Medium; labelled as inferred
> 
> KEEPER_SET | Keeper override, any value | Authoritative; always wins
> 
> UNKNOWN | Reader fault or stale data | Published as unknown, never inferred as off show
> 
> Two guardrails follow:
> 
> Reader silence publishes UNKNOWN and never OFF_SHOW; a failed reader and an animal in its den are indistinguishable to the sensor and entirely different to a visitor at the glass. Species carrying theft or release risk publish coarse location or none.
> 
> Animal Care owns visibility and may suppress publication unilaterally; visitor channels consume a sanitised projection and cannot write back. Publication is damped by hysteresis, staggered notification and suppression for an enclosure already at its occupancy threshold, so the feature does not create the congestion it exists to relieve.
> 
> Visibility prediction is the estate's clearest candidate for bounded autonomous action: the worst outcome is the status quo, it is reversible within minutes, it scores itself continuously against observed reader state with no human labelling, and post-model policy filters prevent it contradicting an observation, closure or keeper override. It therefore publishes without per-instance approval while auto-suspending on an accuracy breach — autonomy calibrated to consequence rather than blanket prohibition.
> 
> Figure 8. Animal Care owns visibility state and may suppress publication; visitor channels consume a sanitised projection and cannot write back. Policy filters apply after the model.
> 
> Regulatory context
> 
> Animal records are a regulated artefact. Zoo licensing requires an accurate stocktake and supports periodic inspection, and association accreditation adds record-keeping and breeding-programme obligations. Two consequences follow. The authoritative animal record is the accredited sector system; the Animal Care Platform is a system of engagement over it, reconciling rather than competing. And a regulatory return cannot be a model output — the figure submitted to a regulator or studbook is a human-authored count with named authorisation and an audit trail, which is the independent reason ADR-10 keeps AI out of the recorded number.

Review observations: the brief does not establish pre-existing tags, ZIMS or accreditation. A later count is not automatically a ground-truth label for every historical estimate when population can change. Readability of the source does not validate those assumptions or the estimation method.


### S-03 — Pete’s Visitor Media, CRM and Offline-Experience Discussion

Written in: Architecture Kata Catch Up transcript, recording dated 14 September 2026, and Pete’s follow-up messages on 15 September. [Transcript upload](https://architecturek-iz73826.slack.com/archives/C0C0J2MSLTG/p1789422502222579); [CRM request](https://architecturek-iz73826.slack.com/archives/C0C0J2MSLTG/p1789488220033629); [visitor-options request](https://architecturek-iz73826.slack.com/archives/C0C0J2MSLTG/p1789488247083139).

Extracted discussion summary, not a verbatim transcript:

- 00:03–02:36 and 28:37–30:04: buy-versus-build CRM ADR requested; Salesforce used as an example. U-01 now confirms buy rather than build; vendor selection is not confirmed.
- 00:03–02:36: RFID for annual-pass holders and paper wristbands with barcode/QR for day visitors, linked to an app. Media and tracking choices were proposals, not a recorded product decision.
- 06:50–09:35: animal-visibility guidance, interior cameras/screens and promotion of quieter zones. Helen’s later H-11/S-02 develops the visibility boundary.
- 13:41–17:34: preloaded curated content, QR access, local refresh points and “last updated” information for offline use. SMS queue notifications and virtual queuing were raised but not settled.
- 17:40–21:48: events and longer visits to support return business and spending; included versus separately priced events remained open.

Review note: these items may be product or domain choices rather than ADRs. Assess identity coupling, privacy, offline reconciliation, procurement and exit costs before classifying them. The uploaded transcript is discussion evidence, not a ratified decision log.


### S-04 — Alex’s AI Evaluation and Safeguard Drafts

Written in: Alex’s Slack posts on 16 September 2026. [High-level evaluation draft](https://architecturek-iz73826.slack.com/archives/C0C0J2MSLTG/p1789554472894809); [expanded testing notes](https://architecturek-iz73826.slack.com/archives/C0C0J2MSLTG/p1789554566028519). Status: snippets offered for adaptation, not ADRs or verified test results. Placeholder technologies, sample thresholds and past-tense testing claims are retained as source text, not endorsed as completed work.

> Some high level snippets on AI testing and evaluation to tweak and include somewhere:
> 
> *AI Integration & Evaluation*
> 1. Scope of AI Usage
> • Components: [e.g., Intelligent Search Indexing, Predictive Resource Scaling]
> • Exclusions: [e.g., Core transactional logic, Authentication flows remain deterministic]
> • Model Dependency: [e.g., External LLM API (Provider X) / On-premise fine-tuned model]
> 2. Testing Strategy
> • Functional Validation: [e.g., Prompt injection resistance tests, Output relevance scoring against golden dataset]
> • Performance SLAs: [e.g., P95 latency < 800ms, Throughput > 100 req/sec]
> • Safety & Compliance: [e.g., Bias detection scans, PII redaction verification]
> 3. Success Metrics
> *Metric*
> *Target Threshold*
> *Measurement Method*
> Accuracy/Relevance
> > 92%
> Automated eval suite on test set
> Latency (P95)
> < 800ms
> Load testing simulation
> Cost Efficiency
> <$0.02 per query
> Monthly spend analysis
> 4. Risk Mitigation
> • Hallucination/Failure: Fallback mechanism to [Rule-based logic / Human-in-the-loop] if confidence score < [X]%.
> • Vendor Lock-in: Abstracted interface layer allowing model swapping without code refactoring.
> • Data Privacy: All inputs sanitized via [Tool/Service] before reaching external models.

> And a bit more expanded information if we want to explain the evaluations more:
> 
> • Bias & Fairness Auditing
>     ◦ Demographic Parity: Evaluated model outputs across diverse user personas (e.g., varying names, locations, cultural contexts) to ensure no systematic disadvantage in response quality or tone.
>     ◦ Training Data Review: Conducted sampling of fine-tuning datasets to identify and mitigate historical biases or stereotypes before deployment.
>     ◦ Metric: Disparity index < 5% across protected groups in output sentiment and relevance scores.
> • Appropriateness & Safety Guardrails
>     ◦ Content Filtering: Implemented a pre-processing layer to detect and block prompts requesting hate speech, harassment, sexually explicit content, or dangerous activities.
>     ◦ Output Moderation: Post-generation checks to ensure responses adhere to community guidelines and do not inadvertently generate harmful advice (e.g., medical/legal misinformation).
>     ◦ Adversarial Testing: Ran "jailbreak" simulations (prompt injection attempts) to verify the model refuses malicious instructions.
> • Contextual Relevance & Tone
>     ◦ Domain Alignment: Validated that outputs remain within the specific architectural domain (e.g., refusing to give cooking advice if the system is for financial planning).
>     ◦ Tone Consistency: Ensured the model maintains a professional, neutral, and helpful persona consistent with brand guidelines.
> • Human-in-the-Loop (HITL) Verification
>     ◦ Sampling Protocol: Randomly selected 5% of high-stakes interactions for human review during the beta phase to catch edge cases automated tests miss.
>     ◦ Feedback Loop: Integrated a "thumbs up/down" mechanism to continuously retrain or adjust prompt engineering based on real-world user corrections.

### S-05 — Early Edge and Transport Design Choices

Written in: Edward’s Prompts_Output.docx working discussion, shared 9 September 2026. [Source upload](https://architecturek-iz73826.slack.com/archives/C0C0J2MSLTG/p1788953410906379); [repository transcription](https://github.com/PeteH-GGB-UK/OReillyArchitectureKata-2026/blob/main/requirements/Prompts_Output.md).

Extracted proposal summary:

- MQTT transports telemetry/events and must not be the system of record.
- Use zoned mains-powered gateways with durable store-and-forward.
- Add small device-side buffers only for observations that cannot safely be lost between device and gateway.
- Prefer wired fibre/Ethernet backhaul where practical; consider redundant line-of-sight point-to-point wireless for remote areas.
- Raise critical threshold alarms locally without waiting for the central platform or internet.

These are early design proposals. Later integrated and capability ADRs capture much of the intent; exact media, topology, zone count, power and capacity choices remain to be checked rather than inferred as selected products.


### S-06 — Chris’s ADR Template and Packaging Request

Written in: Chris’s repository-organisation message on 15 September 2026 and adrs/adr-00-Template.md. [Slack message](https://architecturek-iz73826.slack.com/archives/C0C0J2MSLTG/p1789487218888109); [template](https://github.com/PeteH-GGB-UK/OReillyArchitectureKata-2026/blob/main/adrs/adr-00-Template.md).

Chris asks whether ADRs should be separated into individual Markdown files. The template supplies Context, Decision, Key Differentiators, Alternatives Considered, Risks & Trade-offs (Risk Area / Description / Mitigation), and Conclusion. It is a documentation structure, not a completed architectural decision. At review time the repository’s adrs directory contained the template; labelled decisions remained embedded in the architecture documents.


## Cross-Source Questions for the Classification Review

| Topic | Sources to Compare | Question |
|---|---|---|
| Domain Ownership | H-01; M-01; RO-01; AC-01; VG-03; H-10 | Which records belong to each estate capability, and which regulated animal fields belong to an external system? |
| Events and Commands | H-02; H-09; M-02; M-09; RO-04; AC-03; CS-04 | Which decisions are shared estate commitments, and which domain consequences warrant separate records? |
| Edge Resilience | H-03; M-03; RO-03; AC-02; CS-03; S-05; C-07 | What is decided about gateways and local processing, versus still-open deployment and sizing choices? |
| Local Control and Admission | H-04; M-04; RO-02; VG-01; VG-04 | Should safety independence and offline commercial admission be separate decisions with separate trade-offs? |
| AI Authority | H-05; H-11; RO-05; AC-04; CS-05; VG-05; C-02 | Which actions may be automated, recommended or prohibited, and where are approval gates enforced? |
| Models and Providers | H-06; RO-06; AC-05; AC-06; C-07; R-03 | What is costly to change: provider contracts, model location, data/evaluation assets or the choice of algorithm? |
| Privacy and Public Views | H-07; H-11; CS-01; CS-06; VG-02 | Which shared privacy boundaries need ADRs, versus operational policy or domain design? |
| Analytics and Experiments | H-08; VG-06; C-01; C-06 | Which analytical ownership and causal-evaluation decisions materially constrain future architecture? |
| CRM Procurement | U-01; M-10; S-03 | Record the confirmed buy decision; determine whether vendor/integration/exit choices require a further ADR. |
| Animal Estimation | H-10; S-02; C-03; R-01 | Separate record authority from estimator/sensing choices; confirm feasibility and validation before accepting them. |

## Coverage and Source Limits

The inventory covers the available channel history from 9–16 September 2026, its labelled ADR documents, the catch-up discussion, Helen’s review, Chris’s innovation assessment and template, Alex’s evaluation notes, and Edward’s CRM confirmation. No newer channel messages were returned when rechecked after the 16 September 12:34 BST post. The previous thread search returned no results; this is not a guarantee that inaccessible or unindexed material does not exist.

Helen’s Word export was readable, so her Pages file did not require a new export. Pages-specific comments, revision history or differences not represented in the Word export have not been verified. This inventory captures decision text and associated source information; diagrams remain in the linked source documents. General briefing/rubric guidance and unrelated messages are not promoted into decision candidates.

No source document has been modified, no Slack message sent, and no candidate has been accepted merely because it appears here.
