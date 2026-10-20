# upaction-redirect

Redirect for the bare domain `https://upaction.pro` -> `https://www.upaction.pro` (301, path and query kept).
Hosted on Netlify (free plan) only because NIC.UA cannot point the bare domain at Railway and has no HTTPS for it.
The site itself lives in `upaction-landing` (Railway); nothing here serves content.

Files: `_redirects` (the one rule), `index.html` (fallback), `netlify.toml` (publish this folder).

## Setup (once)
1. Netlify -> Add new site -> Deploy manually -> drop this folder (or import this repo from Git).
2. Site configuration -> Domain management -> Add a domain -> `upaction.pro` (primary). Do not add `www`: it stays on Railway.
3. At NIC.UA change the DNS record `@` A from `135.181.41.169` to `75.2.60.5`. Nothing else.
4. Domain management -> HTTPS: wait for the certificate (Let's Encrypt), then enable "Force HTTPS".

## Check
    curl -sI https://upaction.pro/invite/AbC12345   # 301 -> https://www.upaction.pro/invite/AbC12345
    curl -sI "https://upaction.pro/uk/?utm_source=x" # 301 keeps ?utm_source=x

## Rollback
NIC.UA: set `@` A back to `135.181.41.169`. The Netlify site can stay or be deleted.

## Notes
- `ftp.upaction.pro` is a CNAME to the bare domain, so it follows this change.
- Before the record is changed, check that nothing else uses the bare domain's A record (webmail etc.).
- If the apex ever gets ALIAS/ANAME or moves to a DNS host that supports it, this repo is no longer needed:
  add `upaction.pro` to the Railway service and redirect there.
