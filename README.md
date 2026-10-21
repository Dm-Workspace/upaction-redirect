# upaction-redirect

> **Superseded (2026-10-21):** the bare domain is now served from Cityhost with `cityhost/.htaccess` (a real 301 and a Let's Encrypt
> certificate). The GitHub Pages files below (`index.html`, `404.html`, `CNAME`) are kept only until old DNS caches have expired, then this repo can be archived or deleted.
> The `cityhost/` folder is the live configuration.

Sends visitors of the bare domain `https://upaction.pro` to `https://www.upaction.pro`, keeping the path, query and hash
(so `https://upaction.pro/invite/AbC12345` ends up on the site's invite route). Nothing else lives here:
the site itself is `upaction-landing` (Railway). Served by GitHub Pages only because NIC.UA cannot point the bare domain
at Railway and has no HTTPS for it.

Files: `index.html` (the root), `404.html` (GitHub Pages serves it for every other path), `CNAME` (custom domain), `.nojekyll`.
The redirect is a script plus a meta refresh, not an HTTP 301; the target host is fixed in both files.

## DNS (NIC.UA)
`@` A records: `185.199.108.153`, `185.199.109.153`, `185.199.110.153`, `185.199.111.153`. Nothing else changes.

## HTTPS
Repository Settings -> Pages -> Enforce HTTPS (available after GitHub issues the certificate; can take up to 24 h).

## Rollback
NIC.UA: set `@` A back to `135.181.41.169` (the registrar's parking page).

## Notes
- `ftp.upaction.pro` is a CNAME to the bare domain and follows it.
- A public repository is required for free GitHub Pages: keep nothing private here.
