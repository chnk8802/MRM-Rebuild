# Feature Inventory

This inventory is derived from the source tree, frontend routes, backend routes, models, and shared validation package. Status labels mean **verified in source**, not reconstruction-complete.

## Public website and authentication
- Public home page (`/`)
- Login (`/login`)
- Logout API
- Registration API
- Current-user profile read/update
- Current-user password update
- Unauthorized page

## Dashboard
- Authenticated dashboard at `/app`
- Detailed dashboard widgets/data sources still require page/controller tracing.

## Repair management
- Repair list
- Create repair
- Repair details
- Edit repair
- Assign technician
- Update repair status
- Mark repair pickup
- Repair statistics
- Soft-delete/permanent-delete behavior in backend
- Organization-specific sequential repair IDs
- Service charge and discount tracking
- Amount-paid and payment-status tracking
- Spare-part usage relationship

## Customer management
- Customer list
- Create customer
- Customer details
- Edit customer
- Customer statistics
- Bulk update
- Bulk delete
- Soft delete
- Restore
- Permanent delete
- Active/inactive state
- Outstanding receivable balance
- Customer type classification

## Supplier management
- Supplier list
- Create supplier
- Supplier details
- Edit supplier
- Supplier statistics
- Bulk update
- Bulk delete
- Soft delete
- Restore
- Permanent delete
- Active/inactive state
- Outstanding payable balance

## Technician workflow
- Technician list
- Technicians are represented through the User domain rather than a separate Technician database model.
- Repair assignment targets a User reference.

## User administration
- User list
- Create user
- User details
- Edit user
- User statistics
- Soft delete
- Restore
- Permanent delete
- Activate/deactivate
- Administrative password reset
- Role assignment
- Organization membership for every non-superadmin user

## Payments
- Payment list
- Create payment
- Payment details
- Receivable payments from customers
- Payable payments to suppliers
- Multi-line-item payment allocation
- Partial/unpaid/paid payment-state calculation
- Outstanding-items query
- Outstanding-summary query
- Full-and-final settlement
- Payment statistics
- Payment method tracking
- Payment notes/date/recording-user tracking

## Spare-part usage
- Create individual usage
- Bulk create usage
- List usage
- Usage details
- Update individual usage
- Bulk update
- Delete usage
- Link spare parts to repairs
- Optional supplier relationship
- Quantity and unit-cost tracking
- Amount-paid/payment-status tracking
- Installed-by/installed-at tracking

## Reports
- Owed report
- Collected report
- Frontend Reports screen is restricted to admin-or-higher, while verified backend report endpoints currently require manager-or-higher. This discrepancy must be preserved or deliberately resolved during rebuild validation.

## Organizations / platform administration
- Superadmin organization list
- Create organization
- Organization details
- Platform-level organization API
- Platform plan API
- Organization subscription plan
- Subscription expiry
- Record-count accounting
- Cap override flag
- Superadmin global vs selected-tenant access through `x-org-id`

## Settings
- Settings screen
- Profile screen

## Multi-tenant SaaS infrastructure
- Organization-scoped Mongoose models
- Automatic model-level tenant filtering
- Automatic tenant stamping on new records
- Tenant-scoped aggregations
- Superadmin global access
- Superadmin selected-tenant access
- Subscription record counting
- Shared cross-client/server Zod validation package

## Pending feature-level tracing
The following still need exact UI/API/controller-level documentation:
- dashboard metrics;
- organization plan-management behavior;
- exact report calculations;
- repair status transition rules;
- customer/supplier balance increment rules on creation/edit of source transactions;
- all search/filter/sort/pagination options;
- all frontend loading/empty/error/toast states;
- responsive UI behavior;
- settings behavior;
- external integrations, if any.
