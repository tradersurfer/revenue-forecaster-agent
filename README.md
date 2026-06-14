# Revenue Forecaster Agent

**Sub-agent of the JECI Financial Statements Dashboard.** Takes a business's historical revenue inputs and projects month-by-month growth across multiple scenarios — conservative, base, and aggressive — with AI-generated commentary on key assumptions.

Runs as a standalone API or embedded inside the Financial Statements Dashboard as a callable agent module.

---

## What It Does

```
User inputs:
 ├── Current MRR / ARR
 ├── Growth drivers (new clients, pricing, churn rate)
 ├── Cost structure (fixed vs variable)
 └── Forecast horizon (6 / 12 / 24 months)
          ↓
   Revenue Forecaster Agent
   ├── Scenario builder (3 growth paths)
   ├── Month-by-month projection engine
   ├── Assumption validator (AI flags red flags)
   └── Commentary generator (plain English)
          ↓
   Output:
   ├── Scenario table (Conservative / Base / Aggressive)
   ├── MRR/ARR waterfall chart
   ├── Cash flow projection
   └── Exportable CSV / PDF summary
```

---

## Scenario Logic

| Scenario | Growth Rate | Churn Assumption | Use Case |
|----------|-------------|-----------------|---------|
| Conservative | Flat to -10% | Higher churn | Stress test / downside |
| Base Case | Trend line | Historical average | Planning default |
| Aggressive | +20–40% | Low churn | Fundraise / pitch deck |

---

## Tech Stack

| Layer | Technology |
|-------|-----------|
| Agent | Claude (Anthropic) |
| Frontend | React, Recharts |
| Backend | Node.js / Express |
| Database | Supabase |
| Export | CSV + PDF generation |
| Deployment | Railway / Netlify |

---

## API

```
POST /api/forecast
Body: { mrr, growthRate, churnRate, horizon, scenarios }
Returns: { conservative[], base[], aggressive[], commentary }

GET /api/forecast/:id
Returns: saved forecast with assumptions log

POST /api/forecast/:id/export
Returns: CSV or PDF download
```

---

## Relationship to Financial Statements Dashboard

This agent is a module within the larger `financial-statements-dashboard`. It can be:
- **Called directly** via API as a standalone service
- **Embedded** inside the dashboard as the "Forecast" tab
- **Chained** with the AP/AR agent to incorporate receivables into cash flow projection

---

## Setup

```bash
git clone https://github.com/tradersurfer/revenue-forecaster-agent.git
cd revenue-forecaster-agent
npm install
cp .env.example .env
npm run dev
```

Required env vars:
```
ANTHROPIC_API_KEY=
SUPABASE_URL=
SUPABASE_ANON_KEY=
```

---

## Status

🔄 **In active development** — core projection engine complete, AI commentary layer in progress.

---

## Part of the JECI Group Stack

Built and maintained by [Adrian Jordan](https://github.com/tradersurfer) · [JECI Group](https://jecigroup.com)

**Related:** [`jeci-ap-ar-agent`](https://github.com/tradersurfer/jeci-ap-ar-agent) · [`financial-statements-dashboard`](https://github.com/tradersurfer/financial-statements-dashboard)
