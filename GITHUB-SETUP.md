# Upload Medra to GitHub

## Easiest: browser upload

1. Extract `medra-github-ready.zip` on your computer.
2. Go to https://github.com/new and create a **private** repository named `medra`. Add a README so the repository has a default branch.
3. Open the repository and choose **Add file → Upload files**.
4. Open the extracted `medra` folder. Upload its contents, keeping the folders intact. Upload the project files, not the ZIP itself and not an extra parent folder. Replace GitHub's starter README with the provided README.
5. Click **Commit changes** with the message `Import Medra frontend prototype`.
6. Hidden files such as `.gitignore` and `.gitattributes` may not appear in your file picker. Enable hidden files, or add those through **Add file → Create new file**. GitHub can also restrict browser uploads to `.github/` workflow files; if that occurs, add the workflow later through GitHub Desktop or the terminal. The app does not require the workflow to run.

The top level should show `package.json`, `package-lock.json`, `README.md`, `src/`, `scripts/`, `docs/`, and `previews/`.

## VS Code: publish the local folder

1. Extract the ZIP and open the inner `medra` folder in VS Code.
2. Open **Source Control** and select **Initialize Repository**.
3. Review staged files. Do not include `node_modules/`, `dist/`, `.medra/`, or secrets.
4. Stage the files and commit with `Import Medra frontend prototype`.
5. Choose **Publish Branch**, sign in to GitHub, and select a private repository.

If VS Code asks for Git, install it from https://git-scm.com/downloads and reopen VS Code.

## Terminal alternative

For a new, empty GitHub repository created without README/license/gitignore, run these commands inside the extracted `medra` folder, replacing `YOUR_USERNAME`:

```sh
git init -b main
git add .
git commit -m "Import Medra frontend prototype"
git remote add origin https://github.com/YOUR_USERNAME/medra.git
git push -u origin main
```

Authenticate through GitHub's supported Git credential flow. Do not place an access token in the repository URL or source files. If you used the browser-upload method instead, clone that repository rather than creating another independent Git history.

## Run it

For the preserved preview, open `previews/index.html` directly. For development, install Node.js 24 LTS and run:

```sh
npm ci
npm run dev
```

Then visit http://localhost:5173. Saving JSX rebuilds it; reload the browser to see changes.

## Continue with another coding assistant

Paste this into the assistant in your editor after opening this repository:

> Continue this existing Medra project. Read README.md, docs/CURRENT-STATE.md, docs/permission-matrix.md and docs/onboarding-checklists.md, then inspect the actual src/apps files. Preserve the current role screens, menu items, visual styling and working interactions. This is a frontend-only prototype; do not assume the legacy Supabase notes describe the current source, and do not add backend services or paid subscriptions unless I ask. Use src/apps as the editable source, not the compiled previews. First run npm ci, npm run build and the browser smoke tests; report concrete failures before changing features. Keep Admin, Support and Super Admin as separate experiences. Clearly distinguish demo behavior from live functionality. After changes, rebuild and test the affected role and combined preview.

## Optional: publish a demonstration later

Putting code in a repository does not publish a live website. `npm run build` produces `dist/` for a static host. A publicly hosted demo exposes the staff demo screens too, because there is no real access control. Keep the demonstration separate from any future live marketplace.

Reference: https://docs.github.com/en/migrations/importing-source-code/using-the-command-line-to-import-source-code/adding-locally-hosted-code-to-github
