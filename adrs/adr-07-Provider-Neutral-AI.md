# ADR-07 — Use Provider-Neutral AI Interfaces and Retain Evaluation Assets

Status: Draft for Team Review — reflects the current design; detailed review points remain open.

## Context

Model quality, pricing and availability can change. Embedding provider-specific contracts in domain workflows would make migration costly and can compromise continuity.

Requirement Alignment: NFR-18, NFR-24, NFR-29, NFR-30; replaceable-AI constraint.

## Decision

Place provider-specific implementation behind versioned internal inference interfaces and retain evaluation assets, prompts and contracts independently. Every production use case has a tested non-AI fallback and a documented replacement route. Evaluate replacement behaviour before activation; portability does not mean models are interchangeable. A single central deployment is not mandated.

## Key Differentiators

- Migration control: Keeps vendor changes from propagating through all domain workflows.
- Evidence continuity: Independent evaluation assets allow comparison of replacements.
- Cost of change: Upfront abstraction effort trades against future provider migration and exit costs.

## Alternatives Considered

The alternatives below are a synthesis for team review, not a claim that a formal historical evaluation has been completed.

| Alternative | Assessment |
|---|---|
| Direct vendor integration in each domain | Lowest initial abstraction effort but duplicates coupling and migration work. |
| Thin internal adapters | A proportionate starting approach where shared hosting is unnecessary. |
| Shared inference service | Centralises governance and operations but introduces shared availability and scaling concerns. |
| Self-hosted models | May reduce hosted-provider dependence but shifts infrastructure, licensing and operational costs to the estate. |

## Risks & Trade-offs

| Risk Area | Description | Mitigation |
|---|---|---|
| Provider Dependency | An adapter can hide incompatible model behaviour. | Re-run approved evaluations and shadow trials for replacements. |
| Cost | Price increases or traffic spikes can undermine viability. | Meter use, enforce discretionary ceilings and preserve essential non-AI workflows. |

## Conclusion

Retain this as a draft decision record for team review. The direction is supported by the current documents; unresolved choices below are not implied approvals.

### Review Required

- Select adapter/deployment arrangements and supported contracts per use case.
- Define price-change and shutdown responses, model asset rights and export limitations.
- Agree budgets and rehearse replacement at least annually and after material provider changes.

### Verification

Inject timeout, provider loss and budget exhaustion; test five-second interactive fallback and prediction expiry. Record replacement effort and evaluation results. These are planned checks, not reported test results.

### Revisit Triggers

Revisit on provider withdrawal, material price or licence changes, or when abstraction prevents necessary model capability.

## Sources and Related Documents

- Source entries H-06/M-06, RO-06, AC-06 and R-03 in [Potential ADRs](potentialadrs.md). The inventory preserves the originating document locations and Slack links; its IDs are provenance references, not these new ADR numbers.
- [Requirements 01–06](README.md#requirements)
- [Candidate Review](ADR_Candidates_For_Review.md)
- [Estate Context](../architecture/Estate_C4_Context.md)
- [Visitor Capability](../architecture/Visitor_Journey_and_Growth_C4_Capability.md)
- [Animal Capability](../architecture/Animal_Management_C4_Capability.md)
- [Ride Capability](../architecture/Ride_Operations_C4_Capability.md)
- [Site Operations Capability](../architecture/Crowd_and_Site_Operations_C4_Capability.md)
