# Duriano Coffee Website Documentation

## 1. Overview
This website is a promotional landing page for Duriano Coffee, a fictional specialty coffee brand rooted in Davao City. It is designed for coffee enthusiasts and adventurous drinkers interested in small-batch durian-infused coffee roasts. The site is a frontend-only demo featuring no backend infrastructure, database, or external APIs.

## 2. Run it
To run and verify the project locally:
- Install dependencies: `npm install`
- Start development server: `npm run dev`
- Run TypeScript and Svelte diagnostics: `npm run check`
- Create production build: `npm run build`
- Preview production build: `npm run preview`

## 3. Structure
```text
.
├── src/
│   ├── app.css                   # Global styles, brand tokens, and Ark UI part styles
│   ├── app.html                  # HTML template with Google Sans font preconnect and stylesheet
│   ├── lib/
│   │   ├── assets/favicon.svg    # Brand favicon asset
│   │   └── components/
│   │       ├── Hero.svelte       # Hero section with h1 and primary CTA
│   │       ├── Story.svelte      # 3-paragraph brand narrative
│   │       ├── Brew.svelte       # Product catalog container
│   │       ├── ProductCard.svelte# Individual product card with Ark UI Dialog brew notes
│   │       ├── HowToEnjoy.svelte # 3-step Ark UI Accordion and first-timer tip
│   │       ├── Reviews.svelte    # 3 sample testimonial cards
│   │       ├── FinalCta.svelte   # Dark section closing CTA repeating reservation link
│   │       ├── DevFest.svelte    # DevFest Davao 2026 easter egg band with external links
│   │       └── Footer.svelte     # Fictional Davao address and demo/theme disclaimers
│   └── routes/
│       ├── +layout.svelte        # Root layout importing global CSS and setting favicon
│       └── +page.svelte          # Single landing page assembling the 8 sections and SEO tags
├── specs/
│   ├── constitution.md           # Project rules and boundary constraints
│   ├── spec.md                   # Feature requirements and copy specification
│   ├── plan.md                   # Architectural plan and component mapping
│   └── tasks.md                  # Task checklist for implementation
├── PRODUCT.md                    # Product context initialized by Impeccable
└── docs/
    └── website.md                # System documentation
```

## 4. Page sections
- **Hero (`src/lib/components/Hero.svelte`)**: Displays the main `<h1>` headline, subhead, four-dot motif, and the primary "Reserve a pack" CTA button.
  - Props: `reserveEmail?: string` (defaults to `'hello@durianocoffee.demo'`).
- **Story (`src/lib/components/Story.svelte`)**: Presents the 3-paragraph narrative describing the origin of pairing Mount Apo coffee beans with fresh Davao durian.
  - Props: None.
- **Brew (`src/lib/components/Brew.svelte`)**: Outlines the roast roster and renders a responsive 3-column product grid using `ProductCard`.
  - Props: None.
- **ProductCard (`src/lib/components/ProductCard.svelte`)**: Renders a product card with top colored accent bar, badge, peso price, and a "Details" button opening brew notes in an Ark UI Dialog.
  - Props: `product: Product` (contains `id`, `name`, `description`, `price`, `roast`, `bestBrew`, `servingTip`, `accentColor`, `tintBg`).
- **HowToEnjoy (`src/lib/components/HowToEnjoy.svelte`)**: Features a 3-step collapsible guide (brew, add milk, sip) inside an Ark UI Accordion, alongside a first-timer advice card.
  - Props: None.
- **Reviews (`src/lib/components/Reviews.svelte`)**: Displays three tinted testimonial cards under a permanent "Sample reviews for demo." label.
  - Props: None.
- **FinalCta (`src/lib/components/FinalCta.svelte`)**: Dark-themed section providing visual contrast and repeating the primary "Reserve a pack" mailto link.
  - Props: `reserveEmail?: string` (defaults to `'hello@durianocoffee.demo'`).
- **DevFest (`src/lib/components/DevFest.svelte`)**: Light surface easter egg banner between FinalCta and Footer announcing DevFest Davao 2026 (November 2026), with a "Register now" button and GDG Davao social links.
  - Props: None.
- **Footer (`src/lib/components/Footer.svelte`)**: Dark footer with fictional Davao City address, social placeholders, and mandatory disclaimer notices.
  - Props: None.

## 5. Interactive parts
- **Ark UI Dialog (`@ark-ui/svelte/dialog`)**:
  - Implemented in `src/lib/components/ProductCard.svelte`.
  - Composed of `Dialog.Root`, `Dialog.Trigger`, `Dialog.Backdrop`, `Dialog.Positioner`, `Dialog.Content`, `Dialog.Title`, `Dialog.Description`, and `Dialog.CloseTrigger`.
  - Styled in `src/app.css` using `[data-scope="dialog"]` and `[data-part="..."]` selectors for backdrop blur, modal positioning, rounded corners (`--radius-dialog`), shadow, close button, and typography.
  - Provides native focus trapping, Esc key dismiss, and focus restoration to the trigger button.
- **Ark UI Accordion (`@ark-ui/svelte/accordion`)**:
  - Implemented in `src/lib/components/HowToEnjoy.svelte`.
  - Composed of `Accordion.Root`, `Accordion.Item`, `Accordion.ItemTrigger`, `Accordion.ItemIndicator`, and `Accordion.ItemContent`.
  - Styled in `src/app.css` using `[data-scope="accordion"]` selectors, handling border dividers, minimum 44px tap targets, and chevron indicator rotation via `[data-state="open"]`.
  - Allows one item open at a time and responds to keyboard navigation.

## 6. Design system
- **CSS Variables in `src/app.css`**:
  - Brand accents: `--blue: #4285F4;`, `--red: #EA4335;`, `--yellow: #FBBC05;`, `--green: #34A853;` (decorative elements only).
  - Text & action tokens: `--blue-text: #1967D2;`, `--ink: #202124;`, `--grey: #5F6368;`, `--surface: #F8F9FA;`, `--white: #FFFFFF;`.
  - Tints: `--blue-tint: #E8F0FE;`, `--yellow-tint: #FEF7E0;`, `--green-tint: #E6F4EA;`, `--red-tint: #FCE8E6;`.
  - Radii: `--radius-card: 1.75rem;`, `--radius-dialog: 1.75rem;`, `--radius-pill: 9999px;`.
  - Layout: `--max-width: 72rem;`.
- **Fonts**:
  - Headings and body use Google Sans loaded from Google Fonts in `src/app.html` (weights 400, 500, 700).
  - Fallbacks: `system-ui, -apple-system, 'Segoe UI', Roboto, sans-serif` specified in `src/app.css`.
- **Departures from `DESIGN.md`**:
  - None. All token values, contrast standards, button geometries, and layout spacing match the rules in `DESIGN.md`.

## 7. Accessibility and SEO
- **Heading Hierarchy**: Exactly one `<h1>` in `Hero.svelte`. Sequential descent from `h1` to `h2` for section titles, down to `h3` for product cards and subsection items. No levels are skipped.
- **Alt Text and Screen Reader Support**:
  - Decorative SVG icons and brand dots specify `aria-hidden="true"`.
  - Interactive icons include explicit accessible descriptions via `aria-label` (e.g., dialog close button, GDG Davao social links).
  - Screen reader-only heading `.sr-only` is provided for the footer landmark.
- **Focus Indicators**: Explicit focus rings defined with `:focus-visible` (3px solid `--blue-text` with 2px offset on light surfaces; 3px solid `#8AB4F8` with 2px offset on dark sections).
- **Color Contrast**: All text color pairings achieve >= 4.5:1 contrast against their respective backgrounds (`--ink` on white = 16.1:1, `--grey` on white = 6.1:1, `--blue-text` on white = 5.4:1, white on `--blue-text` = 5.4:1, white on `--ink` = 16.1:1).
- **SEO & Metadata (`src/routes/+page.svelte`)**:
  - `<title>`: "Duriano Coffee — Bold like Davao. Smells like a story."
  - `<meta name="description">`: "Small-batch coffee infused with Davao durian. Creamy, bold, unapologetic. Experience the signature roast from Davao City."
  - Open Graph tags: `og:title`, `og:description`, `og:image`, and `og:type` defined in `<svelte:head>`.

## 8. Constraints
- Fixed frontend-only stack: SvelteKit with Svelte 5 runes and TypeScript, `@ark-ui/svelte`, and plain CSS.
- No backend routes (`+server` files) or SvelteKit form actions.
- No external runtime APIs, database connections, or secrets (`.env` files are excluded).
- No third-party CSS frameworks (e.g., Tailwind) or UI component suites beyond Ark UI.
- External outbound links in the DevFest section open in new tabs with `rel="noopener noreferrer"`.
