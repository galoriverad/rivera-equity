# Rivera Equity (GitHub Pages)

Phone-friendly static dashboard for **Rivera's Equity Fund**, published from this repo as a free GitHub Pages site.

**Live URL (after Pages is enabled):** `https://<github-user>.github.io/rivera-equity/`

Repo name should be `rivera-equity` so the site is served under the `/rivera-equity/` subpath. All asset paths are **relative** (no leading `/`) so the app works under that base.

## What this is

- Same holdings / mix / tick-flash UI as the private PWA dashboard
- **Sign in with Google** (GIS) — client-side only
- Fixed allowlist (no Members API, no Node, no SQLite):
  - `galo.riverad@gmail.com` → **owner** (Admin local overrides in `localStorage`)
  - `blair.besson@gmail.com` → **viewer** (Admin + Members hidden)
- Session stored in `sessionStorage` key `rivera_equity_session`

## Privacy / security note

This repository is **public** if you push it as a normal public GitHub repo. The dashboard seed data (quantities, cost bases, recommendations) ships in `index.html` and is visible to anyone who clones or views the source, even though the login overlay gates casual browsing. Do not put passwords, private keys, or `.env` files here. The Google OAuth **client id** is public by design.

Client-side allowlisting is a soft gate (anyone can inspect JS). Use the private server app for stronger session cookies + Members management.

## Enable GitHub Pages

1. Push this folder as the root of repo `rivera-equity` (or put these files on the `main` branch / `docs` / Pages branch).
2. GitHub → **Settings → Pages → Source**: Deploy from branch `main` / `/ (root)` (or your chosen branch).
3. Wait for the site at `https://<github-user>.github.io/rivera-equity/`.

## Google OAuth Authorized JavaScript origins

In [Google Cloud Console](https://console.cloud.google.com/) → APIs & Services → Credentials → your OAuth 2.0 Client ID, add:

- `https://<github-user>.github.io`
- `https://<github-user>.github.io/rivera-equity`

(No trailing slash on the origin; the second entry is sometimes needed depending on how GIS resolves the origin for project Pages.)

Also useful for local checks:

- `http://localhost:8080` (or whatever static server you use)

Client ID used by this site (also in `config.js`):

`524597924171-tep5eluh0ji0h1t0he3ht8bmdhvonlnf.apps.googleusercontent.com`

## Local preview

```bash
cd rivera-equity-pages
python3 -m http.server 8080
# open http://localhost:8080/
```

## Files

| File | Purpose |
|------|---------|
| `index.html` | Dashboard + login overlay + GIS |
| `config.js` | Public client id + owner/viewer emails |
| `manifest.webmanifest` | PWA manifest (relative paths) |
| `service-worker.js` | Simple static shell cache |
| `icons/` | App icons |
| `.nojekyll` | Tell Pages not to run Jekyll |

## Members

Members management exists only on the private Node server. On Pages, the allowlist is fixed in `config.js`. The Members control shows a short note instead of linking to an API.
