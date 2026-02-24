# Refactor Log & Modern Deployment Guide

This document summarizes the tooling modernization and explains the new build and deployment workflow for the Trillo project.

## 1. Summary of Changes

The goal of this refactor was to replace deprecated and vulnerable tooling with a modern, secure, and robust build process while preserving the project's original source code.

- **Dependency Overhaul**: Replaced `node-sass` (deprecated) with modern Dart `sass`. All dependencies were updated, and security vulnerabilities were fixed.
- **Build Process**: A new build process was created. It now compiles all necessary files into a dedicated `dist` (distribution) folder, which is standard practice for web projects.
- **Deployment Fix**: The deployment process was fixed. It now deploys only the contents of the `dist` folder to GitHub Pages, ensuring a clean and correct live site.
- **Code Quality**: Added `Prettier` for consistent code formatting, `.editorconfig` for editor consistency, and `.browserslistrc` to control browser support for `autoprefixer`.
- **Gitignore**: The `.gitignore` file was updated to ignore the new `dist` folder and other build artifacts.

## 2. The New Build & Deploy Workflow

New set of `npm` scripts in `package.json` to automate everything.

### Key Scripts

- **`npm run build`**: This command prepares the project for deployment. It runs the following steps automatically:
  1. `clean`: Deletes the old `dist` folder to ensure a fresh build.
  2. `prepare:dist`: Creates a new, empty `dist` folder.
  3. `copy:assets`: Copies `index.html` file and the entire `img` directory into the `dist` folder.
  4. `build:css`: Compiles your Sass files (`sass/*.scss`), prefixes them for browser compatibility, and outputs the final `style.css` file into `dist/css/`.

- **`npm run deploy`**: This is the main command used to deploy to live site.
  1. It automatically runs the entire `npm run build` process first.
  2. It then takes the contents of the final `dist` folder and pushes them to the `gh-pages` branch on GitHub, which is what the live site uses.

- **`npm run watch:sass`**: Use this for local development. It watches over `.scss` files and compiles them into the `css/style.css` file whenever a change is made, which works perfectly with Live Server.

## 3. How to Deploy the Project (The New Way)

Here is the new step-by-step workflow.

### Step 1: Develop Locally

- Run `npm run watch:sass` in the terminal.
- Use "Live Server" in VS Code to see the changes in real-time as being edited in HTML and SCSS files.

### Step 2: Deploy to GitHub Pages

- When all is ready to publish the changes, stop the watcher and run a single command:

  ```bash
  npm run deploy
  ```

- Wait a few minutes for GitHub Pages to update. The live site will now reflect the changes.

### Step 3: Commit and Push Your Source Code

- Deploying the site and saving the code are separate steps. After deploying, the implementation should always be committed and push the source code changes.
- Add the changes, commit them with a message, and push to `main`.

  ```bash
  git add .
  git commit -m "a descriptive commit message"
  git push origin main
  ```

This new process is robust, follows modern best practices, and keeps the source code clean while ensuring deployments are simple and reliable.
