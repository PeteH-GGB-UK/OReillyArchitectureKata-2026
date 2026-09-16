# ADR-10 — Separate Analytical Projections From Operational Records

Status: Draft for Team Review — reflects the current design; detailed review points remain open.

## Context

Estate Management needs cross-domain evidence about popularity, cost, availability and improvement outcomes. Reporting must not compete with operational ownership or turn analytical amendments into changes to live records.

Requirement Alignment: FR-15, FR-16; G6 and monthly reporting milestone; record-ownership constraints.

## Decision

Build separate curated analytical projections for strategic reporting, with provenance back to domain records. Feed them through governed integration; change operational records only through their owners. Analytical history and live Site Operations dashboards serve different purposes. Storage, BI products and refresh choices remain open.

## Key Differentiators

- Workload separation: Analytical queries need not burden critical operational workflows.
- Cross-domain history: Curated data supports comparable trends and investment evidence.
- Cost of change: Pipelines, historical storage and report dependencies become expensive to replace.

## Alternatives Considered

The alternatives below are a synthesis for team review, not a claim that a formal historical evaluation has been completed.

| Alternative | Assessment |
|---|---|
| Reports directly on operational databases | Low initial pipeline effort but couples queries and schema changes to operations. |
| Operational read replicas | Offloads some reads, but does not itself reconcile cross-domain meaning or history. |
| Separate analytical store fed by events or batch | Selected direction; supports curation with additional pipelines, delay and reconciliation. |
| Purchased reporting integration | Can implement the selected separation if provenance and ownership controls are adequate. |

## Risks & Trade-offs

| Risk Area | Description | Mitigation |
|---|---|---|
| Data Quality | Reports can misinterpret popularity or omit costs. | Include availability, capacity, observation quality and agreed financial sources. |
| Consistency | Derived views can lag or diverge. | Expose refresh times, reconcile and preserve source lineage. |

## Conclusion

Retain this as a draft decision record for team review. The direction is supported by the current documents; unresolved choices below are not implied approvals.

### Review Required

- Agree reporting schemas, refresh intervals, pipeline owners and analytical recovery arrangements.
- Identify financial inputs not captured by domain workflows.
- Select BI/storage products and establish evidence for all 40 rides and 55 displays/enclosures within the reporting milestone.

### Verification

Trace sampled metrics to source records, rebuild projections, test corrections and compare reports with operational totals under agreed definitions. These are planned checks, not reported test results.

### Revisit Triggers

Revisit if volume, freshness, costs or strategic reporting needs cannot be met by the chosen analytical approach.

## Sources and Related Documents

- Source entries H-08/M-08 and supporting VG-03 in [Potential ADRs](potentialadrs.md). The inventory preserves the originating document locations and Slack links; its IDs are provenance references, not these new ADR numbers.
- [Requirements 01–06](README.md#requirements)
- [Candidate Review](ADR_Candidates_For_Review.md)
- [Estate Context](../architecture/Estate_C4_Context.md)
- [Visitor Capability](../architecture/Visitor_Journey_and_Growth_C4_Capability.md)
- [Animal Capability](../architecture/Animal_Management_C4_Capability.md)
- [Ride Capability](../architecture/Ride_Operations_C4_Capability.md)
- [Site Operations Capability](../architecture/Crowd_and_Site_Operations_C4_Capability.md)
