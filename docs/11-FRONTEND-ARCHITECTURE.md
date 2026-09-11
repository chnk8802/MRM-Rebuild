# Frontend Architecture

## Application shape
The client is a Vite-powered React 19 single-page application. Routing is handled by React Router, API calls by Axios, and server-state/data fetching is supported by TanStack React Query.

## Top-level source areas
Verified `apps/client/src` structure includes:
- `App.jsx` — route composition and access control
- `api/` — domain-specific API service modules
- `assets/` — bundled assets
- `components/` — reusable UI/layout components
- `config/` — browser-side configuration
- `context/` — React context, including auth state
- `hooks/` — reusable hooks such as role/permission checks
- `lib/` — shared helpers
- `pages/` — route-level screens
- `utils/` — utilities
- `index.css` — global/Tailwind styling
- `main.jsx` — application bootstrap

## Page domains
Verified route-level/page groupings:
- `Dashboard.jsx`
- `auth/`
- `common/`
- `customer/`
- `payments/`
- `repairOrder/`
- `reports/`
- `settings/`
- `superadmin/`
- `supplier/`
- `technician/`
- `users/`
- `website/`

The page organization largely mirrors backend business domains, which is useful for reconstruction: rebuild each feature vertically from shared validator -> API service -> backend route/controller/model -> page(s).

## API service layer
The frontend has explicit service modules rather than calling Axios directly everywhere. Verified modules:
- `authService.js`
- `axiosInstance.js`
- `customerService.js`
- `organizationService.js`
- `paymentService.js`
- `planService.js`
- `repairService.js`
- `reportService.js`
- `sparePartUsageService.js`
- `supplierService.js`
- `technicianService.js`
- `userService.js`

This service boundary should be preserved in the rebuild because it centralizes URL construction and HTTP behavior and keeps pages from becoming transport-aware.

## UI technology
Verified client dependencies include:
- Tailwind CSS
- Radix UI primitives
- shadcn-ui tooling
- Lucide icons
- React Hook Form
- Zod + hookform resolvers
- React Hot Toast
- `cmdk`
- React Day Picker / date-fns
- class-variance-authority, clsx, tailwind-merge

These dependencies indicate a component-library approach rather than custom raw HTML controls for every screen.

## Route protection
`App.jsx` provides nested protected routes. The frontend reads auth state from `AuthContext` and permission state from `usePermission()`.

The route hierarchy is role-aware:
- any authenticated role: dashboard, repairs, settings/profile;
- manager+: payments, customers, suppliers, technicians;
- admin+: users list/details and reports;
- admin but not superadmin: user create/edit;
- superadmin: organization management.

Route permissions do not always exactly match backend endpoint permissions; reconstruction must preserve both layers and test them independently.

## Recommended reconstruction strategy
Do not rebuild the entire frontend before the backend contracts exist. Use vertical slices:
1. restore shared validator package;
2. restore Axios instance/auth context;
3. restore one backend domain and its API contract;
4. restore that domain's service module;
5. restore list/detail/create/edit pages;
6. verify role gates and error/loading states;
7. move to the next domain.

This approach keeps each AI task small enough for limited context windows and makes acceptance testing possible after each domain.
