# FMS Helpdesk Email Tracker

A standalone web app for MRF IT team to track and manage emails with `fms.ho@mrfmail.com`.  
Deployed on GitHub Pages. Can be pinned as a Microsoft Teams tab.

---

## What it does

- Signs in via your MRF Microsoft 365 account (no separate password)
- Pulls all emails sent to / received from `fms.ho@mrfmail.com` in the last 30 days
- Shows ticket age (green = fresh, amber = aging, red = overdue)
- Filter by status, direction (IN/OUT), and age
- Update and save ticket status per email (New / Open / Pending / Overdue / Closed)
- Works as a Teams tab

---

## Deployment steps

### Step 1 — Register an Azure AD app

1. Go to https://portal.azure.com → **Azure Active Directory** → **App registrations**
2. Click **New registration**
   - Name: `FMS Helpdesk Tracker`
   - Supported account types: **Accounts in this organizational directory only**
   - Redirect URI: **Single-page application (SPA)** → `https://mrfpaint.github.io/fms-helpdesk-tracker/`
3. Click **Register**
4. Copy the **Application (client) ID** — you'll need it in the next step

5. Go to **API permissions** → **Add a permission** → **Microsoft Graph** → **Delegated**
   - Add: `Mail.Read`
   - Add: `User.Read`
6. Click **Grant admin consent** (ask your M365 admin if you can't)

---

### Step 2 — Update the app config

Open `index.html` and find this line near the bottom:

```js
clientId: 'YOUR_AZURE_APP_CLIENT_ID',
```

Replace `YOUR_AZURE_APP_CLIENT_ID` with the client ID you copied in Step 1.

The tenant ID is already filled in for your MRF tenant.

---

### Step 3 — Push to GitHub Pages

```bash
# In your terminal / Git Bash
cd /path/to/your/project

git init
git remote add origin https://github.com/mrfpaint/fms-helpdesk-tracker.git

git add index.html README.md
git commit -m "Initial deploy: FMS Helpdesk Email Tracker"
git push -u origin main
```

Then on GitHub:
- Go to the repo → **Settings** → **Pages**
- Source: **Deploy from branch** → `main` → `/ (root)`
- Save

Your app will be live at:  
**https://mrfpaint.github.io/fms-helpdesk-tracker/**

---

### Step 4 — Add as a Teams tab

1. Open Microsoft Teams
2. Go to the channel or chat where you want the tab
3. Click **+** (Add a tab) → **Website**
4. Name: `FMS Helpdesk Tracker`
5. URL: `https://mrfpaint.github.io/fms-helpdesk-tracker/`
6. Save

---

## Files

| File | Purpose |
|------|---------|
| `index.html` | The entire app — HTML, CSS, JS in one file |
| `README.md` | This guide |

---

## Notes

- Status changes (Open, Closed, etc.) are saved in the browser's localStorage — they persist across sessions on the same device
- The app fetches emails fresh every time you click **Refresh**
- Works best on desktop; mobile view hides a few columns automatically
- No backend needed — runs entirely in the browser using Microsoft Graph API

---

*MRF Vapocure Paints · IT Department*
