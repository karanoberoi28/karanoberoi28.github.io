# Karan Oberoi — Portfolio Website

A single-page, tab-style personal portfolio site for Karan Oberoi — Data Scientist / AI Builder, currently leading a multidisciplinary AI & analytics team, with a background spanning statistical modelling, machine learning, causal inference, and Generative AI across Aviation, Life Sciences, and Supply Chain.

Live sections: **About** · **Projects** · **Blogs**

## Overview

The site is built as a static, dependency-free "app-like" page: instead of one long scrolling page, About / Projects / Blogs behave like separate tabs. Clicking a nav link (or the logo) swaps the visible section instantly rather than scrolling, and each tab reveals its content with a light fade-up animation.

## Tech Stack

- **HTML5** — semantic, single-file markup (`index.html`)
- **CSS3** — custom properties (CSS variables), CSS Grid/Flexbox, no framework (`css/styles.css`)
- **Vanilla JavaScript** — no build step, no dependencies beyond one CDN library (`js/main.js`)
- **[Chart.js](https://www.chartjs.org/) v4.4.0** — via CDN, used for the mini accuracy chart on the featured project card
- **Google Fonts** — Syne (headings) and DM Sans (body text)

## File Structure

```
.
├── index.html          # All page markup and section content
├── css/
│   └── styles.css      # All styling, layout, and responsive rules
├── js/
│   └── main.js          # Tab switching, animations, chart, dynamic content
└── images/              # Image assets (see below)
    ├── 40 Under 40 Badge 2022.png
    └── 40u40_AIM-1536x864.jpg
```

## Sections

### About (default landing tab)
- Personal introduction and career narrative (data → ML → causal inference → GenAI)
- **Patents** sub-section listing two U.S. patents (pending and granted), each linking out to Google Patents
- **40 Under 40 · 2022 Batch** photo, recognizing Karan's inclusion in Analytics India Magazine's 40 Under 40 Data Scientists

### Projects
A grid of six featured data science projects (NLP, forecasting, computer vision, recommender systems, EDA, and MLOps), each with a short description, tech-stack tags, and GitHub/demo links. The featured NLP project includes a live Chart.js bar chart of per-class accuracy.

### Blogs
Placeholder tab reserved for future articles/write-ups on data science, causal AI, and aviation analytics. Currently shows an empty state ("No articles yet").

## Navigation & Header

- Logo mark: the **40 Under 40 Badge (2022)** image, shown before the name in the header
- Nav links: About / Projects / Blogs (tab switches, not page scrolls)
- Social icons (GitHub, LinkedIn) live in the header, next to the nav links
- Responsive hamburger menu collapses the nav on smaller screens

## Required Image Assets

The site references two images that need to be placed in an `images/` folder alongside `index.html`:

| File | Used in |
|---|---|
| `images/40 Under 40 Badge 2022.png` | Header logo (before the name) |
| `images/40u40_AIM-1536x864.jpg` | About tab — "40 Under 40 · 2022 Batch" photo |

Until these files are added, the corresponding `<img>` tags will render as broken images.

## Running Locally

No build tools or package manager required. Either:

1. Open `index.html` directly in a browser, **or**
2. Serve the folder with any static server, e.g.:
   ```bash
   python3 -m http.server 8000
   ```
   then visit `http://localhost:8000`.

## Notable Implementation Details

- **Tab switching** (`js/main.js`): `showTab(id)` toggles an `.active` class on the matching `.tab-content` section and the corresponding `.nav-link`, and any in-page anchor (`<a href="#about">`, etc.) is intercepted to trigger a tab switch instead of a page jump.
- **Fade-up animations**: elements tagged with `.fade-up` (project cards, patent cards, section headers) animate in with a staggered delay each time their tab becomes active.
- **Dynamic experience counter**: `initExperienceYears()` calculates "years of experience" from a fixed August 2010 start date, so the figure stays accurate without manual updates (currently unused in the markup but available if a `#dsYears` element is added back).

## Customization

- **Colors, spacing, fonts**: all defined as CSS custom properties near the top of `css/styles.css`.
- **Adding a project**: duplicate a `.project-card` block inside `#projects .projects-grid` in `index.html`.
- **Adding a blog post**: replace the `.blogs-empty` placeholder inside `#blogs` with article cards once content is ready.
- **Adding a patent**: duplicate a `.patent-card` block inside `.about-patents .patents-grid`.

---
© 2026 Karan Oberoi · All rights reserved
