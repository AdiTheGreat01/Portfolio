# Aditya Upadhyay — Developer Portfolio

## Overview

This is my personal portfolio site — a single-page site that introduces me, lists my skills, and walks through a couple of projects in more detail through dedicated case study pages. I built it mainly to have a real place to point recruiters and interviewers to, instead of a static resume PDF, and to practice writing clean, dependency-free front-end code without leaning on a framework as a crutch.

The site covers an about section, a skills breakdown, project cards that link out to full case studies, an education section, and a contact section. Everything — including page-to-page navigation between the home page and each case study — runs on plain HTML, CSS, and JavaScript with no build step and no external UI libraries.

## Features

- Single-page layout with a sticky sidebar (bio, socials, dark mode toggle) and a scrollable content area
- Custom hash-based router (`showPage()`) that swaps between the home page and individual case study pages without a page reload
- Deep-linkable case study URLs (e.g. `#monkgully`) that resolve correctly on a fresh page load or refresh
- Dark/light theme toggle with the preference saved in `localStorage`
- Scroll-triggered section animations using the `IntersectionObserver` API instead of a scroll-event listener
- Fully responsive layout, including a stacked mobile layout for the hero section and adaptive grid columns for skills and projects
- Visible focus states and `prefers-reduced-motion` support for accessibility
- Reusable, token-driven CSS (CSS custom properties for color, spacing, and shadows) so the case study pages share one consistent design system

## Tech Stack

- **HTML5** — semantic markup, no templating engine
- **CSS3** — custom properties (design tokens), Flexbox, CSS Grid, media queries
- **JavaScript (ES6+)** — vanilla JS, no frameworks or libraries
- **Google Fonts** — Space Grotesk (display) and Inter (body)
- **Browser APIs** — `IntersectionObserver`, `localStorage`, `history.replaceState`

No backend, no build tooling, no package manager — the site is served as static files.

## Project Architecture

The project is a single HTML file that contains multiple "pages" as sibling `<div class="page">` blocks (home, and one per case study). Only one page is visible at a time; a small router function in `script.js` handles showing/hiding pages, updating the URL hash, and re-triggering the reveal animations for the page that just became visible.

```
index.html  →  markup for every page (home + case studies)
style.css   →  design tokens (CSS variables) + all component/page styles
script.js   →  router, theme toggle, scroll reveal, smooth-scroll links
```

Styling is driven by a shared set of CSS custom properties (colors, radii, shadows, fonts) defined once at the top of `style.css`, so every case study page reuses the same button, card, and tag components instead of redefining styles per page.

## Installation

1. Clone the repository:
   ```bash
   git clone https://github.com/adityaupadhyay01/[repo-name].git
   cd [repo-name]
   ```
2. No dependencies to install — there's no `package.json` or build step.
3. Open `index.html` directly in a browser, or serve it locally for a cleaner experience:
   ```bash
   npx serve .
   ```
   or, with Python:
   ```bash
   python3 -m http.server 8000
   ```

## Usage

- Open the site and scroll through the home page to see the about, skills, projects, and education sections.
- Click a project card (or its "Case Study" link) to open that project's dedicated case study page — this updates the URL hash so the page is shareable/bookmarkable.
- Use "Back to Projects" on a case study page to return to the home page's projects section.
- Toggle the sun/moon icon in the sidebar to switch between light and dark themes; the choice persists across visits.

Live demo: https://portfolio-adithegreat.netlify.app/

## Folder Structure

```
portfolio/
├── index.html          # All page markup (home + case studies)
├── style.css            # Design tokens and all styling
├── script.js             # Router, theme toggle, scroll reveal
├── profile.png           # Profile photo
└── README.md
```

## Challenges & Learnings

**Building a router without a framework.** Since I didn't want to pull in a routing library for a single-page site, I wrote a small hash-based router by hand. The tricky part was making deep links work: if someone loads the site directly on `#monkgully`, the right page needs to show immediately, and elements that use scroll-triggered animations (and never actually scrolled into view, since the page was hidden) need to be shown without waiting on the `IntersectionObserver`.

**Keeping the design consistent across case studies.** After building the first case study page, I noticed I was about to copy-paste and slightly diverge the CSS for the second one. Instead, I pulled the repeated patterns (feature cards, tag pills, roadmap lists) into shared classes driven by the same CSS variables as the rest of the site, so adding a new case study now means reusing existing components rather than writing new CSS.

**Dark mode without a flash of the wrong theme.** Reading the saved theme preference from `localStorage` and applying it before the rest of the page renders took a bit of trial and error to avoid a visible flash of light mode before it switched to dark.

## Future Improvements

- [Add details here — e.g. move project data into a JSON file and render cards dynamically]
- Add real screenshots and live demo links for each case study
- Add basic automated accessibility/performance checks (e.g. Lighthouse CI)
- Consider a lightweight build step for image optimization

## Why This Project Matters

- Demonstrates the ability to build a complete, multi-page user experience using only core web technologies, without relying on a framework
- Shows attention to UI/UX details: dark mode, scroll animations, responsive breakpoints, and accessible focus states
- Reflects a token-based, component-driven approach to CSS that scales cleanly as new pages are added
- Includes a hand-written client-side router, showing an understanding of how routing and history APIs work under the hood
- Prioritizes clean, readable, maintainable code over quick hacks — useful context for reviewing my coding style beyond a resume
- Serves as a living project: new case studies get added as I build more things, so the repo itself shows ongoing, incremental work

## License

[Add details here — e.g. MIT License]
