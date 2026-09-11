# Environment Variables

Verified backend environment loader: `apps/server/config/env.js`.

## Required variables

| Variable | Required | Default | Purpose |
|---|---|---|---|
| `MONGO_URI` | Yes | none | MongoDB connection string |
| `JWT_SECRET` | Yes | none | JWT signature verification/signing secret |
| `JWT_EXPIRE` | Yes | none | JWT lifetime/expiry configuration |
| `NODE_ENV` | Yes | none | Runtime environment; also drives development/production flags |
| `PORT` | No | `5000` | Backend HTTP port |

Startup throws immediately when any required variable is missing.

## Derived flags
The backend derives:
- `IS_DEVELOPMENT = NODE_ENV === 'development'`
- `IS_PRODUCTION = NODE_ENV === 'production'`

## Reconstruction `.env.example`
Use placeholders only; never commit production secrets.

```env
PORT=5000
MONGO_URI=<mongodb-connection-string>
JWT_SECRET=<generate-a-long-random-secret>
JWT_EXPIRE=<for-example-7d>
NODE_ENV=development
```

## Reconstruction requirements
- Preserve fail-fast validation for required variables.
- Do not hard-code secrets.
- Search the remaining client/server code for additional direct `process.env` or `import.meta.env` access before treating this list as complete.
- Document any client-side variable with its exposure implications; Vite variables intended for browser use must be handled as public configuration, not secrets.
