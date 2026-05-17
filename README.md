# SDW Automotive — Fleet Database

> Volkswagen · Audi · SEAT · Škoda Specialist Fleet Management System

A browser-based fleet database for SDW Automotive. Stores all vehicle records, MOT dates, diagnostics, and service history in a live Supabase database — accessible from any computer, no installation needed.

---

## Features

- Vehicle records (registration, make, model, customer details)
- MOT tracking with countdown and expiry alerts
- 12-month automatic reminders
- Diagnostic records with file references and fault code notes
- Full service history per vehicle
- Real-time sync across all devices via Supabase

---

## Setup

### 1. Supabase Database

Create a free account at [supabase.com](https://supabase.com), create a project, then run this SQL in **SQL Editor → New Query**:

```sql
CREATE TABLE vehicles (
  id UUID DEFAULT gen_random_uuid() PRIMARY KEY,
  registration TEXT NOT NULL,
  make TEXT,
  model TEXT,
  customer_name TEXT,
  customer_phone TEXT,
  customer_email TEXT,
  mot_date DATE,
  mot_reminder BOOLEAN DEFAULT true,
  year INT,
  colour TEXT,
  notes TEXT,
  mot_notes TEXT,
  mileage INT,
  created_at TIMESTAMPTZ DEFAULT NOW()
);

CREATE TABLE records (
  id UUID DEFAULT gen_random_uuid() PRIMARY KEY,
  vehicle_id UUID REFERENCES vehicles(id) ON DELETE CASCADE,
  type TEXT,
  title TEXT,
  description TEXT,
  date DATE,
  mileage INT,
  cost NUMERIC,
  files TEXT[],
  created_at TIMESTAMPTZ DEFAULT NOW()
);
```

### 2. Get your credentials

In Supabase go to **Settings → API Keys** and copy:
- **Project URL** — `https://xxxxxx.supabase.co`
- **Publishable / Anon key**

### 3. Open the app

Open `index.html` in any browser. Enter your URL and key on the setup screen. The app remembers your credentials on that device — you only enter them once per computer.

---

## Hosting on GitHub Pages (recommended)

Hosting on GitHub Pages gives you a permanent URL you can open on any computer or bookmark — no files to copy around.

1. Push this repo to GitHub
2. Go to your repo → **Settings → Pages**
3. Under **Source** select `Deploy from a branch`
4. Choose `main` branch, `/ (root)` folder → click **Save**
5. After ~60 seconds your app is live at:
   `https://YOUR-USERNAME.github.io/YOUR-REPO-NAME/`

Open that URL on any computer, enter your Supabase key once, and you're connected.

---

## Usage

| Action | How |
|---|---|
| Add vehicle | Vehicles → Add Vehicle button |
| Log a service | Services → Log Service, or open a vehicle → Add Record |
| Log a diagnostic | Diagnostics → New Diagnostic |
| View MOT status | MOT Tracker tab — sorted by urgency |
| See reminders | Reminders tab — all active 12-month alerts |
| Use on new computer | Open the URL → enter Supabase key once |

---

## Tech Stack

- Plain HTML/CSS/JavaScript — no build tools, no dependencies to install
- [Supabase](https://supabase.com) — free PostgreSQL cloud database
- [GitHub Pages](https://pages.github.com) — free hosting

---

*SDW Automotive · 07815 510002 · info@sdwautomotive.co.uk*
