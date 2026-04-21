# redirect shim for evannsm → evannsmc

I renamed my GitHub from `evannsm` to `evannsmc`, which broke the links in a
paper I already submitted. This repo is the dumb little static site that lives
at the old URL and bounces visitors to the new one.

Old: `https://evannsm.github.io/ws_RTD/...`
New: `https://evannsmc.github.io/ws_RTD/...`

## What's in here

- `index.html` — meta-refresh to the new site root, with a `<link rel="canonical">`
  so crawlers carry the ranking over.
- `installation.html`, `case_studies.html`, `api_reference.html` — one meta-refresh
  per page (matching the top-level `.md` files in `ws_RTD/_frozen_docs/docs/`). These
  give a 200 response, which is better for SEO than the 404 fallback.
- `404.html` — JS catch-all. GitHub Pages serves this for any path that isn't
  explicitly a file in the repo. The script rewrites `window.location.pathname`
  onto `evannsmc.github.io`, preserving the query string and hash. This is what
  handles all the Doxygen-generated pages (`classes.html`, `namespaces.html`, etc.)
  without me having to enumerate them.
- `.nojekyll` — don't let Pages touch the files.
- `.github/workflows/pages.yml` — deploys on push to `main`.

## Deploy

Pushing to `main` on `evannsm/ws_RTD` triggers the workflow. First time only:

1. Settings → Pages → **Source: GitHub Actions**.
2. Push anything; the `pages.yml` workflow builds and deploys.
3. Deployed URL shows up in the Actions run summary.

## Sanity checks after deploy

- `https://evannsm.github.io/ws_RTD/` → hits `index.html` → new root.
- `https://evannsm.github.io/ws_RTD/installation.html` → explicit page redirect.
- `https://evannsm.github.io/ws_RTD/classes.html` (or any Doxygen page) → bounces
  through `404.html`.

## Adding another explicit page

Copy one of the per-page files and replace the three occurrences of the page name.
Only worth doing for pages that are actually cited somewhere (the 404 fallback covers
the rest — the only difference is SEO signal).
