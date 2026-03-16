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

Open <http://localhost:5675/> in your browser.

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
