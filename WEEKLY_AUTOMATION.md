# Weekly On-Hold Workbook Updater

This automation updates `Weekly_Operations_Report_On Hold tickets - Master file.xlsx` by:
- Pulling Zendesk `status:hold` tickets for configured groups
- Extracting/cross-checking Jira keys
- Pulling latest Jira issue status
- Updating workbook rows and appending new tickets

## 1) Configure Groups
Edit `weekly-updater.config.json`:
- `groups`: only the support groups you want included
- `workbookPath` / `outputPath`: workbook file path(s)
- `worksheetName`: target worksheet tab

## 2) Set Environment Variables (PowerShell)

```powershell
$env:ZENDESK_SUBDOMAIN = "your-subdomain"
$env:ZENDESK_EMAIL = "you@company.com"
$env:ZENDESK_API_TOKEN = "your-zendesk-token"

$env:JIRA_BASE_URL = "https://entota.atlassian.net"
$env:JIRA_EMAIL = "you@company.com"
$env:JIRA_API_TOKEN = "your-jira-api-token"
```

## 3) Run Update

```powershell
npm run update:onhold-workbook
```

## 4) Refresh Dashboard
Open `ticket-trend-dashboard-multitab.html` and click `Refresh Now`.
Tab 4 reloads the updated workbook.

## Optional: Weekly Windows Task Scheduler
Create a weekly task that runs:

```powershell
PowerShell -NoProfile -ExecutionPolicy Bypass -File "C:\Users\KASAIN\OneDrive - Capgemini\Desktop\VS Code\scripts\run-weekly-updater.ps1"
```

Use an account/session that has network/API access and valid credentials.
The runner reads credentials from process-level env vars first, then User-level env vars.
