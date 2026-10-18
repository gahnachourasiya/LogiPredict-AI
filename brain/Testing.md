# Quality Assurance & Testing Strategy — LogiPredict AI

> **Product Name:** LogiPredict AI  
> **Official Problem Statement:** SIH PS 26251 — *Indian Army - Predictive Logistics & Forward Supply Chain*  
> **Status:** Active Quality Specification  
> **Target:** Flawless, Resilient SIH Jury Demonstration  

---

## 1. Testing Scope & Methodology

Testing for LogiPredict AI guarantees that mathematical calculations, stock deficit alerts, and simulation projections behave reliably under live evaluation.

```
+-------------------------------------------------------------+
|  Tier 3: SIH Live Demonstration User Journey (4-Min Path)   | -> Highest Priority
+-------------------------------------------------------------+
|  Tier 2: Algorithmic Verification (Forecasts & Runout Math)  | -> Core Priority
+-------------------------------------------------------------+
|  Tier 1: Synthetic Data Integrity & Local Storage Integrity | -> Baseline Priority
+-------------------------------------------------------------+
|  Tier 0: Future Extension Checks (GIS, Weather, IoT)         | -> Isolated Sandbox
+-------------------------------------------------------------+
```

---

## 2. Test Cases for Core MVP

### 2.1 Algorithmic & Functional Verification

| Case ID | Feature Area | Test Scenario | Input / Action | Expected Result | Status |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **TC-DATA-01** | Synthetic Seeding | Cold database reset and seed execution | Run `npm run seed` | 5 synthetic nodes, 4 commodity items, 60-day consumption history generated without error | Planned |
| **TC-CORE-01** | Inventory Ledger | Load multi-echelon stock table | Open Inventory View | Accurate display of current stock, buffer thresholds, and burn rates for each node | Planned |
| **TC-CORE-02** | Forecasting | Calculate 14-day demand forecast | Select Forward Post Delta + Fuel POL | Output generates continuous daily projected demand reflecting observed historical trend | Planned |
| **TC-CORE-03** | Stockout Alert | Verify run-out threshold logic | Forward Post with stock < buffer | Status badge transitions to `[CRITICAL_STOCKOUT]`; run-out date accurately computed | Planned |
| **TC-CORE-04** | Replenishment | Generate automated transfer order | Inspect suggested replenishment | Recommends transfer from Base Depot Alpha to Forward Post Delta with explainability narrative | Planned |
| **TC-CORE-05** | What-If Simulator | Apply consumption surge stress | Adjust slider to +40% surge | Forecasted stock curve accelerates depletion; deficit date moves earlier by calculated days | Planned |
| **TC-CORE-06** | Dispatch Approval | Planner approves suggested order | Click "Approve Transfer Dispatch" | Order status becomes `APPROVED`, inventory balance reserves stock, immutable audit log written | Planned |

### 2.2 Boundary & Robustness Checks

| Case ID | Feature Area | Test Scenario | Input / Action | Expected Result | Status |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **TC-ROB-01** | Slider Extremes | Simulation slider at 0x and 3x | Slide consumption multiplier to limits | Calculations clamp gracefully; UI never renders `NaN` or crashes | Planned |
| **TC-ROB-02** | Zero Historical Data | Query node with 0 consumption | Request forecast for newly added node | Displays informational fallback: *"Insufficient historical data to compute trend"* | Planned |
| **TC-ROB-03** | Injection Defense | Malicious string in filter search | Enter `' OR '1'='1` in search input | Safe parameterization; no SQL errors or data leaks | Planned |

---

## 3. Separate Validation Criteria for Proposed Extensions

These validation criteria are isolated from the core MVP and evaluated only if the corresponding extension is approved:

- **TC-EXT-01 (GIS Map Route Validation):** Verify that synthetic coordinates render within the abstract map viewport without external tile server network timeouts.
- **TC-EXT-02 (Weather Delay Parameter):** Verify that toggling a "Monsoon Delay (+3 days)" modifier increments transit lead times and recalculates stockout dates accordingly.
- **TC-EXT-03 (Mock IoT Telemetry Contract):** Verify that the mock telemetry endpoint validates JSON payload schemas and rejects malformed sensor packets.

---

## 4. SIH Jury Demonstration Protocol (The 4-Minute Walkthrough)

Conduct this validation drill prior to presenting before hackathon evaluators:

1. **Step 1: Context & Synthetic Disclaimer (0:00 - 0:30):**
   - Introduce *LogiPredict AI* for SIH PS 26251 (*Indian Army - Predictive Logistics & Forward Supply Chain*).
   - Point out the permanent `[SYNTHETIC DEMO MODE]` indicator, explaining that all nodes and commodities are abstract mock representations.
2. **Step 2: Operational Health & Impending Stockout (0:30 - 1:30):**
   - Show the Executive Overview: 2 forward posts in critical stockout status.
   - Drill down into *Forward Post Delta* (Class III Fuel/POL): 5 days of supply remaining.
3. **Step 3: Algorithmic Explainability (1:30 - 2:15):**
   - Open Demand Forecast: Show `[ACTUAL]` vs `[PREDICTED]` curves and explain the automated deficit date calculation.
4. **Step 4: What-If Scenario Stress Testing (2:15 - 3:15):**
   - Shift to the Simulation Sandbox: Apply a +30% surge multiplier.
   - Show how the run-out date drops from Day 5 to Day 3.
5. **Step 5: Actioning the Replenishment (3:15 - 4:00):**
   - Review system-recommended dispatch from *Base Depot Alpha* (700L).
   - Click "Approve Transfer Dispatch". Show instant audit log generation and updated depot balances.
