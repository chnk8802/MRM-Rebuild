# Technology Stack

## Source of truth
This document is derived from the original `chnk8802/mrm` repository. That repository is READ-ONLY for this rebuild project.

## Monorepo
- Package manager: npm 11.4.2
- Workspace roots: `apps/*`, `packages/*`
- Task runner: Turborepo (`turbo`)
- Root scripts: `dev`, `build`, `lint`

## Frontend (`apps/client`)
- React 19.2
- React DOM 19.2
- Vite 7.3
- React Router DOM 6.15
- TanStack React Query 5
- Axios
- React Hook Form
- Zod + `@hookform/resolvers`
- Tailwind CSS 3.4
- shadcn-ui conventions / Radix UI primitives
- Lucide React icons
- react-hot-toast
- date-fns
- react-day-picker
- cmdk

The frontend is a Vite SPA, not Next.js. It uses JSX and ES modules.

## Backend (`apps/server`)
- Node.js using ES modules
- Express 4.18
- MongoDB through Mongoose 7.5
- JWT authentication via `jsonwebtoken`
- Password hashing via `bcryptjs`
- Cookie parsing via `cookie-parser`
- CORS
- Helmet security middleware
- dotenv
- Zod validation
- nodemon for local development

## Shared workspace package
`packages/validators` is consumed from both frontend and backend as `@repo/validators`. Reconstruction must preserve shared validation contracts rather than duplicating schemas independently.

## Deployment signals
The frontend contains `vercel.json`, indicating Vercel-oriented SPA deployment configuration. Exact production deployment behavior must be verified separately from repository configuration.

## Reconstruction requirements
1. Preserve the npm workspace/Turborepo structure unless a later architecture document explicitly records an intentional redesign.
2. Keep client and server as separate applications.
3. Keep validation contracts in a shared workspace package.
4. Use compatible versions or document any deliberate version upgrade and resulting code changes.
5. Never copy production secrets into this repository; use `.env.example` placeholders only.
