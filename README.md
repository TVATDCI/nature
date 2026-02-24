# 🌿 Nature Landing Page

A fully responsive landing page project I built during my early days of learning frontend development — originally coded in **April 2024** during my journey through the **Advanced CSS & Sass** course by [Jonas Schmedtmann](https://codingheroes.io/).

This project holds a special place in my learning experience — it’s the first time I truly understood **CSS architecture**, **BEM naming**, **component-driven styling**, and the power of **Sass as a preprocessor**. Now it's part of my portfolio, showing how I learned to organize, scale, and document front-end projects like a professional.

---

## ✨ Project Highlights

- ✅ Built with `SCSS`, compiled using `sass` (Dart Sass)
- ✅ Uses the **7-1 Sass pattern** (a.k.a. **7 Pirates 🏴‍☠️**) for modularity and maintainability
- ✅ Follows **BEM naming conventions**
- ✅ Structured with a clean, component-based folder hierarchy
- ✅ Fully responsive layout with accessibility in mind
- ✅ Uses `autoprefixer` through `postcss-cli` integrated into modern npm scripts
- ✅ No frontend frameworks – just pure HTML & SCSS

---

## 🚀 Deployment

The project is deployed on GitHub Pages.

🔗 [**Live Preview →**](https://tvatdci.github.io/nature/)

**To deploy your changes:**

1. Run `npm run build:css` to compile and prefix your CSS.
2. Run `npm run deploy` to push the project to GitHub Pages.

---

## 🗃️ Folder Structure

```markdown
project-root/
├── css/
│ ├── icon-font.css
│ ├── fonts/
│ │ ├── linea-basic-10.eot
│ │ ├── linea-basic-10.svg
│ │ ├── linea-basic-10.ttf
│ │ └── linea-basic-10.woff
│ └── style.css ✅ Compiled from `sass/main.scss`
├── img/
│ └── ... 📸 All image assets (nat-_.jpg, logo-_, etc.)
├── sass/ 🎨 SCSS source files (modular & clean)
│ ├── abstracts/ 📁 Sass helpers (no actual CSS output)
│ │ ├── \_index.scss 📌 @forward entry point for all abstracts
│ │ ├── \_functions.scss 🔧 Custom Sass functions
│ │ ├── \_mixins.scss 🧩 Reusable mixins
│ │ └── \_variables.scss 🎨 All design variables (colors, spacing, etc.)
│ ├── base/ 📁 Base styles shared globally
│ │ ├── \_animations.scss 💫 Keyframe animations
│ │ ├── \_base.scss 🌍 Basic element resets
│ │ ├── \_typography.scss ✍️ Font styles, headings, paragraphs
│ │ └── \_utilities.scss 📐 Helper classes like `.u-margin-bottom`
│ ├── components/ 📁 Reusable UI blocks
│ │ ├── \_bg-video.scss 📽️ Background video styling
│ │ ├── \_buttons.scss 🔘 Button styles
│ │ ├── \_card.scss 🃏 Card-style component
│ │ ├── \_composition.scss 🧬 Complex layout grouping
│ │ ├── \_feature-box.scss 📦 Feature box UI
│ │ ├── \_form.scss 📝 Form styling
│ │ ├── \_popup.scss 📬 Popup modal styles
│ │ └── \_story.scss 📖 Story section styles
│ ├── layout/ 📁 Major layout structures
│ │ ├── \_footer.scss 👣 Footer layout
│ │ ├── \_grid.scss ➕ CSS Grid / Flexbox structure
│ │ ├── \_header.scss 🏔️ Hero/header section
│ │ └── \_navigation.scss 🧭 Top navbar
│ ├── pages/ 📁 Page-specific styles
│ │ └── \_home.scss 🏡 Styles unique to home page
│ └── main.scss 🧠 The brain – @use entry point for everything
├── index.html 📄 Main HTML file
├── package.json 📦 Node dependencies + scripts
├── package-lock.json
└── README.md
```

---

### 🛠️ Build Process

This project uses a modern SCSS compilation toolchain (without Webpack or Vite), reflecting the tooling refactor:

```bash
npm install         # Install dev dependencies
npm run build:css   # Compile SCSS to CSS (with autoprefixing)
npm run watch:sass  # Watch SCSS files for changes during development
npm run format      # Format code using Prettier
```

### Available npm scripts in package.json

```json
{
  "scripts": {
    "compile:sass": "sass sass/main.scss css/style.css --style=expanded",
    "prefix:css": "postcss css/style.css --use autoprefixer -o css/style.css",
    "watch:sass": "sass sass/main.scss css/style.css --watch --style=expanded",
    "build:css": "npm-run-all compile:sass prefix:css",
    "deploy": "gh-pages -d . --src '{index.html,css/*.css,css/fonts/**,img/**}'",
    "format": "prettier --write ."
  }
}
```

---

### 🧠 What I Learned

- Organizing styles with 7-1 architecture and naming everything with BEM

- Migrating from the legacy `@import` pattern to the modern `@use`/`@forward` module system

- Writing reusable, DRY SCSS using functions, mixins, and variables

- Creating responsive layouts with Flexbox/Grid

- Improving accessibility and interaction with pure HTML/CSS

- Compiling SCSS manually using modern `sass` + `postcss-cli`

- Clean HTML5 markup and semantic structure

## 📜 License & Credits

Built by **Tuanthong Vaidyanond**  
For Udemy **Advanced CSS & Sass** online course with Jonas Schmedtmann. Feb 2026.  
Updated new tolling 24.02.26

© Copyright by Jonas Schmedtmann.  
You are 100% allowed to use this webpage for both personal and commercial use, but NOT to claim it as your own design.  
A credit to the original author, Jonas Schmedtmann, is highly appreciated!
``
