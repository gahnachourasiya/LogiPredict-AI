# Security & Operational Safeguards — LogiPredict AI

> **Product Name:** LogiPredict AI  
> **Official Problem Statement:** SIH PS 26251 — *Indian Army - Predictive Logistics & Forward Supply Chain*  
> **Scope:** Security Architecture, Synthetic Data Integrity, and Demonstration Guardrails  

---

## 1. Prototype Classification & Disclaimer

> [!CAUTION]
> **Academic & Hackathon Scope Disclaimer:**  
> LogiPredict AI is an exploratory prototype designed exclusively for academic demonstration at the Smart India Hackathon. It is **NOT** certified, accredited, authorized, or approved for operational military, defence, or government supply chain use.  
> The system does not connect to any defence network, military intranet, or government database, and contains no classified information.

---

## 2. Synthetic Data Integrity & Air-Gap Posture

1. **Synthetic Data Exclusivity:** All entity records, forward post identifiers, supply categories, and inventory counts are 100% synthetically generated for benchmark testing and evaluation.
2. **Zero Inbound/Outbound Telemetry:** The prototype does not transmit analytics or telemetry to external third-party cloud analytics services.
3. **Localhost Binding:** Development and demonstration services are bound strictly to loopback addresses (`127.0.0.1` / `localhost`) to prevent unauthorized network snooping across open hackathon venue Wi-Fi networks.

---

## 3. Application Security Safeguards

### 3.1 Input Validation & Range Clamping
All API request payloads are validated prior to execution in analytical routines:
- Numeric inputs (e.g. simulation multipliers, requested order quantities) are checked against reasonable upper/lower bounds.
- Negative quantities and invalid string inputs are rejected with standard `400 Bad Request` envelopes.

### 3.2 SQL Injection Prevention
- All database queries against the local SQLite database must use parameterized prepared statements:
  ```javascript
  // Permitted (Prepared Statement)
  const stmt = db.prepare('SELECT * FROM inventory WHERE node_id = ?');
  const results = stmt.all(nodeId);

  // Strictly Forbidden (String Concatenation)
  const results = db.query(`SELECT * FROM inventory WHERE node_id = '${nodeId}'`);
  ```

### 3.3 Cross-Site Scripting (XSS) Mitigation
- Frontend views built with React automatically escape dynamic string insertions.
- Any raw inputs in user notes or audit records are sanitized against script tags before persistence.

---

## 4. Role-Based Access Simulation (RBAC)

For live evaluation, the prototype provides simulated role switching to demonstrate governance controls:

| Role | Operational Scope | Permitted Actions |
| :--- | :--- | :--- |
| **Logistics Planner (HQ)** | System-wide Visibility | View all nodes, generate forecasts, run what-if simulations, approve replenishment dispatches |
| **Forward Post Officer** | Node-restricted Visibility | View local stock balances, log daily consumption, submit emergency supply requisition |
| **Command Auditor / Evaluator** | Compliance & Audit | Inspect immutable audit logs, verify calculation narratives, trigger synthetic data reset |

---

## 5. Demonstration Safeguards

- **Zero Hardcoded Production Credentials:** Demo accounts use standard local development credentials (`planner@logipredict.local` / `demo123`).
- **Sanitized Error Output:** Backend errors return standardized error codes and client-friendly messages. Full system stack traces or filesystem paths are never leaked to the client browser.
- **Fail-Safe Data Recovery:** An automated seed reset script (`npm run db:reset-seed`) is provided to instantly purge and restore the benchmark demonstration scenario if needed.
