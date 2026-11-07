---
title: Tech stack and rules every ticket follows
summary: Next.js + TypeScript strict, Drizzle + Postgres (PGlite in tests), vitest, pnpm; JSON error shape; maths unrounded until display.
reviewed: 2026-11-08
---
# Tech stack and rules

Decided for the whole project (Jira epic BL-1). Do not change these in a ticket; raise it instead.

## Stack
- Next.js (App Router) + TypeScript, `strict: true`
- pnpm is the only package manager
- Postgres through Drizzle ORM. Tests use PGlite (in-memory Postgres), so tests never need a database server
- vitest; `pnpm test` runs every test once (no watch mode)
- Deploy: Vercel; production database: Neon Postgres via `DATABASE_URL`

## Rules
- Every API error is JSON: `{ "error": { "code": "snake_case_code", "message": "Plain sentence." } }`, using the shared error helper
- Rates, money and statistics stay unrounded in code; round only in API responses or the UI
- Every new behaviour ships with tests; a ticket's acceptance criteria are its test list
- No secrets in the repository; configuration comes from environment variables
