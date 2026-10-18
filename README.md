# ChemPath Batch Rota

A single-page bench rota for clinical laboratory shifts. It runs on GitHub Pages with no server.

- **Public view** (default): Schedule, Table, Hours and By lab technologist tabs. Reads `schedule.json`.
- **Admin view**: *Admin sign in* at the bottom of the page. Build and edit the rota here.

## 1. Turn on GitHub Pages
Settings → Pages → Deploy from a branch → `main` → `/ (root)`.
Site: `https://jayb-art.github.io/ChemPath-Batch-Rota/`

## 2. Create the private data repository
All schedules, the team list and restrictions are saved here, so they are not tied to one browser.
1. On GitHub create a **private** repository named `ChemPath-Batch-Rota-data` and tick **Add a README**.
2. Create a fine-grained token (Settings → Developer settings → Personal access tokens) that covers
   **both** `ChemPath-Batch-Rota` and `ChemPath-Batch-Rota-data`, with **Contents: Read and write** and a short expiry.
3. After signing in to the admin view, paste the token when asked. It is kept in that browser only.

If you rename the data repository, change `CONFIG.data` near the top of the script in `index.html`.
The first time you sign in with a token, anything already saved in that browser is copied into the data repository.

## 3. Settings block
Open `index.html`, find `var CONFIG`, and fill in the approver email, the EmailJS values and (optionally) the data repository.

### EmailJS (sends the approval code)
1. Create an EmailJS account and add an email service.
2. Create a template. Set **To Email** to the approver address. Use `{{requester_name}}`, `{{requester_email}}`, `{{code}}`, `{{expires_minutes}}` in the body.
3. Add `https://jayb-art.github.io` to the allowed origins in EmailJS.

## 4. Admin profiles
1. Someone clicks **Admin sign in → Request admin access** with their name and email.
2. A random 8-character code is emailed to the approver only.
3. If the approver agrees, they pass the code on and the person chooses a password.
4. Codes expire after 15 minutes and lock after 5 wrong tries.

## 5. Publishing
Click **Publish schedule**. It writes `schedule.json` to this repository using the same token. **Download file** gives you the file to upload by hand.

## Limits to know
- Admin sign-in profiles and the token are stored per browser, so each new browser needs its own approval and token.
  The schedules themselves load from the data repository.
- Two admins saving at the same moment: the second save re-reads the file and merges, so different periods are never lost.
  If both edit the same period, the last save wins.
- Sign-in checks run in the browser, so they deter casual visitors but are not strong security.
  The real protection is the token and write access to the repositories.
- `schedule.json` is public and holds names and shifts only. Keep the data repository private because it holds restrictions.
