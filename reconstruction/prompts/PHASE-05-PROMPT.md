# Phase 05 Prompt — Frontend Shell

Execute only `reconstruction/05-FRONTEND-SHELL.md`.

Read `docs/11-FRONTEND-ARCHITECTURE.md`, `docs/12-UI-UX-SPECIFICATION.md`, `docs/15-STATE-MANAGEMENT.md`, `reconstruction/manifests/COMPONENT-MANIFEST.md`, and `ROUTE-MANIFEST.md`.

Implement the Vite/React application shell, React Router setup, AuthContext, ThemeContext, Axios instance, React Query provider, role-aware ProtectedRoute behavior, Layout/Sidebar/Topbar, common reusable components, and UI primitives required by later pages.

Preserve selected-org localStorage + `x-org-id` injection and `withCredentials: true`. Do not build all domain pages yet. Validate login routing, unauthorized routing, shell responsiveness, role-aware navigation, and organization selection behavior.