---
name: deploy
description: Publish the Evimero Capital site (index.html) to production. Use when the user asks to deploy, publish, ship, or push the site live. Confirm the actual hosting target with the user the first time, then record it here.
---

# Deploy the Evimero Capital site

Static single-file site (`index.html` + `ms10668863.txt` at the web root). The `ms10668863.txt` file is a **Microsoft 365 domain-ownership verification file and must stay at the site root** — never delete or move it.

## ⚠️ Confirm the hosting target first

The repo does not (yet) contain deployment config (no `CNAME`, no GitHub Actions workflow, no Netlify/Vercel config). Before deploying, **ask the user where the site is actually hosted** and record the answer in this skill so future deploys are one step. Likely options below.

### If GitHub Pages
1. Ensure Pages is enabled in repo settings, serving from the default branch root.
2. Merge changes to the deploy branch; Pages rebuilds automatically.
3. For the custom domain `evimerocapital.com.au`, a `CNAME` file containing `evimerocapital.com.au` must exist at the repo root, and DNS must point at GitHub Pages. (Do not add `CNAME` unless the user confirms Pages is the host.)

### If Netlify / Vercel
- Connect the repo; publish directory = repo root, no build command. Pushes to the production branch auto-deploy.

### If manual / FTP to their own host
- Upload `index.html` and `ms10668863.txt` to the web root. Get the credentials/host from the user (never hardcode secrets in the repo).

## Pre-deploy checklist

1. Run the `preview` skill and screenshot desktop + mobile — confirm the change renders.
2. If SEO/social metadata was touched, run `seo-check`.
3. ⚠️ Remember the **contact form is currently a non-functional stub** (fake success, sends nothing). Don't deploy a "working contact us" claim until it's wired to a real endpoint.
4. Commit with a clear message and push to the correct branch (do not push to a protected branch without permission).
5. Verify the live URL after DNS/CDN propagation.

## Record actual setup here

> _Hosting target: (unknown — confirm with user)_
> _Production branch: (unknown)_
> _Custom domain: evimerocapital.com.au (Microsoft 365 verified via ms10668863.txt)_
