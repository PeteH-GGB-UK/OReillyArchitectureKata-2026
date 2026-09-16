# ADR-02 — Use an Estate Event Platform for Cross-Domain Facts

Status: Draft for Team Review — reflects the current design; detailed review points remain open.

## Context

Ride status, animal-care impacts, admission and site observations serve multiple consumers. Patchy connectivity and reporting require delayed delivery and replay without making every consumer continuously available.

Requirement Alignment: NFR-04, NFR-13, NFR-14, NFR-22; FR-13–16; capability event-integration decisions.

## Decision

Distribute observations and completed business facts through a durable Estate Event Platform with versioned contracts. Use authenticated domain APIs for immediate commands and queries where a direct response is needed. Asynchronous commands remain possible when explicitly designed with ownership and completion semantics; not every interaction must become an event. Consumers must tolerate duplicate and out-of-order delivery.

## Key Differentiators

- Independent processing: Producers need not synchronously coordinate every downstream consumer.
- Replay: Durable facts support recovery and rebuilding derived views.
- Cost of change: Once consumers depend on event contracts and delivery semantics, replacing this integration model requires coordinated migration.

## Alternatives Considered

The alternatives below are a synthesis for team review, not a claim that a formal historical evaluation has been completed.

| Alternative | Assessment |
|---|---|
| Synchronous APIs only | Straightforward request/response behaviour, but couples availability and complicates fan-out to many consumers. |
| Polling or scheduled batch exchange | May be sufficient for slow reporting and purchased-product limitations, but increases latency or repeated queries. |
| Durable publish/subscribe with selective APIs | Selected direction; supports fan-out and replay at the cost of eventual consistency and additional operations. |

## Risks & Trade-offs

| Risk Area | Description | Mitigation |
|---|---|---|
| Event Consistency | Replay can create duplicate tasks or stale operational status. | Use stable identifiers, domain ordering, freshness checks and idempotent consumers. |
| Operational Cost | Broker, adapters and exceptions add support burden. | Size the workload and prefer proportionate managed infrastructure where suitable. |

## Conclusion

Retain this as a draft decision record for team review. The direction is supported by the current documents; unresolved choices below are not implied approvals.

### Review Required

- Select broker, hosting and schema-compatibility approach after workload and support assessment.
- Define acknowledgement, outbox or equivalent publication guarantees, retention and quarantine policies.
- Agree each contract owner and test backlog recovery alongside live traffic.

### Verification

Contract-test supported consumers, inject duplicate and out-of-order facts, and demonstrate no duplicate business effects or loss of acknowledged records within the NFR-04 failure model. Test the NFR-14 backlog recovery target. These are planned checks, not reported test results.

### Revisit Triggers

Revisit if workload, product limitations, operational burden or consistency needs materially change.

## Sources and Related Documents

- Source entries H-02/M-02, H-09/M-09, RO-04, AC-03 and CS-04 in [Potential ADRs](potentialadrs.md). The inventory preserves the originating document locations and Slack links; its IDs are provenance references, not these new ADR numbers.
- [Requirements 01–06](README.md#requirements)
- [Candidate Review](ADR_Candidates_For_Review.md)
- [Estate Context](../architecture/Estate_C4_Context.md)
- [Visitor Capability](../architecture/Visitor_Journey_and_Growth_C4_Capability.md)
- [Animal Capability](../architecture/Animal_Management_C4_Capability.md)
- [Ride Capability](../architecture/Ride_Operations_C4_Capability.md)
- [Site Operations Capability](../architecture/Crowd_and_Site_Operations_C4_Capability.md)
