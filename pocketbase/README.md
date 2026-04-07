# PocketBase Setup — BKKFT Onboarding

## Requirements

- PocketBase running on **port 8090**
- Admin account created (first-time setup at `http://localhost:8090/_/`)

---

## Step 1 — Import Collections Schema

1. Go to `http://localhost:8090/_/` and log in as admin
2. Click **Settings** (gear icon, bottom left)
3. Click **Import collections**
4. Upload `pb_schema.json` from this folder
5. Confirm the import — this creates 4 collections:
   - `cohorts`
   - `new_hires`
   - `quiz_sessions`
   - `quiz_answers`

---

## Step 2 — Configure CORS

1. In PocketBase Admin, go to **Settings → Application**
2. Under **Allowed origins**, add: `http://localhost:3000`
3. Save

If you access the app from another host or port, add that origin here too.

---

## Step 3 — Create First Cohort

Before new hires can register on the app, at least one cohort must exist.

1. Go to **Collections → cohorts**
2. Click **New record**
3. Fill in:
   - `name`: e.g., `April 2026 Batch`
   - `start_date`: e.g., `2026-04-07`
   - `status`: `active`
4. Save

---

## Collections Overview

| Collection | Purpose |
|------------|---------|
| `cohorts` | Onboarding batches (one per group of new hires) |
| `new_hires` | Individual employee records |
| `quiz_sessions` | Each quiz attempt per new hire |
| `quiz_answers` | Individual question answers per session |

---

## Access Rules

All collections have open read/write rules (`""`) by default — no authentication required.
This is intentional for internal network use. If the app is exposed beyond your local network,
restrict rules via the PocketBase Admin → collection rules.

---

## API Base URL

The frontend app is configured to call PocketBase at:

```
http://localhost:8090
```

If you change the PocketBase port or host, update the `PB_URL` constant at the top of `frontend/src/index.html`.
