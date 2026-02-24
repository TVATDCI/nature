## Refactor nature (2026 Modern Tooling)

I don’t want to “modernize it into something else.”
I want to preserve the spirit of the project… but clean the tooling rot.

The engineering maturity. Not rewriting history — refactoring it.

- Dart `sass` instead of `node-sass`
- `postcss-cli` + `autoprefixer`
- `npm-run-all` for sequencing
- `gh-pages` for deployment
- No backend nonsense
- No build folder indirection

It keeps the project “pure HTML/CSS learning artifact” while making the tooling current and secure.

---

## Objective

Preserve original nature static site structure and styling approach while:

- Removing deprecated tooling (`node-sass`)
- Eliminating vulnerable dependencies (`node-tar` chain)
- Modernizing build pipeline
- Maintaining GitHub Pages deployment
- Keeping project philosophy intact (no framework rewrite)

---

## Phase 1 — Dependency Cleanup

### 1. Remove Legacy Dependencies

- Remove:
  - `node-sass`
  - `"save-dev": "^0.0.1-security"`

- Delete:
  - `node_modules`
  - `package-lock.json`

Command sequence:

```
rm -rf node_modules package-lock.json
npm uninstall node-sass save-dev
```

---

## Phase 2 — Install Modern Tooling

### 2. Install Required Dev Dependencies

Install:

```
npm install --save-dev sass autoprefixer postcss-cli npm-run-all gh-pages
```

Ensure `package.json` devDependencies match:

- sass
- autoprefixer
- postcss-cli
- npm-run-all
- gh-pages

No production dependencies required.

---

## Phase 3 — Update package.json Scripts

Replace scripts with:

```
"scripts": {
  "compile:sass": "sass sass/main.scss css/style.css --style=expanded",
  "prefix:css": "postcss css/style.css --use autoprefixer -o css/style.css",
  "watch:sass": "sass sass/main.scss css/style.css --watch --style=expanded",
  "build:css": "npm-run-all compile:sass prefix:css",
  "deploy": "gh-pages -d ."
}
```

Notes:

- Output directly into `/css/style.css`
- Keep structure unchanged
- No dist folder
- GitHub Pages deploys root

---

## Phase 4 — PostCSS Configuration

Create `postcss.config.js` in root:

```
export default {
  plugins: {
    autoprefixer: {}
  }
}
```

If using CommonJS:

```
module.exports = {
  plugins: {
    autoprefixer: {}
  }
}
```

Match module system in package.json.

---

## Phase 5 — Test Build Pipeline

Run:

```
npm run build:css
```

Verify:

- CSS compiles correctly
- Autoprefixer runs
- No warnings
- Site renders exactly the same

Then test watcher:

```
npm run watch:sass
```

---

## Phase 6 — GitHub Pages Verification

Confirm:

- Repository Settings → Pages
- Branch: `gh-pages`
- Folder: `/ (root)`

Deploy:

```
npm run deploy
```

Verify live URL:
[https://tvatdci.github.io/nature/](https://tvatdci.github.io/nature/)

---

## Phase 7 — Security Audit

Run:

```
npm audit
```

Ensure:

- No high severity issues
- No `node-tar` vulnerability

If vulnerabilities appear:

- Update specific packages
- Do NOT add unnecessary dependencies

---

## Optional Enhancements (Keep Original Spirit)

These are optional and should not alter design:

- Add `.browserslistrc` for autoprefixer control
- Add Prettier for formatting consistency
- Add `.editorconfig`
- Add simple README modernization

Do NOT:

- Introduce frameworks
- Convert to Vite
- Add React
- Rebuild architecture

This project is a time capsule — not a startup.

---

Now my advice beyond mechanics.

Do not over-modernize this.

nature is part of my developer origin story.
Keep it clean, but let it show its era.

Make sure to keep:

- Old CSS architecture
- BEM discipline
- Hand-crafted layout
- Pre-grid mindset

It reminds me how far i’ve come.

Modern tools. Same creative fire.
Note: The key is treating this like a “legacy system preservation” project — not a “modernization” project. I am trying find the way to design a “Legacy Projects Preservation Strategy” — how to maintain old repos without rewriting their soul.
