# BestPaidRep.com — OB Standalone Delivery Process

**Established:** April 3, 2026
**Purpose:** Standard process for delivering Opportunity Books to enterprise reps during the POC phase — without using the BPR AI Portal.

---

## Why This Model Exists

During the VAST Data and Globality POC phase, the BPR AI Portal is considered too unstable for client-facing delivery. Each rep receives their own standalone Manus-hosted webpage with a clean, permanent URL.

First used for Drew Sielski, Kevin Cipollaro, and Joey Flynn (Globality POC). Extended to Julia Kalez (VAST Data POC) in April 2026.

---

## The Delivery Model

Each rep gets:
1. A **delivery page** — dark navy/gold branded page with "Welcome, [Name]." hero, audio podcast player, and "View Report" button
2. A **direct OB URL** — the report opens in the browser (no download, no login required)

Both URLs are permanent (hosted on Manus webdev CDN) and do not expire.

---

## Step-by-Step Process

### Step 1 — Build the OB
Build the Opportunity Book as a standalone HTML file using the Gold Standard workflow (11 chapters, magazine layout, executive photos with LinkedIn buttons, citations). Save locally.

### Step 2 — Initialize a New Manus Webdev Project
One project per rep. Example: `julia-ob-is` for Julia Kalez / Intuitive Surgical.

### Step 3 — Copy the OB into the Project's Public Folder
```
cp /path/to/OB.html /home/ubuntu/[project]/client/public/report.html
```
This serves the OB as `text/html` at `[domain]/report.html` — no download prompt.
**Never serve the OB from CDN directly** — CDN serves HTML as `application/octet-stream` (download).

### Step 4 — Upload the Podcast to CDN
```
rclone copy "manus_google_drive:BestPaidRep/Podcasts/[company].mp3" /home/ubuntu/webdev-static-assets/
manus-upload-file --webdev /home/ubuntu/webdev-static-assets/[company].mp3
```
Always use `--webdev` flag for permanent hosting. Without it, the URL expires with the session.

### Step 5 — Build the Delivery Page
Edit `client/src/pages/Home.tsx` using the standard dark luxury editorial template:
- `repName` — rep's first name for the "Welcome, [Name]." hero
- `repTitle` — rep's title and company (e.g., "Enterprise Account Manager • VAST Data")
- `OB_URL` — set to `"/report.html"` (served locally, not CDN)
- `PODCAST_URL` — the CDN URL from Step 4
- `greeting` — 2–3 sentence intro specific to the account

### Step 6 — Checkpoint and Publish
Save a checkpoint, then click Publish in the Manus Management UI.

### Step 7 — Verify the OB URL
```
curl -s -o /dev/null -w "%{http_code} %{content_type}" "https://[domain]/report.html"
```
Must return `200 text/html`. If it returns `application/octet-stream`, move the OB to `client/public/`.

---

## Key Rules

1. **Always use `--webdev` flag** when uploading assets — session-only URLs expire
2. **Never serve OB from CDN directly** — always use `client/public/report.html`
3. **Never rebuild an existing delivery site** to add a new rep — always create a new standalone project
4. **One project per rep** — keeps URLs clean and independently publishable
5. **Save the Manus project checkpoint ID** in the session handoff

---

## Active Delivery URLs

| Rep | Company | Delivery Page | Direct OB URL |
|---|---|---|---|
| Drew Sielski | Globality | bestpocdel-2dfgasjs.manus.space/drew-sielski | Via delivery page |
| Kevin Cipollaro | Globality | bestpocdel-2dfgasjs.manus.space/kevin-chipollaro | Via delivery page |
| Joey Flynn | Globality | bestpocdel-2dfgasjs.manus.space/joey-flynn | Via delivery page |
| Julia Kalez | VAST Data | intuitiveob-vi2eqvap.manus.space | intuitiveob-vi2eqvap.manus.space/report.html |

---

## Template Reference

The standard delivery page template is in the `is-ob-julia` Manus project (`client/src/pages/Home.tsx`).
Design: dark navy `oklch(0.07 0.022 250)`, gold `oklch(0.75 0.12 75)`, Playfair Display + DM Mono typography.
Copy this file as the starting point for every new rep delivery page.
