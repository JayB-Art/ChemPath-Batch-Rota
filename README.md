# ChemPath Batch Rota

A single-page bench rota for clinical laboratory shifts. It runs on GitHub Pages with no server.

- **Public view** (default): Schedule, Hours and By scientist tabs. Reads `schedule.json`.
- **Admin view**: *Admin sign in* at the bottom of the page. Build and edit the rota here.

## 1. Turn on GitHub Pages
Settings → Pages → Deploy from a branch → `main` → `/ (root)`.
Site: `https://jayb-art.github.io/ChemPath-Batch-Rota/`

## 2. Fill in the settings block
Open `index.html` and find `var CONFIG` near the top of the script:

| Setting | What to put |
|---|---|
| `approverEmail` | The one email address that receives approval codes |
| `emailjs.serviceId / templateId / publicKey` | From your EmailJS account (below) |
| `github.owner / repo / branch / path` | Already set to this repository |

### EmailJS (sends the approval code)
1. Create a free account at emailjs.com and add an email service.
2. Create a template. Set **To Email** to the approver address (fixed in the template).
   Use these variables in the body: `{{requester_name}}`, `{{requester_email}}`, `{{code}}`, `{{expires_minutes}}`.
3. In EmailJS, add `https://jayb-art.github.io` to the allowed origins.
4. Copy the Service ID, Template ID and Public Key into `CONFIG`.

Until this is filled in, nobody can create an admin profile.

## 3. Admin profiles
1. Someone clicks **Admin sign in → Request admin access** and enters their name and email.
2. A random 8-character code is emailed to the approver only.
3. If the approver agrees, they give the code to that person, who enters it and chooses a password.
4. The code expires after 15 minutes and locks after 5 wrong tries.

## 4. Publishing
Click **Publish schedule**. The first time, it asks for a GitHub token:
create a *fine-grained* token for this repository only, with **Contents: Read and write** and a short expiry.
It is saved in that browser only. **Download file** gives you `schedule.json` to upload by hand instead.

## Limits to know
- All admin data (team, restrictions, drafts, profiles) lives in the browser used to edit. Use **Backup** and **Restore** to move it.
  Profiles do not travel with backups, so each browser needs its own approval.
- With no server, the sign-in and code checks run in the browser. They stop casual visitors but are not strong security.
  The real protection is the GitHub token and write access to the repository.
- `schedule.json` is public. It holds names and shifts only.
