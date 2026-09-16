# O'Reilly Architectural Katas 2026: AI-Assisted Software Architecture - Von Digitalis Estates

This is the submission for the team **Mostly Autonomous - The Parkitects**. It proposes a resilient, event-driven architecture that uses practical, governed AI to make the estate more profitable while protecting visitor trust, animal welfare and ride safety.

<img width="1312" height="1199" alt="image" src="https://github.com/user-attachments/assets/d6cc5b68-ea17-459a-ab1b-2a0c5b4c413a" />

## Executive summary

Von Digitalis Estates is a large historic estate whose traditional business has failed. The new owner must make the estate profitable by modernising a historic amusement park of around 40 rides and an exotic animal collection of more than 200 animals across 55 enclosures. The estate currently attracts about 5,000 visitors per day and needs to reach 15,000 within three years, while improving repeat visits, understanding attraction demand, and controlling the cost of animal care.

Our architecture responds with four bounded capabilities connected by curated events:

- **Visitor journey and growth:** deterministic ticketing and family passes, consent-led personalisation, visit planning and measurable retention.
- **Crowd and site operations:** privacy-preserving occupancy and queue insight, demand forecasting and approved operational guidance.
- **Ride operations:** inspections, maintenance workflows, resilient telemetry and predictive maintenance recommendations.
- **Animal management:** welfare records, feeding and husbandry workflows, environmental monitoring and explainable anomaly detection.

The central architectural thesis is deliberately conservative about AI: models can detect, forecast, rank and summarise, but accountable people remain responsible for safety, animal-care, maintenance, commercial and operational decisions. Deterministic controls remain local, and the platform continues to operate when cloud connectivity or an AI provider is unavailable.

## Submission evidence map

| Assessment area | Where to find the evidence |
| --- | --- |
| Business context, outcomes and constraints | [The brief](requirements/The_Brief.md) and the executive summary above |
| Progressive C4 architecture, deployment and critical journeys | The four [capability submissions](#capability-architecture) |
| Practical AI use with explicit boundaries | The **AI strategy and guardrails** section in each capability submission |
| Validation, fallback and production monitoring | The **Validation and fallback** and **Architecture fitness functions** sections |
| Reasoning, alternatives and consequences | The **Architectural decision records** section in each capability submission and [ADR template](adrs/adr-00-Template.md) |
| Requirement-to-architecture traceability | The **Traceability summary** section in each capability submission |
| Deliverable sequencing and early value | The **Delivery sequence and conclusion** section in each capability submission |
| AI innovation assessment and enhancement proposals | [AI innovation assessment](requirements/AI_Innovation_Assessment_and_Enhancements.md) |
| Judging criteria and submission priorities | [Judging rubric summary](requirements/Architecture_Kata_Judging_Rubric_Summary.md) and [submission priorities](requirements/Architecture_Kata_Submission_Priorities.md) |

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

Each capability document is a self-contained architecture section with a business outcome, C4 Level 2 container view, C4 Level 3 component view, deployment/resilience view, critical dynamic journey, AI guardrails, ADRs, fitness functions, traceability and delivery sequence.

1. [Visitor Journey and Growth](architecture/Visitor_Journey_and_Growth_C4_Capability.md): ticketing, family passes, consent, visit planning, recommendations and sustainable growth.
2. [Crowd and Site Operations](architecture/Crowd_and_Site_Operations_C4_Capability.md): occupancy, queue estimation, attraction popularity, incidents, staffing signals and public guidance.
3. [Ride Operations](architecture/Ride_Operations_C4_Capability.md): ride status, inspections, maintenance, telemetry and predictive maintenance.
4. [Animal Management](architecture/Animal_Management_C4_Capability.md): animal records, feeding, health, enclosure telemetry, welfare alerts and population monitoring.

The views are intentionally progressive: business outcomes establish the reason for the capability, C4 views establish the structure, dynamic views show how people and systems respond to events, and fitness functions show how the architecture will be tested in operation.

## AI design and governance

AI is used where it creates measurable value and can be evaluated against evidence:

- visitor recommendations, demand forecasting and repeat-visit analysis;
- queue and occupancy forecasting with privacy-preserving data;
- ride anomaly detection, failure-risk estimation and engineering knowledge retrieval;
- animal-health anomaly detection, population estimation and approved care guidance retrieval.

The common controls are:

- **Human accountability:** AI recommendations require an appropriate visitor, duty-manager, engineer, keeper or veterinary review.
- **Hard safety boundaries:** AI cannot override ride interlocks, issue emergency instructions, diagnose or treat animals, suppress alarms, alter entitlements, or authorise consequential operational actions.
- **Deterministic fallback:** rules, inspections, scheduled care, cached entitlements and approved content continue when models, providers or cloud connectivity fail.
- **Evidence and evaluation:** outputs carry confidence, source/evidence references, model and policy versions; evaluation includes normal, degraded, missing-data and known-incident cases.
- **Operational monitoring:** input quality, drift, false positives, missed events, overrides, stale data and actionable-alert rates create owned review tasks.
- **Provider portability:** internal versioned inference contracts separate domain workflows from model providers, prompts and deployment choices.
- **Privacy and least privilege:** consent is enforced at outbound decisions, occupancy defaults to anonymous counts, and welfare/clinical information remains within its owning domain.

## Architecture decisions and trade-offs

The capability documents contain concise, decision-grade ADRs covering the most consequential choices: domain ownership, event-driven integration, edge resilience, local safety controls, privacy, consent, AI boundaries, provider neutrality and build-versus-buy implications. Each decision records its context, choice and consequence. The ADR structure is captured in [ADR-00](adrs/adr-00-Template.md); the next submission-hardening step is to extract the highest-impact decisions into five to ten standalone ADR files with explicit alternatives, rejected options, enforcement mechanisms and revisit triggers.

Important trade-offs made visible in the architecture include:

- resilience and local operation add gateway, synchronisation and reconciliation complexity;
- human approval limits automation speed but preserves safety and accountability;
- provider-neutral AI contracts improve replaceability but add compatibility and evaluation work;
- anonymous analytics protect privacy but reduce individual-level insight;
- event-driven boundaries improve independent evolution but require schema, replay and ownership governance.

## Delivery and operational proof

The proposed delivery sequence starts with authoritative records, ticketing, consent, inspections, care workflows, site status and observability. It then adds resilient telemetry and queue visibility, followed by governed predictive capabilities and finally cross-estate optimisation, personalisation and carefully bounded conversational assistance.

The architecture is intended to be judged by measurable fitness functions rather than by its technology inventory. Representative controls include purchase and entry availability, entitlement integrity, queue estimate accuracy and freshness, ride availability, maintenance lead time, mandatory-care completion, alert acknowledgement, telemetry durability, event delivery, privacy contract tests and AI evidence/drift checks.

Before implementation, the estate should validate baselines and targets with visitors, duty managers, ride engineers, keepers, veterinary specialists, privacy stakeholders and security teams. The numerical targets in the capability documents are explicitly proposed starting points, not facts supplied by the brief.

## Submission checklist

- [x] Executive narrative connecting the estate’s problems to business outcomes.
- [x] Four capability-level architecture submissions with C4, deployment and dynamic views.
- [x] AI use cases for both operators and visitors, with explicit guardrails and human accountability.
- [x] Patchy Wi-Fi, MQTT devices, edge processing, cloud synchronisation and offline behaviour addressed.
- [x] Validation, fallback, observability, fitness functions and provider/model change addressed.
- [x] Requirement, outcome, ADR and fitness-function traceability included in each capability.
- [x] Phased delivery sequence and operational measures included in each capability.
- [ ] Standalone ADR set expanded from the embedded capability ADRs, with alternatives and enforcement detail.
- [ ] Final executive narrative, presentation/video and costed roadmap assembled for the submission package.

## Team members

- Pete Halloran
- Matt Gould
- Alex Jacobs
- Edward Manning
- Helen Keeling
- Chris Lewis
