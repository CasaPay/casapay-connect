# CasaPay concepts

Shared vocabulary for all CasaPay Connect skills.

## Core objects

| Term | Meaning |
|------|---------|
| Operator | The landlord, property manager or coliving/PBSA operator using CasaPay. |
| Tenant | The person paying rent. |
| Property / unit | Where the tenancy is. Payment requests are tied to a tenant and a property. |
| Payment request | A tenant-ready invoice: amount, currency, due date, description (rent, deposit, fee) and a PDF invoice. |
| Payment link | The hosted checkout URL for a payment request, sent to the tenant by email or message. |
| Payment status | Lifecycle of a request (typical: draft → sent/open → paid, or overdue / failed / cancelled / refunded). Always use the exact statuses the connector returns. |
| Payout | The money CasaPay settles to the operator's bank account. One payout can cover several payments, net of any fees. |
| Collection / invoice | An amount a tenant owes. Statuses: unpaid, partial, paid, cancelled, rejected. |
| Payment agreement (PA) | The contract linking a tenant to the operator. Types: cover, ontime, payment, payment_link, guarantor and others. |
| Authorization hold | A payout leg, status created, pending, in_disbursement, settled, failed or cancelled. |

## Payment methods tenants can use

Payment links created through this plugin use card checkout. CasaPay also supports bank transfer and wallets outside this connector. The operator fee on base RentLink is 0%.

## Plans and guarantee products

| Plan | Operator cost | What it adds |
|------|---------------|--------------|
| RentLink | 0% operator fee | Payment requests, invoices, status tracking, reconciliation |
| Cover | From 1.5% of rent | RentLink + payment guarantee (one month of cover by default, higher cover available) |
| On-time | From 2.5% of rent | RentLink + guarantee + guaranteed payout timing (paid due date + 1 day, even if the tenant pays late) |

Prices are "from" figures. Never quote a price as final; the operator's contract and the connector's data take precedence.

## Rules of thumb

- Rent and deposit are different money: keep deposit requests separate from rent requests and label them clearly.
- Amounts: always show currency and two decimals. Do not convert currencies unless asked.
- Dates: show the due date and how many days early or late, in the operator's timezone when known.
