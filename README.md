# ledger-finance-dashboard
 
A clean, interactive finance dashboard built with vanilla JavaScript and Chart.js.
 
---
 
## Tech Stack
 
| Layer | Choice | 
|---|---|---|
| Language | Vanilla JavaScript (ES6+) | 
| Charts | Chart.js 4.4 | 
| Fonts | Google Fonts (Syne, DM Sans, DM Mono) | 
| Styling | Pure CSS with custom properties | 
| State | In-memory JS object + localStorage | 
 
---
 
## Architecture
 
```
finance-dashboard.html
│
├── <style>          CSS custom properties for theming, all component styles
├── <body>           Semantic HTML — sidebar, header, three view panels, modal
└── <script>
    ├── STATE        Single source of truth (transactions, filters, role, theme)
    ├── SEED         48 realistic mock transactions across Aug–Dec 2024
    ├── Computed     getTotals(), getMonthlyData(), getCategoryData(), getFiltered()
    ├── Render       renderAll(), renderSummaryCards(), renderTxnTable(), renderInsights()
    ├── Charts       initCharts() — 4 charts, rebuilt on theme/data change
    ├── CRUD         openModal(), submitForm(), editTxn(), deleteTxn()
    └── Export       exportCSV()
```
 
---
 
## Features Implemented
 
### 1 · Dashboard Overview
- **3 Summary Cards** — Total Balance, Income, Expenses with change indicators and savings rate
- **Area Chart** — 6-month income vs expense trend (Chart.js)
- **Donut Chart** — Spending by category with a percentage legend
- Recent transactions table (last 6)
 
### 2 · Transactions
- Full table with 48 seeded transactions across 5 months
- **Search** — real-time fuzzy search on description and category
- **Filter** — by category (9 options) and by type (income / expense)
- **Sort** — newest, oldest, highest amount, lowest amount
- Live result count showing filtered vs total
- Edit and delete (Admin only)
 
### 3 · Role-Based UI
Roles are switched via the dropdown in the header. No page reload needed.
 
| Feature | Admin | Viewer |
|---|---|---|
| Add transaction button |  Visible |  Hidden |
| Edit / delete row actions |  Visible |  Hidden |
| Export CSV | Allowed | Allowed |
| View all data | Allowed | Allowed |
 
Sidebar avatar, name, and access label also update to reflect the active role.
 
### 4 · Insights
- **Category breakdown** — ranked list with visual progress bars and percentages
- **Month-over-Month** — income/expense comparison Dec vs Nov, savings rate gauge
- **5 Key Observations** — auto-generated text insights from the data (top category, best month, expense trend, savings health, transaction volume)
- **Bar Chart** — income vs expense per month, side-by-side
- **Savings Rate Line Chart** — % saved per month trend
 
### 5 · State Management
Single `STATE` object drives all UI. Three layers:
1. **In-memory** — fast reads/writes, all JS operations
2. **localStorage** — persists transactions, role, and theme across page reloads
3. **Derived state** — computed on demand (totals, filters, chart data) — never stored
 
### 6 · UI / UX
- **Dark / Light mode** — full CSS custom property swap, charts rebuild with new colours
- **Responsive** — 3-column grid collapses to 2 → 1 on mobile; sidebar becomes off-canvas drawer with hamburger toggle
- **Empty states** — filter results zero state, no data fallback
- **Keyboard shortcuts** — `Esc` to close modal, `N` to open add-transaction (when admin, not in input)
- **Modal** — click backdrop or Esc to close, required field validation
- Smooth `fadeUp` animation on view transitions
 
### 7 · Bonus
- **CSV Export** — downloads all transactions as a properly quoted CSV file
- **Data persistence** — localStorage keeps your added/edited/deleted transactions and preferences
- 48 realistic mock transactions (INR, Indian context — Swiggy, DMart, BSNL, Cult.fit etc.)
- Scrollbar styling, hover transitions, micro-animations throughout
 
---
 
##  Views
 
```
Overview       — summary cards + area chart + donut chart + recent 6 transactions
Transactions   — full filterable / sortable table + add/edit modal (admin)
Insights       — observations + bar comparison + savings rate trend
```
 
---
 
##  Category Colour System
 
Each of the 9 spending categories has a consistent background/text colour pair used across all tables, charts, and legends for instant visual pattern recognition.
 
---
 
##  Known Limitations / Assumptions
 
- All data is mock / static seed data for demonstration
- No real authentication — role switching is client-side only
- Chart.js loads from CDN; Google Fonts require internet access
- Tested on Chrome 120+, Firefox 121+, Safari 17+
 
---
 
##  What I'd Add Next
 
- React rewrite with proper component tree and Zustand for state
- REST API with Express + PostgreSQL
- Real auth with JWT / OAuth
- Date range picker for custom period filtering
- Recurring transaction detection
- Budget goals and alerts
- PWA support (offline-first with IndexedDB)
