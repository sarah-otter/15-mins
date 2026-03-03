[README.md](https://github.com/user-attachments/files/25728141/README.md)
# 15 Minutes — Setup Guide

A household chore tracker for Sarah & Anthony. Built as a mobile-first web app backed by Google Sheets.

---

## What you'll set up

```
Google Sheets  ←→  Apps Script  ←→  index.html (GitHub Pages)
```

---

## Step 1 — Create the Google Sheet

1. Go to [sheets.google.com](https://sheets.google.com) → **New spreadsheet**
2. Name it `15 Minutes`

### Create Sheet 1: "Chores"
Click the `+` tab at the bottom → rename it `Chores`

Add these headers in row 1:
| A: Name | B: Frequency | C: Frequency Days |
|---|---|---|
| Clean Bathroom | Weekly | 7 |
| Vacuum Floors | Weekly | 7 |
| Empty Dishwasher | Daily | 1 |
| Mop Kitchen Floor | Every 2 weeks | 14 |
| Change Bedsheets | Weekly | 7 |
| Take Out Bins | Weekly | 7 |
| Wipe Stovetop | Every 3 days | 3 |

> Add/edit chores freely — the app reads whatever is in this sheet.

### Create Sheet 2: "Completions"
Add another tab → rename it `Completions`

Add headers in row 1:
| A: Chore | B: CompletedBy | C: Date |
|---|---|---|

Leave the rest empty — the app will write here automatically.

---

## Step 2 — Add the Apps Script

1. In your Google Sheet, click **Extensions → Apps Script**
2. Delete the default `myFunction()` code
3. Open `Code.gs` from this folder, copy everything, paste it in
4. Click 💾 **Save**
5. Name the project `15 Minutes`

---

## Step 3 — Deploy the Script

1. Click **Deploy → New deployment**
2. Click ⚙️ gear icon next to "Select type" → choose **Web app**
3. Set:
   - Description: `15 Minutes App`
   - Execute as: **Me**
   - Who has access: **Anyone**
4. Click **Deploy**
5. Click **Authorize access** → choose your Google account → Allow
6. **Copy the Web App URL** — it looks like:
   ```
   https://script.google.com/macros/s/AKfy.../exec
   ```

---

## Step 4 — Connect the URL to the app

1. Open `index.html` in a text editor
2. Find this section near the top of the `<script>` tag:

```javascript
const CONFIG = {
  SCRIPT_URL: 'YOUR_APPS_SCRIPT_URL_HERE',
  TZ_OFFSET: 10,  // AEST = 10, change for your timezone
};
```

3. Replace `YOUR_APPS_SCRIPT_URL_HERE` with your Web App URL
4. Save the file

---

## Step 5 — Put it on GitHub Pages

### First time setup
1. Go to [github.com](https://github.com) → sign in (or create account)
2. Click **+** → **New repository**
3. Name it `15-minutes` → set to **Public** → click **Create repository**

### Upload your file
**Option A — via browser (easiest):**
1. On your new repo page, click **uploading an existing file**
2. Drag `index.html` onto the page
3. Click **Commit changes**

**Option B — via Git CLI:**
```bash
git init
git add index.html
git commit -m "Initial commit"
git branch -M main
git remote add origin https://github.com/YOUR_USERNAME/15-minutes.git
git push -u origin main
```

### Enable GitHub Pages
1. In your repo, go to **Settings → Pages**
2. Under **Source**, select **Deploy from a branch**
3. Branch: `main` / Folder: `/ (root)`
4. Click **Save**
5. Wait ~60 seconds, then visit:
   ```
   https://YOUR_USERNAME.github.io/15-minutes/
   ```

---

## Step 6 — Add to iPhone home screen

1. Open the URL in **Safari** on iPhone
2. Tap the **Share** button (box with arrow)
3. Scroll down → tap **Add to Home Screen**
4. Name it `15 Minutes` → tap **Add**

It'll appear on your home screen and open fullscreen like a native app.

---

## Updating chores

- **Add a chore:** Add a new row in the `Chores` sheet. It appears in the app immediately.
- **Change frequency:** Edit column C (number of days).
- **Remove a chore:** Delete the row from the `Chores` sheet.

## Updating the app

If you edit `index.html` locally:
```bash
git add index.html
git commit -m "Update app"
git push
```
GitHub Pages updates automatically within ~60 seconds.

---

## Troubleshooting

| Problem | Fix |
|---|---|
| "Couldn't load data" | Check SCRIPT_URL is correct in index.html |
| Completions not saving | Re-deploy the Apps Script (Deploy → Manage → Edit → Deploy) |
| Sheet not found error | Make sure sheet names are exactly `Chores` and `Completions` |
| App not updating after edit | Hard refresh: hold Shift + tap reload in browser |

---

## File structure

```
15-minutes/
├── index.html     ← The entire app (HTML + CSS + JS)
├── Code.gs        ← Google Apps Script (paste into Apps Script editor)
└── README.md      ← This guide
```
