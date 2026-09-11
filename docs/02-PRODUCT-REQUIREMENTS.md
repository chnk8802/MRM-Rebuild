# Product Requirements

## Purpose
Provide a mobile-repair business with one operational system for customer intake, repair tracking, technician assignment, spare parts, collections/payables, reporting, staff administration, and organization-level SaaS management.

## User types
- Public visitor: can access the public website and login page.
- Staff: authenticated operational user; can access repair/customer-level workflows allowed by backend RBAC.
- Manager: includes staff permissions plus higher-level repair/payment/supplier/technician operations.
- Admin: organization administrator with user/report/statistics capabilities.
- Superadmin: platform-level operator with organization management and cross-tenant selection capabilities.

## Core requirements
### Authentication
- Login/logout.
- Protected profile retrieval/update.
- Password update.
- JWT-based session behavior compatible with cookie or Bearer-token authentication.

### Repairs
- Create, view, edit, assign technician, update status, mark pickup, obtain statistics.
- Generate organization-scoped repair IDs.
- Track payment status, service charge, discount, amount paid, completion, pickup, accessories, notes, due date, IMEI/device details.

### Customers and suppliers
- Search/list/details/create/update.
- Soft deletion, restoration, permanent deletion where allowed.
- Outstanding-balance tracking.
- Bulk operations where exposed by the API.

### Spare parts
- Record spare-part usage against repairs.
- Link optional supplier and installer.
- Track quantity, unit cost, payment status and amount paid.
- Bulk create/update support.

### Payments
- Receivable and payable payment types.
- Allocate payments across line items.
- Prevent overpayment.
- Maintain line-item payment status and party outstanding balance.
- Support full-and-final settlement.
- Provide outstanding-item and summary previews.

### Reporting
- Provide owed and collected reports.
- Preserve organization scoping.

### Multi-tenancy / SaaS
- Scope normal users to their organization.
- Allow superadmin organization selection through request context.
- Enforce subscription record caps for cap-counting models.
- Manage organizations and plans at platform level.

## Non-functional requirements
- Tenant isolation must be enforced server-side, not only in UI.
- Authorization must be enforced on the server.
- Shared validation contracts should remain centralized.
- Destructive operations should preserve current soft-delete semantics unless explicitly documented otherwise.
- Rebuild must include deterministic setup, environment documentation, validation tests, and acceptance criteria.
