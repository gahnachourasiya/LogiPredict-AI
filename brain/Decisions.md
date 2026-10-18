# Architecture Decision Records (ADR) — LogiPredict AI

> **Product Name:** LogiPredict AI  
> **Official Problem Statement:** SIH PS 26251 — *Indian Army - Predictive Logistics & Forward Supply Chain*  
> **Status:** Active Decision Log  

---

## ADR-001: Documentation-First & Zero Premature Implementation

- **Status:** **Accepted**
- **Date:** 2026-10-14
- **Context:** Student hackathon projects commonly incur technical debt, misaligned requirements, and broken demos when coding commences before database schemas, API contracts, and user journeys are finalized.
- **Alternatives Considered:**
  1. *Immediate Full-Stack Coding:* Rapidly code a generic supply chain app and adapt later.
  2. *Documentation-First Foundation:* Fully define PRD, design tokens, data models, APIs, and test plans before writing any application code.
- **Rationale:** Documentation-first ensures zero wasted code, guaranteed alignment on the official problem statement, and instant readiness for jury questions.
- **Consequences:** Implementation begins only after explicit user approval of the documentation foundation.

---

## ADR-002: Official Problem Statement ID 26251 & Product Identity

- **Status:** **Accepted**
- **Date:** 2026-10-14
- **Context:** The workspace directory was initialized as `sih251`, but the official verified SIH Problem Statement ID is **`26251`**, titled *“Indian Army - Predictive Logistics & Forward Supply Chain”* under the Ministry of Defence (MoD) / Defence Services Staff College.
- **Alternatives Considered:**
  1. *Rename the filesystem workspace directory to `sih26251`:* Risks breaking local paths and active editor contexts.
  2. *Retain `sih251` directory while correcting all documentation, titles, metadata, and branding to official PS `26251` and product name `LogiPredict AI`:* Clean, non-destructive, and accurate.
- **Rationale:** Preserves Git and filesystem stability while establishing 100% fidelity to the official source of truth.
- **Consequences:** Root workspace folder remains `sih251`; all UI titles and documentation refer to SIH PS 26251 and LogiPredict AI.

---

## ADR-003: 100% Synthetic & Anonymized Data Policy

- **Status:** **Accepted**
- **Date:** 2026-10-14
- **Context:** The official problem statement involves military forward logistics. Sponsoring organizations do not provide real operational or classified military data to student hackathon teams.
- **Alternatives Considered:**
  1. *Scrape or guess real troop deployments and border coordinates:* Unethical, unverified, and a severe operational security hazard.
  2. *Use 100% synthetic, generalized multi-echelon data:* Model abstract nodes (`Base Depot Alpha`, `Forward Post Delta`) and standardized logistics classes (`Class I Rations`, `Class III Fuel/POL`).
- **Rationale:** Protects operational security, complies with competition ethics, and guarantees that evaluators focus on the algorithmic and workflow value of the software.
- **Consequences:** The UI will feature permanent `[SYNTHETIC DEMO MODE]` badges, and seed data will be generated algorithmically.

---

## ADR-004: Core MVP Scope vs. Proposed Extensions (GIS, IoT, Weather)

- **Status:** **Accepted**
- **Date:** 2026-10-14
- **Context:** The official problem statement mentions technology opportunities including AI demand forecasting, GIS planning, IoT tracking, and integrated logistics. Attempting to build all four simultaneously in an initial student prototype risks delivering a shallow or broken demo.
- **Alternatives Considered:**
  1. *Attempt all simultaneously:* Build partial GIS maps, fake IoT sensor scripts, and basic charts. (High risk of runtime failure).
  2. *Phased Delivery (MVP Core first, Extensions decoupled):* Prioritize the decision pipeline (Inventory -> Forecast -> Deficit Alert -> Replenishment -> Simulation), and treat GIS, weather modifiers, and IoT contracts as optional proposed extensions.
- **Rationale:** Ensures that the core value proposition (anticipating forward supply requirements and optimizing movement) is demonstrable and rock-solid before adding peripheral visual or hardware layers.
- **Consequences:** Core MVP is prioritized in Phases 2-5; GIS and IoT are scheduled for Phase 6 evaluation.

---

## ADR-005: Embedded Local Database (SQLite) vs. Cloud Database

- **Status:** **Accepted (Proposed Default)**
- **Date:** 2026-10-14
- **Context:** Hackathon demonstration venues frequently suffer from congested, unreliable Wi-Fi or institutional firewalls that block outbound database connections.
- **Alternatives Considered:**
  1. *Cloud Database (Supabase / MongoDB Atlas):* Risk of complete demo failure if network drops.
  2. *Embedded SQLite:* 100% deterministic local performance, file-based portability, ACID-compliant transactions, sub-millisecond query latency.
- **Rationale:** Eliminates network failure risks during judging. The prototype will boot and execute flawlessly in a completely air-gapped environment.
- **Consequences:** Relies on local file persistence; can be migrated to PostgreSQL post-hackathon if enterprise scaling is required.
