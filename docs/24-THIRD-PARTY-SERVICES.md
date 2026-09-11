# Third-Party Services

## Verified external/runtime dependencies
The inspected code requires or integrates with the following external/runtime systems:

### MongoDB
Persistence is implemented with Mongoose. `MONGO_URI` is required by the server.

### Browser localStorage
Used for superadmin selected-organization persistence and theme-related client state.

### Vercel-compatible frontend hosting
The client contains `vercel.json`. This proves deployment compatibility/configuration exists in the source, but does not prove the current production account or domain.

### Avatar placeholder service
The user model defaults `avatar` to `https://i.pravatar.cc`. Treat this as a convenience default rather than a critical platform dependency.

## Libraries that are not external account integrations
Radix UI, shadcn-style components, Lucide, React Query, Axios, Zod, React Hook Form, date-fns, bcryptjs, JWT, Helmet, and related packages are code dependencies, not hosted service accounts.

## Not verified in the inspected source
No confirmed payment gateway, email provider, SMS provider, object-storage provider, analytics platform, error-monitoring vendor, or external authentication provider has been identified in the audited source so far.

## Reconstruction rule
Do not invent SaaS integrations. If a future source file proves an external service, add it here with:
- service name
- exact feature using it
- environment variables
- account/configuration steps
- failure behavior
- local-development substitute, if any
