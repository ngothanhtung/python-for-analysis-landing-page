# CLAUDE.md

This file provides guidance for AI assistants working with this repository.

## Project Overview

A **bilingual static landing page** for a "Python for Data Analysis" online course, hosted on GitHub Pages. The site supports Vietnamese and English, with a separate EDUFLOW product page. There is no build step — all files are served as-is.

## Repository Structure

```
python-for-analysis-landing-page/
├── .github/
│   └── workflows/
│       └── static.yml          # GitHub Actions → GitHub Pages deployment
├── .gitignore
├── .repomixignore
├── README-LANGUAGES.md         # Documentation on bilingual strategy
├── index.html                  # Vietnamese landing page (default)
├── index-en.html               # English landing page
├── eduflow.html                # EDUFLOW product page (Vietnamese)
└── Báo giá SOFTECH - EDUFLOW - 2026.pdf  # Pricing document (binary)
```

## Tech Stack

| Technology | Usage |
|---|---|
| HTML5 | All pages are single-file, self-contained documents |
| Tailwind CSS v3 | Loaded via CDN (`https://cdn.tailwindcss.com`); configured inline |
| Google Fonts | Space Grotesk (headings), DM Sans (body) via CDN |
| Vanilla JavaScript | Inline `<script>` tags; no frameworks |
| GitHub Actions | CI/CD pipeline for deployment |
| GitHub Pages | Static site hosting |

**No build tools, no package manager, no local dependencies.**

## Development Workflow

### Making Changes

1. Edit HTML files directly — there is no compilation step.
2. Open the file in a browser to preview (e.g. `open index.html`).
3. No `npm install`, no `yarn`, no build commands needed.

### Deployment

Deployment happens automatically when code is merged/pushed to the `main` branch via `.github/workflows/static.yml`. The workflow:

1. Checks out the repository
2. Configures GitHub Pages
3. Uploads the entire repository as a static artifact
4. Deploys to GitHub Pages

Manual deployment can be triggered from the GitHub Actions tab using `workflow_dispatch`.

### Branching

- `main` — production branch; triggers auto-deploy
- Feature branches should follow the pattern `claude/<description>-<id>` for AI-generated changes

## Page Structure

Each landing page is one self-contained HTML file with these sections (linked via anchor IDs):

| Section | Anchor ID | Description |
|---|---|---|
| Navigation | — | Floating navbar with theme toggle, language switcher, mobile menu |
| Hero | — | Main headline, subtext, CTA button, code visualization |
| About | `#about` | Course overview and benefits |
| Curriculum | `#curriculum` | 5 course modules with detail |
| Testimonials | `#testimonials` | Student reviews |
| Pricing | `#pricing` | Tiered pricing options |
| Enrollment CTA | `#enroll` | Final call-to-action |
| Footer | — | Links, resources, social media |

## Code Conventions

### HTML

- Use semantic HTML5 elements (`<nav>`, `<section>`, `<article>`, `<footer>`, etc.)
- All pages use `lang` attribute on `<html>` (`vi` or `en`)
- `aria-label` attributes on interactive elements (buttons, links with icons)
- Smooth scrolling enabled via `scroll-smooth` class on `<html>`

### CSS / Tailwind

- Tailwind CSS is configured inline in a `<script type="text/javascript">` block in `<head>`:
  - `darkMode: 'class'` — theme switching via class toggle on `<html>`
  - Primary color: `#2563EB` (blue-600)
  - Secondary color: `#3B82F6` (blue-500)
  - CTA/accent color: `#F97316` (orange-500)
  - Font families: `Space Grotesk` (headings), `DM Sans` (body)
- Mobile-first responsive design using Tailwind breakpoints: `sm:`, `md:`, `lg:`
- Respect `prefers-reduced-motion` for animations

### JavaScript

- **Vanilla JS only** — no external libraries or frameworks
- All scripts are inline `<script>` tags placed at the end of `<body>`
- Use `document.getElementById()` / `querySelector()` for DOM access
- Use `classList.toggle()` / `.add()` / `.remove()` for class manipulation
- Use `localStorage` for user preference persistence (e.g. theme)

**Standard scripts in every page:**

1. **Theme Toggle** — toggles `dark` class on `<html>`, saves preference in `localStorage`
2. **Mobile Menu Toggle** — opens/closes the mobile nav; auto-closes on link click

When adding JavaScript, keep the same inline pattern and minimal footprint.

## Bilingual Strategy

| File | Language | `lang` attr |
|---|---|---|
| `index.html` | Vietnamese | `vi` |
| `index-en.html` | English | `en` |

- Both files are feature-equivalent (same sections, same functionality)
- Language switcher buttons (`EN` / `VN`) link between the two files
- When updating content or features, **update both files** to keep them in sync
- See `README-LANGUAGES.md` for additional detail

## Key Features to Preserve

When making any changes, ensure these features continue to work:

- **Dark/Light theme toggle** with localStorage persistence
- **Mobile responsive layout** with hamburger menu
- **Language switcher** (`index.html` ↔ `index-en.html`)
- **Smooth scrolling** to anchor sections
- **Accessibility** attributes on interactive elements

## Common Tasks

### Add a new section

1. Add the section HTML to both `index.html` and `index-en.html`
2. Add a navigation link in both files pointing to the section's `id`
3. Use existing Tailwind utility patterns from surrounding sections for consistency

### Update pricing or course content

1. Edit the relevant section in `index.html` (Vietnamese)
2. Apply the equivalent changes to `index-en.html` (English)
3. If the PDF pricing document needs updating, replace `Báo giá SOFTECH - EDUFLOW - 2026.pdf`

### Update the EDUFLOW page

`eduflow.html` is a separate page for a different product (enrollment management software). It follows the same HTML/Tailwind/JS conventions but has independent content.

### Change colors or fonts

Modify the Tailwind config `<script>` block in the `<head>` of each HTML file. Since there is no shared config file, update all pages that need the change.

## Testing

There is no automated test suite. Manual testing checklist:

- [ ] Open `index.html` in a browser — page renders correctly
- [ ] Open `index-en.html` — content is in English, layout matches Vietnamese version
- [ ] Toggle dark/light theme — persists on page reload
- [ ] Resize to mobile — hamburger menu appears; desktop nav hides
- [ ] Mobile menu opens and closes; closes automatically when a link is clicked
- [ ] Language switcher navigates between `index.html` and `index-en.html`
- [ ] All anchor links scroll to correct sections
- [ ] Check in both Chrome and Firefox

## Files to Never Modify

- `.github/workflows/static.yml` — only modify if explicitly changing deployment configuration
- `Báo giá SOFTECH - EDUFLOW - 2026.pdf` — binary asset; replace rather than edit
