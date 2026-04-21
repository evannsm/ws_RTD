# redirect_evannsm

A redirect-only GitHub Pages site that forwards every request under
`https://evannsm.github.io/ws_RTD/*` to the matching URL under
`https://evannsmc.github.io/ws_RTD/*`.

## Why

The GitHub username `evannsm` was renamed to `evannsmc`. A recently submitted
paper contains links of the form `https://evannsm.github.io/ws_RTD/...` that
now point to a dead site. This repo restores those links by hosting a static
redirect shim at the old URL.

## How it works

- `index.html` — `<meta http-equiv="refresh">` + canonical to the new site root.
- `installation.html`, `case_studies.html`, `api_reference.html` — per-page
  meta-refresh redirects matching the top-level docs from
  `ws_RTD/_frozen_docs/docs/*.md`.
- `404.html` — JavaScript catch-all. For any path GitHub Pages can't find, it
  rewrites `window.location.pathname` onto `evannsmc.github.io`, preserving
  query string and hash. This covers the Doxygen-generated pages (classes,
  namespaces, files, etc.) without enumerating them.
- `.nojekyll` — serve files verbatim.

## Deploy

1. Push this repo to **`github.com/evannsm/ws_RTD`** (the `evannsm` account,
   repo name `ws_RTD` — required so the URL path matches).
2. On GitHub: **Settings → Pages → Source: Deploy from a branch**,
   branch `main`, folder `/` (root).
3. Wait for Pages to build, then confirm:
   - `https://evannsm.github.io/ws_RTD/` → `evannsmc.github.io/ws_RTD/`
   - `https://evannsm.github.io/ws_RTD/installation.html` → new installation page
   - `https://evannsm.github.io/ws_RTD/classes.html` (or any Doxygen page) →
     redirects via `404.html`

## Adding more pages

If you want an explicit meta-refresh for another page (instead of relying on
the 404 catch-all), copy one of the existing `<name>.html` files and update
the three occurrences of the page name.
