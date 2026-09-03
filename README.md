# KAMSWEG Welfare

KALRO Marsabit Staff Welfare Group (KAMSWEG) is a browser-based welfare ledger. It starts its contribution calendar on **1 August 2026**.

## Stack and data model

This implementation is deliberately dependency-light: semantic HTML, modern CSS, and ES modules, with IndexedDB/localStorage-ready browser persistence (localStorage is used so the app can run from a simple local server). It is a functional prototype that works offline and includes a seeded administrator account.

For production, retain this UI and replace `Storage` in `app.js` with an API backed by **Next.js + TypeScript**, **PostgreSQL**, **Prisma**, and **Auth.js**. Store password hashes (Argon2id), roles, audit events and immutable contribution/loan transactions server-side; never retain plaintext passwords in the browser.

Core records:

- `members`: membership number, name, contacts, joined date, status and opening shares.
- `contributions`: a member, month, amount and payment status. The system creates expected monthly contribution rows automatically from 2026-08 onward.
- `loans`: member, principal, interest rate, term, issue date, status, repayment history and outstanding balance.
- `users`: login identity and role. This demo uses a local, illustrative password only.

## Run

Use a local static server (for example `npm start`) and open `http://localhost:5173`.

Demo login: **admin@kamsweg.org** / **Kamsweg2026!**

## Included workflow

1. Sign in.
2. Add a member. Their contribution schedule is immediately generated from their joined month through the current month.
3. Record a paid or pending monthly contribution, or use **Refresh contributions** to generate all missing month records.
4. Add a loan and record repayments. Outstanding balances, loan status, and analytics update automatically.
5. Use the dashboard and analysis filters to inspect the welfare position.

`Reset demo data` is intentionally visible on the login screen for testing. Do not carry this control into production.
