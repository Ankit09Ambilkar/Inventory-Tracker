### Internship at CODTECH IT SOLUTIONS PVT.LTD
### Intern ID - CITS6571

# IMS Pro — SQL Inventory Tracker

A single-page inventory management dashboard with a simulated login flow, product CRUD (Create, Read, Update, Delete), low-stock alerts, and a valuation summary — paired with the SQL schema/queries that would back it in a real deployment.

---

## 📁 Project Structure

| File | Purpose |
|---|---|
| `inventory.html` | Page markup — login screen + main dashboard |
| `inventory_style.css` | Glassmorphism login UI + dashboard styling, plus print-friendly rules |
| `inventory_script.js` | All client-side logic: auth, CRUD, search/filter, rendering |
| `database_queries.sql` | The MySQL schema and queries this front end is designed to map to |

---

## ✨ Features

- **Login gate** — simple email/password check with a "demo credentials" autofill button
- **Dashboard stats** — total items, low-stock alert count, total inventory valuation (auto-calculated)
- **Product table** — search by name/ID, filter by category, edit/delete per row
- **Add / Edit form** — single form that toggles between "Add" and "Update" modes
- **Low-stock badges** — any item with quantity ≤ 5 is flagged
- **PDF export** — "Download PDF" triggers the browser print dialog with dashboard-friendly print CSS
- **Persisted login state** — stays logged in across refresh via `localStorage`

---

## 🔧 How It Works (Tech Stack)

This is a **front-end-only prototype** — there's no server or live database connection yet:

- `inventory_script.js` keeps all product data in an in-memory JavaScript array (`databaseItems`), seeded with 3 sample products
- The **SQL file is a design reference**, not something the app currently calls — it shows what the real schema/queries would look like if this were wired up to an actual MySQL/SQLite backend
- Login only checks a hardcoded email/password and stores a flag in `localStorage` — it isn't real authentication

## 🗄️ Database Design (`database_queries.sql`)

- **`products` table** — `product_id`, `product_name`, `category`, `price`, `stock_quantity`, `created_at`, with `CHECK` constraints preventing negative price/stock
- **Query A** — dashboard stats in one query: total items, low-stock count, total valuation (mirrors what the JS currently computes client-side)
- **Query B** — fetch just the low-stock items
- **Query C** — decrement stock by 1 (simulating a sale)
- **Query D** — bulk restock a whole category
- **Query E** — full product update (mirrors the "Edit Product" form action)

---

## ▶️ Running It

No build step needed:

1. Keep all four files in the same folder
2. Open `inventory.html` in a browser
3. Log in with:
   - **Email:** `admin@gmail.com`
   - **Password:** `admin123`
   (or click "Auto Fill Demo Access")

---

## ⚠️ Known Limitations / Notes for Next Steps

- **No real backend** — data resets on every page refresh since it only lives in a JS array. To make it persistent, you'd connect the front end to an API that runs the queries in `database_queries.sql` against a real database.
- **Not secure** — credentials are hardcoded in plain text in the JS file; fine for a demo/internship project, not for production.
- **`Query C`/`Query E` reference `product_id = 101`** — that's a hardcoded example; a real backend would pass the actual selected row's ID dynamically.
- **Social login icons** are decorative only (no OAuth wired up).

---

## 💡 Suggested Improvements

- Replace the in-memory array with real `fetch()` calls to a backend (Node/Express, Flask, etc.) that executes the SQL in `database_queries.sql`
- Add real authentication (hashed passwords, sessions/JWT) instead of a hardcoded check
- Add pagination for large inventories
- Add input validation (e.g., prevent negative price/qty on the client side, matching the SQL `CHECK` constraints)
