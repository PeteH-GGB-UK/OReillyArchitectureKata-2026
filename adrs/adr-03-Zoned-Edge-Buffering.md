# ADR-03 — Use Zoned Edge Collection With Durable Buffering

Status: Draft for Team Review — reflects the current design; detailed review points remain open.

## Context

Field observations originate across 40 rides and 55 animal displays/enclosures with patchy Wi-Fi. Losing estate-to-cloud connectivity must not automatically stop collection.

Requirement Alignment: NFR-05, NFR-14, NFR-19, NFR-20; unreliable-Wi-Fi constraint; gateway and sensor assumptions.

## Decision

Use managed zoned gateways to identify and validate observations, buffer them durably and forward or replay them when connectivity permits. Size the design for the agreed 24-hour telemetry window at the approved rate. Keep protection independent as described in ADR-04. Local buffering does not imply that every AI model runs at the edge.

## Key Differentiators

- Connectivity resilience: Collection continues while backhaul is unavailable and local equipment remains healthy.
- Device capability: Gateways can support devices that lack substantial storage or processing.
- Cost of change: Installed gateways, power, network links and field-support arrangements are expensive to replace.

## Alternatives Considered

The alternatives below are a synthesis for team review, not a claim that a formal historical evaluation has been completed.

| Alternative | Assessment |
|---|---|
| Direct device-to-cloud | Fewer intermediate components, but depends on device connectivity and buffering capability. |
| Buffer on every device | Distributes failure risk but increases device requirements and fleet variation. |
| Single on-site collector | Simpler central administration but creates a wider failure domain and still needs field connectivity. |
| Zoned gateways | Selected direction; balances local collection with manageable failure zones. |

## Risks & Trade-offs

| Risk Area | Description | Mitigation |
|---|---|---|
| Edge Failure | A failed gateway can interrupt its zone. | Provide health monitoring, replacement procedures and proportionate backup power. |
| Capacity | Unsized buffers may fill before backhaul returns. | Calculate rates and storage; test exhaustion and simultaneous replay. |

## Conclusion

Retain this as a draft decision record for team review. The direction is supported by the current documents; unresolved choices below are not implied approvals.

### Review Required

- Survey radio coverage, power, environmental conditions and non-invasive instrumentation feasibility.
- Agree zone count, device rates, storage, backhaul and device-to-gateway loss handling.
- Specify which local threshold functions exist without depending on the gateway for independent protection.

### Verification

Exercise 24-hour backhaul loss, full buffers, power loss, gateway replacement and failed updates separately. Verify original timestamps, reconciliation and the NFR-14 recovery rate. These are planned checks, not reported test results.

### Revisit Triggers

Revisit when survey results, telemetry volumes or field-support costs invalidate the zoned deployment assumptions.

## Sources and Related Documents

- Source entries H-03/M-03, RO-03, AC-02, CS-03 and S-05 in [Potential ADRs](potentialadrs.md). The inventory preserves the originating document locations and Slack links; its IDs are provenance references, not these new ADR numbers.
- [Requirements 01–06](README.md#requirements)
- [Candidate Review](ADR_Candidates_For_Review.md)
- [Estate Context](../architecture/Estate_C4_Context.md)
- [Visitor Capability](../architecture/Visitor_Journey_and_Growth_C4_Capability.md)
- [Animal Capability](../architecture/Animal_Management_C4_Capability.md)
- [Ride Capability](../architecture/Ride_Operations_C4_Capability.md)
- [Site Operations Capability](../architecture/Crowd_and_Site_Operations_C4_Capability.md)
