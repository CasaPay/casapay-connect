# CasaPay Connect plugin

Rent FinOps for rental operators, powered by [CasaPay](https://casapay.com): payment links, collections, guarantees and payout reconciliation.

## What it does

| Skill | What to ask |
|-------|-------------|
| Payment requests | "Create a payment link for anna@example.com, EUR 850, October rent" |
| Collection status | "Who is overdue?" / "Draft reminders for the late payers" |
| Payment guarantee | "Is this tenant covered?" / "List my active Cover agreements" |
| Reconciliation | "Have I been paid? What payouts are stuck?" |

Any action that creates links or changes agreements is shown as a preview first and runs only after you confirm.

## Connector

The plugin connects to CasaPay's remote MCP server:

- `https://connect.casapay.com/mcp/casapay` (streamable HTTP)

Sign in with your CasaPay operator account when Claude asks you to connect.

## Works in

Claude Cowork, Claude Code and claude.ai.
