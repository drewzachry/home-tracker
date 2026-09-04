# Home Maintenance Tracker

A mobile-first PWA that scans service bills with the Anthropic API and syncs
records to Google Sheets. See `README.md` for the full end-user setup guide
(hosting, Google Sheets, Apps Script, phone install).

## Structure

- `index.html` — the entire app: markup, CSS, and JS in one file. No build
  step, no bundler, no framework.
- `sw.js` — service worker for offline caching / PWA install.
- `manifest.json` — PWA metadata (icons, name, shortcuts).

There is no `package.json`, dependency manifest, test suite, or linter in
this repo — nothing needs to be installed to work on it.

Note: `README.md` also references a `script.gs` (Google Apps Script that
writes scanned records to the user's Sheet), but that file is not checked
into this repo — it lives only in the user's Google Sheets Apps Script
editor.

## Working on this project

- Edit `index.html` directly; it's plain HTML/CSS/vanilla JS.
- To preview locally, serve the directory (e.g. `python3 -m http.server`)
  and open it in a browser — opening `index.html` via `file://` also mostly
  works except for service-worker/PWA behavior, which requires being served
  over http(s).
- Runtime config (Anthropic API key, Spreadsheet ID, Google API key, Apps
  Script URL) is entered by the end user in the app's Setup tab and stored
  client-side — there are no secrets or env vars to configure in this repo.
- Deployment is static hosting (GitHub Pages / Netlify per the README) —
  pushing changes to the hosted branch is the deploy step.
