# Help Docs Workflow

This folder is the **single source of truth** for in-app help content.

## Source and generated folders

- Source (edit here): `help/`
- Generated runtime copy: `public/help/`
- Production renderer artifact: `dist/help/` (copied from `public/` during Vite build)

Do not manually maintain the generated folders. They are synchronized from `help/`.

## Sync command

Run after help edits:

`node scripts/copy-help.cjs`

or:

`npm run copy-help`

## Build/dev notes

- `predev` already runs `copy-help`.
- `build:renderer` already runs `copy-help`.
- If Help navigation/content looks stale in the app, run `copy-help` and restart the app window.
