# Electrician Classes – NSTI Calicut (GitHub Pages)

Static version of the Google Site *Electrician classes* (26 interactive pages), hosted free on GitHub Pages. The home page (`index.html`) is **generated automatically** from the HTML files in `pages/`, arranged in teaching order.

```
├── index.html                 ← AUTO-GENERATED home page (don't edit by hand)
├── admin.html                 ← Admin page: add / replace / delete lessons from the browser
├── pages.json                 ← AUTO-GENERATED list of pages (used by admin.html)
├── site.config.json           ← Site title, subtitle, footer text
├── pages/                     ← Put every lesson / tool HTML file here
├── scripts/build-index.mjs    ← Builds index.html from pages/
└── .github/workflows/build-index.yml  ← Runs the build on every change
```

---

## Part A — One-time setup (about 10 minutes)

### 1. Create the repository
1. Sign in at **github.com** → click **+** (top right) → **New repository**.
2. Name it, e.g. `electrician-classes`. Choose **Public** (GitHub Pages is free for public repos).
3. Click **Create repository**.

### 2. Upload these files
1. On the new repo page, click **uploading an existing file**.
2. Unzip the package on your computer and drag **everything inside it** (including the hidden `.github` folder) into the upload box.
   - Windows hides nothing here, but on **macOS** press `Cmd + Shift + .` in Finder to show the `.github` folder before dragging.
   - If drag-and-drop skips `.github`, create it manually: **Add file → Create new file**, type the name `.github/workflows/build-index.yml`, paste the file's contents, commit.
3. Click **Commit changes**.

### 3. Allow the automatic index update
**Settings → Actions → General → Workflow permissions** → select **Read and write permissions** → **Save**.

### 4. Turn on GitHub Pages
**Settings → Pages → Build and deployment** → Source: **Deploy from a branch** → Branch: **main**, folder **/ (root)** → **Save**.

After 1–2 minutes the site is live at:
`https://<your-username>.github.io/electrician-classes/`

### 5. Create the admin token (once)
1. GitHub → your avatar → **Settings → Developer settings → Personal access tokens → Fine-grained tokens → Generate new token**.
2. Name: `site-admin`. Expiration: 1 year (or your choice).
3. **Repository access → Only select repositories →** pick `electrician-classes`.
4. **Permissions → Repository permissions → Contents → Read and write**. Leave everything else as is.
5. **Generate token** and copy it (starts with `github_pat_`). Keep it private — it is your admin password.

---

## Part B — Adding pages (everyday use)

### Option 1: Admin page (easiest)
1. Open `https://<your-username>.github.io/electrician-classes/admin.html` (also linked in the site footer).
2. Enter owner, repo, and paste the token → **Connect & load pages**.
3. Choose an HTML file (or paste HTML), then fill in:

| Field | Purpose |
|---|---|
| **Title** | Card name on the home page (taken from the file's `<title>` if blank) |
| **Section / Module** | Groups pages, e.g. `Module 1 – Basic Electricity` |
| **Section order** | Position of the section (1, 2, 3…) |
| **Order inside section** | Position of the page within its section |
| **Description** | Optional one-line summary on the card |

4. **Publish page**. Within about a minute, `index.html` is rebuilt with the new page in its correct place.
5. The same page lists all existing pages with a **Delete** button.

### Option 2: Upload directly on GitHub
1. Open the `pages` folder in the repo → **Add file → Upload files** → drop your `.html` file(s) → **Commit**.
2. Ordering comes from either:
   - **File name prefix**: `01-introduction.html`, `02-ohms-law.html`, … (simplest), or
   - **Meta tags** inside the file's `<head>`:
     ```html
     <meta name="section" content="Module 1 – Basic Electricity">
     <meta name="section-order" content="1">
     <meta name="order" content="2">
     <meta name="description" content="Ohm's law with worked examples">
     ```
3. The index rebuilds automatically after the commit.

### Changing order later
Edit a page's `order` / `section-order` (re-publish from Admin with new numbers, or edit the meta tags on GitHub). The home page re-sorts itself.

### Changing site title / footer
Edit `site.config.json` on GitHub → commit → index rebuilds.

---

### Current module layout
| # | Section | Pages |
|---|---|---|
| 1 | Electrical Machines & Control | DOL starter, Logic builder, Alternator synchronisation, Synchronous motor, Single phasing preventer |
| 2 | Circuits & Power Systems | Series & parallel, Power factor improvement, Power system terms, Protective earthing |
| 3 | Electronics | Resistor colour code, Capacitor charging, CRO, Transistor biasing, CE amplifier, UJT, UJT relaxation oscillator, Op-amp, Number systems, Logic gates, IC 555 & CD4017 |
| 4 | Installation, Estimation & Appliances | Estimation & costing, Water pump selection, Shopping mall systems, EV charging, BLDC fan, Induction cooker |

File names follow `<section><order>-<name>.html` (e.g. `305-ce-amplifier.html`) so the folder also lists in teaching order. Every page has a small **⌂ All lessons** button (bottom-left) back to the home page; the Admin page adds it automatically to new uploads.

## Part C — Images and other files
Pages can only show images the site can reach:
- Put images in a folder, e.g. `pages/img/`, via **Add file → Upload files**, and reference them as `<img src="img/diagram.png">` from a page in `pages/`.
- Google Drive / Google Sites image links usually stop working outside Google — download and re-upload them.

## Troubleshooting
| Problem | Fix |
|---|---|
| New page doesn't appear | Repo → **Actions** tab → check the latest "Rebuild index" run. Red ✗ usually means step A3 (write permission) was missed. |
| Admin says `401 Bad credentials` | Token expired or mistyped — create a new one (A5). |
| Admin says `403` / `Resource not accessible` | Token lacks **Contents: Read and write** or wasn't given access to this repo. |
| Site shows old version | GitHub Pages caches ~1 minute — refresh with `Ctrl + F5`. |
| Want to rebuild manually | **Actions → Rebuild index → Run workflow**. |

## Security notes
- The token lives only in your browser; untick **Remember** on shared/lab computers.
- `admin.html` is public but useless without your token. Revoke the token anytime under Developer settings.
