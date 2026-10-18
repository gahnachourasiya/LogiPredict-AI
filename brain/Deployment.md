# Deployment & Demonstration Guide — LogiPredict AI

> **Product Name:** LogiPredict AI  
> **Official Problem Statement:** SIH PS 26251 — *Indian Army - Predictive Logistics & Forward Supply Chain*  
> **Target Environments:** Local Workstation (Proposed Primary Demonstration Mode)  
> **Status:** Proposed Deployment Specification (Application not yet deployed)  

---

## 1. System Requirements & Prerequisites

- **Node.js:** v18.0.0 or higher (v20+ LTS recommended)
- **Package Manager:** `npm` (v9+)
- **Operating System:** Windows 10/11, macOS, or Linux
- **Browser:** Any modern Chromium-based browser (Chrome, Edge, Brave) or Firefox
- **Network Requirement:** **Zero.** Operates completely offline during evaluations.

---

## 2. Configuration & Environment Variables

All configuration is managed via a local `.env` file (copied from `.env.example` upon implementation kickoff):

| Variable | Proposed Default | Description |
| :--- | :--- | :--- |
| `PORT` | `5000` | Port for the backend API service |
| `CLIENT_ORIGIN` | `http://localhost:5173` | Allowed CORS origin for local Vite client |
| `DATABASE_PATH` | `./data/logipredict.sqlite` | Filepath for local embedded SQLite database |
| `NODE_ENV` | `development` | Runtime environment mode |
| `DEMO_SEED_ON_BOOT` | `true` | Automatically seeds synthetic scenario if database is empty |

---

## 3. Local Setup & Execution Guide *(Planned for Implementation Phase)*

> [!NOTE]
> The steps below represent the planned operational workflow once implementation is approved by the user. Application packages are currently withheld pending documentation review.

### Step 1: Clone & Navigate
```bash
git clone <repository_url> sih251
cd sih251
```

### Step 2: Install Dependencies *(Post-Approval)*
```bash
# Server dependencies
cd server
npm install

# Client dependencies
cd ../client
npm install
```

### Step 3: Seed Synthetic Logistics Scenario
```bash
cd ../server
npm run db:seed
```

### Step 4: Launch Dual Development Servers
```bash
# Terminal 1: Backend API
cd server
npm run dev

# Terminal 2: Frontend Dashboard
cd client
npm run dev
```

- **Frontend Interface:** `http://localhost:5173`
- **Backend API:** `http://localhost:5000/api`

---

## 4. Single-Port Static Bundle Mode (Offline Jury Safety Net)

To eliminate any chance of inter-process port blocking on judging machines:

```bash
# 1. Build client bundle
cd client
npm run build

# 2. Start unified server (serves API and compiled frontend statically)
cd ../server
npm start
```
Access the complete application at a single URL: `http://localhost:5000`.

---

## 5. Live Demonstration Recovery Protocol

In the event an evaluator asks to witness a clean start from zero state:
```bash
cd server
npm run db:reset-seed
```
This single command drops all local tables, re-applies schema migrations, and reloads the benchmark 5-node synthetic scenario in under 2 seconds.
