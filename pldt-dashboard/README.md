# Subscriber Lookup Dashboard (PLDT / RED)

Static website: no build step. Open `index.html` or host it on GitHub Pages.

## Files
| Path | What to edit |
|---|---|
| `index.html` | Page layout (header, cards, login screen) |
| `css/style.css` | Styling |
| `js/app.js` | All dashboard logic, login, For Payment remarks, activity log |
| `js/data.js` | Subscriber records (`const DATA={...}` with PLDT, RED, VALIDATORS). Replace to update the database |
| `js/facility-data.js` | Facility checking data (`const FAC={...}`) |
| `js/view-switch.js` | Mobile / Web view toggle |
| `apps-script/Code.gs` | Google Apps Script backend (shared remarks + activity log) |
| `data/DATABASE PLDT_RED.xlsx` | Spreadsheet copy of `js/data.js` (rebuilt from the embedded data) |

## Connect your Google Sheet (shared remarks for all agents/admins)
1. Create a Google Sheet, then Extensions > Apps Script, paste `apps-script/Code.gs`, save.
2. Deploy > New deployment > Web app. Execute as: **Me**. Who has access: **Anyone**. Copy the Web app URL (ends in `/exec`).
3. In `js/app.js`, find `const LOG_URL='';` and put the URL between the quotes.
4. Commit. After editing the script later, redeploy it (Manage deployments > Edit > New version).

Tabs `ActivityLog`, `PaymentLatest`, `PaymentHistory` are created automatically.

## Host on GitHub Pages
Repo Settings > Pages > Deploy from branch > `main` / root. The site is at `https://<user>.github.io/<repo>/`.

## Notes
- Login accounts (email + password) are stored per browser; agent codes come from `js/data.js`.
- The `claude.use('db')` code in `js/app.js` only runs inside claude.ai; on GitHub Pages it is skipped and `LOG_URL` is used.
- `js/data.js` is large (~2.6 MB). GitHub's web editor can't open it, so edit it locally or replace the file by upload.
