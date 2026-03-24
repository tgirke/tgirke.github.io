# Girke Lab Website

Lab website for the Girke Lab at UC Riverside, built with [Quarto](https://quarto.org)
and hosted on GitHub Pages.

Live site: <https://girke.bioinformatics.ucr.edu>

## Local preview

```bash
git clone git@github.com:tgirke/girkelab.git
cd girkelab
quarto preview --no-browser
```

Open link given at command prompt in your browser.

## Structure

```
girkelab/
├── _quarto.yml          # site config: navbar, theme, execution
├── index.qmd            # homepage
├── assets/
│   ├── logo.png         # navbar logo
│   ├── favicon.ico      # browser tab icon
│   └── custom.scss      # CSS overrides on top of slate theme
├── about/index.qmd
├── people/
│   ├── thomas_girke.qmd
│   ├── members.qmd
│   └── contact.qmd
├── research/
│   ├── publications/index.qmd
│   ├── projects/index.qmd
│   └── repositories/index.qmd
├── teaching/index.qmd
├── positions/index.qmd
├── links/
│   ├── public.qmd
│   └── ucr.qmd
└── .github/workflows/publish.yml
```

## Deployment

Every push to `main` triggers GitHub Actions which renders the site
and deploys to GitHub Pages automatically.

**One-time setup:** Go to Settings → Pages → Source → GitHub Actions.

## Safest GitHub commit routine for this site 

```
# 1. Check what git sees — review before committing
git status

# 2. Stage everything (new, modified, and deleted files)
git add -A

# 3. Review exactly what's staged before committing
git diff --staged --stat

# 4. If it looks right, commit
git commit -m "Add lab site structure and members page"

# 5. Push
git push origin main

# Fast one liner
git add -A; git commit -m "edits"; git push origin main

```

