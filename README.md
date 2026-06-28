# Ten Ring

A scoresheet app for SSAA pistol shoots. Score a relay on a phone or tablet at the
mound, total it as you go, and hand out a clean, branded PDF at the end. Works offline,
installs to the home screen, and keeps everything on the device.

Built for **SSAA Waratah Shooting Complex Inc.**

---

## What it does

- **Up to 15 shooters** per shoot — name them, score them, rank them.
- **Club disciplines** built in: Centre Fire / Sport, Standard Pistol, Rapid Fire,
  Service Pistol Mk V — each with the correct series structure and stage timing.
- **Custom discipline editor** — define your own course of fire (shots, series, briefing,
  RO note) without touching the code.
- **Two-shoot mode** — run two relays in one session and export them in a single PDF.
- **Fast entry** — tap a cell, punch the score on the 0–10 keypad, it auto-advances.
  Series totals, grand total and ×10 count update live.
- **Briefings** — a read-to-shooters course of fire for each discipline, with the RO note.
- **Leaderboard** — auto-ranked, on screen and at the top of the printout.
- **PDF export** — SSAA-branded, repeating page header, page numbers, today's scorer,
  and an on-screen RO sign-off signature. Plus a **CSV** export for the spreadsheet.
- **Offline + persistent** — once loaded it runs with no signal, and scores survive a
  refresh or app close.

## Using it

1. Open the app and tap the **gear** (top right) to set the date, Range Officer, today's
   scorer, and how many shooters. Club and Range are pre-filled and editable.
2. Pick the **match** from the toolbar. Tap the **speaker** icon for the briefing to read out.
3. Tap a cell and score with the keypad. Switch shooters with the chips along the top.
4. **Leaderboard** shows the standings. **Export** prints the scoresheet or saves the CSV.
5. The RO can scribble a **sign-off** signature (Setup → RO sign-off, or from Export) that
   prints on the last page.

## Install on a phone

Open the site in the browser, then **Share → Add to Home Screen**. It runs full-screen
like a normal app and works offline after the first load.

## Deploying (GitHub Pages)

This is a static site — no build step.

1. Put all files in the **root** of the repo (`index.html` must be at the top level).
2. **Settings → Pages → Deploy from a branch → `main` / `/ (root)`** → Save.
3. The site appears at `https://<username>.github.io/tenring/`. GitHub Pages is HTTPS,
   which the install and offline features require.

### Updating later

The app caches itself for offline use, so after you change `index.html` you also need to
**bump the cache version** so installed phones pull the new build:

- Open `sw.js` and change `const CACHE = 'tenring-v1'` to `'tenring-v2'` (then `v3`, etc.).

Commit both files. Phones pick up the new version on next open.

## Files

| File | Purpose |
|------|---------|
| `index.html` | The whole app — markup, styles, logic, and the embedded SSAA logo. |
| `manifest.webmanifest` | PWA manifest (name, icons, colours). |
| `sw.js` | Service worker — offline caching. Bump `CACHE` to push updates. |
| `icon-*.png`, `apple-touch-icon.png`, `favicon-64.png` | App icons. |
| `.nojekyll` | Tells GitHub Pages to serve files as-is. |

## Privacy

All data — shooters, scores, signatures — stays in the browser on the device
(`localStorage`). Nothing is uploaded anywhere. Clearing the browser's site data or the
app removes it.

## Notes

- Scores are integer ring values, 0–10. `MISS` records a 0; blank means not yet shot.
- The printout runs roughly two shooters per page for full legibility.
- Built as a single self-contained page in plain HTML/CSS/JS — no frameworks, no build.
