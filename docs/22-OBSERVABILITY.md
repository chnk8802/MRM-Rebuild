# Observability

## Verified state
The inspected source shows centralized Express error handling, structured HTTP status codes, and client-side toast/UI error handling, but no verified dedicated observability vendor or telemetry SDK has been identified yet.

## Minimum reconstruction behavior
The rebuilt application must preserve:
- central Express error middleware
- meaningful HTTP status codes
- non-secret server error logging
- client-visible failure states
- React Query error propagation
- authentication failures as 401
- authorization failures as 403
- validation/domain failures with actionable messages

## Recommended production additions
These are operational recommendations, not claims about the original deployment:
- structured JSON request/error logs
- request correlation IDs
- uptime checks for API and client
- MongoDB connection monitoring
- error tracking for frontend and backend
- dashboards for authentication errors, 5xx rates, payment failures, and transaction failures

Do not add a third-party observability vendor during fidelity reconstruction unless explicitly chosen by the operator.

## Sensitive data rule
Never log passwords, JWT secrets, raw auth cookies, database credentials, or other secrets. Avoid logging full customer records where unnecessary.
