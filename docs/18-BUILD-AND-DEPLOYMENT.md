# Build and Deployment

## Monorepo build
The source repository is an npm workspace managed with Turbo.

Root scripts:
- `npm run dev` -> `turbo run dev`
- `npm run build` -> `turbo run build`
- `npm run lint` -> `turbo run lint`

Client scripts:
- `vite --host`
- `vite build`
- `eslint .`
- `vite preview`

Server scripts:
- `node server.js`
- `nodemon server.js`
- `node scripts/index.js` for plan seeding

## Client deployment
The client contains `vercel.json`, so Vercel-compatible SPA deployment is part of the verified source shape. The reconstructed client must preserve SPA fallback behavior and provide `VITE_API_URL` when the API is not served under the same `/api` origin.

## Server deployment requirements
The Express service requires:
- Node.js runtime compatible with the verified dependencies
- `MONGO_URI`
- `JWT_SECRET`
- `JWT_EXPIRE`
- `NODE_ENV`
- optional `PORT` (defaults to 5000)

The server must be able to reach MongoDB and must run behind HTTPS in production when cookie authentication is used.

## Cross-origin behavior
The verified Express app enables credentialed CORS. The frontend Axios instance sets `withCredentials: true`. Production deployment must therefore configure origins/cookies consistently; do not deploy the frontend/API to incompatible origins without testing authentication cookies.

## Recommended rebuild deployment sequence
1. Provision MongoDB.
2. Deploy API with required environment variables.
3. Run plan seeding if the platform requires initial plans.
4. Verify API root and authentication endpoints.
5. Deploy Vite client.
6. Set `VITE_API_URL` to the API base when required.
7. Verify credentialed login/logout/profile flow.
8. Verify superadmin `x-org-id` requests.
9. Run the validation checklist in `reconstruction/10-VALIDATION.md`.

## Unknown/external deployment details
The repository alone does not prove the exact production hosting provider for the server, MongoDB provider, DNS configuration, TLS termination, backups, or secret-management system. These must be supplied by the operator and must not be fabricated during reconstruction.
