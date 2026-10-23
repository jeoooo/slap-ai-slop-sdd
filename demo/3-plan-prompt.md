Paste after typing `/speckit-plan`. (This is where technology goes.)

---

Stack: SvelteKit (Svelte 5, TypeScript) with Ark UI (`@ark-ui/svelte`). The project is already scaffolded and both are installed; do not add other frameworks or UI libraries.

- One route: `src/routes/+page.svelte`. Break the page into components in `src/lib/components` (Hero, Story, Brew, ProductCard, HowToEnjoy, Reviews, FinalCta, Footer).
- Use the Ark UI Dialog for product details and the Ark UI Accordion for the how-to steps. Import from the package subpaths (for example `@ark-ui/svelte/dialog` and `@ark-ui/svelte/accordion`) and confirm the exact names against the installed package.
- Global CSS in `src/app.css` with CSS variables for the brand tokens. Ark UI is unstyled, so style its parts with the `data-scope` and `data-part` attributes.
- Load Fraunces and Inter from Google Fonts in `src/app.html` (no API key needed), with system font fallbacks. Put the title, meta description and Open Graph tags in `<svelte:head>`.
- Use CSS and inline SVG or emoji for imagery so there is no dependency on a stock-photo service.
- No backend, no .env.
- Finish by running `npm run check` and `npm run build`.

After that, run `/speckit-tasks`, skim the task list on camera, then `/speckit-implement`.
