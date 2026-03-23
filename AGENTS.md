# AGENTS.md
Guide for coding agents working in `/home/marwane/Bureau/Outils/challenge/land`.
## 1) Project summary
- Project: `land_100`
- Stack: static HTML + CSS + vanilla JavaScript
- No framework, no bundler, no npm scripts
- Hub entrypoint: `index.html`
- Data source: `landings.json`
- Landing pages: `100/<NN-slug>/index.html`
- Deploy target: GitHub Pages from `main` (root)
## 2) Repository layout
```text
.
|-- index.html
|-- landings.json
|-- README.md
|-- AGENTS.md
`-- 100/
    |-- 01-meowsocks/
    |   `-- index.html
    `-- 02-academia-premium/
        `-- index.html
```
## 3) Build / run commands
No build step exists. Serve files directly:
```bash
python3 -m http.server 8000
```
Open:
- Hub: `http://localhost:8000/`
- One landing: `http://localhost:8000/100/01-meowsocks/`
- Pattern: `http://localhost:8000/100/<NN-slug>/`
## 4) Lint / validation commands
No eslint or prettier configured. Use lightweight checks.
Validate JSON:
```bash
python3 -m json.tool landings.json > /tmp/landings.validated.json
```
Quick diff sanity:
```bash
git status --short
git diff -- landings.json index.html
```
## 5) Test commands (including single-test workflow)
No automated test runner exists.
Single-test equivalent (data):
```bash
python3 -m json.tool landings.json > /tmp/one-test.json
```
Single-test equivalent (one page):
1. Start server: `python3 -m http.server 8000`
2. Open one target page only (example): `http://localhost:8000/100/02-academia-premium/`
3. Verify: no console errors, layout intact, links and buttons work
Manual smoke suite for changed work:
1. Open hub and check cards render
2. Use each category filter once
3. Open each changed landing
4. Verify keyboard focus visibility
5. Verify local links (`../../index.html`, anchors)
## 6) Data contract: `landings.json`
Top-level keys:
- `version` string
- `updated` date string (`YYYY-MM-DD`)
- `repo` URL string
- `baseUrl` string (usually `100`)
- `landings` array
Per landing entry:
- `id` integer, unique and sequential
- `name` string
- `desc` string
- `category` in: `html-css`, `animations`, `js-interactions`, `3d-webgl`, `video`, `shaders`
- `level` integer from `1` to `5`
- `folder` local slug
- `thumbnail` URL
- `url` optional direct URL
- `tags` string array
- `tech` string array
- `author` string
- `date` `YYYY-MM-DD`
Hub link resolution:
- If `url` is non-empty, hub uses `url`
- Else hub uses `${baseUrl}/${folder}/index.html`
## 7) Code style guidelines
Follow conventions already present in `index.html` and existing landing files.
### General
- Keep scope tight; avoid unrelated refactors
- Use 2-space indentation
- Keep ASCII by default
- Preserve existing file structure and naming patterns
### HTML
- Use semantic tags (`header`, `main`, `section`, `footer`)
- Use double quotes for attributes
- Add accessibility attributes for interactive controls
- Set explicit `type` on `<button>` elements
### CSS
- Reuse variables from `:root`
- Use kebab-case class names
- Keep selectors component-oriented and shallow
- Preserve responsive behavior at existing breakpoints
- Keep transitions intentional (roughly 150-500ms)
### JavaScript
- Vanilla JS only
- Prefer `const`; use `let` only when reassignment is needed
- Use camelCase for vars/functions
- Use semicolons (match existing style)
- Keep helpers small and focused
- Guard optional DOM nodes before use
### Imports and modules
- Current repo uses inline `<script>` blocks (no imports)
- Do not introduce bundlers or module tooling unless asked
- If splitting files later, use explicit relative paths
### Types
- Project is plain JavaScript, not TypeScript
- Do not add TS syntax to runtime files
- Express intent with naming and small pure functions
### Error handling and safety
- Handle expected failures with safe defaults
- Keep UI resilient on missing data/files
- Use `try/catch` around fetch/parse flows when needed
- Escape dynamic text before `innerHTML` insertion
### JSON editing
- Keep key order stable
- Do not add trailing commas
- Update `updated` when entries change
- Re-run JSON validation before commit
## 8) UX/accessibility baseline
- Keep focus states visible (`:focus-visible`)
- Do not rely only on hover for critical actions
- Maintain readable contrast in all sections
- Keep mobile interactions usable (menus, stacked grids)
- Respect `prefers-reduced-motion` for animation-heavy UI
## 9) Git workflow
- Default branch is `main`
- Validate JSON and smoke test changed pages before commit
- Commit only task-related files
- Avoid history rewrites unless explicitly requested
## 10) Agent done checklist
- Re-read changed files for accidental regressions
- Run JSON validation when data changed
- Verify one changed landing in browser
- Verify hub renders and filter still works
- Confirm relative links (`../../index.html`) still resolve
- Keep commit scope minimal and message specific
- Mention any manual checks not executed
- Never edit unrelated files without user request
## 11) Cursor / Copilot rules audit
Checked in this repository:
- No `.cursor/rules/` directory found
- No `.cursorrules` file found
- No `.github/copilot-instructions.md` file found
If these files appear later, treat them as higher-priority local instructions and merge their constraints into this document.
