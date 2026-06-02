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

This is a single-component React app (Vite + React 19). All state and logic lives in `src/App.jsx` — there are no child components, no routing, no state management library, and no backend.

**Known intentional issues (part of the course):**
- Bug: `amount` is stored as a string in state, so `reduce` concatenates instead of summing — the Income/Expenses/Balance totals are wrong.
- Transaction #4 ("Freelance Work") is typed `"expense"` but categorized as `"salary"`.
- No delete functionality despite `.delete-btn` CSS being defined in `App.css`.
- UI styling is minimal/rough by design.

**Data shape** — each transaction:
```js
{ id, description, amount, type, category, date }
// type: "income" | "expense"
// category: "food" | "housing" | "utilities" | "transport" | "entertainment" | "salary" | "other"
// amount: stored as string (the bug), should be Number
```

All state is in-memory only — no persistence across page reloads.
