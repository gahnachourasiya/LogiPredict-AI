# LogiPredict AI — Predictive Logistics & Forward Supply Chain

[![SIH Problem Statement](https://img.shields.io/badge/SIH%202024%20PS-26251-red.svg)](https://sih.gov.in)
[![Organization](https://img.shields.io/badge/Organization-Ministry%20of%20Defence-blue.svg)](#1-official-problem-statement-context)
[![Department](https://img.shields.io/badge/Department-Defence%20Services%20Staff%20College-navy.svg)](#1-official-problem-statement-context)
[![Status](https://img.shields.io/badge/Status-Documentation%20Foundation%20Complete-green.svg)](#5-current-project-status)

> **Product Name:** LogiPredict AI  
> **Official Problem Statement ID:** 26251  
> **Official Title:** Indian Army - Predictive Logistics & Forward Supply Chain.  
> **Ministry / Organization:** Ministry of Defence (MoD)  
> **Department:** Defence Services Staff College  
> **Category:** Software | **Theme:** Transportation & Logistics  
> **Target Event:** Smart India Hackathon (SIH)  
> **Repository Directory:** `sih251/` | **Documentation Hub:** `brain/`  

---

## 1. Official Problem Statement Context

### 1.1 The Operational Challenge
In forward and operationally challenging areas, maintaining assured, timely logistics support to geographically dispersed formations is critical. Currently, demand forecasting, inventory levels, transportation capacity, terrain/weather conditions, and consumption patterns are maintained across disparate information streams. This fragmentation makes it difficult to anticipate supply requirements and optimize the movement of critical materials.

### 1.2 Technology Opportunities Identified in the Official PS
- **AI/ML-based demand forecasting**
- **GIS-enabled logistics planning**
- **IoT-based inventory tracking**
- **An integrated predictive logistics management system**

---

## 2. Proposed Solution: LogiPredict AI

**LogiPredict AI** is a lightweight, explainable, decision-support prototype engineered to unify multi-echelon forward supply data, forecast consumption burn rates, calculate impending stockout dates, and generate automated, priority-weighted replenishment recommendations.

### 2.1 Core Capabilities (Confirmed MVP Scope)
1. **Multi-Echelon Forward Inventory Ledger:** Real-time visibility of current stock across synthetic forward posts, staging dumps, and base depots across critical supply classes (`Class I Rations`, `Class III Fuel/POL`, `Medical`, `Spares`).
2. **Predictive Demand Forecasting:** Time-series statistical projections (7, 14, and 30-day horizons) based on daily consumption patterns.
3. **Run-Out Date & Deficit Anticipation:** Automated calculation of days-of-supply remaining, triggering instant warnings when buffers are breached.
4. **Actionable Replenishment Recommendations:** System-suggested depot-to-post dispatches factoring in surplus availability, priority tiers, and transit lead times.
5. **What-If Scenario Simulation Sandbox:** Interactive stress testing allowing logistics planners to simulate consumption surges (e.g., +30%) or transit weather delays to evaluate supply resilience.
6. **Immutable Audit Logging:** Complete traceability recording every planner approval and dispatch modification.

### 2.2 Proposed Extensions (Phase 6 / Feasibility Dependent)
- **GIS Route Visualizer:** Abstract spatial representation of synthetic nodes and supply corridors.
- **Weather / Terrain Delay Modifiers:** Parametric toggles adjusting base transit lead times.
- **Mock IoT Telemetry Contract:** API schema definition for cargo sensor telemetry.

---

## 3. Strict Synthetic Data & Operational Sensitivity Policy

> [!CAUTION]
> **Academic Hackathon Scope Disclaimer:**  
> LogiPredict AI is an academic prototype for the Smart India Hackathon. It does **NOT** contain, store, or simulate real military locations, genuine unit designations, classified border routes, or actual operational supply numbers.  
> **All data used in development, testing, and evaluation is 100% synthetic and anonymized.** The prototype is an exploratory proof-of-concept and is not certified or authorized for operational military use.

---

## 4. Proposed Technology Stack

| Layer | Proposed Technology | Evaluation Rationale |
| :--- | :--- | :--- |
| **Frontend UI** | React + Vite | Fast hot reloading, modular component ergonomics, zero UI bloat |
| **Styling** | Vanilla CSS Tokens (`tokens.css`) | Maximum visual freedom, command-grade dark interface, zero framework bugs |
| **Backend API** | Node.js (Express) | Asynchronous non-blocking I/O, native JSON handling, standard REST routing |
| **Database** | Embedded SQLite (`better-sqlite3` / `sqlite3`) | 100% reliable local execution, zero-config, immune to hackathon Wi-Fi outages |
| **Data Provenance** | Synthetic Seed Generator (`npm run seed`) | One-click reproducible scenario for seamless jury demonstration |

---

## 5. Repository Structure

```
sih251/
├── brain/                                        # Complete project documentation & specifications
│   ├── Product Requirement Documentation(PRD).md # Official MoD challenge & feature mapping
│   ├── Design.md                                 # Command-grade UI tokens, layouts, and data tags
│   ├── Architecture.md                           # Analytical pipelines & decoupled system modules
│   ├── memory.md                                 # Project context, session memory, and checklists
│   ├── rules.md                                  # Coding standards & strict synthetic data policy
│   ├── security.md                               # RBAC, input sanitization, and academic disclaimer
│   ├── Changes.md                                # Chronological development changelog
│   ├── Decisions.md                              # Architecture Decision Records (ADRs)
│   ├── Implementation_Plan.md                    # 6-phase demonstrable MVP roadmap
│   ├── Database.md                               # Multi-echelon relational schema & seed data spec
│   ├── API_Documentation.md                      # Proposed REST API routes and response envelopes
│   ├── Testing.md                                # QA test suites and 4-minute demo walkthrough
│   ├── Deployment.md                             # Local setup and single-port static bundle guide
│   └── Requirements_Traceability.md              # Official context vs proposed MVP matrix
├── client/                                       # [Planned for Phase 2] Frontend web application
├── server/                                       # [Planned for Phase 2] Backend REST service
└── README.md                                     # Project root documentation
```

---

## 6. Current Project Status

- **Phase 1: Problem Definition & Documentation Foundation:** **COMPLETED**
  - Fully synchronized with official SIH Problem Statement 26251.
  - All 14 specification files created and cross-verified in `brain/`.
- **Phase 2: Project Scaffolding & Synthetic Seeding:** **GATED / ON HOLD**
  - Application code creation and dependency installations are strictly paused pending user review and approval of the documentation foundation.

---

## 7. Execution Guide (Post-Approval)

Once Phase 2 is approved:
```bash
# Backend setup & synthetic data seed
cd server
npm install
npm run db:seed
npm run dev

# Frontend setup (in a separate terminal)
cd client
npm install
npm run dev
```
- Open Dashboard: `http://localhost:5173`
- API Health Check: `http://localhost:5000/api`
