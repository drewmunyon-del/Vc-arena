# Workspace

## Overview

pnpm workspace monorepo using TypeScript. Each package manages its own dependencies.

## Stack

- **Monorepo tool**: pnpm workspaces
- **Node.js version**: 24
- **Package manager**: pnpm
- **TypeScript version**: 5.9
- **API framework**: Express 5
- **Database**: PostgreSQL + Drizzle ORM
- **Validation**: Zod (`zod/v4`), `drizzle-zod`
- **API codegen**: Orval (from OpenAPI spec)
- **Build**: esbuild (CJS bundle)

## Artifacts

### startup-simulator (React + Vite, path: `/`)
**VC Arena — Startup Competition Simulator**
- Dark neon theme (electric cyan primary, amber winners, red crashers)
- Auth via localStorage `currentUserId` — login screen picks identity from DB users
- User id=1 (Admin) is permanently protected: role cannot be changed or deleted
- Pages: Dashboard, Teams, Team Detail (recharts), Judge Panel (score sliders), Simulation (cinematic reveal), Leaderboard (rank change arrows), Admin Panel, User Management

### api-server (Express, path: `/api/*`)
- Drizzle ORM + PostgreSQL; all DB routes serialize Date objects to ISO strings before responding
- Zod used only for request body/param validation (not response parsing)
- Simulation engine: `artifacts/api-server/src/lib/simulation.ts` — 17 event types, 3 intensity levels, possible company collapse

## Seeded Data
- 6 users: Admin (admin), Sarah Chen (judge), Marcus Rivera (judge), Team Alpha, Team Beta (team_member), Guest Viewer (viewer)
- 6 startup teams: NeuralPay, GreenGrid, MediSync, SpaceLogix, EduPilot, CarbonVault
- Competition state: Round 1 of 3, medium intensity, judging phase

## Key Commands

- `pnpm run typecheck` — full typecheck across all packages
- `pnpm run build` — typecheck + build all packages
- `pnpm --filter @workspace/api-spec run codegen` — regenerate API hooks and Zod schemas from OpenAPI spec
- `pnpm --filter @workspace/db run push` — push DB schema changes (dev only)
- `pnpm --filter @workspace/api-server run dev` — run API server locally

See the `pnpm-workspace` skill for workspace structure, TypeScript setup, and package details.
