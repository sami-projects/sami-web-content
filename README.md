# sami-web-content

Technical content-delivery repository for the Sami website.

This repository stores only **published artifacts** (generated content) that the website reads at runtime without redeploying the UI.

## Purpose

- store `dist/manifest.json` and related content files;
- provide a stable runtime source for `VITE_CONTENT_BASE_URL`;
- support rollback via Git commits.

## Expected structure

```text
dist/
  manifest.json
  data/
    help-index.json
    mcp-registry.json
  help/
    **/*.md
```

## Important

- This repository is **generated-only**.
- Do not edit `dist/*` manually.
- **Full bundle** (help + optional MCP): publish script in the main **Sami** app repo (`publish-web-content.cjs`).
- **MCP gallery only** (registry + icons + manifest MCP sections): use [`sami-mcp-gallery`](https://github.com/sami-projects/sami-mcp-gallery) — `npm run publish:web-content-mcp -- --target "<path-to-this-repo>"` after `dist/` already exists with help (see that repo’s README). No Sami checkout required for registry-only work.

## Publish flow

### Full publish (help + MCP) from Sami

Example from `d:\Research\Sami\v01`:

```bash
npm run publish:web-content -- --target "d:\Research\Sami\site\sami-web-content"
```

### MCP-only refresh (from `sami-mcp-gallery`)

When help is already present in `dist/`:

```bash
cd path/to/sami-mcp-gallery
npm run publish:web-content-mcp -- --target "d:\Research\Sami\site\sami-web-content"
```

After generation:

```bash
cd d:\Research\Sami\site\sami-web-content
git add .
git commit -m "publish web content"
git push
```

## Cloudflare Pages (host `dist/` at `https://content.sami.team`)

Repo: [sami-projects/sami-web-content](https://github.com/sami-projects/sami-web-content) (public). No Node build — only static files under `dist/`, plus a root `_headers` file copied into `dist/` on each deploy so browsers can `fetch` from the main site (CORS).

### One-time setup in Cloudflare

1. Dashboard → **Workers & Pages** → **Create** → **Pages** → **Connect to Git**.
2. Authorize GitHub if needed → select **`sami-projects/sami-web-content`** → **Begin setup**.
3. **Project name:** e.g. `sami-web-content` (only affects `*.pages.dev` preview URL).
4. **Production branch:** `main`.
5. **Build settings:**
   - **Framework preset:** `None`
   - **Build command:** `cp _headers dist/_headers`  
     (copies [CORS / `_headers`](https://developers.cloudflare.com/pages/configuration/headers/) into the published output; build runs on Linux.)
   - **Build output directory:** `dist`
6. **Environment variables:** none required for this repo.
7. **Save and Deploy** — first build should succeed; open the assigned `*.pages.dev` URL and check `https://<project>.pages.dev/manifest.json`.

### Custom domain `content.sami.team`

1. In the Pages project → **Custom domains** → **Set up a custom domain** → enter **`content.sami.team`**.
2. Cloudflare adds the DNS record if the zone `sami.team` is already in the same account. Wait until status is **Active**.
3. In **`sami-site`** set `contentBaseUrl` to `https://content.sami.team` in `public/content-config.json` (no trailing slash), deploy the site, then smoke-test Help + MCP catalog.

**Plan B:** if Pages is down, temporarily point `contentBaseUrl` back to  
`https://raw.githubusercontent.com/sami-projects/sami-web-content/main/dist`.

### After each content publish

Commit and push `dist/` (and anything else) to `main` as you already do — Pages rebuilds automatically on push.

