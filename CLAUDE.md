# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Commands

```bash
npm install      # install dependencies
npm run dev      # start dev server at http://localhost:5173
npm run build    # production build
npm run lint     # run ESLint
npm run preview  # preview production build
```

## Architecture

This is a React app (Vite + React 19) split into focused components. `src/App.jsx` holds the top-level transaction state and renders the page layout — all UI logic lives in `src/components/`.

**Component structure:**
```
src/
├── App.jsx                          — transaction state, handleAdd, top-level layout
└── components/
    ├── Summary.jsx                  — computes totalIncome/totalExpenses/balance, renders cards
    ├── AddTransactionForm.jsx       — form state (description, amount, type, category) + submit
    ├── TransactionList.jsx          — filter state + filtered table
    └── TransactionItem.jsx          — single table row
```

There is no routing, no state management library, and no backend.

**Known intentional issues (part of the course):**
- Transaction #4 ("Freelance Work") is typed `"expense"` but categorized as `"salary"`.
- No delete functionality despite `.delete-btn` CSS being defined in `App.css`.
- UI styling is minimal/rough by design.

**Data shape** — each transaction:
```js
{ id, description, amount, type, category, date }
// type: "income" | "expense"
// category: "food" | "housing" | "utilities" | "transport" | "entertainment" | "salary" | "other"
// amount: Number
```

All state is in-memory only — no persistence across page reloads.
