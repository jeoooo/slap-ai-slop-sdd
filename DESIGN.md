# Duriano Coffee: design

Visual and interaction rules for the landing page. The spec says what the page contains; this file says how it looks and feels. If this file and the spec conflict, the spec wins. If this file and `CLAUDE.md` conflict on a token value, `CLAUDE.md` wins.

## Feel

Google-inspired: clean, bright, friendly, lots of white space, soft rounded shapes, Material-style surfaces. The brand is still Duriano Coffee, so the copy stays playful and a little cheeky about the smell. The theme is visual only.

Do not use: the Google logo, the word "Google" as a brand, the multicolor "G", Google product icons or any other Google mark. Avoid stock-coffee clichés (steam swirls, bean piles), heavy gradients, glassmorphism and drop-shadow-heavy cards.

## Color

Defined as CSS variables in `src/app.css`.

| Token | Value | Role |
|---|---|---|
| `--blue` | #4285F4 | Decoration: shapes, borders, illustration fills. Never text. |
| `--red` | #EA4335 | Decoration only. Never text. |
| `--yellow` | #FBBC05 | Decoration and highlights. Text on it is `--ink`. |
| `--green` | #34A853 | Decoration only. Never text. |
| `--blue-text` | #1967D2 | Links, blue text, primary button background. |
| `--ink` | #202124 | Body text, headings, dark section backgrounds. |
| `--grey` | #5F6368 | Secondary text. |
| `--surface` | #F8F9FA | Alternate section background, card fill. |
| `--white` | #FFFFFF | Page background, text on dark and on the primary button. |

Optional tints for badges and card accents: blue #E8F0FE, yellow #FEF7E0, green #E6F4EA, red #FCE8E6, always with `--ink` text.

Contrast, measured:

| Pair | Ratio | Use |
|---|---|---|
| ink on white | 16.1 | Body and headings |
| grey on white | 6.1 | Secondary text |
| grey on surface | 5.7 | Secondary text on grey sections |
| blue-text on white | 5.4 | Links, blue text |
| blue-text on surface | 5.1 | Links on grey sections |
| white on blue-text | 5.4 | Primary button label |
| ink on yellow | 9.4 | Text on yellow highlights |
| ink on each tint | 13.7 to 15.0 | Badges, card accents |
| light blue #8AB4F8 on ink | 7.6 | Links on dark sections |
| blue #4285F4 on white | 3.6 | Fails 4.5:1. Not for text. |
| red, green on white | 3.9, 3.1 | Fail 4.5:1. Not for text. |
| white on blue #4285F4 | 3.6 | Fails. Do not use it for the button. |

Mostly white and `--surface`, with one `--ink` section for rhythm. The four brand colors appear together as small accents (a four-dot motif, section markers, card top borders), never as large color fields.

## Typography

- Google Sans for everything, loaded from Google Fonts (weights 400, 500, 700). Fallbacks: `system-ui, -apple-system, "Segoe UI", Roboto, sans-serif`.
- Headings weight 500 to 700, body weight 400. No second typeface.
- Fluid sizes with `clamp()`. Approximate range: h1 2.5rem to 4.25rem, h2 1.75rem to 2.75rem, h3 1.25rem to 1.5rem, body 1rem to 1.125rem.
- Line height 1.15 to 1.25 for headings, 1.6 for body. Paragraphs at most 65ch.
- Sentence case. Left-aligned, except the hero headline and the final CTA, which are centered.
- Light Bisaya or Tagalog phrases ("Sulayi na!") may be set in italics.

## Layout and spacing

- Mobile-first. Design at 375 px, then widen. No horizontal scroll at 375 px or 1280 px.
- One content width: `max-width: 72rem`, centered, 1rem side padding on mobile and 2rem from 768 px.
- 8 px spacing scale: 0.5, 1, 1.5, 2, 3, 4, 6 rem. Sections get 4rem vertical padding on mobile and 6rem from 768 px.
- Product cards: one column on mobile, three from 768 px, equal height within a row.
- No sticky header, no floating widgets.

## Shape and depth

- Radius: 1.75rem on cards and dialogs, 999px on buttons and chips. Rounded, never sharp.
- Depth comes from tonal surfaces (`--surface` on white) and a 1px border in `--ink` at low opacity. At most one soft shadow, on the dialog.
- Imagery is CSS and inline SVG or emoji. Simple round and pill shapes in the four brand colors may echo durian spikes. Meaningful images have alt text; decorative shapes use `aria-hidden="true"`.

## Components

- **Primary button** ("Reserve a pack"): `--blue-text` background, white text, weight 500, pill, min height 3rem, horizontal padding 1.75rem. Hover darkens slightly and adds a focus-safe state layer. State never relies on color alone.
- **Secondary button** ("Details"): transparent, 1px `--blue-text` border, `--blue-text` text, pill. On the dark section: light blue #8AB4F8 border and text.
- **Product card**: white or `--surface`, 1px border, a 4px top border in one brand color per card, name, one-line description, peso price, then the Details button.
- **Dialog** (Ark UI): centered, max width 32rem, `--ink` backdrop at about 50% opacity, a visible close button labelled for assistive tech.
- **Accordion** (Ark UI): full-width rows separated by 1px rules, a chevron that rotates when open, step number in a small tinted circle. One item open at a time.
- **Review quote**: tinted card, quote text, name. The "Sample reviews for demo." label sits above the group, always visible.
- **DevFest band**: a full-width `--surface` band with the four-dot brand motif, a small "Coming soon · November 2026" chip (yellow tint), a short h2, one primary "Register now" button, then three round social icon links (inline SVG, 44 px targets, each with an accessible name). It is the one place the page talks about something outside the coffee; keep it light and short. It sits between the final CTA and the footer, so its button is a secondary-weight pill to avoid a second primary button in view.
- **Footer**: `--ink` background, white text, always showing "Demo site, not a real business." and "Google-inspired theme, not affiliated with Google."

Style Ark UI parts with `[data-scope="dialog"][data-part="content"]` style selectors. Do not override their behavior.

## Interaction

- Focus ring: 3px solid `--blue-text` with 2px offset on light surfaces, 3px solid #8AB4F8 on `--ink`. Never `outline: none` without a replacement.
- Hover and focus transitions at most 200 ms. Respect `prefers-reduced-motion`: no transform or scroll animation when it is set.
- Dialog open and close fade only. Accordion height may animate, but not under reduced motion.
- Tap targets at least 44 by 44 px.

## Voice in the UI

Short, warm, a little cheeky about the smell. Sentence case. Button labels are verbs ("Reserve a pack", "Details"). No exclamation marks outside "Sulayi na!". No health claims.

## Do not

- Add colors, fonts or icon libraries beyond this file.
- Use `--blue`, `--red`, `--green` or `--yellow` for text.
- Use more than one primary button in the same viewport.
- Hide the demo and affiliation disclaimers.
