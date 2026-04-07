# BestPaidRep.com — OB Delivery Platform SOP
**Last Updated:** April 7, 2026
**Platform:** `intuitiveob-vi2eqvap.manus.space`
**Manus Project:** `is-ob-julia` | Checkpoint: `f5023c65`
**GitHub Repo:** `Kilakj57/bestpaidrep-reports`

---

## The Delivery Platform

All Opportunity Books are delivered via a single Manus-hosted site at:

**`https://intuitiveob-vi2eqvap.manus.space`**

Each rep gets their own permanent URL at `/{rep-slug}`. The OB opens full-screen directly in the browser — no downloads, no portals, no login required. A red confidentiality banner appears at the top of every page.

---

## Active Rep URLs — Copy and Send Directly

| Rep | Company | Account | URL | OB Status |
|---|---|---|---|---|
| Julia Kalez | VAST Data | Intuitive Surgical | https://intuitiveob-vi2eqvap.manus.space/julia-kalez | Gold Standard OB Live (Full-Screen) |
| Erica Brouillette | VAST Data | Kaiser Permanente | https://intuitiveob-vi2eqvap.manus.space/erica-brouillette | Gold Standard OB Live (Full-Screen) |
| Drew Sielski | Globality | Dell Technologies | https://intuitiveob-vi2eqvap.manus.space/drew-sielski | OB Live (Card Format) |
| Kevin Cipollaro | Globality | Biogen | https://intuitiveob-vi2eqvap.manus.space/kevin-chipollaro | OB Live (Card Format) |
| Joey Flynn | Globality | Newell Brands | https://intuitiveob-vi2eqvap.manus.space/joey-flynn | OB Live (Card Format) |

---

## How to Add a New Rep (6 Steps)

1. Build the OB HTML using the Gold Standard process (11 chapters).
2. Copy OB into public folder: `cp /path/to/Account_GS_OB.html /home/ubuntu/is-ob-julia/client/public/account-name-ob.html`
3. Create `client/src/pages/RepName.tsx` using the full-screen iframe template (see below).
4. Add route to `client/src/App.tsx`: `<Route path="/rep-slug" component={RepName} />`
5. Run `pnpm run build`, then `webdev_save_checkpoint`, then Publish.
6. Update this SOP with the new rep URL.

## Full-Screen Iframe Page Template

```tsx
export default function RepName() {
  return (
    <div style={{ margin: 0, padding: 0, background: "#0A1628", minHeight: "100vh", display: "flex", flexDirection: "column" }}>
      <div style={{ background: "#DC2626", color: "#fff", textAlign: "center", padding: "0.5rem", fontSize: "0.75rem", fontWeight: 700, letterSpacing: "0.1em", textTransform: "uppercase", fontFamily: "Inter, sans-serif", flexShrink: 0 }}>
        Confidential — Prepared Exclusively for [Rep Name] ([Company]) — Do Not Distribute
      </div>
      <iframe src="/account-name-ob.html" title="[Account] — Intelligence Brief" style={{ width: "100%", flex: 1, border: "none", display: "block", minHeight: "calc(100vh - 32px)" }} allow="fullscreen" />
    </div>
  );
}
```

---

## How to Refresh in a New Sandbox

1. Manus project `is-ob-julia` persists via the webdev system — no re-cloning needed.
2. OB HTML files are in `client/public/` and deploy with the site.
3. Rep page components are in `client/src/pages/` — one .tsx per rep.
4. Routes registered in `client/src/App.tsx`.
5. Recovery checkpoint: `f5023c65` (April 7, 2026 baseline).

---

## Key Rules — Never Break These

1. Never rebuild the delivery site to add a rep — always add a new page and route.
2. Never change existing rep URLs — reps and managers have them saved.
3. Always use full-screen iframe format for new OBs.
4. OB HTML files must be in `client/public/` — not on session CDN URLs (those expire).
5. Commit this SOP to GitHub after every delivery platform change.

---

## OB Build Queue

| Rep | Account | Priority |
|---|---|---|
| Drew Sielski | Dell Technologies | Next |
| Kevin Cipollaro | Biogen | Next |
| Joey Flynn | Newell Brands | Next |
