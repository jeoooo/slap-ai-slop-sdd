# Implementation Tasks: Duriano Coffee Landing Page

An ordered checklist derived from `specs/constitution.md`, `specs/spec.md`, `specs/plan.md`, and `DESIGN.md`.

## Setup and Foundation
- [x] Task 1: Setup HTML, fonts, and SEO metadata in `src/app.html`
  - Load Google Sans (weights 400, 500, 700) from Google Fonts with sans-serif fallbacks.
  - Set language, viewport, and title defaults.
- [x] Task 2: Setup brand tokens and styles in `src/app.css`
  - Define CSS variables: `--blue`, `--red`, `--yellow`, `--green`, `--blue-text`, `--ink`, `--grey`, `--surface`, `--white`, and accent tints.
  - Reset, layout grid, typography, fluid type clamps, focus ring styling (3px `--blue-text` with 2px offset on light, #8AB4F8 on ink).
  - Unstyled Ark UI data attributes styling (`data-scope` and `data-part` for dialog and accordion).

## Components Implementation (Sections in Order)
- [x] Task 3: Implement Page Header & SEO in `src/routes/+page.svelte`
  - Populate `<svelte:head>` with title, meta description, and Open Graph tags (`og:title`, `og:description`, `og:image`).
- [x] Task 4: Section 1 - Hero Component (`src/lib/components/Hero.svelte`)
  - Headline `<h1>`: "Coffee that dares you to smell it first."
  - Subhead: "Small-batch coffee infused with Davao durian. Creamy, bold, unapologetic."
  - Primary CTA button: "Reserve a pack" linking to `mailto:reserve@durianocoffee.demo`.
  - Four-dot brand motif accent.
- [x] Task 5: Section 2 - Story Component (`src/lib/components/Story.svelte`)
  - 2-3 short fictional paragraphs about pairing Davao durian with local-roasted beans.
  - Light Bisaya touch ("Sulayi na!").
- [x] Task 6: Section 3 - The Brew & Product Cards (`src/lib/components/Brew.svelte`, `src/lib/components/ProductCard.svelte`)
  - 3 products: Classic Duriano (medium roast, creamy finish), Dark Husk (dark roast, bold and smoky), Iced Durian Latte Mix (ready-to-mix sachet) with sample peso prices.
  - Ark UI Dialog for brew notes: roast, best way to brew, serving tip.
  - Accessible dialog triggers, backdrop, close button, focus trapping, and Esc key support.
- [x] Task 7: Section 4 - How to Enjoy It (`src/lib/components/HowToEnjoy.svelte`)
  - 3 steps (brew, add milk, sip) in an Ark UI Accordion (one open at a time, keyboard accessible, rotating chevron).
  - 1 tip for first-timers.
- [x] Task 8: Section 5 - Sample Reviews (`src/lib/components/Reviews.svelte`)
  - Label: "Sample reviews for demo." prominently displayed.
  - 3 short quotes with reviewer names and tinted accent cards.
- [x] Task 9: Section 6 - Final CTA (`src/lib/components/FinalCta.svelte`)
  - Repeat primary CTA "Reserve a pack" (`mailto:reserve@durianocoffee.demo`).
- [x] Task 10: Section 7 - DevFest Davao 2026 Band (`src/lib/components/DevFest.svelte`)
  - Surface band between FinalCta and Footer.
  - Event details: Coming soon, November 2026, registration open.
  - "Register now" secondary-style button link to `https://apohub.gdgdavao.org/e/devfest-davao-2026`.
  - 3 GDG Davao social links (Facebook, GitHub, LinkedIn) with `target="_blank"`, `rel="noopener noreferrer"`, and accessible labels.
- [x] Task 11: Section 8 - Footer (`src/lib/components/Footer.svelte`)
  - Ink background, white text.
  - Fictional Davao City address and social placeholders.
  - Required disclaimers: "Demo site, not a real business." and "Google-inspired theme, not affiliated with Google."
- [x] Task 12: Page Assembly & Routing (`src/routes/+page.svelte`)
  - Import and assemble all 8 sections in precise order.

## Design Polish & Quality Verification
- [x] Task 13: Run Impeccable design init, critique, audit, and polish
  - Ensure color contrast >= 4.5:1, touch targets >= 44x44px, no horizontal overflow at 375px/1280px.
  - Run `npm run check` and `npm run build`.
