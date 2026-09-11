# Route Manifest

Status: initial verified frontend route inventory. Each route will later be expanded with API dependencies, UI states, permissions, source files, and acceptance tests.

## Public routes
| Route | Screen | Access |
|---|---|---|
| `/` | Website Home | Public |
| `/login` | Login | Anonymous only; authenticated users redirect to `/app` |
| `/unauthorized` | Access Denied | Public route used for permission failures |

## Authenticated routes
| Route | Screen | Minimum access |
|---|---|---|
| `/app` | Dashboard | Authenticated |
| `/app/repairs` | Repair List | Authenticated |
| `/app/repairs/new` | Repair Create | Authenticated |
| `/app/repairs/:id` | Repair Details | Authenticated |
| `/app/repairs/:id/edit` | Repair Edit | Authenticated |
| `/app/settings` | Settings | Authenticated |
| `/app/settings/profile` | Profile | Authenticated |

## Manager and above
| Route | Screen |
|---|---|
| `/app/payments` | Payment List |
| `/app/payments/new` | Payment Create |
| `/app/payments/:id` | Payment Details |
| `/app/customers` | Customer List |
| `/app/customers/new` | Customer Create |
| `/app/customers/:id` | Customer Details |
| `/app/customers/:id/edit` | Customer Edit |
| `/app/suppliers` | Supplier List |
| `/app/suppliers/new` | Supplier Create |
| `/app/suppliers/:id` | Supplier Details |
| `/app/suppliers/:id/edit` | Supplier Edit |
| `/app/technicians` | Technician List |

## Admin and above
| Route | Screen | Notes |
|---|---|---|
| `/app/users` | User List | admin+ |
| `/app/users/:id` | User Details | admin+ |
| `/app/reports` | Reports | admin+ |
| `/app/users/new` | User Create | admin+, but superadmin explicitly blocked |
| `/app/users/:id/edit` | User Edit | admin+, but superadmin explicitly blocked |

## Superadmin only
| Route | Screen |
|---|---|
| `/app/organizations` | Organization List |
| `/app/organizations/new` | Organization Create |
| `/app/organizations/:id` | Organization Details |

## Fallback
Unknown routes redirect to `/`.

## Authorization behavior
`ProtectedRoute` waits for auth loading, redirects unauthenticated users to `/login`, redirects insufficient roles to `/unauthorized`, and supports explicit role blocking. The role hierarchy is implemented through the permission hook and must be cross-verified against backend authorization middleware.
