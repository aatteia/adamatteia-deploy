# adamatteia-deploy — GitHub Pages deploy repo

This repository contains **only built output** for https://adamatteia.com. It is the deployment
target for the `aatteia/adamatteia-website-alt3` source repo.

**Do not edit files here directly.** All changes must go through the source repo and the build
pipeline. Editing HTML/CSS/JS here directly will be overwritten on the next deploy.

## How this works

| Layer | Service |
|---|---|
| Static host | GitHub Pages — serves `main` branch |
| DNS + HTTPS | Cloudflare — proxying `adamatteia.com` |
| Source | `/Users/aatteia/working/adamatteia-website-alt3` |

To update the live site, make changes in the source repo and run:

```bash
cd /Users/aatteia/working/adamatteia-website-alt3
./deploy.sh
```

Or non-interactively:

```bash
NODE_ENV=production npm run build
for item in ../adamatteia-deploy/*; do
  name=$(basename "$item")
  case "$name" in CNAME|.nojekyll|.gitignore|CLAUDE.md) ;; *) rm -rf "$item" ;; esac
done
cp -r out/* ../adamatteia-deploy/
cd ../adamatteia-deploy && git add -A && git commit -m "<message>" && git push origin main
```

Full publishing notes: `/Users/aatteia/working/adamatteia-website-alt3/docs/publishing.md`

## This project does NOT use Vercel

Do not attempt `vercel deploy`, `vercel link`, or any Vercel CLI/MCP commands.
