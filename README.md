# Scholarship Grievance Redressal System (SGRS)

A role-based web app for lodging, tracking and resolving scholarship-related
grievances with **multi-level escalation**, **notifications** and **dashboards**.

Records are stored in a **shared Supabase (Postgres) backend**, so every device —
a student's phone, an officer's laptop — sees the same live data.

Organisation shown: MBC & DNC Directorate.

---

## 1. Live site

**https://bcmbcdirectorate.github.io/sgrs/**

Open it in any browser on any device. It talks to the backend over the internet.

## 2. Demo logins

| Role | Email | Password |
|---|---|---|
| Student | `student@demo.in` | `student123` |
| Institution | `institution@demo.in` | `inst123` |
| Officer — Level 1 (District) | `l1@demo.in` | `l1pass` |
| Officer — Level 2 (Directorate) | `l2@demo.in` | `l2pass` |
| Officer — Level 3 (Appellate) | `l3@demo.in` | `l3pass` |
| Administrator | `admin@demo.in` | `admin123` |

On the sign-in screen you can also click any demo account to auto-fill it.

## 3. What it does

- **File a grievance** (student or institution) — category, scheme, application no.,
  description, priority. An ID like `SGRS/2026/0001` is generated automatically.
- **Track by ID** publicly, without signing in — status plus full timeline.
- **Multi-level escalation** — Level 1 (Institution/District) → Level 2 (Directorate) →
  Level 3 (Appellate Authority).
- **SLA-based auto-escalation** — L1: 7 days, L2: 5 days, L3: 3 days. A breach escalates
  the grievance automatically and records it in the timeline.
- **Officer actions** — mark under review, add remark, resolve, reject, or escalate.
- **Notifications** — in-app bell + notifications page; filers and the concerned
  officers are notified on every status change.
- **Dashboards** — role-aware stats, overdue list, filters and a category chart.

## 4. Backend (Supabase)

- Project region: Mumbai (`ap-south-1`), free plan.
- Tables: `profiles`, `credentials`, `grievances`, `grievance_events`,
  `notifications`, `notification_reads`, `counters`.
- `login(email, password)` is a Postgres function that verifies the password with
  bcrypt (`pgcrypto`) and returns the profile. Passwords live in `credentials`,
  which the public API **cannot read** (row-level security with no policy).
- `next_grievance_id()` generates the sequential grievance ID.

## 5. Security — please read

This is a **pilot** build. Logins are real (passwords are hashed, and the credential
table is not exposed), but the data tables use **permissive row-level security**, because
the app authenticates against a custom `login()` function rather than Supabase Auth.
In practice that means anyone who has the site URL can read and write grievances through
the API — fine for a demo or a closed pilot with non-sensitive data, but **not** suitable
for real citizen data as-is.

The upgrade path (recommended before any real rollout): switch to **Supabase Auth**
(email/password) and replace the permissive policies with rules keyed to `auth.uid()`,
so students see only their own grievances and officers only their level. The app's data
layer is isolated, so this can be done without redesigning the screens.

## 6. Files

- `index.html` — the entire application (HTML + CSS + JS + Supabase SDK inlined).

---

Pilot build. Sample accounts only.
