# ADR-09 — Use Authoritative Consent With Enforcement at Dispatch

Status: Draft for Team Review — reflects the current design; detailed review points remain open.

## Context

Customer records, ticketing and campaigns may span purchased products and estate applications. Cached permission or queued campaigns can outlive a withdrawal.

Requirement Alignment: FR-04; NFR-10; Visitor capability consent controls.

## Decision

Maintain an explicit authoritative communication-permission model and enforce current eligibility at dispatch, including queued campaigns. Event delivery alone must not authorise sending. The product that owns consent and the mechanism that supplies dispatch decisions remain open; this record does not select a dedicated consent service.

## Key Differentiators

- Timely withdrawal: Permissions must affect dispatch within the required five minutes.
- Consistent authority: Prevents conflicting CRM and visitor-platform permission records.
- Cost of change: Moving authority later requires coordinated data, channel and workflow migration.

## Alternatives Considered

The alternatives below are a synthesis for team review, not a claim that a formal historical evaluation has been completed.

| Alternative | Assessment |
|---|---|
| CRM-owned consent | May reuse purchased functionality if all channels can enforce it reliably. |
| Dedicated consent authority | Can provide a shared cross-channel contract but adds a service and operational dependency. |
| Another existing platform owns consent | Viable if it provides the required authority, withdrawal and dispatch integration. |
| Independent channel-owned permissions without reconciliation | Risks contradictory records and stale sending decisions; not selected. |

## Risks & Trade-offs

| Risk Area | Description | Mitigation |
|---|---|---|
| Consent Consistency | Copies can become stale or overwrite a withdrawal. | Define authority, ordering and reconciliation; test queued dispatch. |
| Vendor Fit | A campaign product may not support required checks. | Prove end-to-end withdrawal and dispatch behaviour before selection. |

## Conclusion

Retain this as a draft decision record for team review. The direction is supported by the current documents; unresolved choices below are not implied approvals.

### Review Required

- Select the authoritative product, fields and dispatch-control arrangement.
- Define behaviour when current permission cannot be established.
- Separate this architectural choice from the general obligation to respect permission.

### Verification

Exercise withdrawal across every supported channel, including already queued messages, and verify the five-minute limit and auditable eligibility decisions. These are planned checks, not reported test results.

### Revisit Triggers

Revisit when a new channel or product changes permission ownership or cannot meet dispatch controls.

## Sources and Related Documents

- Source entries consent portions of H-07/M-07 and VG-02 in [Potential ADRs](potentialadrs.md). The inventory preserves the originating document locations and Slack links; its IDs are provenance references, not these new ADR numbers.
- [Requirements 01–06](README.md#requirements)
- [Candidate Review](ADR_Candidates_For_Review.md)
- [Estate Context](../architecture/Estate_C4_Context.md)
- [Visitor Capability](../architecture/Visitor_Journey_and_Growth_C4_Capability.md)
- [Animal Capability](../architecture/Animal_Management_C4_Capability.md)
- [Ride Capability](../architecture/Ride_Operations_C4_Capability.md)
- [Site Operations Capability](../architecture/Crowd_and_Site_Operations_C4_Capability.md)
