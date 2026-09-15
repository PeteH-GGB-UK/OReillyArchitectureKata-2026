Architecture Kata Submission Priorities

*How to give Von Digitalis Estates a strong semi-final submission*

**Recommendation. **Submit a concise, evidence-led architecture proposal: make the business outcomes, trade-offs, AI boundaries and delivery path immediately visible. The judges are looking for architectural thinking and communication, not the largest document set.

# What the judges are signalling

- Clear thought and clear communication: why a decision was made, not merely what was selected.

- Business-outcome focus and deliberate prioritisation.

- Strong ADRs with alternatives and consequences.

- AI that creates real value, can tolerate vendor or model change, and is validated and monitored.

- The appropriate level of detail: enough to establish credibility without AI-generated volume.

# Prioritised submission checklist

## 1. Executive narrative

**Why it matters: **It establishes the decision frame before a judge sees a technology choice.

- Two to three pages: business outcomes, constraints, assumptions and the architecture thesis.

- For the estate: profitable growth, safer operations, animal welfare, ride reliability and scale from 5,000 to 15,000 visitors per day.

- State the three to five decisions that most affect the plan and the trade-offs accepted.

## 2. Small, coherent diagram set

**Why it matters: **The diagrams must let business and technical judges navigate the solution in minutes.

- C4 context: visitors, operations staff, vets, maintenance crews, suppliers, payment services, estate devices and external data.

- Container/system diagram: ticketing and family passes; visitor and queue telemetry; rides; animal-care records; event/data platform; AI services.

- One or two critical journeys: ride anomaly to maintenance intervention, and animal-health alert to accountable human veterinary action.

## 3. Five to ten decision-grade ADRs

**Why it matters: **ADRs are the clearest evidence of reasoning and trade-offs.

- Each ADR: context, options, choice, consequences, rejected alternative, and how it will be enforced or revisited.

- Cover boundaries, event-driven versus synchronous flows, device ingestion, data ownership, safety, privacy, resilience and build-versus-buy.

- Make every major diagram element traceable to a requirement and ADR.

## 4. AI design and governance

**Why it matters: **AI must be useful, controllable and credible in a safety-sensitive physical estate.

- Specify value cases: queue and demand prediction, ride maintenance prediction, visitor recommendations, and animal-health anomaly detection.

- State the hard boundaries: generative AI is advisory only; it must not autonomously treat animals, override safety controls or make accountable operational decisions.

- Describe evaluation, human review, monitoring and drift detection, fallback behaviour, audit trails and model/provider replacement.

## 5. Requirement and outcome traceability

**Why it matters: **This prevents a technically attractive proposal from feeling disconnected from the brief.

- Use one compact matrix: requirement, capability, architecture element, ADR and measure of success.

- Include functional requirements, quality attributes, assumptions and explicit constraints.

## 6. Phased delivery roadmap

**Why it matters: **A credible sequence shows the proposal can create value before its most ambitious capabilities arrive.

- Phase 1: ticketing/family passes, basic operational telemetry, observability and data foundation.

- Phase 2: ride maintenance and animal-care monitoring, with human-led response workflows.

- Phase 3: demand management, personalisation and carefully governed conversational AI.

- Show dependencies, indicative cost, risk and expected benefit by phase.

## 7. Operational proof

**Why it matters: **Production readiness is demonstrated by measurable, owned controls rather than a long technology list.

- Set fitness functions: ticketing availability, queue-time reduction, maintenance alert lead time, animal-health alert response, repeat visits and AI quality.

- Cover device identity, privacy and retention, security, observability, incident response and testing.

## 8. Reviewer experience

**Why it matters: **A well-structured repository and presentation allow the quality of the thinking to be seen.

- Use a short README: problem, outcomes, diagrams, ADRs and roadmap.

- Keep a glossary and link diagrams directly to the decisions they illustrate.

- Tell one business story in the presentation rather than narrating every component.

# What the Q4 2025 finalists supplied

| **Finalist** | **Evidence supplied** | **Lesson to adopt** |
| --- | --- | --- |
| **Five Nines1st** | **End-to-end documentation; requirements and capability mapping; ADRs; high-level designs; risk and mitigation; phased plan; explicit AI, IoT, streaming and data-platform design.** | **Trace requirements to capabilities, ADRs and diagrams. Make the architecture an argument for business outcomes, not an inventory of cloud services.** |
| **Nimrods2nd** | **C4 context plus separate C2/C3 diagrams for reservation, operations and data intelligence; value-stream systems; ADRs; ML forecasting, mathematical optimisation and agentic workflows; roadmap with costs.** | **Use progressive diagrams and organise the solution by the value streams people recognise, such as visitor journeys, estate operations and data intelligence.** |
| **Kata-na3rd** | **C1/C2/C3 views; 16 ADRs; threat model; testing; fitness functions; cost analysis; phased delivery; complete MLOps pipeline and explicit limits on generative AI in financial or safety-critical areas.** | **Pair AI ambition with governance, measurable outcomes and a clear prohibition on unsafe autonomous decisions.** |

# The common winning pattern

| **Pattern** | **Why it matters** |
| --- | --- |
| **Business problem to architecture traceability** | **Shows prioritisation rather than solutioneering.** |
| **Progressive C4-style diagrams** | **Allows business and technical reviewers to enter at the right level.** |
| **ADRs with alternatives** | **Makes architectural judgement and trade-offs inspectable.** |
| **Operable AI lifecycle** | **Shows models can be evaluated, monitored, governed and changed.** |
| **Phased value with costs and metrics** | **Makes the architecture credible as an investment and delivery plan.** |
| **Security, reliability and governance** | **Demonstrates responsibility for a production physical-world system.** |

# Minimum viable semi-final package

- Executive narrative (2-3 pages).

- Context and container diagrams, plus two critical journey diagrams.

- Five to ten ADRs and a compact requirement-to-outcome matrix.

- AI governance and safety section, with evaluation and fallback design.

- Phased roadmap, risks, costs and measurable fitness functions.

- Concise repository README and a presentation built around business outcomes.

# Sources reviewed

- Architecture Kata Intro Judging Rubric Summary.docx (local rubric summary)

- Five Nines Q4 2025 finalist: https://github.com/Oleggio/five-nines-arch-katas

- Nimrods Q4 2025 finalist: https://github.com/jonmanahan/Architectural-Katas-Q4-2025-AI-Enabled-Architecture-Team-Nimrod

- Kata-na Q4 2025 finalist: https://github.com/TheKataLog/Kata-na
