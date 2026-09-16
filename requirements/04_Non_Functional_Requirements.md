# Non-Functional Requirements

## Target Status and Measurement Rules

The brief's growth ambition is approximately 5,000 to 15,000 daily visitors; it does not specify concurrent users, sensor rates or service levels.

Define a versioned workload profile for 15,000 daily visitors, including peak arrival rate, concurrent sessions, transaction mix, device count, event rate and payload sizes. Daily attendance alone is not a load-test specification.

Define operating hours, service boundaries, observation windows and exclusions before measuring availability or response times. Report external dependency delays separately without hiding their effect on users.

Test offline, reconnecting and degraded conditions as well as normal operation. Local admission decisions, buffered staff records and central services are distinct measurement boundaries.

Open thresholds are explicitly identified below. They must be agreed before the relevant capability is accepted; they are not assumed to have passed. 

## 1. Performance and Capacity

| ID / Requirement | Operating Condition | Threshold / Acceptance Criteria | Verification Method |
|---|---|---|---|
| NFR-01 — Scalability | Forecast year-3 peak workload, including visitor transactions and telemetry. | Sustain the approved peak profile for two hours and a 2× burst for 15 minutes while meeting NFR-02, with no acknowledged data loss. Device and transaction rates remain a sizing decision. | Load and soak tests using a documented workload model; inspect saturation, backlog and data-loss metrics. |
| NFR-02 — Performance | Approved peak load; online services healthy and supported devices connected. | p95 local admission decision ≤2 seconds; p95 ordinary read/write API response ≤2 seconds; p95 purchase confirmation ≤5 seconds after payment authorisation is received. | Instrument end-to-end journeys and run load tests; report payment-provider latency separately. |

## 2. Availability, Resilience and Recovery

| ID / Requirement | Operating Condition | Threshold / Acceptance Criteria | Verification Method |
|---|---|---|---|
| NFR-03 — Software-service availability | Admission software during opening hours; central ride and animal-care software workflows during their agreed service hours. Physical ride availability is measured separately by FF-RO-01 in the [Ride Operations capability](../architecture/Ride_Operations_C4_Capability.md). | Each service ≥99.9% availability per calendar month within its service window, excluding approved planned interruptions. Define successful user transactions separately for each service. | Synthetic user journeys and incident records; calculate service-specific availability and report local fallback separately. |
| NFR-04 — Reliability | Retries, duplicate delivery, consumer restarts and temporary dependency failures. | Zero duplicate business effects and zero loss of acknowledged records within the tested failure model; recoverable failures are retried or placed in a visible exception queue. | Inject duplicate events and failures; reconcile source records, acknowledgements and resulting business actions. |
| NFR-05 — Offline continuity | Estate-to-cloud link unavailable while local power and equipment remain healthy. | Buffer telemetry and staff observations for 24 hours at the approved peak rate; support admission for a four-hour window using eligible signed entitlements. Expired or unverifiable access follows an explicit staff procedure. | Disconnect backhaul for the specified windows; test expiry, revocation exposure, duplicate use, storage exhaustion and reconnection. Admission risk policy requires approval before release. |
| NFR-06 — Recoverability | Loss of a central application instance or primary data store. | Central admission, ride and animal-care records: recovery time ≤1 hour and recovery-point data loss ≤5 minutes; analytical reporting: ≤24 hours for both. External payment reconciliation must resolve transaction discrepancies. | Restore backups into an isolated environment and rehearse failover quarterly; measure actual recovery time, recovered data and reconciliation results. |

## 3. Safety and Operational Assurance

| ID / Requirement | Operating Condition | Threshold / Acceptance Criteria | Verification Method |
|---|---|---|---|
| NFR-07 — Safety independence | Cloud, network or AI unavailable, delayed or producing invalid output. | No dependency of certified ride controls or essential local welfare alarms on cloud/AI; no unauthorised return to service. Raise ≥99.9% of tested local welfare alerts within 30 seconds of a confirmed threshold breach, where the care plan permits that interval. | Review control boundaries with qualified staff; inject failures in a safe test environment and verify alarms and approval gates. More urgent hazards require separate assessment and faster limits. |

## 4. Security, Privacy and Compliance

| ID / Requirement | Operating Condition | Threshold / Acceptance Criteria | Verification Method |
|---|---|---|---|
| NFR-08 — Access control | Every protected user, device and service request, including privileged operations. | All protected interfaces authenticate identities and enforce least-privilege permissions; all tested unauthorised actions are denied. Privileged human access requires MFA. | Role/permission tests, device-identity tests and access reviews; include revoked accounts and credentials. |
| NFR-09 — Data protection | Sensitive data transmitted, stored, backed up or reaching its retention limit. | Encryption on all sensitive-data paths and stores; no secrets in source code or logs. All data classes have approved retention rules and auditable deletion processing. Exact retention periods remain to be agreed. | Configuration review, secret scanning and sampled retention/deletion tests, including backup lifecycle handling. |
| NFR-10 — Privacy and consent | Personal data collection and consent-based visitor communications. | Every collection purpose is documented; no marketing dispatch proceeds without the required current permission. Consent withdrawal reaches dispatch controls within five minutes. | Trace collection purposes; test withdrawal against queued campaigns and inspect recipient eligibility records. |
| NFR-11 — Auditability | Admission decisions, maintenance approvals, animal-care amendments and privileged actions. | Every specified action records actor, timestamp, object and outcome in a tamper-evident trail; offline actions retain original and synchronisation times. | Exercise each action type, inspect audit completeness and test unauthorised log alteration. |
| NFR-12 — Compliance | Before release and after material changes to operations or data use. | Every identified applicable obligation has an owner, implementation evidence and review status; no unresolved mandatory release blocker. Applicability must be assessed for the estate's actual jurisdiction. | Maintain an obligations register and obtain relevant specialist reviews; record release decisions and outstanding actions. |

## 5. Data Quality and Integrity

| ID / Requirement | Operating Condition | Threshold / Acceptance Criteria | Verification Method |
|---|---|---|---|
| NFR-13 — Data quality and freshness | Operational data published internally or to visitors. | Every status or estimate includes observation time and validity/quality metadata. Withdraw live queue estimates after five minutes without valid observations; show ride status as unconfirmed after two minutes. Other limits require domain approval. | Inject missing, invalid and delayed observations; verify API and user-interface behaviour at each expiry boundary. |
| NFR-14 — Consistency and reconciliation | Offline updates, conflicting edits, duplicated events and out-of-order delivery. | Resolve updates under documented domain rules; silently overwrite no conflicting safety, care or entitlement record. After a 24-hour outage, clear the backlog within two hours at provisioned capacity while serving live traffic, excluding quarantined items awaiting review. | Replay mixed live/backlog traffic with conflicts; verify domain invariants, exception visibility and final records against source evidence. |
| NFR-15 — Data provenance | Observations, estimates and corrections used in operational decisions. | Every such record retains source identity, observation and ingestion times, transformation/version reference and correction history; estimates are distinguishable from verified observations. | Trace sampled dashboard values and decisions back to source records; test corrections and reprocessing. |

## 6. Operability and Cost

| ID / Requirement | Operating Condition | Threshold / Acceptance Criteria | Verification Method |
|---|---|---|---|
| NFR-16 — Observability | Critical service failure, processing backlog or gateway disconnection. | Detect and route tested critical faults within five minutes; every critical service has health, latency, error and backlog monitoring plus a linked response procedure. Immediate local welfare alarms follow NFR-07. | Synthetic incidents and alert-routing exercises; inspect diagnostic coverage and runbooks. |
| NFR-17 — Deployability | Routine application release or failed deployment. | Roll back a failed release within ten minutes; preserve acknowledged records and required local continuity. Database changes must support the planned rollback path. | Staged deployment with deliberate failure, rollback and record reconciliation. |
| NFR-18 — Cost control | Normal operation, usage spikes and provider price changes. | Attribute ≥95% of measured technology spend to a capability or shared platform; alert at 80% of approved budget and constrain discretionary AI at its approved ceiling. Absolute budgets and provider metering delays remain to be agreed. | Reconcile billing with internal usage; simulate budget exhaustion and price changes without disabling essential workflows. |
| NFR-19 — Device and edge manageability | Gateway/sensor onboarding, update, failed update or replacement. | Inventory every managed device and its owner, configuration and software version. Authenticate updates where supported; failed gateway updates recover to a known-good version within 15 minutes. Document safe replacement procedures for devices without remote-update support. | Canary update, interrupted-update and replacement drills; verify identity rotation and buffered-data handling. |
| NFR-20 — Physical operating suitability | Outdoor locations, enclosure conditions and loss of mains power. | Select equipment against a surveyed environmental and power profile, with no unsupported location deployed. Provision critical gateways/local alert equipment for at least one hour of backup power as an initial planning target. | Site survey, equipment-specification review and power-loss endurance tests; confirm per-location environmental limits before procurement. |

## 7. Maintainability and Integration

| ID / Requirement | Operating Condition | Threshold / Acceptance Criteria | Verification Method |
|---|---|---|---|
| NFR-21 — Maintainability | Representative changes to domain rules, implementation or integrations. | Demonstrate that an internal domain change can be released without changing unrelated domains when published contracts remain compatible; maintain an accountable owner for every component. | Rehearse a representative change and review dependency impact, deployment requirements and ownership. |
| NFR-22 — Interoperability | Purchased products, estate services and devices exchanging information. | Every production interface has a versioned contract, owner, authentication model and error/retry semantics; all supported consumer contracts pass before release. | Contract tests and integration tests covering schema evolution, malformed messages and dependency failures. |
| NFR-23 — Testability | Release acceptance and material architecture/model changes. | Every critical continuity, recovery, approval and AI-fallback scenario has a repeatable test, approved expected outcome and retained result; no untested critical scenario is accepted. | Execute the scenario suite in a representative environment, supplemented by controlled field drills; record environment limitations. |

## 8. AI Quality and Governance

| ID / Requirement | Operating Condition | Threshold / Acceptance Criteria | Verification Method |
|---|---|---|---|
| NFR-24 — Demonstrable value | Promotion of an AI use case from shadow evaluation into operational use. | Meet pre-agreed use-case accuracy, error-cost, latency and value thresholds against a non-AI baseline. Numerical model thresholds remain open until labelled data and business consequences are assessed; no promotion before approval. | Held-out evaluation and shadow trial against the baseline; report false positives, false negatives, costs and relevant operating segments. |
| NFR-25 — Uncertainty handling | Sparse, unfamiliar, conflicting or low-quality model inputs. | Every estimate exposes a validated uncertainty indicator or clear limitation; all tested insufficient-evidence cases trigger the defined abstention/fallback policy. Do not treat an LLM's self-reported confidence as calibrated probability. | Challenge sets with missing data and unfamiliar conditions; assess calibration where meaningful and verify abstention behaviour. |
| NFR-26 — Decision authority | AI recommendations or attempted tool actions. | Engineer approval for ride return to service, qualified approval for care changes and verified population updates, and duty-manager approval for closures/emergency instructions. Only explicitly permitted low-risk actions, such as ranking approved visitor content, may run automatically. | Maintain an action-authority matrix; test each approval gate and all prohibited action paths, including spoofed approvals. |
| NFR-27 — Grounding and traceability | Generated engineering or animal-care guidance. | Every substantive procedural recommendation cites an accessible approved source; unsupported requests produce an explicit limitation. Retain source versions and model/prompt versions for investigation. | Domain-reviewed answer tests, citation checks and provenance sampling; measure factual support, not citation presence alone. |
| NFR-28 — Model monitoring | Production inference, evaluation refresh or model update. | Log model version and operational metrics for every inference; check drift/quality on an agreed cadence. Route detected breaches within five minutes and disable unsafe models within ten minutes of confirmed breach; safety-critical actions remain independently gated. | Inject threshold breaches and rehearse disablement; use labelled follow-up outcomes for errors not detectable immediately. Per-model quality thresholds remain to be approved. |
| NFR-29 — AI resilience | Model timeout, provider outage or budget exhaustion. | Interactive AI falls back within five seconds; essential non-AI workflows continue. Batch predictions expire under their defined freshness policy rather than appearing current indefinitely. | Block provider access, inject latency and exhaust test budgets; verify fallback outputs and prediction expiry. |
| NFR-30 — Provider replaceability | Provider withdrawal, material price change or replacement-model evaluation. | Every production AI capability has a tested non-AI fallback and documented replacement route; rehearse at least annually and after material provider changes. Replacements must pass NFR-24 before activation. | Simulate shutdown and price change; test adapters/export paths and rerun evaluations. Record actual migration effort rather than assuming models are interchangeable. |
| NFR-31 — AI security | Untrusted prompts, retrieved content and model-initiated tool calls. | No unauthorised tool execution or restricted-data disclosure in the approved adversarial test suite; tool permissions are enforced independently of model output. | Prompt-injection, retrieval-access and tool-abuse tests; review failures before promotion and repeat after material changes. |

## 9. Usability and Accessibility

| ID / Requirement | Operating Condition | Threshold / Acceptance Criteria | Verification Method |
|---|---|---|---|
| NFR-32 — Visitor usability | First-time users purchasing a ticket or finding an available attraction on supported devices. | ≥90% complete each representative task unaided; median ticket-purchase time ≤3 minutes, excluding external payment authentication. | Moderated usability testing with representative visitors; report sample size, task failures and timings. |
| NFR-33 — Staff usability | Field staff recording defects or care observations, online and offline. | ≥95% complete representative tasks without assistance; routine observations recorded within 60 seconds; every pending or failed synchronisation is visible. | Field trials on supported devices under realistic lighting, connectivity and working conditions. |
| NFR-34 — Accessibility | Critical visitor and staff journeys using agreed assistive technologies and interaction modes. | No unresolved critical accessibility barrier in the agreed test matrix; all critical journeys meet the selected accessibility standard and level, to be confirmed before design acceptance. | Automated checks plus manual keyboard, screen-reader and representative user testing. |
| NFR-35 — Localisation | Every supported language, locale and fallback path. | All critical-journey text and date, time, currency and number formats are localised; no missing translation blocks task completion. Supported languages remain a product decision. | Locale test matrix, translation review and missing-translation/fallback tests. |
