# Product

<!-- impeccable:product-schema 1 -->

## Platform

web

## Users

Coffee lovers, adventurous culinary explorers, and Davao locals/visitors seeking distinctive artisanal regional coffee with bold character.

## Product Purpose

Introduce Duriano Coffee, a fictional specialty Davao durian coffee brand, engaging visitors with playful and authentic storytelling, product details, brew instructions, and an easy path to reserve a pack.

## Positioning

"Bold like Davao. Smells like a story." Small-batch coffee infused with Davao durian: creamy, bold, unapologetic, balancing rich roasted coffee with tropical durian notes.

## Operating Context

Responsive web landing page running in mobile and desktop browsers (375px to 1280px+), optimized for quick loading, smooth interaction, and high accessibility without backend dependencies.

## Capabilities and Constraints

- Fixed stack: SvelteKit (Svelte 5 runes, TypeScript), Ark UI (`@ark-ui/svelte`), plain CSS in `src/app.css`.
- Zero backend: no server endpoints, no database, no external API keys, no `.env`.
- Accessible by default: single `<h1>`, strict heading hierarchy, WCAG AA contrast (>= 4.5:1), visible focus rings, full keyboard operation for Ark UI Dialog and Accordion components.
- Responsive with zero horizontal scroll at 375px and 1280px.

## Brand Commitments

- Brand: Duriano Coffee.
- Tagline: "Bold like Davao. Smells like a story."
- Tone: Playful, warm, cheeky about the smell, with light Bisaya/Tagalog touches ("Sulayi na!").
- Visual Theme: Google-inspired aesthetic with Google Sans typography, soft Material-style rounded surfaces, and the four Google brand colors (#4285F4, #EA4335, #FBBC05, #34A853) used purely as decorative accents. Fictional brand, not affiliated with Google.

## Evidence on Hand

- Spec requirements in `specs/spec.md` and design rules in `DESIGN.md`.
- Fictional product roster: Classic Duriano (medium roast), Dark Husk (dark roast), Iced Durian Latte Mix (sachet).
- Fictional reviews clearly designated with "Sample reviews for demo."
- Real community event easter egg: DevFest Davao 2026 (November 2026) linking to https://apohub.gdgdavao.org/e/devfest-davao-2026 and official GDG Davao social channels.

## Product Principles

1. **Spec-first and authentic**: Every section matches the spec; no placeholder text, no health claims, clear demo disclaimers.
2. **Accessible and responsive**: Seamless experience from mobile to wide screen with accessible interactive widgets and legible high-contrast typography.
3. **Warm and delightful**: Balance the playful Davao durian persona with polished, friendly Google-inspired design.

## Accessibility & Inclusion

WCAG 2.1 AA compliance: contrast ratio >= 4.5:1 for all text, visible focus rings (3px outline with 2px offset), aria labels for icon buttons and external links, focus trap and Esc handling on modal dialogs, and accordion keyboard support.
