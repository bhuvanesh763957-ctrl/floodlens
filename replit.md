# FloodLens

A bilingual flood-intelligence and disaster-management web app for Tamil Nadu, with sourced weather, an interactive map, and public community reports.

## Run & Operate

- `pnpm --filter @workspace/api-server run dev` — run the API server (port 5000)
- `pnpm --filter @workspace/floodlens run dev` — run the FloodLens web app
- `pnpm --filter @workspace/floodlens run typecheck` — typecheck the FloodLens frontend
- `pnpm run typecheck` — full typecheck across all packages
- `pnpm run build` — typecheck + build all packages
- `pnpm --filter @workspace/api-spec run codegen` — regenerate API hooks and Zod schemas from the OpenAPI spec
- `pnpm --filter @workspace/db run push` — push DB schema changes (dev only)
- Required env: `DATABASE_URL` — Postgres connection string

## Stack

- pnpm workspaces, Node.js 24, TypeScript 5.9
- API: Express 5
- DB: PostgreSQL + Drizzle ORM
- Validation: Zod (`zod/v4`), `drizzle-zod`
- API codegen: Orval (from OpenAPI spec)
- Build: esbuild (CJS bundle)

## Where things live

- `artifacts/floodlens/` — React/Vite app, route pages, map, weather, and reporting flows
- `artifacts/api-server/src/routes/reports.ts` — community report and summary endpoints
- `lib/api-spec/openapi.yaml` — API contract source of truth
- `lib/db/src/schema/communityReports.ts` — persisted community report schema

## Architecture decisions

- Open-Meteo provides public forecast/current-weather fields; weather data is not treated as proof of flooding or an official warning.
- Community reports are public, anonymous, and unverified on submission. Verification is not exposed as a public write action.
- Official announcements, warnings, verified contacts, and facility operating status remain unavailable until a reliable source is connected.

## Product

- Overview, Tamil Nadu map, weather, reports and report tracking, district announcements, route guidance, nearby services, emergency guidance, notification permissions, and English/Tamil preferences.

## User preferences

- Never present sample or community-submitted flood data as verified live operational data.
- Never invent government announcements, flood warnings, emergency numbers, or facility status.

## Gotchas

- Re-run API code generation after every OpenAPI change.
- The frontend is served at `/`; API calls use the shared `/api` service path.

## Pointers

- See the `pnpm-workspace` skill for workspace structure, TypeScript setup, and package details
