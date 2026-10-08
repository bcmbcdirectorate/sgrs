# Scholarship Grievance Redressal System (SGRS)

A working, role-based web app for lodging, tracking and resolving scholarship-related
grievances with **multi-level escalation**, **notifications** and **dashboards**.

Organisation shown: MBC & DNC Directorate.

---

## 1. Run it

It is a single self-contained file — **no server, no install, no internet needed**.

- **Quickest:** double-click `index.html` (it opens in any browser).
- **Local server (optional):** `python3 -m http.server 8000` then open `http://localhost:8000`.

Data is stored in your browser (`localStorage`), so it survives refreshes on that
browser. The app starts with an **empty register** — no demo grievances. The six
login accounts are pre-created so you can sign in and add your own records.

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
- **SLA-based auto-escalation** — each level has a resolution window (L1: 7 days,
  L2: 5 days, L3: 3 days). If a grievance breaches its window it is escalated to the
  next level automatically, and the change is recorded in the timeline.
- **Officer actions** — mark under review, add remark, resolve, reject, or escalate.
- **Notifications** — an in-app bell + notifications page; filers and the concerned
  officers are notified on every status change.
- **Dashboards** — role-aware stats, "needs attention" (overdue) list, filters
  (status / category / priority / search) and a category breakdown chart for the
  directorate.

## 4. Go live for free (pick one)

The app is a single static file, so any free static host works.

**Option A — Netlify Drop (fastest, no account needed to start)**
1. Go to `https://app.netlify.com/drop`.
2. Drag the `index.html` file (or the whole folder) onto the page.
3. You get a live URL instantly. Claim it with a free account to keep it.

**Option B — GitHub Pages (free, permanent)**
1. Create a repository, e.g. `sgrs`.
2. Upload `index.html` (rename it `index.html` if needed).
3. Settings → Pages → Source: `main` branch, `/root` → Save.
4. Your site appears at `https://<your-username>.github.io/sgrs/`.

**Option C — Vercel / Cloudflare Pages**
Import the repository or drag-and-drop the folder; no build step is required
(it is plain HTML/CSS/JS).

## 5. Important note for real use

This build keeps data **in the browser only**, which makes it perfect for a demo,
a pilot, or a stakeholder walkthrough. For a real, multi-user rollout where students,
institutions and officers share one live database, it needs a **backend** (e.g. a small
API + database) and login against your own user directory. The current UI, roles,
workflow and escalation logic are built so that this backend can be added without
redesigning the screens — the data layer is isolated and easy to swap.

## 6. Files

- `index.html` — the entire application (HTML + CSS + JS inlined).
- Screenshots — preview of the main screens.

---

Demo build. Sample data is illustrative only.
