# ADR-11 — Buy an Integration-Capable CRM

Status: Accepted — CRM buy decision only; product selection remains open.

## Context

The estate requires customer management and consent-based campaigns to support repeat business. CRM is a standard capability, and no estate-specific benefit from recreating it has been identified.

Requirement Alignment: FR-04; purchased-platform assumption; estate context.

## Decision

Buy an existing CRM rather than build a bespoke CRM. The chosen product must support integration with other estate systems through an API or another suitable mechanism such as MCP or CLI; support for all three is not required. Edward has confirmed the team’s buy decision. Vendor selection and detailed consent/customer authority remain open.

## Key Differentiators

- Commodity capability: Reuse established customer and campaign functionality.
- Delivery and support: Avoid funding bespoke implementation and long-term maintenance without an identified differentiating benefit.
- Integration and exit: Evaluate fit, export and integration alongside purchase cost. No numerical cost comparison has yet been supplied.

## Alternatives Considered

The buy-versus-build outcome is confirmed in source U-01. Product-level alternatives and costs have not yet been evaluated in this record.

| Alternative | Assessment |
|---|---|
| Build a bespoke CRM | Rejected in the confirmed discussion: no benefit was identified that justifies recreating standard CRM capability. |
| Buy and configure an existing CRM | Selected; integrate estate-specific workflows without rebuilding the product. |
| Buy with extensive customisation | Not a separate accepted choice; assess whether customisation would erase the expected benefit and increase lock-in. |

## Risks & Trade-offs

| Risk Area | Description | Mitigation |
|---|---|---|
| Procurement | Licensing, API limits or functionality may conflict with estate needs. | Evaluate total cost and prove required integration before product selection. |
| Data Ownership | CRM can duplicate customer or consent authority. | Agree field ownership with ticketing and Visitor Journey; coordinate with ADR-09. |
| Exit | Export limits or customisation may make replacement expensive. | Verify usable export, contractual limits and a migration route. |

## Conclusion

Retain the confirmed buy decision and complete product selection through the review points below.

### Review Required

- Select a product after functional-fit, licensing, security, integration and export assessment.
- Salesforce remains an example, not the selected vendor.
- Reconcile older FR-04 and procurement-risk wording that still describes the buy decision as outstanding when the team integrates this record into the submission.

### Verification

Run a small integration trial for customer updates, campaign eligibility, withdrawal, event publication and export. Record actual costs and limitations; do not infer them from the buy decision. These are planned checks, not reported test results.

### Revisit Triggers

Revisit if no purchasable product can meet essential requirements within acceptable integration, operating and exit costs.

## Sources and Related Documents

- Source entries U-01, with supporting M-10 and S-03 in [Potential ADRs](potentialadrs.md). The inventory preserves the originating document locations and Slack links; its IDs are provenance references, not these new ADR numbers.
- [Requirements 01–06](README.md#requirements)
- [Candidate Review](ADR_Candidates_For_Review.md)
- [Estate Context](../architecture/Estate_C4_Context.md)
- [Visitor Capability](../architecture/Visitor_Journey_and_Growth_C4_Capability.md)
- [Animal Capability](../architecture/Animal_Management_C4_Capability.md)
- [Ride Capability](../architecture/Ride_Operations_C4_Capability.md)
- [Site Operations Capability](../architecture/Crowd_and_Site_Operations_C4_Capability.md)
