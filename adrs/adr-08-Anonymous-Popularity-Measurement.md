# ADR-08 — Measure Popularity Without Routine Individual Tracking

Status: Draft for Team Review — reflects the current design; detailed review points remain open.

## Context

The estate needs attraction usage and queue insight. The current requirements assume aggregate counts, throughput and availability are sufficient without routinely identifying individual movements.

Requirement Alignment: FR-13, FR-16; anonymous-popularity assumption; restricted-sharing constraint and privacy risks.

## Decision

Use anonymous observations and aggregate usage for routine queue and popularity measurement. Keep admission identity and consented customer engagement separate from crowd observations. Do not establish a persistent identifiable movement history for this purpose. The sensing technology and point of aggregation require review.

## Key Differentiators

- Information need: Counts and availability address the stated popularity requirement.
- Data exposure: Avoids coupling ordinary crowd measurement to identity systems.
- Cost of change: A later tracking design would change sensing, schemas, retention and identity integration.

## Alternatives Considered

The alternatives below are a synthesis for team review, not a claim that a formal historical evaluation has been completed.

| Alternative | Assessment |
|---|---|
| Anonymous counters or aggregation at collection | Fits the selected direction; accuracy and placement still need validation. |
| Identifiable observations aggregated centrally | Could support richer movement analysis but introduces identity and retention exposure; not selected for routine popularity. |
| Periodic manual sampling | Useful baseline or fallback; has staffing cost and limited continuous coverage. |

## Risks & Trade-offs

| Risk Area | Description | Mitigation |
|---|---|---|
| Measurement Quality | Counts can misrepresent demand when rides are closed or sensors miss observations. | Combine counts with availability, capacity and quality metadata. |
| Privacy | Camera or pass integrations could silently introduce identity linkage. | Review data contracts, collection purposes and retained observations before rollout. |

## Conclusion

Retain this as a draft decision record for team review. The direction is supported by the current documents; unresolved choices below are not implied approvals.

### Review Required

- Choose collection mechanisms and determine where anonymisation or aggregation occurs.
- Validate the aggregate-data sufficiency assumption and set retention rules.
- Confirm that the concrete sensing commitment warrants this standalone ADR under the cost-of-change test.

### Verification

Inspect collection and event contracts for prohibited identity linkage; compare counts with manual observations and test how closures affect popularity reporting. These are planned checks, not reported test results.

### Revisit Triggers

Revisit only if a demonstrated business need cannot be met with aggregate observations or the sensing approach materially changes.

## Sources and Related Documents

- Source entries sensing portions of H-07/M-07 and CS-01 in [Potential ADRs](potentialadrs.md). The inventory preserves the originating document locations and Slack links; its IDs are provenance references, not these new ADR numbers.
- [Requirements 01–06](README.md#requirements)
- [Candidate Review](ADR_Candidates_For_Review.md)
- [Estate Context](../architecture/Estate_C4_Context.md)
- [Visitor Capability](../architecture/Visitor_Journey_and_Growth_C4_Capability.md)
- [Animal Capability](../architecture/Animal_Management_C4_Capability.md)
- [Ride Capability](../architecture/Ride_Operations_C4_Capability.md)
- [Site Operations Capability](../architecture/Crowd_and_Site_Operations_C4_Capability.md)
