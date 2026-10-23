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
- Fictional brand. Footer says "Demo site, not a real business."
- Before saying you are done, run `npm run check` and `npm run build` and fix any errors.
- Design: use the impeccable skill (`/impeccable`, https://impeccable.style) for UI work. Run its critique and audit before saying you are done. The spec wins if they conflict.
- Commit with Conventional Commits (https://www.conventionalcommits.org/): `type(scope): description`, e.g. `feat(hero): add headline`. Small commits, imperative and lowercase, no co-author line. Never push or force.

## Brand tokens (use as CSS variables in src/app.css)
- --espresso: #2B1B12; --cream: #F6EBD3; --gold: #E8C547; --husk: #5B7F2B (use #3F5E1C for text)
- Fonts: Fraunces (headings), Inter (body)
