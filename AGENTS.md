# AGENTS.md

## Architecture
- This is a static single-page site. All of it lives in `index.html`, which is about 1.6 MB because the images (the `IMG` map in the bottom `<script>`) and two looping MP4 videos are inlined as base64 data URIs.
- `netlify.toml` sets `publish = "."`. There is no build step and no package.json.
- The page started as an exact copy of the original Avera prototype at luminous-sunburst-1b0e59.netlify.app. Keep the copy, layout, and behavior identical unless asked to change them.

## Conventions
- Vanilla JS in small IIFEs: menu, scroll progress, marquee, reveal-on-scroll, hero parallax, the typing search demo, value-proposition tabs, and offscreen video pausing. All motion respects `prefers-reduced-motion`.
- Images are set from `IMG[data-img]` at runtime. To add one, add a key to `IMG` and an `<img data-img="key">`.
- Don't open `index.html` whole, because the base64 blobs are huge. Search it, or strip `data:` URIs before reading.
- The waitlist form (first name, last name, company, email) is submitted via AJAX to the Supabase `leads` table in the Avera project (zyjcmhduqzdtxlxcaqno). RLS lets the publishable key insert rows only, never read them. The page is hosted on GitHub Pages, so Netlify Forms no longer work.
- `.github/workflows/supabase-keepalive.yml` pings Supabase twice a week so the free project doesn't auto-pause.
