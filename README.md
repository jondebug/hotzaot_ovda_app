# הקרן המשפחתית — Family Shared Fund

A single-page web app for tracking shared finances across three couples (איתי ויסמין, ניר ואופרי, הילה ויונתן). Each couple is entitled to exactly one third of the pool's net profit; the app computes who is owed what and suggests minimal settle-up transfers.

## Run

Just open `index.html` in any modern browser — no build, no server.

```sh
open index.html
```

All data is stored in the browser's `localStorage` under the key `familyFund.v1`.

## Features

- **Dashboard** — total profit, total income, total expenses, share per couple
- **Balance Board** — per-couple balance with status (מקבל/חייב/מאוזן)
- **Settle-up** — greedy suggestions: most-negative pays most-positive
- **Transactions** — add / edit / delete shared income, shared expenses, and transfers
- **History** — searchable, filterable by type and couple
- **Export / Import** — JSON backup so data can survive a cleared cache or move between devices
- **Clear All** — destructive action gated by a typed-confirmation modal

## Math

```
totalProfit       = Σ income − Σ expenses
targetPerCouple   = totalProfit / 3
balance(couple)   = targetPerCouple
                  − (income_received − expenses_paid)
                  + (transfers_paid  − transfers_received)
```

Sign convention: **positive** = the couple is owed by the pool, **negative** = the couple owes the pool. Transfers move balances toward zero without changing total profit. Sum of balances is always 0 (within floating-point tolerance).

## Tech

- HTML / Tailwind CSS (Play CDN) / [Alpine.js](https://alpinejs.dev) for reactivity
- Heebo font, Hebrew RTL layout, `Intl.NumberFormat('he-IL', { style: 'currency', currency: 'ILS' })`
- No build step, no transpilation, no React, no dependencies to install
