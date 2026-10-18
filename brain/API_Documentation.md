# REST API Specifications — LogiPredict AI

> **Product Name:** LogiPredict AI  
> **Official Problem Statement:** SIH PS 26251 — *Indian Army - Predictive Logistics & Forward Supply Chain*  
> **Status:** **PROPOSED** (Awaiting Phase Approval & Implementation)  
> **Base URL:** `http://localhost:5000/api`  
> **Default Headers:** `Content-Type: application/json`, `Accept: application/json`  

---

## 1. Inventory & Node Endpoints *(PROPOSED)*

### 1.1 List All Nodes
- **`GET /api/nodes`**
- **Description:** Returns all synthetic logistics nodes (Depots, Transit Hubs, Forward Posts).
- **Response `200 OK`:**
  ```json
  {
    "success": true,
    "data": [
      {
        "id": "node-fp-delta",
        "name": "Synthetic Forward Post Delta",
        "nodeType": "FORWARD_POST",
        "sector": "Sector North",
        "capacityUnits": 1000
      }
    ]
  }
  ```

### 1.2 Get Multi-Echelon Inventory Status
- **`GET /api/inventory`**
- **Query Parameters:** `nodeId` (optional), `category` (optional), `status` (optional: `SAFE`, `WARNING`, `CRITICAL`)
- **Response `200 OK`:**
  ```json
  {
    "success": true,
    "data": [
      {
        "id": "inv-001",
        "nodeId": "node-fp-delta",
        "nodeName": "Forward Post Delta",
        "itemId": "item-fuel-pol-3",
        "itemName": "High Altitude Diesel (POL)",
        "category": "FUEL_POL",
        "currentStock": 350,
        "safetyBufferStock": 500,
        "dailyBurnRate": 70,
        "daysOfSupply": 5.0,
        "stockStatus": "WARNING"
      }
    ]
  }
  ```

---

## 2. Demand Forecasting & Run-Out Endpoints *(PROPOSED)*

### 2.1 Get Forecast Trajectory & Run-Out Projection
- **`GET /api/forecast/:nodeId/:itemId`**
- **Query Parameters:** `horizonDays` (default `14`, options: `7`, `14`, `30`)
- **Description:** Generates time-series demand projections and computes the projected stock exhaustion curve.
- **Response `200 OK`:**
  ```json
  {
    "success": true,
    "data": {
      "nodeId": "node-fp-delta",
      "itemId": "item-fuel-pol-3",
      "currentStock": 350,
      "projectedRunoutDate": "2026-10-19",
      "daysRemaining": 5.0,
      "burnRateDailyAverage": 70.0,
      "historicalBurn": [
        { "date": "2026-10-12", "actual": 68 },
        { "date": "2026-10-13", "actual": 72 }
      ],
      "forecast": [
        { "date": "2026-10-15", "predictedDemand": 70, "projectedStock": 280 },
        { "date": "2026-10-16", "predictedDemand": 70, "projectedStock": 210 },
        { "date": "2026-10-17", "predictedDemand": 71, "projectedStock": 139 },
        { "date": "2026-10-18", "predictedDemand": 69, "projectedStock": 70 },
        { "date": "2026-10-19", "predictedDemand": 70, "projectedStock": 0 }
      ]
    }
  }
  ```

---

## 3. Replenishment Recommendation Endpoints *(PROPOSED)*

### 3.1 Fetch System Replenishment Recommendations
- **`GET /api/replenishments`**
- **Query Parameters:** `status` (default `RECOMMENDED`, options: `ALL`, `APPROVED`, `DISPATCHED`)
- **Response `200 OK`:**
  ```json
  {
    "success": true,
    "data": [
      {
        "id": "rep-2026-001",
        "sourceNode": { "id": "node-depot-alpha", "name": "Base Supply Depot Alpha", "availableSurplus": 4500 },
        "destinationNode": { "id": "node-fp-delta", "name": "Forward Post Delta" },
        "item": { "id": "item-fuel-pol-3", "name": "High Altitude Diesel (POL)" },
        "recommendedQuantity": 700,
        "priority": "CRITICAL_STOCKOUT",
        "status": "RECOMMENDED",
        "generatedReason": "Current stock (350L) breaches buffer (500L). Projected exhaustion in 5 days at 70L/day."
      }
    ]
  }
  ```

### 3.2 Approve / Modify Replenishment Dispatch
- **`POST /api/replenishments/:id/action`**
- **Request Body:**
  ```json
  {
    "action": "APPROVE",
    "approvedQuantity": 750,
    "plannerNotes": "Authorized priority convoy dispatch with +50L contingency buffer."
  }
  ```
- **Response `200 OK`:** Returns updated replenishment record and writes audit trail entry.

---

## 4. What-If Scenario Simulation Endpoints *(PROPOSED)*

### 4.1 Run Comparative What-If Simulation
- **`POST /api/simulation/evaluate`**
- **Description:** Computes the impact of stressed operational parameters on forward supply lines without modifying persistent database records.
- **Request Body:**
  ```json
  {
    "nodeId": "node-fp-delta",
    "itemId": "item-fuel-pol-3",
    "consumptionMultiplier": 1.35,
    "transitDelayDays": 2.0,
    "horizonDays": 14
  }
  ```
- **Response `200 OK`:**
  ```json
  {
    "success": true,
    "data": {
      "baselineDaysOfSupply": 5.0,
      "simulatedDaysOfSupply": 3.7,
      "stockoutDeficitDate": "2026-10-17",
      "requiredReplenishmentBoost": 480,
      "comparisonTrajectory": [
        { "day": 1, "baselineStock": 280, "simulatedStock": 255 },
        { "day": 2, "baselineStock": 210, "simulatedStock": 160 },
        { "day": 3, "baselineStock": 140, "simulatedStock": 66 },
        { "day": 4, "baselineStock": 70, "simulatedStock": 0 }
      ]
    }
  }
  ```

---

## 5. Proposed Extensions *(OPTIONAL / PHASE 2)*

### 5.1 Geospatial Corridor Topology *(Proposed Extension)*
- **`GET /api/gis/corridors`**
- **Description:** Returns abstract geographic nodes and connecting supply corridors with synthetic terrain delay factors.

### 5.2 Sensor / Telemetry Ingestion Contract *(Proposed Future Contract)*
- **`POST /api/iot/telemetry`**
- **Description:** Mock endpoint accepting cargo temperature / RFID pallet scan events. *Marked as non-operational prototype specification.*

---

## 6. Demonstration & System Control Endpoints *(PROPOSED)*

### 6.1 Cold Reset & Seed Synthetic Operational Data
- **`POST /api/demo/reset-seed`**
- **Description:** Resets database tables and reloads the benchmark 5-node, 4-commodity synthetic scenario for evaluation.
