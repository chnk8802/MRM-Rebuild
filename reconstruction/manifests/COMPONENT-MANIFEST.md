# Component Manifest

This manifest maps verified frontend component families from the source repository.

## Application shell
- `apps/client/src/components/Layout/Layout.jsx` — authenticated application shell
- `apps/client/src/components/Layout/Sidebar.jsx` — role-aware navigation/sidebar
- `apps/client/src/components/Layout/Topbar.jsx` — top application bar

## Common reusable components
Verified under `apps/client/src/components/common/`:
- `AsyncComboBox.jsx` — asynchronous/selectable entity lookup
- `Can.jsx` — permission-aware conditional rendering
- `ConfirmDialog.jsx` — destructive/confirmation interaction
- `DatePicker.jsx`
- `DateRangePicker.jsx`
- `DateTimePicker.jsx`
- `DateTimeRangePicker.jsx`
- `FilterPopover.jsx`
- `FilterSelect.jsx`
- `OrgSelector.jsx` — superadmin organization context selection
- `PageHeader.jsx`
- `RowActions.jsx`
- `TableFooter.jsx`
- `ThemeSelector.jsx` — present in source directory inventory

## UI primitives
`apps/client/src/components/ui/` contains the shadcn/Radix-style primitive layer. Reconstruct these before feature pages so page code can use stable primitives.

## Context/state components
- `apps/client/src/context/AuthContext.jsx`
- `apps/client/src/context/ThemeContext.jsx`

## Route protection / permissions
- `ProtectedRoute` in `apps/client/src/App.jsx`
- `usePermission` hook under `apps/client/src/hooks/`
- `Can.jsx` for component-level permission rendering

## Page families
- Dashboard
- Authentication
- Common/error pages
- Customers
- Payments
- Repairs
- Reports
- Settings/profile
- Superadmin organizations
- Suppliers
- Technicians
- Users
- Public website/home

## Reconstruction rules
1. Build primitive UI components first.
2. Build common components next.
3. Build authenticated shell and contexts.
4. Build route-level pages last.
5. Preserve permission checks both at route and component level.
6. Do not replace reusable source patterns with one-off page implementations.

## Remaining deep-detail work
Exact props, column definitions, loading/empty states, and page-specific compositions should be extracted per component/page if pixel/behavioral parity is required.
