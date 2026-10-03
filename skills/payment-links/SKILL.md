---
name: payment-links
description: Creates CasaPay payment links and card checkout sessions for one-off payments (rent, deposits, fees) and checks submitted payment requests. Use when the user says "create a payment link", "send a rent link", "bill tenant X", "get a checkout link for this invoice", "payment requests that failed" or "invoice the deposit".
---

# Payment links and checkout sessions

Read `references/casapay-concepts.md` for terms.

## Tools

- `create_payment_link`: one-off card checkout link for a tenant email, amount and title. Creates or reuses the tenant, the agreement and the invoice, and returns a gateway.casapay.com URL. Needs `confirm=true` and an `idempotency_key`.
- `create_checkout_session`: checkout link for an EXISTING invoice (`invoice_id`).
- `list_payment_requests`: invoices submitted by email alias or manually, before they become Collections. Use `without_invoice=true` to find requests that never produced an invoice, and report the failure reasons exactly as returned (null means unknown).
- `list_invoices`: use first to check for an existing open invoice, so you don't create duplicates.

## Creating a payment link

1. Collect: payer email, amount (in the organisation's currency, check with `list_organisations`), title shown to the payer, optional due date (default 14 days) and optional phone.
2. Check `list_invoices` with `tenant_email` for an open invoice for the same purpose. If there is one, offer `create_checkout_session` instead.
3. Show a preview (payer, amount and currency, title, due date) and wait for an explicit yes.
4. Call the tool with `confirm=true` and a fresh `idempotency_key`. Reuse the same key only when retrying the same request.
5. Return the URL. The tools don't email the tenant, so tell the user to share the link themselves.

For several links, list them all in one preview table and confirm once.

## Don'ts

- Never set `confirm=true` without the user's agreement.
- Don't invent tenants, amounts or links.
- Only card checkout is available through the connector. Don't promise bank transfer or wallet links.
