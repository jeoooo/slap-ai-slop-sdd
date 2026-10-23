---
name: landing-page-qa
description: Use after building or changing the landing page to check it against the scoring checklist (stack, brand, sections, accessibility, SEO, responsive, CTA).
---

Check src/routes/+page.svelte, src/lib/components/*, src/app.css and src/app.html against this list and report PASS/FAIL per item with the file and line or selector:
1. Brand matches (name, palette, fonts, tone)
2. All 7 sections present, in order
3. No lorem ipsum, no health claims
4. One <h1>, correct heading order
5. All images have meaningful alt
6. Text contrast >= 4.5:1
7. No horizontal scroll at 375 px
8. Visible keyboard focus; the dialog traps focus, closes on Esc and returns focus; the accordion works with the keyboard
9. Meta description and Open Graph tags (in <svelte:head>)
10. Primary CTA in hero and final section, and it works
11. Stack: only SvelteKit and Ark UI; no backend files (+server, form actions), no .env, no external API calls
12. Interactive parts use Ark UI (Dialog, Accordion), not hand-rolled widgets
Do not fix anything. Report only.
