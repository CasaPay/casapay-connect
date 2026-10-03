---
name: rent-collection-status
description: Reports CasaPay collection status - overdue invoices, ageing buckets, who has or hasn't paid - and drafts tenant reminders. Use when the user asks "who hasn't paid rent", "collection status", "overdue tenants", "arrears report", "has X paid" or "chase late payers".
---

# Collection status

Read `../payment-links/references/casapay-concepts.md` first. Keep the two legs of money apart: collection (tenant paid CasaPay) and payout (CasaPay paid the operator).

## Tools

- `get_overdue_report`: ageing buckets (1-7, 8-30, 31-60, 60+ days) and per-currency totals, plus the largest overdue invoices. Use it for any portfolio question and use its totals as given.
- `list_invoices`: filters for `status`, `overdue`, `tenant_email`, `tenant_name`, `type` (regular = rent, one_time = payment requests) and due or created dates. Use for "has X paid?" and for lists.
- `get_invoice`: one invoice in full, with a `money_flow` summary of both legs.

## Steps

1. Call `list_organisations` if the user might have several, and name the organisation in the answer.
2. Run the report or list that answers the question. Never add up amounts across calls or currencies yourself.
3. Lead with a one-line summary, then a table: tenant, invoice no., amount, due date, days overdue, agreement.
4. Say which leg a status refers to. If the tenant has paid but the payout hasn't settled, point to the `rent-reconciliation` skill.
5. Report nulls as they are (e.g. tenant name missing).
6. `list_invoices` returns `outstanding_by_currency` for the returned rows only, so with a small `limit` it is not the portfolio total. For totals use `get_overdue_report`, or raise `limit` to 100 and say when results may be truncated.

## Chasing

The connector can't send messages. Draft a short, polite reminder per tenant (amount, due date, invoice number), firmer as the delay grows but never threatening. If the invoice has no open link, offer `create_checkout_session`. The user sends the messages.
