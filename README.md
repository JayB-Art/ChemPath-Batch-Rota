# ChemPath Batch Rota

A single-page bench rota for clinical laboratory shifts. No server or account is needed.

- **Public view** (default): Schedule, Hours, and By scientist tabs. Reads `schedule.json`.
- **Admin view**: click *Admin sign in* at the bottom of the page. Build and edit the rota here.

## Publish with GitHub Pages
1. In the repo go to **Settings → Pages**, set Source to *Deploy from a branch*, branch `main`, folder `/ (root)`.
2. The site appears at `https://jayb-art.github.io/ChemPath-Batch-Rota/`.

## Updating the public schedule
1. Open the site, click **Admin sign in**, create a password (first time only) and edit the rota.
2. Click **Download schedule.json**.
3. In GitHub, upload it to the repo root, replacing the old file, and commit.
4. The public page updates within a minute or two.

## Where data lives
Admin data (team, restrictions, drafts) is stored in the browser you edit in. Use **Backup** to save it
as a file and **Restore** to load it on another computer. Keep backups private.

## Security
The admin password is checked in the browser, so it only deters casual visitors. The real protection is that
only people with write access to this repository can change what the public sees. `schedule.json` is public,
so it should contain only names and shifts. It does not include restrictions or days off.
