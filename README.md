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

