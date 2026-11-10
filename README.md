# imaginalvision.com

Cassandra's Imaginal Vision landing page: one static `index.html` (inline CSS and JS, dark and light), plus `images/`, `themaking/` and the brainstorm pages under `docs/`.

## Deploying

This is the Cloudflare Pages project `imaginalvision`, created by **direct upload**. It is **not** connected to GitHub, so merging to `main` ships nothing. After a merge, upload `main` yourself:

```bash
d=$(mktemp -d) && git archive main | tar -x -C "$d" && rm -f "$d/.gitignore"
cd "$d" && CLOUDFLARE_ACCOUNT_ID=<JP's account id> CLOUDFLARE_API_TOKEN=<a Pages-capable token from the vault> \
  npx -y wrangler@4 pages deploy . --project-name imaginalvision --branch main --commit-hash <short sha of main>
```

Then compare the live page with `main` (`curl -s https://imaginalvision.com/ | diff - index.html`). From April 5 to November 10 2026 `main` sat undeployed because of this.

`_headers` (HSTS, frame and permissions policy) takes effect only on Pages.
