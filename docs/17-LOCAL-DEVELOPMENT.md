# Local Development

## Prerequisites
- Node.js compatible with the repository's npm tooling.
- npm 11.x or compatible.
- MongoDB instance accessible through `MONGO_URI`.

## Install
From repository root:
```bash
npm install
```

The root workspace includes `apps/*` and `packages/*` and uses Turbo.

## Required server environment
Create a server environment file with at least:
```env
PORT=5000
MONGO_URI=<mongodb-connection-string>
JWT_SECRET=<secure-secret>
JWT_EXPIRE=<jwt-expiry>
NODE_ENV=development
```

Do not commit real secrets.

## Run
Root development command:
```bash
npm run dev
```

Verified root script delegates to `turbo run dev`. Client dev uses `vite --host`; server dev uses `nodemon server.js`.

## Build
```bash
npm run build
```

## Lint
```bash
npm run lint
```

## Local verification
- API root responds with `Mobile Repair API Running...`.
- Frontend loads public home route `/`.
- `/login` renders for unauthenticated users.
- Protected `/app` redirects to login when unauthenticated.
- Authenticated API calls include cookies or Bearer token.
- MongoDB writes for tenant-scoped entities include an organization context.

## Seed support
The server exposes a `seed:plans` script (`node scripts/index.js`). Inspect and reproduce plan seed behavior before relying on platform organization creation.
