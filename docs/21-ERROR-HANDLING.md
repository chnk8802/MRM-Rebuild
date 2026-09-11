# Error Handling

## Server pattern
The Express app mounts a centralized `handleError` middleware after all route modules. Controllers generally wrap logic in `try/catch` and forward failures to `next(error)`. Domain code uses a `createError(status, message)` helper for expected failures.

## Expected error classes
Reconstruction should preserve distinguishable outcomes for:
- 400 invalid input / invalid IDs / invalid operation state.
- 401 missing, invalid or stale authentication.
- 403 insufficient role.
- 404 missing tenant-scoped resource.
- validation failures from shared Zod schemas.
- database and transaction failures.
- subscription record-cap failures.

## Financial errors
Payment operations explicitly reject overpayment, already-paid items, waived repairs, ineligible repair statuses, missing parties and no-outstanding-balance full-and-final requests.

## Frontend behavior
The client should convert server failures into user-readable feedback, preserve form input where appropriate, and provide retry/recovery paths for transient reads. Authentication failures should transition the user back to the login flow rather than leave protected screens in a broken state.

## Reconstruction requirement
Do not reduce all failures to generic 500 responses. Preserve meaningful HTTP status and message semantics while ensuring internal stack traces and secrets are not leaked to production clients.
