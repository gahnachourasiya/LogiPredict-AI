# Requirements Traceability Matrix (RTM) — LogiPredict AI

> **Product Name:** LogiPredict AI  
> **Official Problem Statement:** SIH PS 26251 — *Indian Army - Predictive Logistics & Forward Supply Chain*  
> **Status:** Baseline Traceability  

This matrix links the official problem statement challenges, team-proposed functional specifications, target implementation modules, and planned verification test cases.

---

## 1. Traceability Matrix

| Requirement ID | Provenance & Source | Requirement Description | Target Module / Component | Verification Test Case | Implementation Status | Test Status |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **OFFICIAL-01** | Official PS 26251 Context | Challenge of maintaining assured and timely supply to geographically dispersed forward formations | Architecture System Topology & Multi-Echelon Ledger | `TC-E2E-01` | Architecture Specified | Planned |
| **OFFICIAL-02** | Official PS 26251 Context | Difficulty anticipating requirements due to fragmented consumption & demand information | `server/services/forecastEngine.js` | `TC-CORE-02` | Specification Complete | Planned |
| **OFFICIAL-03** | Official PS 26251 Context | Need to optimise movement of critical supplies across multiple holding echelons | `server/services/replenishmentEngine.js` | `TC-CORE-04` | Specification Complete | Planned |
| **PROP-REQ-01** | Team Proposed MVP | Multi-Echelon Synthetic Inventory Ledger tracking stock, burn rate, and days-of-supply | `client/src/views/InventoryView.jsx`, `server/routes/inventory.js` | `TC-CORE-01` | Specification Complete | Planned |
| **PROP-REQ-02** | Team Proposed MVP | Time-Series Demand Forecasting Engine generating 7/14/30-day forward projections | `server/services/forecastEngine.js`, `client/src/components/ForecastChart.jsx` | `TC-CORE-02` | Specification Complete | Planned |
| **PROP-REQ-03** | Team Proposed MVP | Automated Stockout Deficit Calculation and Safety Buffer Warning Indicators | `server/services/runoutCalculator.js`, `client/src/components/MetricCards.jsx` | `TC-CORE-03` | Specification Complete | Planned |
| **PROP-REQ-04** | Team Proposed MVP | Actionable Replenishment Recommendation Generator with Explainability Narrative | `server/services/replenishmentEngine.js`, `client/src/views/ReplenishmentView.jsx` | `TC-CORE-04` | Specification Complete | Planned |
| **PROP-REQ-05** | Team Proposed MVP | What-If Scenario Simulation Sandbox for testing consumption surges and transit delays | `server/services/simulationService.js`, `client/src/views/SimulationSandbox.jsx` | `TC-CORE-05` | Specification Complete | Planned |
| **PROP-REQ-06** | Team Proposed MVP | One-Click Replenishment Dispatch Approval with Immutable Audit Trail Logging | `server/services/auditService.js`, `client/src/views/AuditLogView.jsx` | `TC-CORE-06` | Specification Complete | Planned |
| **PROP-REQ-07** | Team Proposed MVP | Reproducible Synthetic Operational Scenario Seeder (Zero Real Military Data) | `server/scripts/seedSyntheticData.js` | `TC-DATA-01` | Specification Complete | Planned |
| **PROP-EXT-01** | Proposed Extension | Geospatial (GIS) Map Route View with synthetic nodes and transit corridors | `client/src/components/GISRouteMap.jsx` *(Optional Phase 6)* | `TC-EXT-01` | Deferred / Under Review | Deferred |
| **PROP-EXT-02** | Proposed Extension | Terrain / Weather Delay Modifier adjusting base transit lead times | `server/services/transitModel.js` *(Optional Phase 6)* | `TC-EXT-02` | Deferred / Under Review | Deferred |
| **PROP-EXT-03** | Future Exploration | Mock IoT Sensor Telemetry Ingestion Contract | `server/routes/iot.js` *(API Contract Only)* | `TC-EXT-03` | Deferred / Future | Deferred |

---

## 2. Requirements Accounting Summary

- **Official Problem Dimensions Traced:** 3
- **Team-Proposed Core MVP Requirements:** 7 (All fully documented; 0 implemented pending sign-off)
- **Proposed Optional Extensions:** 3 (Clearly isolated to prevent prototype overengineering)
- **Implemented Codebase:** 0 (Strict documentation-first gating maintained)
- **Verification Readiness:** 100% of core requirements mapped to explicit test cases in `Testing.md`.
