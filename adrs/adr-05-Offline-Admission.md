# ADR-05 — Validate Signed Admission Entitlements Locally During Disconnection

Status: Draft for Team Review — reflects the current design; detailed review points remain open.

## Context

Admission should remain usable through bounded loss of connectivity, but disconnected gates cannot always know current revocation or simultaneous use elsewhere.

Requirement Alignment: FR-01; NFR-05, NFR-11, NFR-14; disconnected-entry assumptions and risks.

## Decision

Use local deterministic validation of eligible signed, time-bounded entitlements, retain a durable admission journal and reconcile with authoritative ticketing after reconnection. The four-hour planning window is subject to approval of risk and procedures. This does not authorise offline payments or select a pass medium.

## Key Differentiators

- Visitor continuity: Reduces dependence on immediate central availability at entry.
- Bounded trust: Signature and expiry checks help establish eligibility, but do not eliminate delayed revocation or duplicate use.
- Cost of change: Affects ticket issuance, gate software, purchased-product fit and reconciliation contracts.

## Alternatives Considered

The alternatives below are a synthesis for team review, not a claim that a formal historical evaluation has been completed.

| Alternative | Assessment |
|---|---|
| Online validation with manual exceptions | Simpler current-state checks; disruption transfers work to staff and can create queues. |
| Signed entitlements and local journal | Selected direction; permits bounded continuity with explicit reconciliation and exposure. |
| On-site authoritative admission service | Could coordinate gates locally but introduces another service and an estate-network dependency. |

## Risks & Trade-offs

| Risk Area | Description | Mitigation |
|---|---|---|
| Admission Integrity | Disconnected gates may accept revoked or reused passes. | Agree exposure, local duplicate checks, expiry and staff exception procedures. |
| Reconciliation | Conflicting or repeated journals can distort admission history. | Use stable entry identifiers, controlled retries and visible exception handling. |

## Conclusion

Retain this as a draft decision record for team review. The direction is supported by the current documents; unresolved choices below are not implied approvals.

### Review Required

- Approve the outage window, revocation policy and acceptable duplicate-use exposure.
- Prove signing, key rotation, caching and journal support with the selected ticketing product.
- Define expired-pass and lost-device procedures and reconcile gate records.

### Verification

Disconnect gates for the agreed window; test expiry, invalid signatures, delayed revocation, duplicate presentation, full storage and reconnection without duplicate business effects. These are planned checks, not reported test results.

### Revisit Triggers

Revisit if fraud exposure, physical gate design or ticketing capability makes the offline approach unsuitable.

## Sources and Related Documents

- Source entries VG-04, admission portions of H-04/M-04 and S-03 in [Potential ADRs](potentialadrs.md). The inventory preserves the originating document locations and Slack links; its IDs are provenance references, not these new ADR numbers.
- [Requirements 01–06](README.md#requirements)
- [Candidate Review](ADR_Candidates_For_Review.md)
- [Estate Context](../architecture/Estate_C4_Context.md)
- [Visitor Capability](../architecture/Visitor_Journey_and_Growth_C4_Capability.md)
- [Animal Capability](../architecture/Animal_Management_C4_Capability.md)
- [Ride Capability](../architecture/Ride_Operations_C4_Capability.md)
- [Site Operations Capability](../architecture/Crowd_and_Site_Operations_C4_Capability.md)
