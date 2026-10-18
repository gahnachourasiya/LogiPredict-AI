# Engineering Standards & Governance Rules — LogiPredict AI

> **Product Name:** LogiPredict AI  
> **Official Problem Statement:** SIH PS 26251 — *Indian Army - Predictive Logistics & Forward Supply Chain*  
> **Scope:** Development Standards, Synthetic Data Integrity, and Quality Guardrails  

---

## 1. Golden Rules of the Project

1. **Synthetic Data Policy (Zero Real Military Data):**  
   Under no circumstances will real-world military formations, live unit designations, classified border locations, tactical coordinates, or genuine supply quantities be incorporated into this repository. All sample data must be 100% synthetic, generalized, and explicitly flagged as mock demonstration data.
2. **Explainability Over Black Boxes:**  
   In predictive logistics for high-stakes environments, opaque statistical models that cannot explain their calculations are unacceptable. Every demand forecast and replenishment suggestion must expose its mathematical variables (e.g. burn rate, lead time, buffer thresholds).
3. **Deterministic & Offline-First:**  
   Every feature demonstrated must function completely offline on the presenter's laptop without reliance on external cloud APIs or unstable venue Wi-Fi.
4. **Minimalism (Anti-Overengineering):**  
   Build only the features required to demonstrate the core value proposition of SIH PS 26251. Do not introduce microservices, distributed streaming, or heavy enterprise frameworks for a student hackathon prototype.

---

## 2. Directory Layout & Module Structure

When implementation is approved, the project structure will follow this layout:

```
sih251/
├── brain/                         # All documentation, ADRs, PRD, and architecture specs
├── client/                        # Frontend application (React + Vite)
│   ├── public/                    # Static assets
│   ├── src/
│   │   ├── components/            # UI components (MetricCards, ForecastChart, RoleToggle)
│   │   ├── views/                 # Top-level views (Overview, Inventory, Forecasts, Simulation)
│   │   ├── services/              # Client API consumers
│   │   ├── styles/                # tokens.css and component styles
│   │   ├── App.jsx                # Layout coordinator
│   │   └── main.jsx               # Client bootstrapping
│   └── package.json
├── server/                        # Backend service (Node.js + Express)
│   ├── src/
│   │   ├── routes/                # API routes (inventory, forecast, replenishments, simulation)
│   │   ├── services/              # Forecasting algorithms, run-out calculator, replenishment logic
│   │   ├── models/                # SQLite database queries and schema definitions
│   │   ├── scripts/               # Synthetic scenario seed generator (seedSyntheticData.js)
│   │   └── server.js              # Server initialization
│   └── package.json
└── README.md                      # Project root documentation
```

---

## 3. Naming Standards

| Element | Format | Example |
| :--- | :--- | :--- |
| **Synthetic Nodes** | kebab-case slug | `node-depot-alpha`, `node-fp-delta` |
| **Logistics Items** | kebab-case slug | `item-ration-class1`, `item-fuel-pol-3` |
| **Component Files** | PascalCase | `ForecastChart.jsx`, `ReplenishmentCard.jsx` |
| **Service Modules** | camelCase | `forecastEngine.js`, `runoutCalculator.js` |
| **CSS Tokens** | kebab-case | `--color-bg-base`, `--color-critical` |
| **API Routes** | plural nouns, lowercase | `/api/inventory`, `/api/replenishments` |
| **Database Tables** | snake_case, plural | `nodes`, `items`, `consumption_records` |

---

## 4. Error Handling & Validation Standards

- **Server-Side Validation:** All endpoints accepting parameters (such as simulation multipliers or replenishment approvals) must validate ranges before calculation:
  - Consumption multipliers clamped to `[0.5, 3.0]`.
  - Transit delay clamped to `[0, 14]` days.
  - Quantities must be positive integers.
- **Unified JSON Response Envelopes:**
  ```json
  // Success
  { "success": true, "data": { ... }, "timestamp": "2026-10-14T..." }

  // Error
  { "success": false, "error": { "code": "INVALID_PARAMS", "message": "..." } }
  ```
- **Resilient UI States:** Visual charts and tables must display clean empty/loading states rather than breaking with unhandled JavaScript errors.
