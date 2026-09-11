# API Reference

> This is a verified, progressively extracted API map from the read-only source repository. Payload schemas and controller-side business rules will be added as their implementations are inspected.

## Base application routes

The Express app mounts these API roots:

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

All routes below are relative to those mount points.

## Authentication

Base: `/api/auth`

| Method | Path | Auth | Handler |
|---|---|---|---|
| POST | `/register` | Public | `registerUser` |
| POST | `/login` | Public | `loginUser` |
| POST | `/logout` | Public route definition | `logoutUser` |
| GET | `/profile` | `protect` | `getProfile` |
| PATCH | `/profile` | `protect` | `updateProfile` |
| PATCH | `/profile/password` | `protect` | `updatePassword` |

Note: logout is not wrapped by `protect` at the route definition level. Preserve source behavior unless controller inspection proves an intentional hidden requirement.

## Repairs

Base: `/api/repairs`. All repair routes first apply `protect`.

| Method | Path | Minimum role | Handler |
|---|---|---|---|
| GET | `/stats` | manager | `getRepairStats` |
| GET | `/` | staff | `getRepairs` |
| POST | `/` | manager | `createRepair` |
| GET | `/:id` | staff | `getRepairById` |
| PATCH | `/:id` | manager | `updateRepair` |
| DELETE | `/:id` | superadmin | `deleteRepair` |
| PATCH | `/:id/assign` | manager | `assignTechnician` |
| PATCH | `/:id/status` | staff | `updateRepairStatus` |
| PATCH | `/:id/pickup` | staff | `pickupRepair` |

Important permission asymmetry: staff may update repair status and pickup state, while creation/general edits require manager. Deletion requires superadmin.

## Customers

Base: `/api/customers`. All customer routes apply `protect`.

| Method | Path | Minimum role | Handler |
|---|---|---|---|
| GET | `/stats` | admin | `getCustomerStats` |
| PATCH | `/bulk` | manager | `bulkUpdateCustomers` |
| POST | `/bulk` | admin | `bulkDeleteCustomers` |
| GET | `/` | staff | `getCustomers` |
| POST | `/` | staff | `createCustomer` |
| GET | `/:id` | staff | `getCustomerById` |
| PATCH | `/:id` | staff | `updateCustomer` |
| DELETE | `/:id` | admin | `deleteCustomer` |
| PATCH | `/:id/restore` | admin | `restoreCustomer` |
| DELETE | `/:id/permanent` | superadmin | `permanentlyDeleteCustomer` |

This confirms soft-delete + restore + permanent-delete behavior, with escalating permissions.

## Suppliers

Base: `/api/suppliers`. All supplier routes apply `protect`.

| Method | Path | Minimum role | Handler |
|---|---|---|---|
| GET | `/stats` | admin | `getSupplierStats` |
| PATCH | `/bulk` | admin | `bulkUpdateSuppliers` |
| POST | `/bulk` | admin | `bulkDeleteSuppliers` |
| GET | `/` | staff | `getSuppliers` |
| POST | `/` | admin | `createSupplier` |
| GET | `/:id` | staff | `getSupplierById` |
| PATCH | `/:id` | manager | `updateSupplier` |
| DELETE | `/:id` | admin | `deleteSupplier` |
| PATCH | `/:id/restore` | admin | `restoreSupplier` |
| DELETE | `/:id/permanent` | superadmin | `permanentlyDeleteSupplier` |

## Payments

Base: `/api/payments`. All payment routes apply `protect`. Every verified payment operation currently requires manager or above.

| Method | Path | Minimum role | Handler |
|---|---|---|---|
| GET | `/stats` | manager | `getPaymentStats` |
| POST | `/full-and-final` | manager | `createFullAndFinalPayment` |
| GET | `/outstanding-items` | manager | `getOutstandingItems` |
| GET | `/outstanding-summary` | manager | `getOutstandingSummary` |
| GET | `/` | manager | `getPayments` |
| POST | `/` | manager | `createPayment` |
| GET | `/:id` | manager | `getPaymentById` |

The API explicitly models outstanding balances and a specialized full-and-final payment flow; these must be reconstructed as distinct business operations rather than reduced to generic payment CRUD.

## Remaining route modules to extract in detail

- users
- technicians
- reports
- organization tenant routes
- platform organization routes
- platform plan routes
- spare-part usage

For each remaining module, this file must ultimately contain: HTTP method, path, auth, minimum role, request body, query params, response shape, error cases, model side effects, and frontend callers.
