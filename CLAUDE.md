# Duriano Coffee landing page

## Scope
- Frontend only. This is a website demo: no backend, no API, no database, no full-stack work.

## Stack (fixed, do not change)
- SvelteKit with Svelte 5 (runes) and TypeScript, plus Ark UI (`@ark-ui/svelte`). Both are already installed in the starter project.
- Plain CSS only (global file `src/app.css`). No Tailwind, no other UI library. Ark UI is unstyled: style its parts with CSS using the `data-scope` and `data-part` attributes.

## Rules
- One page: `src/routes/+page.svelte`. Reusable pieces go in `src/lib/components`.
- No backend: no `+server` files, no form actions, no database, no external API calls, no .env, no API keys.
- Use Ark UI for interactive parts (Dialog, Accordion). Do not hand-roll them.
- Mobile-first. One <h1>, heading order never skips, meaningful alt text, text contrast >= 4.5:1, visible keyboard focus.
- Real copy only: no lorem ipsum, no health claims. Sample reviews labelled "Sample reviews for demo."
- The DevFest Davao 2026 section is a real event promoted as an easter egg: use only the facts in the spec (coming soon, November 2026, registration open, the four links). Outbound links use `target="_blank"` with `rel="noopener noreferrer"`.
- Fictional brand. Footer says "Demo site, not a real business." and "Google-inspired theme, not affiliated with Google."
- Before saying you are done, run `npm run check` and `npm run build` and fix any errors.
- Read `DESIGN.md` before any UI work and follow it for color, type, layout, components and interaction. Spec first, then `CLAUDE.md` tokens, then `DESIGN.md`.
- Design: use the impeccable skill (`/impeccable`, https://impeccable.style) for UI work. Run its critique and audit before saying you are done. The spec wins if they conflict.
- Commit with Conventional Commits (https://www.conventionalcommits.org/): `type(scope): description`, e.g. `feat(hero): add headline`. Small commits, imperative and lowercase, no co-author line. Never push or force.

## Brand tokens (use as CSS variables in src/app.css)
- --blue: #4285F4; --red: #EA4335; --yellow: #FBBC05; --green: #34A853 (decoration only, never text); --blue-text: #1967D2 (links, text, primary button); --ink: #202124; --grey: #5F6368; --surface: #F8F9FA; --white: #FFFFFF
- Fonts: Google Sans for headings and body (Google Fonts, no API key), with system sans-serif fallbacks
- Theme: Google-inspired (Google Sans, the four Google brand colors on white, Material-style rounded shapes). Visual theme only: no Google logo, name or product marks.
