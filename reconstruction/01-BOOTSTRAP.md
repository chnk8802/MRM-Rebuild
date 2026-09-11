# Phase 01 — Bootstrap

## Goal
Create the monorepo skeleton and toolchain without implementing business features.

## Create
- Root `package.json` with npm workspaces for `apps/*` and `packages/*`.
- Root Turbo configuration and scripts for `dev`, `build`, and `lint`.
- `apps/client` Vite/React application.
- `apps/server` Node/Express ES-module application.
- `packages/validators` shared package.
- `.gitignore` and `.env.example` placeholders.

## Client baseline
Install React 19, React DOM, Vite, React Router, Axios, React Query, React Hook Form, Zod/resolvers, Tailwind/PostCSS, Radix primitives, Lucide, toast utilities and class helpers matching `docs/23-DEPENDENCIES.md`.

## Server baseline
Install Express, Mongoose, dotenv, jsonwebtoken, bcryptjs, cookie-parser, cors, helmet, Zod and the shared validators package.

## Acceptance criteria
- `npm install` succeeds from root.
- `npm run dev` starts client and server through Turbo.
- Client renders a placeholder route.
- Server responds on `/`.
- Shared validators package can be imported from both client and server.
- No feature logic is added yet.
