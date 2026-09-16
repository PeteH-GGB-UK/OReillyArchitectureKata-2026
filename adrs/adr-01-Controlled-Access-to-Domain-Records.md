# ADR-01 — Control Operational Updates Through the Owning Domain

Status: Draft for Team Review — reflects the current design; detailed review points remain open.

## Context

Ride, animal-care, visitor and site records are used by several estate capabilities. Direct cross-domain updates would couple workflows to another domain’s storage and could bypass approval and audit rules. Purchased platforms must participate without creating competing authorities.

Requirement Alignment: FR-05, FR-09, FR-14; NFR-14, NFR-21, NFR-22; record-ownership constraints.

## Decision

Operational amendments pass through the owning domain’s controlled interface. Other domains consume published information or use authorised queries; they do not directly write to its operational tables. Ride Operations owns ride and maintenance records; Animal Care owns care workflows and operational observations; Site Operations owns daily coordination. Estate Management consumes evidence for strategic oversight. This decision does not require one database or deployment per domain.

## Key Differentiators

- Accountability: The record owner enforces validation, approval and audit consistently.
- Product fit: Purchased platforms can remain authoritative behind controlled integration interfaces.
- Cost of change: Moving authority later requires record migration, interface changes and changes to staff responsibilities.

## Alternatives Considered

The alternatives below are a synthesis for team review, not a claim that a formal historical evaluation has been completed.

| Alternative | Assessment |
|---|---|
| Modular estate application with shared storage | Credible where modules enforce ownership internally; can reduce operational complexity. Does not inherently conflict with the chosen authority rule. |
| Separate domain applications with controlled interfaces | Matches the capability designs, but introduces distributed integration and reconciliation costs. Physical deployment remains to be agreed. |
| Direct cross-domain table updates | Simplifies some initial integrations, but permits consumers to bypass domain rules and creates schema coupling; not selected. |

## Risks & Trade-offs

| Risk Area | Description | Mitigation |
|---|---|---|
| Data Ownership | Customer, consent and external animal-record authority are not fully allocated. | Agree a field-level authority map before implementing integrations. |
| Integration | Controlled interfaces require availability and version management. | Define contracts, failure behaviour and visible reconciliation exceptions. |

## Conclusion

Retain this as a draft decision record for team review. The direction is supported by the current documents; unresolved choices below are not implied approvals.

### Review Required

- Agree the authority map across CRM, ticketing and Visitor Journey.
- Confirm whether an external animal record is actually used; do not assume ZIMS adoption.
- Choose deployment and storage boundaries separately from logical ownership.

### Verification

Test that unauthorised cross-domain writes are denied and valid amendments retain audit evidence. Exercise conflicting offline updates and a compatible internal domain change. These are planned checks, not reported test results.

### Revisit Triggers

Revisit when a purchased platform replaces an owner, an external record becomes authoritative, or cross-domain transactional needs cannot be met affordably.

## Sources and Related Documents

- Source entries H-01/M-01, RO-01, AC-01 and VG-03 in [Potential ADRs](potentialadrs.md). The inventory preserves the originating document locations and Slack links; its IDs are provenance references, not these new ADR numbers.
- [Requirements 01–06](README.md#requirements)
- [Candidate Review](ADR_Candidates_For_Review.md)
- [Estate Context](../architecture/Estate_C4_Context.md)
- [Visitor Capability](../architecture/Visitor_Journey_and_Growth_C4_Capability.md)
- [Animal Capability](../architecture/Animal_Management_C4_Capability.md)
- [Ride Capability](../architecture/Ride_Operations_C4_Capability.md)
- [Site Operations Capability](../architecture/Crowd_and_Site_Operations_C4_Capability.md)
