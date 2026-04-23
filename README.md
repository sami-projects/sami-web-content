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
- Updates must be produced by the publish script from the main Sami project.

## Publish flow

Example from `d:\Research\Sami\v01`:

```bash
npm run publish:web-content -- --target "d:\Research\Sami\site\sami-web-content"
```

After generation:

```bash
cd d:\Research\Sami\site\sami-web-content
git add .
git commit -m "publish web content"
git push
```

