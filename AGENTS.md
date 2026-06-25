# TalentScout

Full-stack talent recruitment platform. Two independent packages (no monorepo tooling).

## Stack

- **Backend:** NestJS 11, PostgreSQL 17, Drizzle ORM, Bun
- **Frontend:** Next.js 16, React 19, Tailwind CSS v4, Bun
- **All UI text, seed data, and Swagger descriptions are in Spanish**

## Commands

Work in `talentscout-backend/` or `talentscout-front/` — no root scripts.

| Action | Backend | Frontend |
|--------|---------|----------|
| Install | `bun install` | `bun install` |
| Dev server (port 3000) | `bun run start:dev` | — |
| Dev server (port 3001) | — | `bun dev` |
| Build | `bun run build` | `bun run build` |
| Lint | `bun run lint` | `bun run lint` |
| Format | `bun run format` | (not configured) |
| Tests | `bun run test` (unit, Jest) | (none) |
| E2E | `bun run test:e2e` | (none) |
| Docker DB up | `bun run docker:up` | — |
| DB generate migration | `bun run db:generate` | — |
| DB migrate | `bun run db:migrate` | — |
| DB seed | `bun run db:seed` | — |

## Backend — key facts

- **Tests use Jest** (configured inline in `package.json`, transform via `ts-jest`). `*.spec.ts` files live alongside code or under `test/` for e2e.
- **Swagger** at `/api` (auto-generated from decorators).
- **ValidationPipe** global (whitelist, forbidNonWhitelisted, transform).
- **Database** requires PostgreSQL; `docker compose up -d` (or `bun run docker:up`) starts it.
- **Seed data has a merge conflict** in `src/db/seed.ts` — two implementations are separated by `<<<<<<< HEAD` / `=======` / `>>>>>>> 369bb5a`. Resolve before running `bun run db:seed`.
- **No auth/guards** implemented yet — roles table exists but is not enforced.
- Most controllers use `any` for DTOs (only `applicants` has `class-validator` + Swagger DTOs).
- Module pattern: `Module -> Controller -> Service -> Repository`.
- `.env` is committed with dev creds (`postgres/postgres`).

## Frontend — key facts

- **No testing setup** — no test runner installed.
- **React Compiler** enabled (`next.config.ts`: `reactCompiler: true`).
- **Tailwind v4** — uses `@tailwindcss/postcss` (not classic PostCSS plugin).
- **Path alias** `@/*` maps to `./src/*`.
- Pages contain hardcoded demo data (jobs, candidates) — not yet connected to the API.
- **Bun** is the runtime (`bun dev`, `bun build`).

## Conventions

- All new code and responses should be in **Spanish**.
- **Bun** is the package manager and runtime for both packages (never `npm`/`yarn`).
