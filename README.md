# 🏠 Home Maintenance Tracker — Setup Guide

A mobile-first PWA that scans service bills with AI, syncs to Google Sheets, and installs on your phone's home screen.

---

## What You Have

| File | Purpose |
|------|---------|
| `index.html` | The entire app (one file, runs in any browser) |
| `sw.js` | Service worker — enables offline mode & PWA install |
| `manifest.json` | PWA metadata — home screen icon, name, theme |
| `script.gs` | Google Apps Script — writes scanned records to your Sheet |

---

## Step 1 — Host the App (free, 5 min)

### Option A: GitHub Pages (recommended)
1. Create a free account at **github.com**
2. Click **+** → **New repository** → name it `home-tracker` → Public → Create
3. Upload all 4 files (`index.html`, `sw.js`, `manifest.json`, `manifest.json`)
4. Go to **Settings → Pages → Source → main branch → Save**
5. Your app URL: `https://YOUR-USERNAME.github.io/home-tracker`

### Option B: Netlify (drag & drop)
1. Go to **app.netlify.com** and sign up free
2. Drag the entire folder onto the deploy zone
3. Done — you get a URL instantly like `https://random-name.netlify.app`

---

## Step 2 — Set Up Google Sheets

### 2a — Create your Sheet
1. Go to **sheets.google.com** → Blank spreadsheet
2. Rename it `Home Maintenance Tracker`
3. Copy the Sheet ID from the URL:
   ```
   https://docs.google.com/spreadsheets/d/THIS-PART-IS-YOUR-ID/edit
   ```

### 2b — Deploy the Apps Script
1. In your Sheet: **Extensions → Apps Script**
2. Delete any existing code, paste the contents of `script.gs`
3. Click **Deploy → New Deployment**
   - Type: **Web App**
   - Execute as: **Me**
   - Who has access: **Anyone**
4. Click **Deploy** → copy the **Web App URL**

### 2c — Get a Google API Key (for reading data)
1. Go to **console.cloud.google.com**
2. Create a project (or use an existing one)
3. Go to **APIs & Services → Library** → search **Google Sheets API** → Enable
4. Go to **APIs & Services → Credentials → Create Credentials → API Key**
5. Copy the key (optionally restrict it to Sheets API + your domain)

---

## Step 3 — Configure the App

1. Open your hosted app URL in your phone's browser
2. Tap **⚙️ Setup** tab
3. Enter:
   - **Anthropic API Key** — from [console.anthropic.com](https://console.anthropic.com) (for bill scanning)
   - **Spreadsheet ID** — the ID from Step 2a
   - **Google API Key** — from Step 2c
   - **Apps Script URL** — from Step 2b
4. Tap **Save & Test Connection** — you should see "Connected to Google Sheets!"

---

## Step 4 — Install on Your Phone

### iPhone (Safari)
1. Open your app URL in **Safari** (must be Safari)
2. Tap the **Share** button (box with arrow) at the bottom
3. Scroll down → tap **Add to Home Screen**
4. Tap **Add** — done! 🎉

### Android (Chrome)
1. Open your app URL in **Chrome**
2. Tap **⋮** menu → **Add to Home screen**
3. Or watch for the automatic install banner

---

## How It Works

```
📷 Scan a bill
    ↓
🤖 Claude AI extracts: system, who serviced it, dates, cost
    ↓
✏️ You review & confirm (editable fields)
    ↓
💾 Saves to app + syncs row to Google Sheets
    ↓
📅 One-tap Google Calendar reminder for next service date
```

---

## Google Sheets Structure

The script auto-creates a **Log** sheet with these columns:

| ID | System | Category | Location | Installed | Last Maint | Performed By | Work Done | Cost | Next Due | Status | Notes | Scanned |
|----|--------|----------|----------|-----------|------------|-------------|-----------|------|----------|--------|-------|---------|

Status cells are auto-colored: 🔴 Overdue / 🟡 Due Soon / 🟢 OK

---

## Troubleshooting

**"Sheets sync failed"** — Check that your Apps Script is deployed with "Anyone" access, and the URL is correct in Setup.

**"API error 401"** — Your Anthropic key may be wrong or expired. Re-enter it in Setup.

**Can't install to home screen on iPhone** — Must use Safari, not Chrome or another browser.

**Sheet not updating** — Make sure you clicked "Deploy" (not just "Save") in Apps Script, and copied the deployment URL (not the editor URL).

---

*Built with Claude · Anthropic API · Google Sheets API · Progressive Web App*
