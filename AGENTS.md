# AGENTS.md

## Architecture
- Static single-page site, hosted on GitHub Pages from `main` (https://charlottepapy.github.io/avera-landing/). Everything lives in `index.html`, which is about 1.6 MB because the images (the `IMG` map in the bottom `<script>`) and two looping MP4 videos are inlined as base64 data URIs.
- There is no build step and no package.json. `netlify.toml` is a leftover from the old Netlify hosting and is unused.

## Content
- The copy follows the Avera Pivot Brief (Drive › Avera › Pivot): Avera sources industrial deadstock in Mexico: it finds idle stock in one plant and gets it to the plant that needs it. Never say that Avera buys stock (the founders asked for this). Never use "marketplace", waitlist, commission, substitutes or self-serve framing; never show prices, margin or counterparties; no em dashes.
- Guarantee terms are not validated yet: say "guarantee" with terms "set out in every quote", nothing more specific.
- Bilingual: every string is a pair of sibling elements with `lang="es"` and `lang="en"`; CSS hides the one that does not match `<html lang>`. Placeholders use `data-ph-es` / `data-ph-en`. Spanish is the default; English browsers get English; the choice is stored in localStorage.

## Conventions
- Vanilla JS in small IIFEs: language switch, menu, scroll progress, marquee, reveal-on-scroll, hero parallax, the typing request demo, value-proposition tabs, contact form and offscreen video pausing. All motion respects `prefers-reduced-motion`.
- Images are set from `IMG[data-img]` at runtime. To add one, add a key to `IMG` and an `<img data-img="key">`.
- Don't open `index.html` whole, because the base64 blobs are huge. Search it, or strip `data:` URIs before reading.

## Contact form
- Submitted via AJAX to the Supabase `leads` table in the Avera project (zyjcmhduqzdtxlxcaqno) with the publishable key. RLS and column grants let that key insert only these columns: first_name, last_name, company, email, phone, city, need, idle_stock, page. It can never read rows. A new field needs a new column and an insert grant.
- Each insert fires the `leads_notify` trigger, which calls the `notify-new-lead` Edge Function to email averamarketplace@gmail.com through Resend (needs the RESEND_API_KEY secret).
- `.github/workflows/supabase-keepalive.yml` pings Supabase twice a week so the free project doesn't auto-pause.
