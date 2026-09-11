# Environment Manifest

## Server

| Variable | Required | Default | Purpose | Source |
|---|---:|---|---|---|
| `PORT` | No | `5000` | Express listen port | `apps/server/config/env.js` |
| `MONGO_URI` | Yes | — | MongoDB connection string | `apps/server/config/env.js` |
| `JWT_SECRET` | Yes | — | JWT signing/verification secret | `apps/server/config/env.js` |
| `JWT_EXPIRE` | Yes | — | JWT lifetime | `apps/server/config/env.js` |
| `NODE_ENV` | Yes | — | Runtime mode; derives development/production flags | `apps/server/config/env.js` |

## Client

| Variable | Required | Default | Purpose | Source |
|---|---:|---|---|---|
| `VITE_API_URL` | No | `/api` | Axios API base URL | `apps/client/src/api/axiosInstance.js` |

## Runtime state/config not stored as environment variables
- `x-org-id` request header — selected superadmin organization context.
- `ORG_STORAGE_KEY` — shared constant used to store selected organization in browser localStorage.
- auth token cookie named `token` — consumed by backend authentication middleware.

## Secret handling
Never commit live values. Use `.env.example` placeholders only. Generate a strong `JWT_SECRET` separately for each environment.

## Reconstruction acceptance
- Server must fail fast if any required variable is missing.
- Client must function with same-origin `/api` when `VITE_API_URL` is unset.
- Cross-origin environments must preserve `withCredentials: true` behavior and compatible CORS/cookie configuration.
