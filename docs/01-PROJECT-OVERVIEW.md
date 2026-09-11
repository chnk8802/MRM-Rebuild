# Project Overview

## Product
MRM is a multi-tenant mobile repair management SaaS application. It combines a public website, authenticated operational dashboard, organization administration, repair workflow management, customer/supplier ledgers, payments, spare-part usage, reports, users, technicians, and platform-level organization/plan management.

## Verified architecture
- Monorepo managed with npm workspaces + Turbo.
- `apps/client`: React 19 + Vite SPA.
- `apps/server`: Express 4 API + Mongoose/MongoDB.
- `packages/validators`: shared Zod schemas and constants used by client and server.
- Multi-tenant data isolation is enforced through request context plus a Mongoose org-scope plugin.
- Authentication uses JWT accepted from an HTTP cookie or Bearer token.
- Roles are hierarchical: guest < staff < manager < admin < superadmin.

## Primary business domains
1. Authentication and profiles.
2. Users and technicians.
3. Customers.
4. Suppliers.
5. Repairs.
6. Spare-part usage.
7. Receivable and payable payments.
8. Reports.
9. Organizations and subscription plans.
10. Public marketing website and authenticated application shell.

## Reconstruction objective
Recreate observable behavior and source-verified business rules from an empty repository without relying on the original code at runtime. The original `chnk8802/mrm` repository is reference-only and must never be modified.

## Known reconstruction risk areas
- Exact UI styling and responsive behavior still require page-by-page extraction.
- Some controller-level rules still require full extraction.
- External production infrastructure and secrets are not recoverable from source alone.
- Any apparent source inconsistency must be documented before deciding whether the rebuild should preserve or correct it.
