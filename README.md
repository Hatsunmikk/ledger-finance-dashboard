# ledger-finance-dashboard

A finance dashboard built with vanilla JS and Chart.js. Single HTML file, no build step needed.

---

## Running it

Just open `finance-dashboard.html` in a browser. That's it.

If you want a local server for any reason:
```bash
npx serve .
# or
python3 -m http.server 8080
```

---

## Stack

- Vanilla JavaScript (ES6+)
- Chart.js 4.4 for charts
- Google Fonts — Syne, DM Sans, DM Mono
- Pure CSS with custom properties for theming
- localStorage for persistence

No frameworks, no npm install required.

---

## How it's structured

Everything lives in `finance-dashboard.html`:

```
finance-dashboard.html
│
├── <style>     all component styles, CSS variables for dark/light theme
├── <body>      sidebar, header, three view panels, add/edit modal
└── <script>
    ├── STATE       single source of truth — transactions, filters, role, theme
    ├── SEED        48 mock transactions seeded across Aug–Dec 2024
    ├── Computed    getTotals(), getMonthlyData(), getCategoryData(), getFiltered()
    ├── Render      renderAll(), renderSummaryCards(), renderTxnTable(), renderInsights()
    ├── Charts      initCharts() — 4 charts, rebuilt on theme or data change
    ├── CRUD        openModal(), submitForm(), editTxn(), deleteTxn()
    └── Export      exportCSV()
```

I kept it all in one file intentionally — easier to run, easier to review. In a real project this would be split into components.

---

## Features

**Overview**
- Balance, Income, Expenses summary cards with savings rate indicator
- 6-month area chart (income vs expenses)
- Spending breakdown donut chart with category legend
- Recent transactions table

**Transactions**
- 48 seeded transactions across 5 months
- Search, filter by category and type, sort by date or amount
- Live count of filtered vs total results
- Edit and delete — admin only

**Role-based UI**

Roles switch via the dropdown in the header, no reload needed.

| | Admin | Viewer |
|---|---|---|
| Add transaction | yes | no |
| Edit / delete | yes | no |
| View data | yes | yes |
| Export CSV | yes | yes |

The sidebar avatar and access label also update when you switch roles.

**Insights**
- Category spending breakdown with percentage bars
- Month-over-month comparison (income, expenses, net savings)
- Savings rate progress bar
- Auto-generated observations from the data
- Bar chart and savings rate trend line

**State management**

Single `STATE` object as the source of truth. Derived values (totals, filtered list, chart data) are computed on demand rather than stored. localStorage syncs on every mutation so your data survives page reloads.

**UI stuff**
- Dark and light mode — full CSS variable swap, charts rebuild with new colours
- Responsive — sidebar goes off-canvas on mobile with a hamburger toggle
- Empty states for zero filter results
- Keyboard shortcuts: `Esc` closes modal, `N` opens add transaction (admin only, when not in an input)
- Fade animation on view transitions

**Extras**
- CSV export of all transactions
- 48 realistic transactions in INR — Swiggy, DMart, BSNL, Cult.fit etc.

---

## Known limitations

- All data is mock — no real backend
- Role switching is client-side only, no real auth
- Chart.js and fonts load from CDN so you need internet
- Tested on Chrome 120+, Firefox 121+, Safari 17+

---

## What I'd do differently with more time

- Rewrite in React with proper component separation
- Add a real backend — Express + PostgreSQL
- Proper auth instead of the client-side role toggle
- Date range picker for filtering by period
- Budget targets and alerts
- PWA / offline support with IndexedDB
