# System Architecture

## Overview
MRM is a JavaScript monorepo for a mobile-repair business application. The verified source structure separates a React/Vite frontend from an Express/MongoDB backend and shares validation through a workspace package.

```text
Browser
  -> React/Vite SPA (`apps/client`)
      -> React Router protected routes
      -> Axios / React Query API calls
          -> Express API (`apps/server`)
              -> authentication/authorization middleware
              -> route modules
              -> controllers/services
              -> Mongoose models
                  -> MongoDB

Shared validation:
  `packages/validators` -> client + server
```

## Backend request pipeline
The Express application applies Helmet, permissive credentialed CORS, JSON/urlencoded parsers, and cookie parsing before mounting domain routes. A central `handleError` middleware is mounted after the API routes.

Verified API mount points:
- `/api/platform/organizations`
- `/api/platform/plans`
- `/api/auth`
- `/api/users`
- `/api/technicians`
- `/api/customers`
- `/api/suppliers`
- `/api/repairs`
- `/api/spare-part-usage`
- `/api/payments`
- `/api/reports`
- `/api/organizations`

The server source is organized into `config`, `controllers`, `middleware`, `models`, `routes`, `services`, `utils`, `scripts`, and `blueprints`.

## Frontend architecture
The client is a React SPA with these major source areas:
- `api/` — HTTP/API access
- `components/` — reusable UI and layout components
- `config/` — client configuration
- `context/` — React context, including authentication
- `hooks/` — reusable hooks including permission checks
- `lib/` — shared library helpers
- `pages/` — route-level screens
- `utils/` — utility functions
- `assets/` and `public/` — static assets

`App.jsx` is the verified route composition root. It uses nested React Router routes and a `ProtectedRoute` wrapper.

## Authorization model
The frontend explicitly describes a hierarchical role model matching backend authorization behavior:

```text
staff < manager < admin < superadmin
```

Authenticated users can access the dashboard, repair workflows, and settings. Manager-or-higher users receive payments, customers, suppliers, and technician workflows. Admin-or-higher users receive user listing/details and reports. Superadmins receive platform organization management. Some user-create/edit routes explicitly block the `superadmin` role, indicating organization-admin-only behavior that must be preserved exactly during reconstruction.

## Rebuild rule
This document describes verified architecture only. Detailed database schemas, controller behavior, role middleware, API payloads, and screen behavior must be derived from their source files before implementation begins.
