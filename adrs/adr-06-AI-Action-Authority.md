# ADR-06 — Enforce AI Action Authority Through Domain Workflows

Status: Draft for Team Review — reflects the current design; detailed review points remain open.

## Context

Predictions and generated guidance can be wrong or manipulated. Existing requirements reserve consequential operational and commercial authority for controlled workflows and qualified people.

Requirement Alignment: NFR-24–29, NFR-31; human-authority and deterministic-commerce constraints.

## Decision

Enforce permissions, deterministic rules and approval gates outside model output, at the domain action boundary. AI provides evidence and recommendations; only explicitly permitted low-risk actions may execute automatically. It cannot authorise ride return to service, care changes, closures, emergency instructions or commercial record changes. An approval asserted by a model is not an approval credential.

## Key Differentiators

- Accountability: Qualified staff retain responsibility and auditable decisions.
- Independent enforcement: Model behaviour cannot grant itself permissions.
- Cost of change: Moving authority into autonomous tools would change security, workflow and assurance across domains.

## Alternatives Considered

The alternatives below are a synthesis for team review, not a claim that a formal historical evaluation has been completed.

| Alternative | Assessment |
|---|---|
| Existing domain workflow gates | Fits accountable record ownership; requires consistent enforcement across applications. |
| Shared policy service plus domain validation | Can centralise policy, but adds dependency and does not remove domain checks. |
| Restricted read-only AI tools | Useful for some assistants, but insufficient alone for permitted task creation or other bounded actions. |
| Prompt-only approval instructions | Cannot establish the required independent enforcement; not selected. |

## Risks & Trade-offs

| Risk Area | Description | Mitigation |
|---|---|---|
| Authority | Different documents assign closure responsibility differently. | Agree an action-authority matrix distinguishing technical release from operational closure. |
| AI Security | Retrieved content or tool calls may attempt to bypass controls. | Enforce permissions independently and run adversarial tests. |

## Conclusion

Retain this as a draft decision record for team review. The direction is supported by the current documents; unresolved choices below are not implied approvals.

### Review Required

- Choose enforcement mechanisms and ownership rather than assuming a new policy service is required.
- Agree the explicit low-risk action list; automatic animal-visibility publication is not accepted by this record.
- Confirm approval credentials, escalation, evidence and model-promotion rules.

### Verification

Test permitted and prohibited actions, spoofed approval, prompt injection, missing evidence and provider failure. Retain expected results and human-authority audit trails. These are planned checks, not reported test results.

### Revisit Triggers

Revisit before adding any new autonomous action or expanding access to domain write tools.

## Sources and Related Documents

- Source entries H-05/M-05, RO-05, AC-04, CS-05, VG-01 and VG-05 in [Potential ADRs](potentialadrs.md). The inventory preserves the originating document locations and Slack links; its IDs are provenance references, not these new ADR numbers.
- [Requirements 01–06](README.md#requirements)
- [Candidate Review](ADR_Candidates_For_Review.md)
- [Estate Context](../architecture/Estate_C4_Context.md)
- [Visitor Capability](../architecture/Visitor_Journey_and_Growth_C4_Capability.md)
- [Animal Capability](../architecture/Animal_Management_C4_Capability.md)
- [Ride Capability](../architecture/Ride_Operations_C4_Capability.md)
- [Site Operations Capability](../architecture/Crowd_and_Site_Operations_C4_Capability.md)
