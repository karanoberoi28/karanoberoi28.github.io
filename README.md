# Alex Morgan — Data Science Portfolio

A personal portfolio website built with pure HTML, CSS, and JavaScript.
No frameworks. No build tools. No dependencies to install.

---

## Quickstart (VS Code + Live Server)

### Step 1 — Open the project folder
1. Open **VS Code**
2. Click `File → Open Folder`
3. Select the `ds-portfolio` folder

### Step 2 — Install the Live Server extension
1. Click the **Extensions** icon in the left sidebar (or press `Ctrl+Shift+X`)
2. Search for **"Live Server"** by Ritwick Dey
3. Click **Install**

### Step 3 — Launch the site
1. In the VS Code file explorer, right-click **`index.html`**
2. Select **"Open with Live Server"**
3. Your browser opens automatically at `http://127.0.0.1:5500`
4. Every time you save a file, the browser refreshes instantly ✓

---

## Alternative: Python HTTP server (no extension needed)

If you have Python installed:

```bash
cd ds-portfolio
python -m http.server 5500
```

Then open: **http://localhost:5500**

---

## Project structure

```
ds-portfolio/
├── index.html           ← entire page structure
├── requirements.txt     ← tools & libraries reference
├── README.md            ← this file
├── css/
│   └── styles.css       ← all visual styles
├── js/
│   └── main.js          ← charts, animations, interactions
└── assets/
    ├── images/          ← put your profile photo here
    └── resume.pdf       ← put your resume PDF here
```

---

## Customise it for yourself

Open `index.html` and find these items to update:

| What to change | How to find it |
|---|---|
| Your name | Search `Alex Morgan` — appears in title, navbar, footer |
| Hero tagline | Search `Data Makes Everything Clearer` |
| About text | Search `<!-- ABOUT -->` section |
| Contact details | Search `contact-details` |
| Social links | Search `social-links` |
| Project cards | Search `<!-- PROJECTS -->` section |
| Skills list | Search `<!-- SKILLS -->` section |
| Resume PDF | Replace `assets/resume.pdf` with yours |

---

## Deployment (free)

### GitHub Pages
1. Push this folder to a GitHub repo
2. Go to `Settings → Pages`
3. Set source to `main` branch, `/ (root)`
4. Your site is live at `https://yourusername.github.io/repo-name`

### Netlify (drag & drop)
1. Go to https://netlify.com
2. Drag the `ds-portfolio` folder onto the deploy zone
3. Done — live URL in 30 seconds

---

## Libraries used (loaded via CDN — no install needed)

- **Chart.js 4.4.0** — hero accuracy chart + project bar chart
- **Google Fonts** — Syne (headings) + DM Sans (body)

Both load automatically when the browser has internet access.
