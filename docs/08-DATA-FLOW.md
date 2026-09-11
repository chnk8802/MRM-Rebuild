# Data Flow

## Payment creation flow
Verified from `payment.controller.js` and related models.

### Receivable payment
1. Manager-or-higher submits a payment with `type = receivable`, a customer, payment method, and one or more repair line items.
2. Request body is validated with shared Zod schema `paymentSchema`.
3. Subscription record-cap enforcement runs through `checkRecordCap()` before creating the Payment record.
4. Backend verifies the customer exists and is not soft deleted.
5. Each repair is loaded and validated:
   - repair must exist and not be soft deleted;
   - repair status must be in the eligible-for-payment set;
   - repair must not already be `paid`;
   - repair must not be `waived`;
   - submitted amount must not exceed remaining balance.
6. Repair total owed is computed as `serviceCharge - discount`.
7. Payment `totalAmount` equals the sum of submitted line-item amounts.
8. Inside a database transaction:
   - Payment document is created;
   - every repair's `amountPaid` is incremented;
   - repair `paymentStatus` is recalculated as unpaid / partial / paid;
   - Customer `outstandingBalance` is decreased by the payment total.
9. Newly-created Payment is reloaded with customer/supplier/recordedBy/line-item references populated.
10. API returns HTTP 201.

### Payable payment
The payable flow mirrors receivables, but line items reference `SparePartUsage` and the party is a Supplier.

For each spare-part usage:
- total owed = `unitCost * quantity`;
- remaining balance = total owed minus existing `amountPaid`;
- overpayment is rejected;
- the Supplier's `outstandingBalance` decreases when payment is recorded.

## Payment status algorithm
The verified helper behaves as follows:

```text
if total owed == 0       -> paid
else if amount paid <= 0 -> unpaid
else if amount paid >= total owed -> paid
else                     -> partial
```

This exact behavior matters for zero-value items and boundary conditions.

## Full-and-final settlement
Endpoint: `POST /api/payments/full-and-final`.

For receivables:
1. Load all outstanding eligible repairs for a customer.
2. Compute remaining amount for every repair.
3. Create one Payment containing one line item per outstanding repair.
4. Mark all participating repairs paid and increment their `amountPaid` values.
5. Set customer `outstandingBalance` to exactly zero.

For payables the same logic operates over outstanding SparePartUsage records and sets supplier `outstandingBalance` to zero.

If there are no outstanding items, the API rejects the request rather than creating a zero-value settlement.

All mutation steps are wrapped in a transaction helper. Reconstruction must preserve atomicity: a Payment must not be committed while related balances or line-item payment states fail to update.

## Outstanding preview flow
Two manager-or-higher endpoints support payment preparation:
- `/api/payments/outstanding-items`
- `/api/payments/outstanding-summary`

Both accept a payment `type` plus the matching customer or supplier identifier.

The items endpoint returns up to 100 outstanding source records.

The summary endpoint aggregates:
- outstanding record count;
- total remaining monetary amount.

Receivable remaining formula:
`(serviceCharge - discount) - amountPaid`

Payable remaining formula:
`(unitCost * quantity) - amountPaid`

## Organization scoping through the flow
Payment, Repair, SparePartUsage, Customer, and Supplier are organization-scoped models. Therefore normal model queries and aggregations receive the current organization filter automatically via the Mongoose plugin and request context.

This means payment processing is tenant-contained even when controllers do not manually include `orgId` in each query.

## Rebuild validation cases
- reject payment against nonexistent party;
- reject deleted party/source item;
- reject overpayment;
- reject ineligible repair status;
- reject paid or waived repair;
- correctly transition unpaid -> partial -> paid;
- full-and-final sets all included source records paid;
- party outstanding balance remains consistent;
- transaction rollback leaves no partial mutation;
- one tenant cannot pay or inspect another tenant's records.
