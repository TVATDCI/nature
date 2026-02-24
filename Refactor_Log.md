# Refactor Log & Deployment Guide

This document summarizes the tooling modernization and explains the build and deployment workflow for the **nature** project.

## 1. Summary of Changes

The goal was to replace deprecated and vulnerable tooling with a modern, secure build process while preserving the project's original source code, structure, and spirit — no dist folder, no framework rewrite.

- **Dependency Overhaul**: Replaced `node-sass` (deprecated) with modern Dart `sass`. All dependencies updated, security vulnerabilities fixed.
- **Build Pipeline**: Sass compiles directly to `css/style.css`. PostCSS + autoprefixer runs in place on the same file. No intermediate output files, no dist folder.
- **Deployment**: `gh-pages` deploys from the project root using a `--src` glob, pushing only `index.html`, `css/*.css`, `css/fonts/**`, and `img/**` to the `gh-pages` branch. Source files and tooling are never exposed.
- **Code Quality**: Added `Prettier` for consistent code formatting, `.editorconfig` for editor consistency, and `.browserslistrc` to control browser support for `autoprefixer`.
- **Gitignore**: Updated to ignore `node_modules/` and other build artifacts. No dist folder — none is used.

## 2. The Build & Deploy Workflow

### Key Scripts

- **`npm run compile:sass`**: Compiles `sass/main.scss` → `css/style.css` (expanded output).
- **`npm run prefix:css`**: Runs autoprefixer via PostCSS on `css/style.css` in place.
- **`npm run build:css`**: Runs `compile:sass` then `prefix:css` in sequence. This is the full CSS build.
- **`npm run watch:sass`**: Watches `sass/` and recompiles on every save. Use this during local development with Live Server.
- **`npm run deploy`**: Pushes only the site's deliverable files to the `gh-pages` branch on GitHub using a `--src` glob. Does **not** push `sass/`, `node_modules/`, or any tooling config.
- **`npm run format`**: Runs Prettier across the project for consistent formatting.

### Why No dist Folder

This project deliberately avoids a dist build step. The HTML and images are authored directly in the root — there is nothing to copy or transform. Only the CSS needs a build step (Sass → autoprefixer), and the output goes straight to `css/style.css` where `index.html` already references it. The `gh-pages --src` glob handles clean deployment without any staging folder.

## 3. How to Work on the Project

### Step 1: Develop Locally

```bash
npm run watch:sass
```

Open `index.html` with Live Server in VS Code. Changes to `.scss` files compile automatically and the browser reloads.

### Step 2: Deploy to GitHub Pages

When ready to publish:

```bash
npm run build:css
npm run deploy
```

`build:css` ensures the final compiled and prefixed CSS is up to date before pushing. `deploy` sends only the deliverable files to the `gh-pages` branch.

Wait a few minutes for GitHub Pages to update. Live site: [https://tvatdci.github.io/nature/](https://tvatdci.github.io/nature/)

### Step 3: Commit and Push Source Code

Deployment and source control are separate steps. After deploying, commit and push the source:

```bash
git add .
git commit -m "a descriptive commit message"
git push origin main
```

## 4. Project Philosophy

This is a legacy preservation refactor — not a modernization. The original CSS architecture (BEM, hand-crafted layout, pre-grid mindset) is untouched. Only the tooling was updated to keep the project buildable and deployable without security vulnerabilities.

Do not introduce frameworks, convert to Vite, or rebuild the architecture. This project is a time capsule.
