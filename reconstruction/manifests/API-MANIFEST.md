# API Manifest

This manifest captures verified backend endpoints and role thresholds. `min role` means the backend's hierarchical `authorize()` middleware accepts that role and any higher role.

## Auth — `/api/auth`
| Method | Path | Min role | Handler |
|---|---|---|---|
| POST | `/register` | public | `registerUser` |
| POST | `/login` | public | `loginUser` |
| POST | `/logout` | public route | `logoutUser` |
| GET | `/profile` | authenticated | `getProfile` |
| PATCH | `/profile` | authenticated | `updateProfile` |
| PATCH | `/profile/password` | authenticated | `updatePassword` |

## Repairs — `/api/repairs`
| Method | Path | Min role | Handler |
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

## Customers — `/api/customers`
| Method | Path | Min role | Handler |
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

## Suppliers — `/api/suppliers`
| Method | Path | Min role | Handler |
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

## Payments — `/api/payments`
| Method | Path | Min role | Handler |
|---|---|---|---|
| GET | `/stats` | manager | `getPaymentStats` |
| POST | `/full-and-final` | manager | `createFullAndFinalPayment` |
| GET | `/outstanding-items` | manager | `getOutstandingItems` |
| GET | `/outstanding-summary` | manager | `getOutstandingSummary` |
| GET | `/` | manager | `getPayments` |
| POST | `/` | manager | `createPayment` |
| GET | `/:id` | manager | `getPaymentById` |

## Spare part usage — `/api/spare-part-usage`
| Method | Path | Min role | Handler |
|---|---|---|---|
| POST | `/bulk` | staff | `bulkCreateSparePartUsage` |
| PATCH | `/bulk` | admin | `bulkUpdateSparePartUsage` |
| GET | `/` | staff | `getSparePartUsages` |
| POST | `/` | staff | `createSparePartUsage` |
| GET | `/:id` | staff | `getSparePartUsageById` |
| PATCH | `/:id` | manager | `updateSparePartUsage` |
| DELETE | `/:id` | manager | `deleteSparePartUsage` |

## Users — `/api/users`
| Method | Path | Min role | Handler |
|---|---|---|---|
| GET | `/stats` | admin | `getUserStats` |
| GET | `/` | admin | `getUsers` |
| POST | `/` | admin | `createUser` |
| GET | `/:id` | staff | `getUserById` |
| PATCH | `/:id` | admin | `updateUser` |
| DELETE | `/:id` | admin | `deleteUser` |
| PATCH | `/:id/restore` | **no authorize middleware in verified route** | `restoreUser` |
| PATCH | `/:id/deactivate` | admin | `deactivateUser` |
| PATCH | `/:id/activate` | admin | `activateUser` |
| DELETE | `/:id/permanent` | superadmin | `deleteUserPermanently` |
| PATCH | `/:id/reset-password` | admin | `resetPassword` |

> Reconstruction warning: `/:id/restore` is behind `protect` because the router applies it globally, but the verified route does not call `authorize()`. Treat this as observed behavior and verify whether it is intentional before changing it.

## Technicians — `/api/technicians`
| Method | Path | Min role | Handler |
|---|---|---|---|
| GET | `/` | manager | `getTechnicians` |

## Reports — `/api/reports`
| Method | Path | Min role | Handler |
|---|---|---|---|
| GET | `/owed` | manager | `getOwedReport` |
| GET | `/collected` | manager | `getCollectedReport` |

## Other mounted domains still requiring endpoint-level extraction
- `/api/organizations`
- `/api/platform/organizations`
- `/api/platform/plans`

## Cross-cutting behavior
- All protected routes use JWT authentication.
- JWT may come from cookie or Bearer header.
- Tenant scope is injected through model middleware using request context.
- Superadmin may select a tenant using `x-org-id`.
- Validation is largely shared through `@repo/validators` Zod schemas.
