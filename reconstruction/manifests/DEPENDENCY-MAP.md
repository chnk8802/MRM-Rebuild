# Dependency Map

## Workspace graph

```text
root mobile-repair-app
├── apps/client
│   └── depends on @repo/validators
├── apps/server
│   └── depends on @repo/validators
└── packages/validators
```

Root orchestration uses Turbo and npm workspaces.

## Client dependency groups
Runtime/framework:
- React 19
- React DOM 19
- React Router DOM 6
- Vite

Data/API:
- Axios
- TanStack React Query

Forms/validation:
- React Hook Form
- `@hookform/resolvers`
- Zod
- `@repo/validators`

UI:
- Tailwind CSS
- Radix UI primitives
- shadcn-style generated primitives
- class-variance-authority
- clsx
- tailwind-merge
- tailwindcss-animate
- Lucide React
- cmdk

Date/UI utilities:
- date-fns
- react-day-picker

Notifications:
- react-hot-toast

## Server dependency groups
HTTP/security:
- Express 4
- Helmet
- CORS
- cookie-parser

Persistence:
- Mongoose 7

Authentication:
- jsonwebtoken
- bcryptjs

Validation/config:
- Zod
- dotenv
- `@repo/validators`

Development:
- nodemon

## Architectural dependency rules
- Client and server both import domain constants/schema definitions from `@repo/validators`.
- Models depend on shared constants for enums.
- Controllers depend on models, validation schemas, and utility helpers.
- Routes depend on controllers plus auth/RBAC middleware.
- Client pages depend on API service modules, reusable components, React Query, and shared validators.
- Axios instance is the client transport root and injects tenant context.
- Tenant-scoped Mongoose models depend on request context through `orgScopePlugin`.

## Rebuild ordering implied by dependencies
1. Workspace/root config.
2. Shared validators/constants.
3. Server environment/database utilities.
4. Models and tenant plugin.
5. Middleware.
6. Controllers/services.
7. Routes/app/server entrypoint.
8. Client UI primitives/common components.
9. Context/API layer.
10. Feature pages/routes.
11. Tests and deployment.
