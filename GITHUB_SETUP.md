# ApniNotes Website — GitHub Setup Guide (No Firebase, 100% Free)

Everything (website + admin panel + database + PDF files) lives in ONE GitHub
repository. No card, no billing account, ever.

---

## Step 1 — Create a GitHub account & repository
1. Go to github.com and sign up (free) if you don't have an account.
2. Click the **+** icon (top-right) → **New repository**.
3. Name it something like `apninotes-website`.
4. Set it to **Public** (required for the free GitHub Pages hosting + free
   raw file reading used below).
5. Click **Create repository**.

## Step 2 — Upload all the website files
In your new repo, click **Add file → Upload files**, then drag in
everything from this folder, **keeping the same structure**:
```
apninotes-website/
├── index.html
├── admin.html
├── github-config.js
├── data/
│   └── data.json
├── files/
│   ├── syllabus/
│   └── pyq/
└── assets/
    ├── logo.png
    └── leadership-poster.jpg
```
Commit the upload (the default commit message is fine).

## Step 3 — Fill in `github-config.js`
Open `github-config.js` in this repo (pencil/edit icon on GitHub), and fill in:
```js
const GITHUB_OWNER  = "your-github-username";
const GITHUB_REPO   = "apninotes-website";
```
Commit the change. This tells `index.html` where to fetch live data from.

## Step 4 — Turn on GitHub Pages (makes the site live)
1. In your repo, go to **Settings → Pages**.
2. Under "Build and deployment", set **Branch** to `main`, folder `/ (root)`.
3. Click **Save**. Within a minute or two you'll get a link like:
   `https://your-github-username.github.io/apninotes-website/`
4. That's your live website. Admin panel is the same link + `/admin.html`.

## Step 5 — Create a Personal Access Token (this is your admin "password")
This token lets `admin.html` save data straight into your repo. Create a
**fine-grained** token so it can ONLY touch this one repo — nothing else on
your GitHub account is at risk.
1. Go to **github.com/settings/tokens?type=beta** (Settings → Developer
   settings → Personal access tokens → Fine-grained tokens).
2. Click **Generate new token**.
3. Give it a name, e.g. `apninotes-admin`.
4. Expiration: choose something like 1 year (you can regenerate anytime).
5. **Repository access** → Only select repositories → choose
   `apninotes-website`.
6. **Permissions** → Repository permissions → **Contents** → set to
   **Read and write**. Leave everything else as "No access".
7. Click **Generate token**, then **copy it immediately** — GitHub only
   shows it once. Paste it somewhere safe (a notes app), you'll need it now.

## Step 6 — Log into the admin panel
1. Open `https://your-github-username.github.io/apninotes-website/admin.html`
2. Enter:
   - **GitHub Username**: your username
   - **Repository Name**: `apninotes-website`
   - **Personal Access Token**: the token you just copied
3. Click **Connect & Log In**.
4. Add a subject, upload a syllabus PDF, save — refresh your live website
   after ~30–60 seconds and it'll show up.

---

## Important notes

- **Never share the `/admin.html` link publicly.** Anyone with your token
  could edit your site. Your token is only saved in YOUR browser
  (localStorage) — it is not visible to visitors of your normal website.
- **If you ever think your token leaked**, go back to
  github.com/settings/tokens and delete it, then generate a new one.
- **PDF file size**: keep individual PDFs under ~20 MB for smooth uploads
  through the browser. For bigger files, upload them via GitHub's own
  "Add file → Upload files" screen directly into `files/syllabus/` or
  `files/pyq/`, then paste the resulting raw URL manually if needed.
- **This is all still 100% free** — GitHub Pages hosting, the repository
  storage (up to a very generous limit for a project like this), and the
  API calls the admin panel makes all cost nothing and never ask for a card.
- To use your own domain (apninotes.com) instead of the github.io link,
  go to Settings → Pages → Custom domain, and point your domain's DNS
  (in Hostinger) to GitHub Pages following GitHub's custom-domain docs.
