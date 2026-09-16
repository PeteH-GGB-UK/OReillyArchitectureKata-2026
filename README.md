# O'Reilly Architectural Katas 2026: AI-Assisted Software Architecture - Von Digitalis Estates

This is the submission for the team **Mostly Autonomous - The Parkitects**. It proposes a resilient, event-driven architecture that uses practical, governed AI to make the estate more profitable while protecting visitor trust, animal welfare and ride safety.

<img width="1312" height="1199" alt="image" src="https://github.com/user-attachments/assets/d6cc5b68-ea17-459a-ab1b-2a0c5b4c413a" />

## Executive summary

Von Digitalis Estates is a large historic estate whose traditional business has failed. The new owner must make the estate profitable by modernising a historic amusement park of around 40 rides and an exotic animal collection of more than 200 animals across 55 enclosures. The estate currently attracts about 5,000 visitors per day and needs to reach 15,000 within three years, while improving repeat visits, understanding attraction demand, and controlling the cost of animal care.

Our architecture is grounded in the [estate system context](architecture/Estate_C4_Context.md) and responds with four bounded capabilities connected by curated events:

- **Visitor journey and growth:** deterministic ticketing and family passes, consent-led personalisation, visit planning and measurable retention.
- **Crowd and site operations:** privacy-preserving occupancy and queue insight, demand forecasting and approved operational guidance.
- **Ride operations:** inspections, maintenance workflows, resilient telemetry and predictive maintenance recommendations.
- **Animal management:** welfare records, feeding and husbandry workflows, environmental monitoring and explainable anomaly detection.

The central architectural thesis is deliberately conservative about AI: models can detect, forecast, rank and summarise, but accountable people remain responsible for safety, animal-care, maintenance, commercial and operational decisions. Deterministic controls remain local, and the platform continues to operate when cloud connectivity or an AI provider is unavailable.

## Submission evidence map

| Assessment area | Where to find the evidence |
| --- | --- |
| Business goals, requirements, constraints, risks and assumptions | [requirements documents](#requirements) |
| System context, capability boundaries, deployment views and critical journeys | [architecture documents](#capability-architecture) |
| Architecture decisions, alternatives, consequences and revisit triggers | [architecture decision records](#architecture-decisions-and-trade-offs) |

## Requirements

The requirements baseline is captured in six documents:

1. [Business Goals and Drivers](requirements/01_Business_Goals_and_Drivers.md)
2. [Business Challenges and Pain Points](requirements/02_Business_Challenges_and_Pain_Points.md)
3. [Functional Requirements](requirements/03_Functional_Requirements.md)
4. [Non-Functional Requirements](requirements/04_Non_Functional_Requirements.md)
5. [Assumptions and Constraints](requirements/05_Assumptions_and_Constraints.md)
6. [Risks and Mitigations](requirements/06_Risks_and_Mitigations.md)

## Outcomes and success measures

| Outcome | Architectural response | Evidence of success |
| --- | --- | --- |
| Grow from 5,000 to 15,000 visitors per day sustainably | Reliable ticketing and family passes, better visit planning, queue insight, consent-led engagement and measured experiments | Purchase and entry availability, queue accuracy, repeat-visit and referral uplift |
| Improve visitor experience and attraction insight | Anonymous occupancy and throughput data, freshness-aware queue estimates and approved alternatives | Queue estimate error, stale-data controls, attraction popularity and visitor-flow reporting |
| Reduce ride disruption without compromising safety | Authoritative inspection and maintenance records, resilient telemetry and engineer-reviewed predictive maintenance | Ride availability, reduced unplanned downtime, warning lead time and inspection compliance |
| Improve animal welfare and control care costs | Welfare system of record, husbandry workflows, local alerts and evidence-backed anomaly detection | Alert response, husbandry completion, telemetry durability and actionable AI alerts |
| Operate through patchy Wi-Fi | Zoned gateways, local deterministic processing, encrypted store-and-forward and replay | Backhaul-outage tests, alert latency, data durability and gateway fault isolation |
| Keep AI trustworthy and replaceable | Versioned inference contracts, provider-neutral evaluation assets, audit evidence, drift detection and human review | Model quality, drift review completion, confidence/evidence coverage and fallback tests |

## Capability architecture

The architecture evidence comprises the system context plus four capability documents. Each capability document is a self-contained architecture section with a business outcome, C4 Level 2 container view, C4 Level 3 component view, deployment/resilience view, critical dynamic journey, AI guardrails, ADR references, fitness functions, traceability and delivery sequence.

1. [Estate C4 System Context](architecture/Estate_C4_Context.md): the C4 Level 1 system boundary, actors, external dependencies and authority boundaries for the integrated estate digital system.
2. [Visitor Journey and Growth](architecture/Visitor_Journey_and_Growth_C4_Capability.md): ticketing, family passes, consent, visit planning, recommendations and sustainable growth.
3. [Crowd and Site Operations](architecture/Crowd_and_Site_Operations_C4_Capability.md): occupancy, queue estimation, attraction popularity, incidents, staffing signals and public guidance.
4. [Ride Operations](architecture/Ride_Operations_C4_Capability.md): ride status, inspections, maintenance, telemetry and predictive maintenance.
5. [Animal Management](architecture/Animal_Management_C4_Capability.md): animal records, feeding, health, enclosure telemetry, welfare alerts and population monitoring.

The views are intentionally progressive: business outcomes establish the reason for the capability, C4 views establish the structure, dynamic views show how people and systems respond to events, and fitness functions show how the architecture will be tested in operation.

## AI design and governance

AI is used where it creates measurable value and can be evaluated against evidence:

- visitor recommendations, demand forecasting and repeat-visit analysis;
- queue and occupancy forecasting with privacy-preserving data;
- ride anomaly detection, failure-risk estimation and engineering knowledge retrieval;
- animal-health anomaly detection, population estimation and approved care guidance retrieval.

The common controls are:

- **Human accountability:** AI recommendations require an appropriate visitor, duty-manager, engineer, keeper or veterinary review. Consequential action authority is enforced outside the model at domain workflow boundaries, as recorded in [ADR-06](adrs/adr-06-AI-Action-Authority.md).
- **Hard safety boundaries:** AI cannot override ride interlocks, issue emergency instructions, diagnose or treat animals, suppress alarms, alter entitlements, or authorise consequential operational actions. Independent ride and welfare protection is captured in [ADR-04](adrs/adr-04-Independent-Local-Protection.md).
- **Deterministic fallback:** rules, inspections, scheduled care, cached entitlements and approved content continue when models, providers or cloud connectivity fail. Offline admission continuity is bounded by [ADR-05](adrs/adr-05-Offline-Admission.md).
- **Evidence and evaluation:** outputs carry confidence, source/evidence references, model and policy versions; evaluation includes normal, degraded, missing-data and known-incident cases.
- **Operational monitoring:** input quality, drift, false positives, missed events, overrides, stale data and actionable-alert rates create owned review tasks.
- **Provider portability:** internal versioned inference contracts separate domain workflows from model providers, prompts and deployment choices, with evaluation assets retained independently under [ADR-07](adrs/adr-07-Provider-Neutral-AI.md).
- **Privacy and least privilege:** consent is enforced at outbound decisions, occupancy defaults to anonymous counts, and welfare/clinical information remains within its owning domain. The related decisions are [ADR-08](adrs/adr-08-Anonymous-Popularity-Measurement.md), [ADR-09](adrs/adr-09-Consent-Authority-and-Dispatch.md) and [ADR-01](adrs/adr-01-Controlled-Access-to-Domain-Records.md).

## Architecture decisions and trade-offs

The major design choices live as standalone ADRs. They make the cost of change, rejected alternatives, verification approach and revisit triggers explicit rather than leaving trade-offs embedded only in the capability narratives.

The current ADR set is:

1. [ADR-01: Control Operational Updates Through the Owning Domain](adrs/adr-01-Controlled-Access-to-Domain-Records.md)
2. [ADR-02: Use an Estate Event Platform for Cross-Domain Facts](adrs/adr-02-Estate-Event-Platform.md)
3. [ADR-03: Use Zoned Edge Collection With Durable Buffering](adrs/adr-03-Zoned-Edge-Buffering.md)
4. [ADR-04: Keep Safety and Welfare Protection Independent of Estate Software](adrs/adr-04-Independent-Local-Protection.md)
5. [ADR-05: Validate Signed Admission Entitlements Locally During Disconnection](adrs/adr-05-Offline-Admission.md)
6. [ADR-06: Enforce AI Action Authority Through Domain Workflows](adrs/adr-06-AI-Action-Authority.md)
7. [ADR-07: Use Provider-Neutral AI Interfaces and Retain Evaluation Assets](adrs/adr-07-Provider-Neutral-AI.md)
8. [ADR-08: Measure Popularity Without Routine Individual Tracking](adrs/adr-08-Anonymous-Popularity-Measurement.md)
9. [ADR-09: Use Authoritative Consent With Enforcement at Dispatch](adrs/adr-09-Consent-Authority-and-Dispatch.md)
10. [ADR-10: Separate Analytical Projections From Operational Records](adrs/adr-10-Separate-Analytical-Projections.md)
11. [ADR-11: Buy an Integration-Capable CRM](adrs/adr-11-Buy-CRM.md)

Important trade-offs made visible in the architecture include:

- resilience and local operation add gateway, synchronisation and reconciliation complexity, captured in [ADR-03](adrs/adr-03-Zoned-Edge-Buffering.md) and [ADR-05](adrs/adr-05-Offline-Admission.md);
- human approval limits automation speed but preserves safety, welfare and commercial accountability, captured in [ADR-04](adrs/adr-04-Independent-Local-Protection.md) and [ADR-06](adrs/adr-06-AI-Action-Authority.md);
- provider-neutral AI contracts improve replaceability but add compatibility and evaluation work, captured in [ADR-07](adrs/adr-07-Provider-Neutral-AI.md);
- anonymous analytics protect privacy but reduce individual-level insight, captured in [ADR-08](adrs/adr-08-Anonymous-Popularity-Measurement.md);
- event-driven boundaries improve independent evolution but require schema, replay and ownership governance, captured in [ADR-01](adrs/adr-01-Controlled-Access-to-Domain-Records.md), [ADR-02](adrs/adr-02-Estate-Event-Platform.md) and [ADR-10](adrs/adr-10-Separate-Analytical-Projections.md);
- buying CRM accelerates commodity customer management but leaves vendor fit, export, consent ownership and integration proof to product selection, captured in [ADR-11](adrs/adr-11-Buy-CRM.md).

## Delivery and operational proof

The proposed sequence starts with authoritative records, ticketing, consent, inspections, care workflows, site status and observability. It then adds resilient telemetry and queue visibility, followed by governed predictive capabilities and finally cross-estate optimisation, personalisation and carefully bounded conversational assistance.

The architecture is intended to be judged by measurable fitness functions rather than by its technology inventory. Representative controls include purchase and entry availability, entitlement integrity, queue estimate accuracy and freshness, ride availability, maintenance lead time, mandatory-care completion, alert acknowledgement, telemetry durability, event delivery, privacy contract tests, AI evidence/drift checks and analytical traceability.

Before implementation, the estate should validate baselines and targets with visitors, duty managers, ride engineers, keepers, veterinary specialists, privacy stakeholders and security teams. The numerical targets in the capability documents are explicitly proposed starting points, not facts supplied by the brief. The ADR verification sections define planned checks for the highest-cost decisions, including event replay, gateway outage recovery, independent protection failure tests, offline admission reconciliation, AI action denial, provider loss, consent withdrawal and analytical rebuilds.

## Team members

- Pete Halloran
- Matt Gould
- Alex Jacobs
- Edward Manning
- Helen Keeling
- Chris Lewis
