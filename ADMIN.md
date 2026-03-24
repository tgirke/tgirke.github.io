# Girke Lab Site — Administration Guide

Internal documentation for site maintenance and content updates.  
Live site: <https://girke.bioinformatics.ucr.edu/>  
Repository: <https://github.com/tgirke/tgirke.github.io>

---

## Table of Contents

- [Repository structure](#repository-structure)
- [Local setup and preview](#local-setup-and-preview)
- [Daily workflow](#daily-workflow)
- [GitHub Actions and deployment](#github-actions-and-deployment)
- [Adding and updating content](#adding-and-updating-content)
- [Theme and styling](#theme-and-styling)
- [Google Search Console](#google-search-console)
- [Troubleshooting](#troubleshooting)

---

## Repository structure

```
tgirke.github.io/
├── _quarto.yml               # site config: navbar, theme, metadata
├── index.qmd                 # homepage
├── assets/
│   ├── logo.png              # navbar logo
│   ├── custom.scss           # light mode CSS overrides (UCR blue navbar)
│   └── custom-dark.scss      # dark mode CSS overrides
├── bio/index.qmd             # biography page
├── contact/index.qmd         # contact page
├── members/
│   ├── index.qmd             # members landing page
│   └── members.qmd           # members content
├── research/
│   └── publications/
│       └── publications.qmd  # publication list (reverse numbered)
├── software/index.qmd        # software packages
├── teaching/index.qmd        # teaching and courses
├── positions/index.qmd       # open positions
├── CNAME                     # custom domain — do not delete
├── README.md                 # public-facing repo description
└── ADMIN.md                  # this file
```

---

## Local setup and preview

```bash
# Clone the repo
git clone git@github.com:tgirke/tgirke.github.io.git
cd tgirke.github.io

# Preview locally (ChromeOS/headless Linux — always use --no-browser)
quarto preview --no-browser
# Open http://localhost:5675/ in browser

# Render full site
quarto render
```

Requires Quarto installed locally: <https://quarto.org/docs/get-started/>

---

## Daily workflow

```bash
git pull                        # always pull before editing
# ... make changes ...
quarto preview --no-browser     # check locally
git add -A
git commit -m "Description of changes"
git push origin main            # triggers automatic deploy via GitHub Actions
```

---

## GitHub Actions and deployment

Every push to `main` triggers `.github/workflows/publish.yml` which renders
the site and deploys to GitHub Pages automatically. Since this site has no R
code chunks, the build is fast (~1-2 minutes).

Monitor builds at: <https://github.com/tgirke/tgirke.github.io/actions>

**Important:** The `CNAME` file at the repo root must never be deleted — it
maps the custom domain `girke.bioinformatics.ucr.edu` to this repo. All other
lab repos (`GEN242` etc.) inherit this domain automatically.

---

## Adding and updating content

### Publications

The publications page uses a reverse-numbered CSS counter. The list is in
`research/publications/publications.qmd`. Each entry uses `1.` as the list
marker — the CSS handles the countdown display.

When adding new publications, add them at the **top** of the list and update
the counter in `assets/custom.scss`:

```scss
div.publications ol {
  counter-reset: pub-counter 109;  /* set to total publications + 1 */
}
```

### Members

Edit `members/members.qmd` directly. Follow the existing card layout pattern
for consistency.

### Navigation

The navbar is configured in `_quarto.yml`. To add a new section:

**1.** Create a new `.qmd` file or directory  
**2.** Add an entry to the navbar in `_quarto.yml`:

```yaml
navbar:
  left:
    - text: "New Section"
      href: newsection/index.qmd
```

---

## Theme and styling

The site uses the **slate** Quarto theme (dark) with a UCR blue (`#003da5`)
navbar in light mode.

**`assets/custom.scss`** — light mode overrides:
- UCR blue navbar (`#003da5`)
- Navbar text and icon colors
- Publication list reverse counter
- Code output box styling

**`assets/custom-dark.scss`** — dark mode overrides:
- Dark navbar (`#1a1a1a`)
- Sidebar and text colors
- Code output box styling

To change the navbar color, update `background-color` in `custom.scss`:

```scss
.navbar {
  background-color: #003da5 !important;  /* UCR blue */
}
```

---

## Google Search Console

The site is verified with Google Search Console via a meta tag in `_quarto.yml`:

```yaml
format:
  html:
    include-in-header:
      text: |
        <meta name="google-site-verification" content="YOUR_CODE">
```

**Do not remove this tag** — removing it loses Search Console verification.

Sitemap is submitted at:
`https://girke.bioinformatics.ucr.edu/sitemap.xml`

All project repos (`GEN242` etc.) inherit verification from this root domain
automatically — no separate verification needed for those.

---

## Troubleshooting

### Site not updating after push

Check the Actions tab for build errors. If the build succeeded but the site
looks old, hard-refresh the browser (`Ctrl+Shift+R`).

### Custom domain lost after deploy

If `girke.bioinformatics.ucr.edu` stops working, check:
1. The `CNAME` file exists in the repo root
2. GitHub Pages settings show the custom domain — **Settings → Pages**
3. The `CNAME` is listed under `resources:` in `_quarto.yml` so it gets
   copied to `docs/` on every build:

```yaml
project:
  resources:
    - CNAME
```

### Dark mode icons invisible

If the toggle or search icons are not visible in dark or light mode, the fix
is in `custom.scss` and `custom-dark.scss` — see the icon fix rules targeting
`a.quarto-color-scheme-toggle` and `div#quarto-search`.
