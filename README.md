<div align="center">

<img src="assets/silangan-icon.png" alt="Silangan" width="140"/>

# Silangan

**An AI-Powered Consumption Simulator Bridging Household Solar Feasibility Guidance and Government Demand-Side Energy Planning**

[![TypeScript](https://img.shields.io/badge/TypeScript-5.x-3178C6?style=flat-square&logo=typescript&logoColor=white)](https://www.typescriptlang.org/)
[![React](https://img.shields.io/badge/React-18-61DAFB?style=flat-square&logo=react&logoColor=black)](https://react.dev/)
[![NestJS](https://img.shields.io/badge/NestJS-Backend-E0234E?style=flat-square&logo=nestjs&logoColor=white)](https://nestjs.com/)
[![PostgreSQL](https://img.shields.io/badge/PostgreSQL-Supabase-4169E1?style=flat-square&logo=postgresql&logoColor=white)](https://supabase.com/)
[![Prisma](https://img.shields.io/badge/Prisma-ORM-2D3748?style=flat-square&logo=prisma&logoColor=white)](https://www.prisma.io/)
[![Redis](https://img.shields.io/badge/Redis-Sessions-DC382D?style=flat-square&logo=redis&logoColor=white)](https://redis.io/)
[![n8n](https://img.shields.io/badge/n8n-AI%20Agent-EA4B71?style=flat-square&logo=n8n&logoColor=white)](https://n8n.io/)
[![Docker](https://img.shields.io/badge/Docker-Containerized-2496ED?style=flat-square&logo=docker&logoColor=white)](https://www.docker.com/)
[![Status](https://img.shields.io/badge/Status-Project%20Initiation-yellow?style=flat-square)](#project-plan--gantt-chart)
[![License](https://img.shields.io/badge/License-Private-red?style=flat-square)](#license)

*Replacing guesswork with a data-grounded answer — for the household deciding on solar, and the government deciding where to spend.*

</div>

---

## Table of Contents

<details>
<summary>Click to expand</summary>

1. [Overview](#overview)
2. [Background & Problem](#background--problem)
3. [What Silangan Does](#what-silangan-does)
4. [Intended Users & Stakeholders](#intended-users--stakeholders)
5. [Core Features](#core-features)
6. [Expected Benefits](#expected-benefits)
7. [Scope & Boundaries](#scope--boundaries)
8. [System Architecture](#system-architecture)
9. [Tech Stack](#tech-stack)
10. [Repository Structure (Planned Monorepo)](#repository-structure-planned-monorepo)
11. [Data Model](#data-model)
12. [Environment Variables](#environment-variables)
13. [Getting Started](#getting-started)
14. [Development Workflow](#development-workflow)
15. [Project Plan / Gantt Chart](#project-plan--gantt-chart)
16. [Team & Roles](#team--roles)
17. [Documentation](#documentation)
18. [References](#references)
19. [License](#license)

</details>

---

## Overview

<div align="center">
  <img src="assets/ppt/SILANGAN-1.png" alt="Silangan — title slide" width="900"/>
</div>

<br/>

**Silangan** is a dual-purpose, data-driven decision-support system (DSS) built to close a household-level service-delivery gap during the Philippines' national energy emergency: neither individual households nor the Department of Energy (DOE), the Energy Regulatory Commission (ERC), and Lucena City's LGU currently have a scalable channel for personalized, trustworthy rooftop-solar guidance — or for seeing, at the barangay level, where unrealized solar adoption potential is concentrated enough to justify outreach or incentive spending.

The system closes both gaps through a single household-facing AI consumption simulator. A household builds a usage profile from its appliance holdings, behavior, and environment; the system projects daily, weekly, monthly, and yearly consumption; and — where a household uploads an actual utility bill — cross-checks the simulated total against it to produce a **validation confidence score**. Solar sizing, investment, ROI, and financing guidance are gated behind that validation step, so every recommendation a household receives, and every data point that reaches government, is grounded in a bill-confirmed profile rather than a guess. Every validated household interaction simultaneously feeds anonymized, confidence-weighted data into a **barangay-level** aggregate view that DOE, ERC, and the Lucena City LGU can act on directly — the household tool *is* the mechanism by which that government-facing data gets collected.

> **Academic Project (Information Management — Decision Support Systems)**
> Manuel S. Enverga University Foundation — Lucena City
> Team LUXUS · Abandia, K. · Altamarino, M. F. · Iloilo, J. · Valencia, J. L.

---

## Background & Problem

<div align="center">
  <img src="assets/ppt/SILANGAN-2.png" alt="At the exact moment the national grid needs demand-side relief, the households most exposed to rising rates are the least equipped to act on it with confidence." width="900"/>
</div>

<br/>

On **March 24, 2026**, President Ferdinand R. Marcos Jr. signed **Executive Order No. 110**, declaring a State of National Energy Emergency in response to disruptions in global oil supply — including the closure of the Strait of Hormuz — and activating the whole-of-government **UPLIFT** conservation framework.

<div align="center">
  <img src="assets/ppt/SILANGAN-4.png" alt="EO 110 — State of National Energy Emergency" width="900"/>
</div>

<br/>

This has coincided with a sustained rise in residential electricity rates, against a backdrop of favorable policy and falling hardware costs that households still aren't converting into adoption:

<div align="center">
  <img src="assets/ppt/SILANGAN-3.png" alt="Key statistics — rate increases, national solar targets, residential share of rooftop potential" width="900"/>
</div>

<br/>

<div align="center">
  <img src="assets/ppt/SILANGAN-5.png" alt="Why aren't Filipino households moving toward solar, even with favorable policy and falling hardware costs?" width="900"/>
</div>

<br/>

The gap is not primarily a policy or hardware problem — it's an informational one. Academic research consistently shows that even where solar is affordable and policy is favorable, households can't independently determine whether it's financially worthwhile for their specific home:

<div align="center">
  <img src="assets/ppt/SILANGAN-6.png" alt="Literature: installers as a biased information source, trust as the real bottleneck, information vs. financing as separate barriers" width="900"/>
</div>

<br/>

For the average Filipino household, closing this gap independently would normally mean hiring an electrical engineer or energy auditor — a cost and access barrier most households can't clear. In the absence of that analysis, households either avoid solar altogether or rely on installer sales pitches, informal peer accounts, or outright myths about cost, maintenance, and net metering:

<div align="center">
  <img src="assets/ppt/SILANGAN-7.png" alt="Households can't tell if solar is financially worth it for their home — and government can't tell where unrealized solar potential is concentrated enough to justify outreach or incentive spending." width="900"/>
</div>

---

## What Silangan Does

<div align="center">
  <img src="assets/ppt/SILANGAN-8.png" alt="One household interaction does two jobs — validated feasibility report for the family, aggregate demand-side data for government" width="900"/>
</div>

<br/>

One household interaction does two jobs at once: it gives the family a **validated, costed solar feasibility report**, and it anonymously feeds the **aggregate demand-side data** that DOE, ERC, and the Lucena City LGU need to plan their emergency response — through five core engines:

1. **Consumption Simulation & Validation** — builds a usage profile from appliances, habits, and environment, then cross-checks it against an uploaded utility bill to produce a validation confidence score that unlocks every feature that follows.
2. **Solar Feasibility Engine** — turns a validated profile into a recommended PV system size, installation cost estimate, and ROI/payback timeline — no electrical engineer required.
3. **Predictive Forecasting & What-If Scenarios** — forecasts future consumption trends, segments households by usage profile, and lets a household preview the effect of a chosen solar system size on their bill before buying.
4. **AI Energy Analyst & Financing Referral** — explains in plain language why simulated and billed data diverge, and matches each household's investment tier to green-loan providers and DOE/LGU incentive programs.
5. **Demand-Side Planning Engine** — aggregates and anonymizes validated household data into a live, **barangay-level** view of unrealized solar adoption potential that DOE, ERC, and the Lucena City LGU can act on directly.

---

## Intended Users & Stakeholders

<div align="center">
  <img src="assets/ppt/SILANGAN-10.png" alt="Silangan stakeholders" width="900"/>
</div>

<br/>

| Group | Role |
|---|---|
| **Households** | Primary users — Meralco/electric-cooperative customers considering rooftop solar; receive a personalized feasibility report: sizing, cost, ROI, financing referrals |
| **DOE** | Aggregate, anonymized adoption-potential data to target outreach and incentive spending |
| **ERC** | Real-world adoption/ROI data reflecting how current net-metering rules actually perform |
| **Lucena City LGU** | A ready-made, barangay-level dataset, replacing manual permitting/outreach surveys |
| **Electric Cooperatives & Utilities** | Indirect — published rates feed savings projections; may receive aggregate demand signals back |
| **Solar Installers** *(secondary)* | Use a household's feasibility report as a warm lead / starting point for a formal quotation |
| **Financing & Green-Loan Providers** *(secondary)* | Receive referral matches once a household's investment tier is known — do not process or approve loans |

---

## Core Features

<div align="center">
  <img src="assets/ppt/SILANGAN-9.png" alt="Silangan feature grid" width="900"/>
</div>

<br/>

Silangan's operational structure is built around nine interlocking business processes, moving a household from raw consumption data to a costed, explainable, actionable feasibility report:

1. **Household Profile Management** — registration, authentication, and location tagging used to localize barangay irradiance and pricing assumptions.
2. **Consumption Data Intake** — appliance-and-behavior-driven AI simulation, manual monthly entry, and utility bill upload/parsing (image or PDF).
3. **Consumption Analysis & Validation** — average/peak load, seasonal variation, cluster segmentation, and the simulated-vs-billed alignment/confidence score.
4. **Solar Sizing & Investment Estimation** — recommended PV capacity (kWp), installation cost, and consumption offset %, using barangay irradiance and property data.
5. **ROI & Savings Forecasting** — projected monthly/annual savings, payback period, net-metering credit assumptions, and what-if scenario simulation.
6. **AI Energy Analyst & Literacy** — plain-language explainers and personalized recalibration guidance when simulated and billed data diverge.
7. **Feasibility Report Generation** — consolidates sizing, investment, and forecast outputs into a savable, exportable household report.
8. **Financing & Incentive Referral** — matches a household's investment tier to green-loan providers and DOE/LGU incentive programs.
9. **Demand-Side Government Reporting** — aggregates anonymized, confidence-weighted household data into barangay-level adoption-potential summaries for DOE/ERC/LGU planning cycles.

---

## Expected Benefits

<div align="center">
  <img src="assets/ppt/SILANGAN-11.png" alt="Silangan provides a centralized, data-driven feasibility platform" width="900"/>
</div>

<br/>

By translating a household's actual consumption data into a costed, explainable, personalized recommendation, Silangan replaces installer-mediated, potentially biased information with a neutral, data-grounded starting point for a household's decision — while simultaneously giving DOE, ERC, and the Lucena City LGU the granular, barangay-level visibility they currently lack to target outreach and incentive spending under Executive Order No. 110.

---

## Scope & Boundaries

**Silangan does:**
- Cover household consumption simulation, bill-based validation, solar feasibility, ROI/financing referral, and barangay-level government reporting end-to-end.
- Model **residential household electricity accounts only** — Meralco or electric-cooperative customers.
- Aggregate and report institutional analytics **specifically for Lucena City, at the barangay level** — this is the current scope per the approved SRS, replacing earlier regional/multi-municipality framing.
- Provide a low-bandwidth SMS/USSD channel for **manual kWh entry only** during outages or connectivity gaps.

**Silangan deliberately does not:**
- Sell, install, or dispatch solar equipment — it produces feasibility guidance and installer referrals only.
- Underwrite, process, or approve any loan or subsidy application — it surfaces financing/incentive referral matches only.
- Extend to commercial, industrial, or institutional electricity accounts.
- Replace on-site structural or electrical engineering inspection — solar sizing relies on barangay irradiance data and published market pricing.
- Expose individual household identities or raw consumption data to DOE, ERC, or LGU users — government-facing outputs are anonymized and aggregated at the barangay level only.

---

## System Architecture

Silangan uses a client–server architecture: a React frontend talks to a NestJS backend over HTTP/HTTPS and WebSocket, the backend owns all database access through Prisma, and an n8n workflow (containerized in Docker) handles AI processing as a separate service the backend calls over HTTP.

```mermaid
flowchart LR
    subgraph Client["Client"]
        A["Browser (Household / Government)"]
    end

    subgraph Frontend["apps/web — React + Zustand + Tailwind"]
        B["Interface Layer"]
    end

    subgraph Backend["apps/api — NestJS"]
        C["Web Service\n(REST API + WebSocket, JWT auth)"]
        D["Database Access Layer\n(Prisma ORM)"]
    end

    subgraph Data["Data Layer"]
        E[("PostgreSQL — Supabase")]
        F[("Redis — Session Storage")]
    end

    subgraph AI["services/ai-agent"]
        G["n8n Workflows (Docker)"]
    end

    A -- HTTPS --> B
    B -- "HTTP/HTTPS (standard ops)" --> C
    B -- "WebSocket (real-time)" --> C
    C --> D
    D --> E
    C -- session read/write --> F
    C -- HTTP --> G
```

**Request flow:**
1. The client (household or government user) authenticates and receives a JWT-backed session token; sessions are held in **Redis**.
2. Standard CRUD and calculation requests (profile, appliances, simulation, validation, solar sizing, ROI, reports) go over **HTTP/HTTPS** as RESTful JSON.
3. Real-time flows (e.g. AI Companion chat) use a **WebSocket** connection between the interface layer and the web service.
4. The web service never talks to Postgres directly — it always goes through the **Database Access Layer (Prisma)**.
5. AI-dependent features (consumption analysis narration, divergence explanations, forecasting assistance) are delegated from the backend to the **n8n** workflow service over HTTP; n8n returns structured text/JSON the backend relays to the client.

Password recovery uses OTP verification through an external email service; unfinished bill uploads or simulation builds auto-save progress to session storage so a household can resume without re-entering appliance data.

---

## Tech Stack

| Layer | Technology | Notes |
|---|---|---|
| **Frontend Framework** | React 18 | Household + Government portals in one SPA |
| **Frontend State** | Zustand | Lightweight global state management |
| **Frontend Styling** | Tailwind CSS | Utility-first styling |
| **Frontend Auth (client)** | Firebase (Google Sign-In) | Google OAuth on the client side |
| **Backend Framework** | NestJS (Node.js) | Modular REST API + WebSocket gateway |
| **Backend Auth** | JWT (sessionized tokens) | Role-based access control (household / government / admin) |
| **ORM** | Prisma | Type-safe database access layer |
| **Database** | PostgreSQL (hosted on Supabase) | Primary relational store |
| **Session Store** | Redis | Authenticated session + temp session data |
| **AI Workflow Engine** | n8n (containerized via Docker) | Consumption analysis, divergence explanations, forecasting assistance |
| **Communication** | REST (JSON) + WebSocket | GET/POST/PATCH/DELETE + persistent real-time channel |
| **Frontend Hosting** | Vercel | — |
| **Backend Hosting** | Render | — |
| **Package/Monorepo Tooling** | pnpm workspaces + Turborepo *(proposed)* | See [Repository Structure](#repository-structure-planned-monorepo) |
| **Language** | TypeScript (frontend & backend) | End-to-end type safety |

---

## Repository Structure (Planned Monorepo)

> 🚧 **This is the target structure for the repository**, established during Project Initiation (see [Project Plan](#project-plan--gantt-chart) → *Setup Development Environment and Tools*). Folders will be scaffolded incrementally as each module in the Gantt chart's Development Phase is picked up — this is the architecture the team is building toward, not a snapshot of what exists on day one.

```
Silangan/
├── apps/
│   ├── web/                          # React + Zustand + Tailwind frontend
│   │   ├── src/
│   │   │   ├── app/                  # Root layout, router config
│   │   │   ├── components/           # Shared/dumb UI components
│   │   │   ├── features/
│   │   │   │   ├── auth/             # Login, register, OTP recovery
│   │   │   │   ├── household/
│   │   │   │   │   ├── profile/
│   │   │   │   │   ├── appliances/           # Appliance Library
│   │   │   │   │   ├── consumption-log/      # Daily Consumption Log
│   │   │   │   │   ├── simulator/            # Consumption Simulation
│   │   │   │   │   ├── bill-validation/
│   │   │   │   │   ├── solar-feasibility/
│   │   │   │   │   ├── roi-whatif/
│   │   │   │   │   ├── ai-companion/
│   │   │   │   │   ├── financing/
│   │   │   │   │   └── reports/
│   │   │   │   └── government/
│   │   │   │       ├── dashboard/
│   │   │   │       ├── barangay-analytics/
│   │   │   │       ├── validation-coverage/
│   │   │   │       └── reports/
│   │   │   ├── store/                # Zustand stores
│   │   │   ├── lib/                  # API client, WebSocket client, utils
│   │   │   └── styles/
│   │   ├── public/
│   │   ├── index.html
│   │   ├── tailwind.config.ts
│   │   └── package.json
│   │
│   └── api/                          # NestJS backend
│       ├── src/
│       │   ├── modules/
│       │   │   ├── auth/             # Auth, JWT, OTP, RBAC
│       │   │   ├── household/        # Profile management
│       │   │   ├── appliance/        # Appliance library
│       │   │   ├── consumption/      # Manual log + bill intake
│       │   │   ├── simulation/       # AI consumption simulation
│       │   │   ├── validation/       # Bill validation / confidence score
│       │   │   ├── solar/            # Solar sizing & investment
│       │   │   ├── financial/        # ROI, savings, net-metering
│       │   │   ├── financing/        # Financing & incentive referral
│       │   │   ├── government/       # Barangay aggregation & reports
│       │   │   └── ai-bridge/        # Calls out to the n8n AI agent
│       │   ├── common/               # Guards, interceptors, pipes, filters
│       │   ├── config/               # Env/config module
│       │   ├── prisma/
│       │   │   ├── schema.prisma
│       │   │   └── migrations/
│       │   ├── main.ts
│       │   └── app.module.ts
│       ├── test/
│       └── package.json
│
├── services/
│   └── ai-agent/                     # n8n workflow definitions
│       ├── workflows/
│       ├── docker-compose.yml
│       └── README.md
│
├── packages/                         # Shared code across apps/services
│   ├── types/                        # Shared DTOs/interfaces (Household, ConsumptionRecord, ...)
│   └── config/                       # Shared ESLint/TSConfig
│
├── docs/
│   ├── paper.pdf                     # Midterm project paper
│   ├── srs.pdf                       # Software Requirements Specification
│   └── gantt-chart.csv               # Project plan (source of truth for this README's timeline)
│
├── assets/
│   ├── ppt/                          # README figures
│   └── silangan-icon.png
│
├── .github/
│   └── workflows/                    # CI: lint, typecheck, test on PR (planned)
│
├── .env.example
├── package.json                      # Workspace root
├── pnpm-workspace.yaml
├── turbo.json
└── README.md
```

---

## Data Model

The database is designed around a household layer (feeds each household's own feasibility pipeline) and a government layer (feeds barangay-level aggregation only). Referential integrity via primary/foreign keys ensures every recommendation, cost estimate, and forecast traces back to the household data that produced it.

| Entity | Layer | Purpose |
|---|---|---|
| `Household` | Household | Account, credentials, location (region/city/**barangay**), household size |
| `SimulationRecord` | Household | AI-simulated consumption at daily → yearly granularity |
| `ConsumptionRecord` | Household | Manual entry or uploaded-bill consumption |
| `ConsumptionProfile` | Household | Rolled-up average/peak consumption + usage cluster segment |
| `ValidationRecord` | Household | Simulated-vs-billed alignment/confidence score |
| `PropertyProfile` | Household | Roof/floor area, floors, orientation/sun angle |
| `SolarRecommendation` | Household | Recommended kWp, offset %, linked to irradiance + property data |
| `InvestmentEstimate` | Household | Total installation cost tied to a recommendation |
| `ROIForecast` | Household | Projected savings, payback period, applicable net-metering policy |
| `NetMeteringPolicy` | Household | Credit rate + effectivity date used by ROI forecasts |
| `FinancingPartner` / `FinancingReferral` | Household | Green-loan/incentive matches per investment tier |
| `BarangayIrradiance` | Government | Barangay-level average daily solar hours (replaces earlier regional-level irradiance framing) |
| `BarangayAggregateReport` | Government | Anonymized, confidence-weighted adoption-potential index per barangay |

> Full attribute lists, data types, and the complete ER/class diagrams are documented in [`docs/paper.pdf`](docs/paper.pdf) (Section III–IV) and [`docs/srs.pdf`](docs/srs.pdf) (Section 2.5 · Appendix B).

---

## Environment Variables

A `.env.example` will be committed at the repository root once `apps/api` is scaffolded. Planned variables:

```bash
# --- Backend (apps/api) ---
NODE_ENV=development
PORT=4000
DATABASE_URL=postgresql://user:password@host:5432/silangan   # Supabase connection string
JWT_SECRET=
JWT_EXPIRES_IN=1d
REDIS_URL=redis://localhost:6379
OTP_EMAIL_SERVICE_API_KEY=                                     # Password recovery / re-auth
AI_AGENT_BASE_URL=http://localhost:5678                        # n8n webhook base URL

# --- Frontend (apps/web) ---
VITE_API_BASE_URL=http://localhost:4000
VITE_FIREBASE_API_KEY=
VITE_FIREBASE_AUTH_DOMAIN=
VITE_FIREBASE_PROJECT_ID=

# --- AI Agent (services/ai-agent) ---
N8N_BASIC_AUTH_USER=
N8N_BASIC_AUTH_PASSWORD=
```

---

## Getting Started

> The steps below describe the intended setup for this monorepo once initial scaffolding lands (see [Project Plan](#project-plan--gantt-chart)). They will be updated as each piece comes online.

### Prerequisites

- **Node.js** 20+ and **pnpm** 9+
- **Docker** + **Docker Compose** (for the local n8n AI agent service, and optionally local Postgres/Redis)
- A **Supabase** project (hosted PostgreSQL) or a local Postgres instance
- A **Firebase** project with Google Sign-In enabled

### Installation

```bash
# 1. Clone the repository
git clone https://github.com/<your-org>/Silangan.git
cd Silangan

# 2. Install all workspace dependencies
pnpm install

# 3. Copy environment templates
cp .env.example .env
cp apps/api/.env.example apps/api/.env
cp apps/web/.env.example apps/web/.env

# 4. Generate the Prisma client and run migrations
pnpm --filter api prisma migrate dev

# 5. Start the AI agent service (n8n, in Docker)
docker compose -f services/ai-agent/docker-compose.yml up -d

# 6. Run frontend + backend together (via Turborepo)
pnpm turbo run dev
```

- Frontend → `http://localhost:5173`
- Backend API → `http://localhost:4000`
- n8n editor → `http://localhost:5678`

---

## Development Workflow

Since the repository is being created during Project Initiation, the following conventions apply from the first commit:

**Branching**
- `main` — protected, always deployable.
- `feature/<module>-<short-description>` — e.g. `feature/consumption-simulation-engine`
- `fix/<short-description>`
- `docs/<short-description>`

**Commits** — [Conventional Commits](https://www.conventionalcommits.org/):
```
feat(simulation): add appliance-based daily consumption calculator
fix(validation): correct alignment score rounding
docs(readme): update repository structure
chore(deps): bump prisma to 5.x
```

**Pull Requests**
- One module/feature per PR, scoped to a single line item in the [Gantt chart](#project-plan--gantt-chart) where possible.
- At least one reviewer approval before merging to `main`.
- CI (lint, typecheck, build) must pass — see `.github/workflows/` (planned).

**Testing** — aligned to the Gantt chart's Testing Phase: unit tests per module (Jest, backend) and integration tests across the API before merging into `main`; QA sign-off tracked per the Testing Phase deliverables below.

---

## Project Plan / Gantt Chart

<details>
<summary>Click to expand project timeline</summary>

Full phase-by-phase plan, as defined in `docs/gantt-chart.csv`. **We are currently in the Design Phase (System Design), per the plan below.**

| Phase | Task | Deliverables | Start | End (Est.) | Personnel |
|---|---|---|---|---|---|
| Pre-project | Project Brainstorming | Initial project briefing, meetings and assignment of roles | 31-Aug-26 | 4-Sep-26 | Team |
| Pre-project | Stakeholder Identification | Stakeholder list, stakeholder profiles, interview questions and interview findings | 5-Sep-26 | 6-Sep-26 | Team |
| Project Initiation | SRS Documentation | Initial requirements gathering and documenting system objectives, functional and non functional requirements, features and scope | 6-Sep-26 | 15-Sep-26 | Team |
| Project Initiation | System Architecture and UML Diagram Development | System architecture diagram, use case diagram, activity diagrams, sequence diagrams and class diagram | 6-Sep-26 | 15-Sep-26 | Team |
| Project Initiation | SRS Finalization | SRS final revisions, consistency checking and team review | 16-Sep-26 | 17-Sep-26 | Team |
| Project Initiation | SRS Submission | Approved and submitted SRS document | 16-Sep-26 | 17-Sep-26 | Project Manager |
| Project Initiation | Setup Development Environment and Tools | Git repository, project structure, development environment, development tools and AI integration environment | 21-Sep-26 | 23-Sep-26 | Full-Stack Developer |
| Project Initiation | Project Monitoring 1 | Progress report, project status, issues/risks log | 23-Sep-26 | 23-Sep-26 | Project Manager |
| Design Phase | System Design | High-level system design, module structure and system workflow | 24-Sep-26 | 27-Sep-26 | Software Architect |
| Design Phase | UI/UX Research and Wireframing | User flow, UI/UX research findings and low-fidelity wireframes | 4-Oct-26 | 10-Oct-26 | UI/UX Designer |
| Design Phase | UI/UX Mockup Design | High-fidelity UI mockups for household and government interfaces | 4-Sep-26 | 10-Sep-26 | UI/UX Designer |
| Design Phase | UI/UX Simulation | Interactive UI prototype and simulated user navigation flow | 4-Oct-26 | 10-Oct-26 | UI/UX Designer |
| Design Phase | AI Workflow Design | AI workflow, data flow, prompt/processing design and AI integration specifications | 11-Oct-26 | 13-Oct-26 | Software Architect |
| Design Phase | Design Database Schema | Entity relationship diagram, database tables, relationships, constraints and data dictionary | 11-Oct-26 | 13-Oct-26 | Database Architect |
| Design Phase | API Design | API endpoint specifications, request/response structures, authentication requirements and API documentation | 14-Oct-26 | 17-Oct-26 | Backend Developer |
| Design Phase | Project Monitoring 2 | Design progress report, updated project status and issues/risks log | 18-Oct-26 | 18-Oct-26 | Project Manager |
| Presentation | Prototype Presentation | Presentation of SRS, Diagrams, Business and Data flows and Software Prototype | 19-Oct-26 | 30-Oct-26 | — |
| Development Phase | Configure Database Access Layer | Configured database connection, ORM configuration, models, migrations and database access layer | 19-Oct-26 | 22-Oct-26 | Backend Developer |
| Development Phase | Authentication and Authorization Module Initialization | User authentication, registration, login, session management and authorization foundation | 5-Oct-26 | 9-Oct-26 | Backend Developer |
| Development Phase | Access Control Management Module | Role-based access control and household/government permission management | 8-Oct-26 | 10-Oct-26 | Backend Developer |
| Development Phase | Appliance Specification Log Module | Appliance library, appliance specifications, appliance usage records and daily consumption logs | 10-Oct-26 | 15-Oct-26 | Development Team |
| Development Phase | Consumption Simulation Module | Consumption calculator, future consumption simulator, usage inputs and simulated consumption results | 13-Oct-26 | 20-Oct-26 | Development Team |
| Development Phase | AI Automation Workflow Development | AI processing workflow, consumption analysis automation and AI recommendation integration | 16-Oct-26 | 22-Oct-26 | AI Engineer |
| Development Phase | Solar Feasibility & Validation Module | Utility bill validation, validation confidence score, solar feasibility assessment and solar system recommendation | 20-Oct-26 | 27-Oct-26 | Development Team |
| Development Phase | Consumption Reports and Analytics Module | Consumption analytics, usage breakdowns, consumption trends and household consumption reports | 24-Oct-26 | 29-Oct-26 | Development Team |
| Development Phase | ROI, Savings and Financing Modules | Solar savings estimates, ROI/payback analysis, what-if analysis and financing/incentive recommendations | 27-Oct-26 | 2-Nov-26 | Development Team |
| Development Phase | Project Monitoring 3 | Development progress report, project status, issues/risks log and completed module tracking | 2-Nov-26 | 2-Nov-26 | Project Manager |
| Development Phase | Data Collection and Forecasting Module | Historical consumption dataset, processed consumption records and forecasting/predictive model integration | 3-Nov-26 | 10-Nov-26 | AI Engineer |
| Development Phase | Government Panel and Analytics Module | Government dashboard, regional solar potential analytics, consumption aggregation and geographic analysis | 7-Nov-26 | 14-Nov-26 | Development Team |
| Development Phase | Validation Coverage Module | Regional validation coverage metrics, validation confidence aggregation and coverage analytics | 12-Nov-26 | 17-Nov-26 | Development Team |
| Development Phase | Government Reports Module | Regional demand-side planning reports, solar adoption reports and government analytics summaries | 15-Nov-26 | 19-Nov-26 | Development Team |
| Development Phase | Profile Management Module | Household profile management, property information, account settings and profile update functions | 18-Nov-26 | 21-Nov-26 | Development Team |
| Development Phase | Frontend and Backend Integration | Integrated frontend and backend modules, API integration, data flow integration and end-to-end feature connection | 20-Nov-26 | 25-Nov-26 | Development Team |
| Development Phase | Project Monitoring 4 | Development completion report, project status, issues/risks log and integration progress | 25-Nov-26 | 25-Nov-26 | Project Manager |
| Testing Phase | Unit & Integration Testing | Unit test results, integration test results, test cases and defect reports | 26-Nov-26 | 2-Dec-26 | QA Tester |
| Testing Phase | System Performance Optimization | Performance test results, optimized system components, database/query optimization and response-time improvements | 1-Dec-26 | 5-Dec-26 | Software Architect |
| Testing Phase | Progress Monitoring 5 | Testing progress report, defect tracking, project status and issues/risks log | 5-Dec-26 | 5-Dec-26 | Project Manager |
| Finalization | Finalize System Documentation | Final technical documentation, user documentation, API documentation and updated system diagrams | 7-Dec-26 | 11-Dec-26 | Documentation Specialist |
| Finalization | Software Deployment | Production-ready build, deployed system, deployment configuration and deployment documentation | 10-Dec-26 | 14-Dec-26 | Development Team |
| Finalization | Feedback and User Monitoring | User feedback forms, usability findings, feedback summary and system improvement recommendations | 15-Dec-26 | 18-Dec-26 | QA Tester |
| Finalization | Project Monitoring 6 | Final project progress report, project status, remaining issues and completion assessment | 18-Dec-26 | 18-Dec-26 | Project Manager |
| Presentation | Project Presentation Preparation | Presentation slides, system demonstration flow, technical presentation materials and speaker assignments | 19-Dec-26 | 22-Dec-26 | Team |
| Presentation | Project Presentation | Completed system demonstration, project presentation and presentation materials | 23-Dec-26 | 23-Dec-26 | Team |
| Closing | Final Review and Evaluation | Final system evaluation, quality review, evaluation results and final revisions | 24-Dec-26 | 26-Dec-26 | Team |
| Closing | Project Closure | Project completion report, final deliverables checklist and project closure documentation | 27-Dec-26 | 27-Dec-26 | Project Manager |
| Post-deployment | Project Portfolio Submission | Final project portfolio, source code, documentation, screenshots and project artifacts | 28-Dec-26 | 30-Dec-26 | Team |
| Post-deployment | System Maintenance | Maintenance plan, bug fixes, monitoring procedures and future enhancement recommendations | 2-Jan-27 | 9-Jan-27 | Development Team |

</details>

---

## Team & Roles

**Team LUXUS** — Manuel S. Enverga University Foundation, Lucena City

| Member | Primary Roles |
|---|---|
| **Jhon Lloyd M. Valencia** | Project Manager · Software Architect · Frontend Developer · Backend Developer · Documentation |
| **Kyle Allen M. Abandia** | Co-Project Manager · Software Architect · AI Agent Developer · Database Development · System Development · Frontend Developer · Backend Developer |
| **Maurenzio Franck M. Altamarino** | UI/UX Designer · Database Development · System Development · Frontend Developer |
| **Jerome Iloilo** | UI/UX Designer · Documentation |

*All four members share Development Team and QA Testing responsibilities across every module, per the [project plan](#project-plan--gantt-chart)'s "Development Team" / "QA Tester" assignments.*

---

## Documentation

| Document | Description |
|---|---|
| [`docs/paper.pdf`](docs/paper.pdf) | Midterm project paper — problem framing, conceptual data model, ER diagram |
| [`docs/srs.pdf`](docs/srs.pdf) | Software Requirements Specification v1.0 — functional/non-functional requirements, UI/UX conventions, class & sequence diagrams, use case diagram |
| [`docs/gantt-chart.csv`](docs/gantt-chart.csv) | Source-of-truth project timeline (reproduced in full above) |

---

## References

- Institute for Climate and Sustainable Cities. (2025, July 15). *Philippines has over 1,800MW potential solar capacity nationwide – ICSC.*
- Law.Asia. (2025, August 22). *Tapping free sunshine for Philippine energy.*
- Mahadevan, M., Meeks, R., & Yamano, T. (2023). *Reducing information barriers to solar adoption: Experimental evidence from India.* Energy Economics, 120.
- Manila Electric Company. (2026, July 10). *Higher residential rates this July 2026* [Press release].
- National Renewable Energy Laboratory. (n.d.). *PVWatts calculator.* U.S. Department of Energy.
- Neo, H. Y. R., Wong, N. H., Ignatius, M., & Cao, K. (2024). *A hybrid machine learning approach for forecasting residential electricity consumption: A case study in Singapore.* Energy & Environment, 35(8), 3923–3939.
- Presidential Communications Office. (2026, March 24). *President Marcos declares State of National Energy Emergency; activates UPLIFT as whole-of-government response framework.*
- Pinas Solar. (2026, July 22). *Meralco rate history Philippines (2015–2026): Monthly ₱/kWh data.*
- Rai, V., Reeves, D. C., & Margolis, R. (2016). *Overcoming barriers and uncertainties in the adoption of residential solar PV.* Renewable Energy, 89, 498–505.
- Reeves, D. C., Haley, M., Uyanna, A., & Rai, V. (2022). *Information interventions can increase technology adoption through information network restructuring.* iScience, 25(8).
- Republic Act No. 9513, Renewable Energy Act of 2008. (2008, December 16). Official Gazette of the Republic of the Philippines.
- SolarQuarter. (2026, February 11). *Philippines accelerates rooftop solar rollout with major overhaul of net metering regulations.*

---

## License

Private and proprietary — academic project for Information Management (Decision Support Systems). All rights reserved. Unauthorized use, reproduction, or distribution of any part of this codebase is strictly prohibited unless otherwise agreed with the team.

---

<div align="center">

<img src="assets/silangan-icon.png" alt="Silangan" width="64"/>

**Silangan** — Team LUXUS · Manuel S. Enverga University Foundation, Lucena City

*Replacing guesswork with a data-grounded answer.*

</div>
