# Feature-to-File Map

This map connects major product features to verified source areas so a reconstruction AI can work feature-by-feature.

## Authentication
Frontend:
- `apps/client/src/pages/auth/`
- `apps/client/src/context/AuthContext.jsx`
- `apps/client/src/api/authService.js`
- `apps/client/src/App.jsx`

Backend:
- `apps/server/routes/auth.routes.js`
- `apps/server/controllers/auth.controller.js`
- `apps/server/middleware/auth.middleware.js`
- `apps/server/models/user.model.js`

Shared:
- `packages/validators/src/schemas/auth.schema.js`
- user constants/schemas

## Users / technicians
Frontend:
- `pages/users/`
- `pages/technician/`
- `api/userService.js`
- `api/technicianService.js`

Backend:
- `routes/user.routes.js`
- `routes/technician.routes.js`
- `controllers/user.controller.js`
- `models/user.model.js`

## Organizations / plans
Frontend:
- `pages/superadmin/organization/`
- `api/organizationService.js`
- `api/planService.js`
- `components/common/OrgSelector.jsx`

Backend:
- `routes/organization.routes.js`
- `routes/platformRoutes/organization.routes.js`
- `routes/platformRoutes/plan.routes.js`
- `controllers/organization.controller.js`
- `controllers/plan.controller.js`
- `models/organization.model.js`
- `models/plan.model.js`

## Repairs
Frontend:
- `pages/repairOrder/`
- `api/repairService.js`

Backend:
- `routes/repair.routes.js`
- `controllers/repair.controller.js`
- `models/repair.model.js`
- repair calculation/filter utilities

Shared:
- `packages/validators/src/schemas/repair.schema.js`
- repair constants

## Customers
Frontend:
- `pages/customer/`
- `api/customerService.js`

Backend:
- `routes/customer.routes.js`
- `controllers/customer.controller.js`
- `models/customer.model.js`

Shared:
- `customer.schema.js`
- customer constants

## Suppliers
Frontend:
- `pages/supplier/`
- `api/supplierService.js`

Backend:
- `routes/supplier.routes.js`
- `controllers/supplier.controller.js`
- `models/supplier.model.js`

Shared:
- `supplier.schema.js`

## Spare-part usage
Frontend:
- feature UI within repair flows plus `api/sparePartUsageService.js`

Backend:
- `routes/sparePartUsage.routes.js`
- `controllers/sparePartUsage.controller.js`
- `models/sparePartUsage.model.js`

Shared:
- `sparePartUsage.schema.js`

## Payments
Frontend:
- `pages/payments/`
- `api/paymentService.js`

Backend:
- `routes/payment.routes.js`
- `controllers/payment.controller.js`
- `models/payment.model.js`
- `utils/payment.filters.js`
- `utils/repair.calculations.js`
- transaction helpers

Shared:
- `payment.schema.js`
- payment constants

## Reports / dashboard
Frontend:
- `pages/reports/Reports.jsx` or report page family
- `pages/Dashboard.jsx`
- `api/reportService.js`

Backend:
- `routes/report.routes.js`
- `controllers/report.controller.js`
- stats endpoints across domain controllers

## Shared UI / navigation
- `components/Layout/`
- `components/common/`
- `components/ui/`
- `hooks/usePermission*`
- `context/ThemeContext.jsx`

## Cross-cutting tenant/security infrastructure
- `middleware/auth.middleware.js`
- `middleware/rbac.middleware.js`
- `utils/common/requestContext.js`
- `utils/common/orgScope.plugin.js`
- `utils/common/checkRecordCap.js`
- `models/organization.model.js`

## Reconstruction use
For any feature, read its frontend, backend, model, and shared-validator rows together. Do not reconstruct from a page file alone because important rules live in models, middleware, and shared validators.
