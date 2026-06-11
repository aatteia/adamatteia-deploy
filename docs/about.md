# adamatteia-deploy

## What this repo is

This is the **deployment target** for https://adamatteia.com. It contains only built static files — no source code lives here.

GitHub Pages serves whatever is in the `main` branch of this repo directly at `adamatteia.com`. Cloudflare sits in front as the DNS provider and handles HTTPS.

**Do not edit files in this repo directly.** All changes should be made in the source repo and deployed via its `deploy.sh` script.

---

## How the pipeline works

```
[source repo]  →  npm run build  →  out/  →  copied here  →  git push  →  adamatteia.com
```

The source repo builds the site to a static `out/` folder, clears this repo's contents (preserving `CNAME`, `.nojekyll`, `.gitignore`), copies the new build in, then commits and pushes. GitHub Pages picks up the change within 1–3 minutes.

---

## Current live site

**Source:** `/Users/aatteia/working/adamatteia-website-alt3`  
**Deployed:** 12 June 2026

---

## Deploying a new or updated site

From the source repo, run:

```bash
./deploy.sh
```

This repo must exist at `../adamatteia-deploy` relative to the source repo for the script to work. Do not move or rename this directory.

If you are deploying a brand new design from a different source repo, the same rule applies — the final step is always copying static output into this repo and pushing it. See the source repo's `docs/publishing.md` for full details.

---

## Files that must never be deleted

| File | Purpose |
|---|---|
| `CNAME` | Tells GitHub Pages to serve this repo at `adamatteia.com` — deleting it breaks the custom domain |
| `.nojekyll` | Prevents GitHub Pages from running Jekyll on the output — required for Next.js static exports |
