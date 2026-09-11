# UI / UX Specification

## Current verified UI architecture
The frontend is a React/Vite SPA using Tailwind CSS, Radix UI primitives, shadcn-style components, Lucide icons, React Hook Form, React Hot Toast and React Router.

The authenticated shell uses:
- `components/Layout/Layout.jsx`
- `components/Layout/Sidebar.jsx`
- `components/Layout/Topbar.jsx`

The page hierarchy includes Dashboard plus auth, customer, payment, repair, report, settings, superadmin, supplier, technician, user and website page groups.

## Global interaction requirements
- Unauthorized unauthenticated access redirects to `/login`.
- Permission failures redirect to `/unauthorized`.
- Loading states must exist while auth state resolves.
- Route visibility and navigation visibility must reflect role hierarchy.
- Forms must use the shared validation semantics rather than duplicating incompatible rules.
- Server errors should surface as actionable UI feedback without leaking sensitive details.

## Screen groups to reproduce
### Public
- Marketing home page.
- Login page.
- Access-denied page.

### Authenticated common
- Dashboard.
- Settings.
- Profile.
- Repair list/create/details/edit.

### Manager+
- Payment list/create/details.
- Customer list/create/details/edit.
- Supplier list/create/details/edit.
- Technician list.

### Admin+
- User list/details.
- Reports.
- Admin-only user create/edit behavior as implemented by source routing.

### Superadmin
- Organization list/create/details.

## Layout specification status
The existence and composition boundaries of Layout, Sidebar and Topbar are verified. Exact spacing, color tokens, mobile breakpoints, menu collapse behavior, table layout, dialog sizing, empty states and per-screen field arrangement still require page-by-page source extraction.

## Reconstruction rule
Do not invent a new design system. First reproduce the existing visual hierarchy and interaction patterns from source. Any redesign should be a separate, explicitly approved phase after parity.
