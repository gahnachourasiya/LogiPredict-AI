# Product Requirement Documentation (PRD) — LogiPredict AI

> **Product Name:** LogiPredict AI  
> **Official Problem Statement ID:** 26251  
> **Official Problem Title:** Indian Army - Predictive Logistics & Forward Supply Chain.  
> **Organization:** Ministry of Defence (MoD)  
> **Department:** Defence Services Staff College  
> **Category:** Software  
> **Theme:** Transportation & Logistics  
> **Target Event:** Smart India Hackathon (SIH)  
> **Document Status:** Baseline / Refined with Official Problem Statement  
> **Last Updated:** 2026-10-14  

---

## 1. Problem Statement & Background

### 1.1 Official Problem Statement (Source of Truth)
- **Problem Statement ID:** 26251
- **Title:** Indian Army - Predictive Logistics & Forward Supply Chain.
- **Organization:** Ministry of Defence (MoD)
- **Department:** Defence Services Staff College
- **Category:** Software
- **Theme:** Transportation & Logistics

### 1.2 Official Problem Description
> *"The problem statement identifies difficulty in maintaining assured and timely logistics support to forward formations across geographically dispersed and operationally challenging areas.*  
> *Demand forecasting, inventory levels, transportation capacity, terrain/weather conditions, and consumption patterns are maintained across multiple information streams. This makes it difficult to anticipate requirements and optimise the movement of critical supplies."*

### 1.3 Technology Opportunities Identified in the Official PS
The official problem statement identifies four key technological opportunities:
1. **AI/ML-based demand forecasting**
2. **GIS-enabled logistics planning**
3. **IoT-based inventory tracking**
4. **An integrated predictive logistics management system**

> [!IMPORTANT]
> **Source Boundary & Discipline:**  
> The official problem statement does not provide a dataset link, video reference, contact information, detailed API requirements, prescribed technology stack, or mandatory architectural specification. These details must not be invented or assumed as government directives. All advanced technologies (such as GIS routing and live IoT tracking) are treated as technological opportunities and evaluated for prototype feasibility rather than assumed as mandatory day-one deliverables.

---

## 2. Proposed Solution: LogiPredict AI

To address the challenges identified in SIH PS 26251 within a student hackathon scope, the team proposes **LogiPredict AI** — an integrated, predictive supply chain decision-support system designed to unify fragmented logistics streams, anticipate forward supply requirements, and provide actionable replenishment insights.

### 2.1 Solution Mapping to Official Problem Dimensions

| Official Problem Dimension | Challenge Identified in PS | LogiPredict AI Proposed Capability | Prototype Scope Status |
| :--- | :--- | :--- | :--- |
| **Demand Forecasting** | Fragmented historical consumption makes anticipating needs difficult | Machine learning & statistical time-series forecasting to project forward formation demand | **Core MVP** |
| **Inventory Levels** | Multi-stream inventory tracking leads to stock opacity and unexpected stockouts | Centralized stock ledger tracking buffer thresholds, reorder points, and projected run-out dates | **Core MVP** |
| **Transportation & Supply Planning** | Hard to optimise movement of critical supplies to forward formations | Replenishment recommendation engine calculating dispatch quantities and priority tiers | **Core MVP** |
| **Scenario Simulation** | Inability to evaluate disruptions, surges, or delayed supply lines | What-if simulation sandbox to test demand spikes, transit disruptions, and buffer adjustments | **Core MVP** |
| **Terrain / Weather Conditions** | Dispersed, operationally challenging conditions impact transit times | Parameterized transit delay factors and seasonal consumption modifiers | **Proposed MVP Model** (Data-dependent) |
| **GIS-Enabled Planning** | Spatial visualization of geographic constraints | Geospatial node mapping and transit corridor visualization | **Proposed Extension** (Feasibility dependent) |
| **IoT-Based Tracking** | Physical tracking of cargo containers or warehouse pallets | Mock telemetry ingestion contract and sensor state interface | **Future / Potential Integration** |

---

## 3. Synthetic Data & Operational Sensitivity Policy

> [!CAUTION]
> **Operational Security & Data Integrity Notice:**  
> LogiPredict AI is an academic hackathon prototype. It does not use, store, or simulate real military operational plans, troop deployments, unit designations, classified forward locations, or actual supply quantities.  
> **All data utilized during development and demonstration is 100% synthetic and anonymized.** Synthetic nodes use abstract nomenclature (e.g., `Base Depot Alpha`, `Transit Hub Delta`, `Forward Post Foxtrot`), and commodities are generalized into standard logistical categories (e.g., `Ration Packs (Class I)`, `Fuel / POL (Class III)`, `Medical Packs`, `General Spares`).

---

## 4. Target Users & User Personas

| Persona | Operational Context | Primary Goals | Key Pain Points |
| :--- | :--- | :--- | :--- |
| **Forward Logistics Officer** (`Base / Post Level`) | Monitors local supply stocks at forward holding points | Real-time visibility of local stock, automated run-out date warnings, fast re-order requests | Fragmented manual ledgers, unexpected stock exhaustion, poor communication with central depots |
| **Formation Logistics Planner** (`Divisional / Depot HQ`) | Coordinates multi-post supply dispatches and convoy planning | Anticipate forward requirements 7-30 days ahead; prioritize dispatches based on criticality | Siloed information streams, reactive dispatching, difficult manual multi-factor planning |
| **Command Analyst / Evaluator** (`Staff College / Jury`) | Evaluates system integrity, forecast explainability, and decisions | Validate forecast accuracy, inspect scenario simulation outcomes, audit system recommendations | Opaque "black box" models, unverified data pipelines, complex non-standard deployments |

---

## 5. Scope Definition

### 5.1 Confirmed Minimum Viable Product (MVP) Scope
1. **Unified Inventory Ledger:** Real-time visibility of current stock levels across synthetic forward posts and base depots across critical supply categories.
2. **Consumption Tracking & Data Ingestion:** Logging and visualizing historical consumption rates with synthetic seasonality.
3. **Predictive Demand Forecasting:** Time-series projection (e.g., moving averages, exponential smoothing, or regression) predicting forward demand over 7, 14, and 30-day horizons.
4. **Stockout Risk & Run-Out Date Calculation:** Automated calculation of days-of-supply remaining based on current inventory and forecasted burn rates.
5. **Replenishment Recommendation Engine:** Rule-based and priority-weighted generation of transfer recommendations from base depots to forward posts.
6. **What-If Scenario Simulation:** Interactive sandbox allowing users to simulate consumption surges (e.g., +25% consumption) or supply delivery delays (e.g., +4 days transit delay).
7. **Explainability & Audit Trails:** Clear breakdown of why a replenishment order was recommended, including historical audit logging of administrative approvals.

### 5.2 Proposed Extensions (Subject to Data & Team Feasibility Confirmation)
- **GIS / Spatial Planning View:** Interactive map representing abstract synthetic nodes, supply routes, and transit statuses using Leaflet or GeoJSON.
- **Weather / Terrain Impact Factor:** Simple parameter modifier (e.g., seasonal pass closure or heavy precipitation) that multiplies transit lead times.

### 5.3 Potential Future Integrations (Out of Scope for Hackathon MVP)
- Live IoT hardware sensor telemetry (RFID / GPS container tracking).
- Integration with classified defence enterprise networks or production military ERPs.
- Autonomous fleet routing algorithms requiring real-time military grade GIS rasters.

---

## 6. Functional Requirements (FR)

| Req ID | Category | Description | Priority |
| :--- | :--- | :--- | :--- |
| **FR-01** | Inventory Monitoring | Display current inventory quantities, safety stock levels, and replenishment status by node and item category | High (MVP) |
| **FR-02** | Demand Forecasting | Generate predictive consumption forecasts for forward nodes over selectable horizons (7d, 14d, 30d) | High (MVP) |
| **FR-03** | Run-Out Estimation | Calculate projected run-out dates based on current inventory and forecasted daily burn rate | High (MVP) |
| **FR-04** | Shortage Alerting | Trigger visual warning indicators when projected stock breaches designated safety buffer thresholds | High (MVP) |
| **FR-05** | Replenishment Engine | Generate suggested dispatch transfer orders (source node, destination node, quantity, urgency priority) | High (MVP) |
| **FR-06** | Scenario Simulator | Allow users to adjust consumption multipliers and transit delays to compare baseline vs. stressed inventory | High (MVP) |
| **FR-07** | Recommendation Actioning| Enable logistics officers to approve, modify, or reject recommended dispatches with audit logs | High (MVP) |
| **FR-08** | Synthetic Data Seeder | Provide one-click data generation for reproducible, realistic multi-echelon demo scenarios | High (MVP) |
| **FR-09** | Geospatial Route View | Visual GIS representation of nodes and supply corridors with transit latency indicators | Medium (Proposed) |
| **FR-10** | Weather / Delay Factors | Ingest weather/terrain delay coefficients into the transit lead-time calculation | Low (Proposed) |

---

## 7. Non-Functional Requirements (NFR)

- **NFR-01: Explainability:** Every automated recommendation must display its underlying calculation logic (e.g., `Current Stock (120) - Forecasted Burn (15/day x 10 days) = -30 Deficit`).
- **NFR-02: Self-Contained Local Execution:** 100% operational in an isolated local environment without external cloud API dependencies.
- **NFR-03: Performance:** Forecast recalculation and scenario simulation response times under 500ms on standard student laptop hardware.
- **NFR-04: Reliability:** Zero runtime crashes during rapid filter switching and scenario parameters tuning.
- **NFR-05: Security & Hygiene:** Parameterized database queries, strict client-side escaping, and zero hardcoded secrets.

---

## 8. Success Metrics for SIH Evaluation

1. **Jury Demonstration Pacing:** Ability to demonstrate complete forward supply anticipation, stockout alert, and simulated disruption response in under 4 minutes.
2. **Clarity of Thought:** Clear distinction between synthetic prototype demonstration and real-world military logistics complexities.
3. **Actionability:** Evaluators can clearly see how predictive analytics converts disparate data into concrete logistics actions rather than just passive charts.
