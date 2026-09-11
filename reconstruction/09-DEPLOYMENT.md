# Phase 09 — Deployment

## Goal
Prepare reproducible production deployment without embedding environment-specific secrets in source.

## Verified deployment clues
- The client repository contains `vercel.json`.
- Client is a Vite SPA.
- Server is a standalone Node/Express process requiring MongoDB and environment variables.

## Deployment requirements
- Build client with Vite.
- Configure SPA fallback/routing so nested React Router URLs resolve correctly.
- Deploy server as a Node service capable of persistent MongoDB access.
- Configure `MONGO_URI`, `JWT_SECRET`, `JWT_EXPIRE`, `NODE_ENV`, and optional `PORT` through secret/environment management.
- Confirm cookie attributes and CORS policy for the actual frontend/backend domains.
- Run plan seed/setup if required for a fresh environment.

## Production checks
- HTTPS only.
- Secure JWT secret.
- No development stack traces returned to clients.
- CORS does not unintentionally allow hostile origins with credentials.
- Database backups and restore process exist.
- Health check endpoint responds.
- Logging captures server errors without secrets.

## Acceptance criteria
A clean deployment from documentation succeeds without consulting the original repository or undocumented console settings, except for infrastructure credentials explicitly listed as external prerequisites.
