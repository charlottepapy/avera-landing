# Avera landing page

Avera sources industrial deadstock in Mexico: it finds parts and materials sitting idle in one plant and delivers them to the plant that needs them, in days instead of weeks. This repository holds the public landing page, in Spanish and English.

Live: https://charlottepapy.github.io/avera-landing/ (GitHub Pages, served from `main`).

## Technology

- One self-contained static `index.html`: HTML, CSS, vanilla JavaScript, with images and videos inlined.
- Google Fonts (Inter, Inter Tight).
- The contact form writes to Supabase (table `leads`); see `AGENTS.md`.

## Run locally

Open `index.html` in a browser, or serve the folder with any static server.

## Publish

Work on a branch, then merge into `main`. GitHub Pages updates about a minute later.
