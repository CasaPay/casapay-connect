---
name: rent-guarantee
description: Shows CasaPay payment agreements - Cover and On-time guarantees, payment links, guarantors - with cover amounts and status, and changes agreement status when asked. Use when the user asks "is this tenant covered", "list agreements", "rent guarantee", "Cover vs On-time", "close this agreement" or "what's covered".
---

# Agreements and guarantees

Read `../payment-links/references/casapay-concepts.md` for plan details.

## Tools

- `list_payment_agreements`: filter by `agreement_type` (cover, ontime, payment, payment_link, guarantor, tnt_guarantor, agreement_only, complete_package), `status` (active, signing, closed, terminated, imported, draft) and `tenant_email`. Rows show monthly rent, `cover_amount`, start, end and predicted end.
- `transition_payment_agreement`: changes status through the official state machine. Illegal transitions are rejected. Needs `confirm=true` and an `idempotency_key`.

## Coverage check

1. Find the tenant's agreements by email or by type.
2. Report type, status, cover amount, start and end. An agreement of type `cover` or `ontime` carries a guarantee. `payment_link` and `payment` do not.
3. Flag tenants with overdue invoices and no active cover or ontime agreement (cross-check with `list_invoices`).
4. For late rent on a guaranteed tenancy, show the invoice with `get_invoice`. Its `money_flow` shows whether CasaPay has paid the operator.

## Closing or changing an agreement

State the agreement reference, current status and target status. Closing stamps an end date automatically and can't always be undone. Wait for an explicit yes, then call with `confirm=true`.

## Limits

The connector has no claims tool. For a claim on unpaid rent, send the user to CasaPay support. Subscription fees for the guarantee service are CasaPay's own invoices to the tenant and aren't visible here. Prices are "from" figures. This is product information, not insurance or legal advice.
