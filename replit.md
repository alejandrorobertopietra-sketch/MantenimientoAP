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

## Key Commands

- `pnpm run typecheck` — full typecheck across all packages
- `pnpm run build` — typecheck + build all packages
- `pnpm --filter @workspace/api-spec run codegen` — regenerate API hooks and Zod schemas from OpenAPI spec
- `pnpm --filter @workspace/db run push` — push DB schema changes (dev only)
- `pnpm --filter @workspace/api-server run dev` — run API server locally

See the `pnpm-workspace` skill for workspace structure, TypeScript setup, and package details.

## CMMS Application

**OpsCMMS** — Industrial Maintenance Management System

### Artifacts
- `artifacts/cmms` — React + Vite frontend (port from PORT env, preview at `/`)
- `artifacts/api-server` — Express 5 REST API (port 8080)

### Features Built
- Auth: Session-based login (express-session + SHA-256+salt), roles: admin/supervisor/technician
- Assets: CRUD + history, types: machine/electrical/installation/water_tank/office/zone
- Work Orders: Create/list/detail, types: preventive/corrective/incident, priority/status tracking, parts consumed
- Preventive Plans: Schedule-based maintenance plans with auto work-order generation
- Parts: Inventory management with minimum stock alerts
- Stock Movements: In/out tracking, auto-decrement on work order parts
- Dashboard: Summary KPIs + recent activity + upcoming maintenance
- Users: CRUD (admin only), role management, active/inactive toggle
- Layout: Desktop sidebar + mobile bottom tab nav + slide-out sheet

### Database (PostgreSQL via Drizzle ORM)
Tables: users, assets, work_orders, work_order_parts, preventive_plans, parts, stock_movements, activity_log

### Seed Data
- 5 users: admin/admin123, jperez/supervisor1, clopez/tecnico1, mgarcia/tecnico2, rrodriguez/tecnico1
- 10 assets, 10 parts, 6 work orders, 5 preventive plans

### Pages
- `/` — Login
- `/dashboard` — KPI cards, activity feed, upcoming maintenance, quick actions
- `/assets` — Asset list with status/type filters
- `/assets/new` — Create asset
- `/assets/:id` — Asset detail + history
- `/work-orders` — Work order list with status/type/priority filters
- `/work-orders/new` — Create work order
- `/work-orders/:id` — Detail + parts + status change
- `/preventive` — Preventive plans + generate OT
- `/parts` — Parts inventory + create/edit dialog
- `/stock` — Stock movements + register movement dialog
- `/users` — User management (admin only)
