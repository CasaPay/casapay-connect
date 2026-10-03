---
name: rent-reconciliation
description: Reconciles CasaPay collections and payouts - what tenants paid, what CasaPay paid out, what is stuck and why - and exports the result. Use when the user says "reconcile rent", "have I been paid", "stuck payouts", "month-end close", "where is this payment" or "revenue summary".
---

# Payout and revenue reconciliation

Money moves in two steps: (1) the tenant pays CasaPay (invoice status), (2) CasaPay pays the operator (authorization hold: created, pending, in_disbursement, settled). Only `settled` with a `processed_at` means the money landed. "Have I been paid?" means step 2.

## Tools

- `get_payout_report`: settled vs stuck payouts, grouped by hold status, with missing payout IBANs flagged and a diagnosis. Filters: `status`, `unsettled_only`, `target_from`, `target_to`.
- `get_revenue_summary`: per-currency revenue for a date range.
- `get_invoice`: one invoice with `money_flow` (tenant leg and payout leg).
- `list_invoices`: lists to cross-check.

## Steps

1. Name the organisation and the currency. Never combine currencies.
2. Run `get_payout_report` (add dates for a period) and `get_revenue_summary` for the same range.
3. Summarize: settled, in disbursement, pending, failed, cancelled, with counts and per-currency totals from the tools.
4. Explain blockers using the report's diagnosis. If holds have no payout IBAN, the operator must add a bank account in CasaPay admin. List overdue holds (target date passed, not processed) separately from future ones.
5. If the user gives a bank statement, match payouts to bank credits by amount and date (+/-3 days) with code, and list unmatched lines.
6. For a spreadsheet, build Summary, Settled, Unsettled and Exceptions sheets with the xlsx skill.

## Rules

- Use tool totals. Don't re-add paginated results by hand.
- Read-only. Reconciliation never changes anything in CasaPay.
- Report nulls and unlinked payouts as they are.
