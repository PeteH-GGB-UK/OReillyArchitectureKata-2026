# Assumptions and Constraints

Estate-wide assumptions underpinning the proposed architecture, followed by constraints that restrict its design. Assumptions are working premises, not confirmed facts. Constraints distinguish external limits from boundaries imposed by the proposed architecture.

## Assumptions

### Infrastructure and Integration

- **Gateway Deployment:** Suitable locations, power and intermittent backhaul can be provided for zoned gateways, making local collection and later synchronisation feasible.
- **Sensor Installation:** Priority rides and enclosures can be instrumented without altering their essential safety or welfare arrangements, supporting observation alongside existing physical operations.
- **Bounded Disconnection:** Operationally useful continuity can be provided through temporary outages. The current planning assumptions are four hours of offline admission and 24 hours of telemetry buffering; these are provisional design bounds.
- **Purchased Platforms:** Suitable CRM and other commodity products expose sufficient APIs, data export and integration facilities to participate in the estate architecture without duplicating ownership of business records.

### Data and Intelligence

- **Operational Records:** Staff can reconstruct reliable initial registers from paper records and observations, then maintain them digitally. This underpins domain-owned records and cross-estate reporting.
- **Training and Evaluation Data:** Routine operations will yield enough representative, verified outcomes to evaluate selected models against non-AI baselines. Predictive capabilities depend on this future data, rather than an assumed historical dataset.
- **Anonymous Popularity Measurement:** Aggregate counts, throughput and attraction availability provide sufficient information for useful popularity and queue analysis without identifying individual visitors.
- **Piranha Sensing:** The proposed combined estimator assumes suitable PIT tagging and detection, useful feeding-time imagery and independent keeper observations. Existing tags, exact manual counts and a quarterly counting schedule are unconfirmed premises of that design.
- **External Animal Records:** The newer ZIMS integration proposal assumes an external authoritative animal record is available and accessible. This remains conditional: existing ZIMS use and accreditation are not established by the brief.

### People and Operations

- **Staff Participation:** Keepers, engineers and operations staff have capacity to maintain records, review recommendations and respond to alerts; the funded IT team can support the selected platforms and field equipment.
- **Disconnected Entry:** The estate can accept a bounded period of admission using previously issued entitlements, with staff handling exceptions and subsequent reconciliation. This assumes an acceptable level of delayed revocation and duplicate-use exposure.
- **Visitor Channels:** A useful proportion of visitors will use digital guidance, while others use signage and staff assistance. The visitor journey therefore does not depend on universal smartphone ownership or app adoption.

## Constraints

### Environmental and Financial Constraints

- **Unreliable Wi-Fi:** The design cannot depend on continuous estate-wide Wi-Fi connectivity. Cloud-dependent functions require an explicit estate-to-cloud path and a defined behaviour when that path is unavailable.
- **Proportionate Expenditure:** Infrastructure and recurring operating costs must be affordable for the estate's business model. No fixed ceiling is supplied, but an unlimited-budget design is excluded; major networking, compute and AI expenditure needs a proportionate business justification.

### Safety and Authority Constraints

- **Independent Protection:** Cloud services and AI must not sit in the immediate ride-safety or essential animal-welfare control path. Telemetry and analytical functions cannot override local protection.
- **Human Authority:** AI cannot authorise ride return to service, treatment, verified population changes, closures or emergency instructions. These actions remain with the appropriate qualified or authorised staff.
- **Deterministic Commerce:** AI cannot alter prices, payments, refunds, ticket entitlements or communication permissions. Such changes pass through authorised business rules and workflows.

### Data and Integration Constraints

- **Record Ownership:** Shared analytics and event infrastructure cannot become competing systems of record. Changes to authoritative records must pass through their owning domain's controlled interfaces.
- **Restricted Data Sharing:** Crowd measurement uses anonymous observations by default. Visitor-facing services receive only approved operational information, excluding clinical records and restricted animal-location details; personalisation and communications remain subject to recorded permissions.
- **Replaceable AI:** Essential workflows cannot require a particular model or provider to remain available. Provider-specific implementation stays behind internal interfaces, with a usable non-AI fallback.
