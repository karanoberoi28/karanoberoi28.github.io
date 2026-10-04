# Karan Oberoi — Portfolio Website

A single-page, tab-style personal portfolio site for Karan Oberoi — Data Scientist / AI Builder, currently leading a multidisciplinary AI & analytics team, with a background spanning statistical modelling, machine learning, causal inference, and Generative AI across Aviation, Life Sciences, and Supply Chain.

Live sections: **About** · **Projects** · **Blogs** · **SLMs**

## Overview

The site is built as a static, dependency-free "app-like" page: instead of one long scrolling page, About / Projects / Blogs / SLMs behave like separate tabs. Clicking a nav link (or the logo) swaps the visible section instantly rather than scrolling, and each tab reveals its content with a light fade-up animation.

The **Blogs** and **SLMs → Overview / Architecture** sections don't hardcode their content in the HTML — it's loaded at runtime from JSON files in `data/`, so new posts or new architecture write-ups can be added without touching `index.html` or `js/main.js`.

## Tech Stack

- **HTML5** — semantic, single-file markup (`index.html`)
- **CSS3** — custom properties (CSS variables), CSS Grid/Flexbox, no framework (`css/styles.css`)
- **Vanilla JavaScript** — no build step, no dependencies beyond one CDN library (`js/main.js`)
- **[Chart.js](https://www.chartjs.org/) v4.4.0** — via CDN; wired up by `initProjectChart()` for a per-class accuracy chart, currently unused until a `#projectChart1` canvas is added back to the Projects tab
- **Google Fonts** — Lora (headings) and Inter (body text)
- **Inline SVG diagrams** — hand-built flowcharts (no external diagramming library) for the SLM Architecture content, styled to match the site's color tokens

## File Structure

```
.
├── index.html                   # Page markup and static section content
├── css/
│   └── styles.css               # All styling, layout, and responsive rules
├── js/
│   └── main.js                  # Tab switching, animations, chart, dynamic content loaders
├── data/
│   ├── blogs.json                # Blog post content (title, thumbnail, full HTML body)
│   ├── slm-overview.json         # SLMs → Overview tab content (intro + "What Makes a Model Small?")
│   └── slm-architecture.json     # SLMs → Architecture tab content (pipeline, transformer block, design choices)
└── images/
    ├── 40 Under 40 Badge 2022.png
    ├── 40u40_AIM-1536x864.jpg
    ├── slm_pipeline.svg          # End-to-end pipeline diagram (Architecture tab)
    ├── slm_full_architecture.svg # Detailed Transformer-block diagram (Architecture tab)
    ├── slm_simple_flow.svg       # Standalone 5-step flow diagram (Text → Tokens → Embeddings → Transformer Blocks → Next-Token Probabilities)
    └── blogs/
        ├── pringles_1.jpg / pringles_2.jpg
        ├── causal_inference_1.jpg
        └── physics_informed_ml_1.jpg
```

## Sections

### About (default landing tab)
- Personal introduction and career narrative (data → ML → causal inference → GenAI)
- **Patents** sub-section listing two U.S. patents (pending and granted), each linking out to Google Patents
- **40 Under 40 · 2022 Batch** photo, recognizing Karan's inclusion in Analytics India Magazine's 40 Under 40 Data Scientists

### Projects
Currently a placeholder ("Nothing here yet — this section is being rebuilt") while the project grid is reworked.

### Blogs
A floating thumbnail grid, populated at runtime from `data/blogs.json`. Clicking a thumbnail opens the full post in an in-page reader panel (`#blogReader`) rather than navigating away. If `data/blogs.json` can't be fetched (e.g. opening `index.html` directly instead of via a local server), the original "No articles yet" empty state is shown instead.

Current posts:
- *Pringles or a Hyperbolic Paraboloid* — the geometry behind Pringles' shape
- *Correlation Is Easy. Causation Is the Job.* — a causal-inference primer
- *Why Physics-Informed Machine Learning Is Having a Moment* — blending physics constraints with ML

### SLMs
A sub-tabbed section (its own row of pill-style sub-tabs) covering Small Language Models:

| Sub-tab | Status |
|---|---|
| **Overview** | Live — loaded from `data/slm-overview.json`. What an SLM is and what "small" actually means (parameter count, memory/latency/cost, task-specific optimization). Default sub-tab shown on load. |
| **Architecture** | Live — loaded from `data/slm-architecture.json`. The end-to-end pipeline (tokenizer → embeddings → Transformer blocks ×N → output head) with an inline SVG flowchart, a detailed zoom into a single Transformer block (Layer Norm → Attention → Dropout → residual add → Layer Norm → Feed-Forward → Dropout → residual add) with a second diagram, and the design choices that keep SLMs small (distillation, quantization, pruning, parameter sharing). |
| Benchmarks | Placeholder ("Coming soon") |
| Resources | Placeholder ("Coming soon") |
| Projects | Placeholder ("Coming soon") |
| Edge Deployment | Placeholder ("Coming soon") |

> Note: a few of the placeholder sub-tabs' `data-subtab` values and visible labels are mismatched in the current markup (a pre-existing naming inconsistency) — worth a pass when that content gets built out.

## Navigation & Header

- Logo mark: the **40 Under 40 Badge (2022)** image, shown before the name in the header
- Nav links: About / Projects / Blogs / SLMs (tab switches, not page scrolls)
- Social icons (GitHub, LinkedIn) live in the header, next to the nav links
- Responsive hamburger menu collapses the nav on smaller screens

## Dynamic, JSON-Driven Content

Both the Blogs grid and the SLMs → Overview/Architecture panels follow the same pattern: static placeholder markup in `index.html`, populated client-side by `fetch()`-ing a JSON file in `data/`.

- **Blogs** (`initBlogs()` in `main.js`) — fetches `data/blogs.json`, an array of `{ title, thumbnail, body }` objects, and renders one floating card per post. `body` is simple, self-hosted HTML (`<p>`, `<img>`, `<strong>`, links) shown in the in-page reader.
- **SLM Overview / Architecture** (`loadSlmSection()`, called via `initSlmOverview()` and `initSlmArchitecture()`) — a single shared loader function fetches the relevant JSON file (an optional `intro` plus a `sections` array of `{ heading, body, diagram, diagram_alt }`) and renders it into the matching sub-tab panel. `diagram` is a path to an inline SVG flowchart; `diagram_alt` is its accessible alt text.

In both cases, if the JSON file is missing, empty, or can't be fetched — most commonly because `index.html` was opened directly from disk instead of served over `http://` — the original static "empty state" markup (e.g. "No articles yet", "Coming soon") is shown instead, so the page never breaks.

## Required Image Assets

| File | Used in |
|---|---|
| `images/40 Under 40 Badge 2022.png` | Header logo (before the name) |
| `images/40u40_AIM-1536x864.jpg` | About tab — "40 Under 40 · 2022 Batch" photo |
| `images/slm_pipeline.svg` | SLMs → Architecture — "The End-to-End Pipeline" diagram |
| `images/slm_full_architecture.svg` | SLMs → Architecture — "Inside a Transformer Block" diagram |
| `images/slm_simple_flow.svg` | Standalone 5-step overview diagram (not yet wired into a tab) |
| `images/blogs/*.jpg` | Blog post thumbnails and inline post images, referenced by `data/blogs.json` |

Until these files are present at the referenced paths, the corresponding `<img>` tags (or `background` references) will render as broken images.

## Running Locally

No build tools or package manager required. Because Blogs and SLM content load via `fetch()`, the site must be served over HTTP (opening `index.html` directly from disk will fall back to the empty states for those sections):

```bash
python3 -m http.server 8000
```

then visit `http://localhost:8000`.

## Notable Implementation Details

- **Tab switching** (`js/main.js`): `showTab(id)` toggles an `.active` class on the matching `.tab-content` section and the corresponding `.nav-link`, and any in-page anchor (`<a href="#about">`, etc.) is intercepted to trigger a tab switch instead of a page jump.
- **Sub-tab switching**: `initSlmSubtabs()` handles the SLMs section's own row of sub-tabs independently of the top-level `showTab()` logic, toggling `.active` on the matching `.subtab-link` and `.subtab-content`.
- **Fade-up animations**: elements tagged with `.fade-up` (project cards, patent cards, section headers, and dynamically-rendered blog/SLM content) animate in with a staggered delay each time their tab becomes active.
- **Blog reader modal**: `openBlogPost()` / `closeBlogPost()` populate and toggle an in-page panel (`#blogReader`) rather than navigating to a separate page; closable via the ✕ button, backdrop click, or Escape key.
- **Dynamic experience counter**: `initExperienceYears()` calculates "years of experience" from a fixed August 2010 start date, so the figure stays accurate without manual updates (currently unused in the markup but available if a `#dsYears` element is added back).

## Customization

- **Colors, spacing, fonts**: all defined as CSS custom properties near the top of `css/styles.css`.
- **Adding a project**: duplicate a `.project-card` block inside `#projects .projects-grid` in `index.html` (once the Projects tab is rebuilt from its current placeholder).
- **Adding a blog post**: append a new `{ title, thumbnail, body }` object to `data/blogs.json` — no HTML changes needed. Drop the thumbnail/inline images into `images/blogs/`.
- **Adding SLM content**: append a new `{ heading, body, diagram, diagram_alt }` object to the `sections` array in `data/slm-overview.json` or `data/slm-architecture.json`. `diagram` is optional; omit it for a text-only section.
- **Adding a patent**: duplicate a `.patent-card` block inside `.about-patents .patents-grid`.

---
© 2026 Karan Oberoi · All rights reserved
