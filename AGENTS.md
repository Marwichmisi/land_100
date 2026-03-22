# AGENTS.md
Guidance for coding agents working in `land_100`.

## 1) Project Summary
- Stack: static HTML/CSS/JS (no framework).
- Hub entrypoint: `index.html`.
- Data source: `landings.json`.
- Landing pages: `100/<NN-slug>/index.html`.
- Deploy target: GitHub Pages from `main` and root `/`.

## 2) Repository Layout
```text
.
|-- index.html
|-- landings.json
|-- README-LANDINGS.md
|-- AGENTS.md
`-- 100/
    |-- 01-meowsocks/
    |   `-- index.html
    `-- 02-.../
        `-- index.html
```

## 3) Build, Lint, and Test Commands
No package manager scripts are configured.
Use these commands directly.

### Run locally
```bash
python3 -m http.server 8000
```
Open:
- Hub: `http://localhost:8000/`
- Single landing: `http://localhost:8000/100/01-meowsocks/`

### Lint equivalent: validate JSON
```bash
python3 -m json.tool landings.json > /tmp/landings.validated.json
```

### Smoke test (manual)
1. Open hub.
2. Confirm no browser console errors.
3. Confirm cards render and thumbnails load.
4. Click each card and verify destination.

### Single test guidance (important)
There is no formal test runner.
For "run one test", use one of the checks below:

Single file validation:
```bash
python3 -m json.tool landings.json > /tmp/one-check.json
```

Single page smoke test:
```bash
python3 -m http.server 8000
# then open http://localhost:8000/100/01-meowsocks/
```

## 4) Data Contract: landings.json
Top-level keys:
- `version` string
- `updated` date string (`YYYY-MM-DD`)
- `repo` repo URL
- `baseUrl` folder root, usually `100`
- `landings` array

Each landing object should include:
- `id` integer, unique
- `name` string
- `desc` string
- `category` one of allowed categories
- `level` integer from 1 to 5
- `folder` local folder slug
- `thumbnail` image URL
- `url` optional direct URL (external or custom)
- `tags` string array
- `tech` string array
- `author` string
- `date` `YYYY-MM-DD`

Allowed categories:
- `html-css`
- `animations`
- `js-interactions`
- `3d-webgl`
- `video`
- `shaders`

Link resolution behavior in hub:
- Use `url` when non-empty; otherwise resolve `baseUrl/folder/index.html`.

## 5) Code Style Rules
Follow current code conventions in this repo.

### General
- Keep changes scoped to the task.
- Do not rewrite architecture unless asked.
- Use ASCII by default.

### HTML
- Use semantic blocks (`header`, `main`, `section`, `footer`).
- Use double quotes for attributes.
- Keep 2-space indentation.
- Add `aria-*` and labels for interactive elements.

### CSS
- Reuse variables from `:root`.
- Class naming: kebab-case.
- Keep selectors shallow and component-oriented.
- Keep interaction transitions around 150-300ms.

### JavaScript
- Use `const` unless reassignment is required.
- Use `let` only when needed.
- Use camelCase for variables and function names.
- Keep helper functions focused and small.
- Escape dynamic text before `innerHTML` injection.

### JSON
- Keep key order stable across entries.
- Do not add trailing commas.
- Keep `id` unique and sequential.
- Validate JSON before commit.

## 6) Error Handling and UX Baselines
- Missing thumbnail must not break the card.
- Missing URL should show disabled state clearly.
- Keep keyboard focus visible.
- Do not rely on hover only for critical behavior.
- Ensure cards stay compact (preview-first layout).

## 7) Images, Icons, and Assets
- Prefer real thumbnails (Unsplash or repo assets).
- Prefer SVG icons for UI and status markers.
- Use emoji only as a last resort.
- Always provide useful `alt` text on content images.

## 8) Git Workflow
- Default branch is `main`.
- Before commit, validate JSON and run a local smoke test.
- Keep commit messages specific and action-based.

## 9) Cursor/Copilot Rules Audit
Checked in this repository:
- No `.cursor/rules/` directory found.
- No `.cursorrules` file found.
- No `.github/copilot-instructions.md` found.

If any of these files are added later, treat them as higher-priority local instructions and merge their rules into this document.
