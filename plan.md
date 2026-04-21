# Redirect site plan: evannsm.github.io/ws_RTD → evannsmc.github.io/ws_RTD

## Context
- Paper links point to `https://evannsm.github.io/ws_RTD/...` (old username).
- All content now lives at `https://evannsmc.github.io/ws_RTD/...` (new username).
- This repo must deploy to `evannsm/ws_RTD` (GitHub Pages, Project site) so that
  `https://evannsm.github.io/ws_RTD/<path>` resolves here and forwards users.
- Mirror 1:1 with HTML meta-refresh + `<link rel="canonical">`.

## Strategy
1. `index.html` — meta-refresh to new root.
2. `404.html` — JS catch-all that rewrites path/query/hash onto `evannsmc.github.io`.
   Covers every Doxygen-generated page we can't enumerate statically.
3. Per-page meta-refresh HTMLs for the known top-level docs (from `_frozen_docs/docs/*.md`):
   - `installation.html`
   - `case_studies.html`
   - `api_reference.html`
4. `.nojekyll` — serve files verbatim, no Jekyll processing.
5. `README.md` — explain what the repo is for and deploy instructions.

## Tasks
- [x] Inspect `ws_RTD/_frozen_docs/docs/` to learn the top-level page names.
- [x] Write `index.html` (root redirect).
- [x] Write `404.html` (path-preserving JS catch-all).
- [x] Write per-page meta-refresh HTMLs for known `.md` pages.
- [x] Add `.nojekyll`.
- [x] Rewrite `README.md` with purpose + deploy steps.
- [x] Push to `github.com/evannsm/ws_RTD` (remote already configured as `github-evannsm:evannsm/ws_RTD`).
- [x] Switch deploy to GitHub Actions: add `.github/workflows/pages.yml`.
- [x] Rewrite README in first-person / notes-to-self voice.
- [ ] User action: Settings → Pages → **Source: GitHub Actions** (one-time toggle).
- [ ] User action: visit `https://evannsm.github.io/ws_RTD/installation.html` to verify.
