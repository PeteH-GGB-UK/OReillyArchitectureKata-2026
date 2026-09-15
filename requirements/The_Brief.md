# O'Reilly Architectural Katas 2026: AI-Assisted Software Architecture - Von Digitalis Estates

This document is the briefing pack for the **Architectural Katas 2026: AI-Assisted Software Architecture** competition. Teams are asked to design a modern architecture for a fictional business, the **Von Digitalis Estates**, with a strong emphasis on how AI can solve business and operational problems. 【1-3ec6e3】

---

## The Scenario

The fictional **Von Digitalis Estates** is a large historic estate that needs to become profitable after its traditional business failed. The new owner, the 72nd Countess Von Digitalis, wants to modernise operations and monetise the estate through digital solutions. 【1-3ec6e3】

The estate contains:

- A historic amusement park with around **40 rides**. 【1-3ec6e3】
- An exotic animal collection with **more than 200 animals** across **55 enclosures**. 【1-3ec6e3】

---

## Business Context

The estate currently receives approximately **5,000 visitors per day** and hopes to increase that to **15,000 visitors per day within three years**. Failure to grow revenue may force the family to sell assets. 【1-3ec6e3】

Key challenges include:

1. Little understanding of which attractions are most popular.
2. High costs associated with animal care.
3. Difficulty increasing repeat visitors.
4. Need to improve overall profitability. 【1-3ec6e3】

---

## Required Capabilities

### Visitor and Ticketing Services

- Online ticket purchasing.
- Family pass management.
- General visitor management capabilities. 【1-3ec6e3】

### Visitor Analytics

- Understanding visitor movement and attraction popularity.
- Data to support staffing and investment decisions. 【1-3ec6e3】

### Animal Monitoring

- Tracking animal health.
- Monitoring feeding habits and consumption.
- Monitoring population levels of specific species (including the fictional "jumping piranha" collection). 【1-3ec6e3】

### Revenue Growth

- Identifying ways to attract new visitors.
- Encouraging repeat visits.
- Increasing profitability. 【1-3ec6e3】

---

## Technical Constraints

The solution must account for:

- Patchy Wi-Fi coverage across the estate.
- Cloud services being available.
- A need to move data from the estate to the cloud.
- Availability of MQTT-capable IoT devices deployed throughout the park. 【1-3ec6e3】

---

## AI Focus

A major requirement is demonstrating how AI can help both:

- The estate operators.
- The estate's customers and visitors. 【1-3ec6e3】

The judges specifically want teams to focus on innovative and practical AI usage rather than simply adding AI features for their own sake. 【1-3ec6e3】

---

## Deliverables

Teams are expected to provide:

- A short narrative describing how AI solves the estate's problems.
- Architecture diagrams for AI-related solutions.
- Architecture Decision Records (ADRs) documenting AI decisions and trade-offs.
- Optional implementation details.
- Semi-finalists must provide a five-minute video presentation. 【1-3ec6e3】

The document strongly emphasises:

- Clear communication.
- Simple, understandable diagrams.
- Well-documented architectural decisions. 【1-3ec6e3】

---

## What the Judges Are Looking For

The judging criteria focus on:

- Innovative use of AI.
- Suitability of the solution to the problem and constraints.
- Appropriate architectural detail.
- Handling uncertainty around rapidly changing AI technologies.
- Alignment of AI components with broader architecture.
- Validation and verification of AI outputs. 【1-3ec6e3】

A key design question raised is:

> How do you avoid being locked into a single AI provider, and how do you monitor whether AI systems remain effective and trustworthy in production? 【1-3ec6e3】

---

## Key Takeaway

This is fundamentally an **AI-centric architecture challenge**. The strongest solution will likely combine:

- Cloud-native architecture.
- IoT sensors and edge computing.
- Visitor analytics and behavioural insights.
- AI-driven animal health monitoring.
- Personalised visitor experiences.
- Marketing and retention systems.
- Strong governance, observability, and AI validation mechanisms. 【1-3ec6e3】

For a team with strong Azure and AI experience, a compelling approach would likely combine **IoT + Digital Twins + Agentic AI + predictive analytics + personalised visitor experiences**, while explicitly addressing connectivity limitations, model governance, portability, and AI observability. 【1-3ec6e3】