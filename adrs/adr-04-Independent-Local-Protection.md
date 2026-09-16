# ADR-04 — Keep Safety and Welfare Protection Independent of Estate Software

Status: Draft for Team Review — reflects the current design; detailed review points remain open.

## Context

Existing ride protection and essential local welfare protection must continue during network, cloud, gateway or AI failure. The actual capabilities and interfaces of installed equipment require specialist verification.

Requirement Alignment: NFR-07, NFR-23; independent-protection constraint; ride safety and welfare risks.

## Decision

Preserve an independent protection path outside the estate software’s command authority. Integration may obtain permitted observations, but cannot override ride interlocks, suppress essential protection or operate life-support equipment through AI. Admission continuity is a separate commercial decision in ADR-05. The detailed isolation mechanism is not yet selected.

## Key Differentiators

- Failure independence: Failure of monitoring and analytics must not remove protection.
- Existing equipment: Integration must respect validated local arrangements.
- Cost of change: Altering the boundary can require substantial engineering, operational change and assurance.

## Alternatives Considered

The alternatives below are a synthesis for team review, not a claim that a formal historical evaluation has been completed.

| Alternative | Assessment |
|---|---|
| Existing isolated protection with separate observational sensors | Avoids a control connection; may duplicate sensing and requires validated installation. |
| Controlled read-only interface from existing equipment | Can reuse observations where supported; requires verification that the interface cannot affect protection. |
| Cloud or AI-dependent protective control | Outside the agreed requirements; not a viable alternative being recommended for evaluation. |

## Risks & Trade-offs

| Risk Area | Description | Mitigation |
|---|---|---|
| Safety Boundary | A purported observation interface could introduce an unintended dependency. | Review interfaces with qualified specialists and test dependency failures safely. |
| Existing Equipment | Current protection coverage is assumed rather than verified. | Survey and document actual controls and local response arrangements. |

## Conclusion

Retain this as a draft decision record for team review. The direction is supported by the current documents; unresolved choices below are not implied approvals.

### Review Required

- Confirm which observations can be safely obtained and select the isolation design per equipment class.
- Identify qualified reviewers and retain their boundary assessment.
- Review whether this remains a standalone ADR once the concrete mechanism is chosen; the general independence requirement also remains a constraint.

### Verification

In a safe environment, demonstrate that cloud, network, gateway and AI failures cannot disable protection or permit unauthorised return to service. Retain specialist review evidence. These are planned checks, not reported test results.

### Revisit Triggers

Revisit when equipment is replaced or integration changes could affect the protection boundary.

## Sources and Related Documents

- Source entries H-04/M-04, RO-02 and protection aspects of AC-02 in [Potential ADRs](potentialadrs.md). The inventory preserves the originating document locations and Slack links; its IDs are provenance references, not these new ADR numbers.
- [Requirements 01–06](README.md#requirements)
- [Candidate Review](ADR_Candidates_For_Review.md)
- [Estate Context](../architecture/Estate_C4_Context.md)
- [Visitor Capability](../architecture/Visitor_Journey_and_Growth_C4_Capability.md)
- [Animal Capability](../architecture/Animal_Management_C4_Capability.md)
- [Ride Capability](../architecture/Ride_Operations_C4_Capability.md)
- [Site Operations Capability](../architecture/Crowd_and_Site_Operations_C4_Capability.md)
