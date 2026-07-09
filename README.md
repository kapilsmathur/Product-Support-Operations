# Ticket Trend Dashboard

Static dashboard files plus a workbook updater used to refresh the On Hold ticket view.

## Files

- `index.html`: GitHub Pages entry point. Redirects to the main dashboard.
- `ticket-trend-dashboard-multitab.html`: main multi-tab dashboard.
- `ticket-trend-dashboard.html`: single dashboard variant.
- `scripts/update-onhold-workbook.mjs`: workbook updater.
- `weekly-updater.config.json`: updater configuration.

## Publish To GitHub Pages

1. Create a new empty GitHub repository.
2. Push this folder to the `main` branch.
3. In GitHub, open `Settings` > `Pages`.
4. Under `Build and deployment`, choose `Deploy from a branch`.
5. Select branch `main` and folder `/ (root)`.
6. Save and wait for the Pages URL.

Because `index.html` exists at the repo root, GitHub Pages will open the dashboard automatically.

## Push With Git

Run these commands from this folder after Git is installed:

```powershell
git init
git add .
git commit -m "Initial dashboard publish"
git branch -M main
git remote add origin https://github.com/YOUR-USERNAME/YOUR-REPO.git
git push -u origin main
```

## Update The Workbook Locally

Set the required environment variables in PowerShell:

```powershell
$env:ZENDESK_SUBDOMAIN = "your-subdomain"
$env:ZENDESK_EMAIL = "you@company.com"
$env:ZENDESK_API_TOKEN = "your-zendesk-token"

$env:JIRA_BASE_URL = "https://entota.atlassian.net"
$env:JIRA_EMAIL = "you@company.com"
$env:JIRA_API_TOKEN = "your-jira-api-token"
```

Then run:

```powershell
npm install
npm run update:onhold-workbook
```

After the workbook update finishes, open `ticket-trend-dashboard-multitab.html` and use `Refresh Now`.

## Notes

- `.gitignore` excludes `node_modules/` and `*.xlsx` so dependencies and workbook data are not published.
- If you want a different dashboard file as the landing page, update `index.html`.