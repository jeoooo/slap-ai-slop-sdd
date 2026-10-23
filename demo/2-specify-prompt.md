Paste after typing `/speckit-specify`. (What and why only. Do not mention technology here.)

---

Build a landing page for a fictional Davao durian coffee brand called **Duriano Coffee**.

**Brand**
- Tagline: "Bold like Davao. Smells like a story."
- Tone: playful, warm, a little cheeky about the smell. English with light Bisaya/Tagalog touches (e.g. "Sulayi na!" = "Try it!").
- Theme: Google-inspired. Clean, friendly and bright, like a Google product page, with Material-style rounded shapes. The brand stays Duriano Coffee.
- Palette: Google blue #4285F4, red #EA4335, yellow #FBBC05, green #34A853 on white, with ink #202124 for text and a light grey surface #F8F9FA. Use #1967D2 for blue text and the primary button. The four brand colors are decoration only, never text.
- Font: Google Sans for headings and body.

**Sections, in order**
1. Hero: headline "Coffee that dares you to smell it first." Subhead "Small-batch coffee infused with Davao durian. Creamy, bold, unapologetic." Primary CTA "Reserve a pack" (a mailto link to a fictional address).
2. Story: 2-3 short paragraphs about pairing a Davao durian with local-roasted beans. Fictional.
3. The Brew: three product cards with name, one-line description and a sample price in pesos: Classic Duriano (medium roast, creamy finish), Dark Husk (dark roast, bold and smoky), Iced Durian Latte Mix (ready-to-mix sachet). Each card has a "Details" button that opens a dialog with brew notes (roast, best way to brew, serving tip).
4. How to enjoy it: three steps (brew, add milk, sip) shown as expandable items, one open at a time, plus one tip for first-timers.
5. Sample reviews: 3 short quotes, labelled "Sample reviews for demo."
6. Final CTA: repeat "Reserve a pack."
7. DevFest Davao 2026 (a small easter egg, a real event promoted on this demo site): a friendly band that says the event is coming soon in November 2026 and that registration is open. Main link "Register now" goes to https://apohub.gdgdavao.org/e/devfest-davao-2026. Below it, three social links for GDG Davao: Facebook https://www.facebook.com/gdgdavao, GitHub https://github.com/gdgdavao, LinkedIn https://www.linkedin.com/company/gdg-davao/. Do not invent a date, venue, speakers or prices.
8. Footer: fictional Davao City address, social placeholders, "Demo site, not a real business." and "Google-inspired theme, not affiliated with Google."

**Requirements and acceptance criteria**
- Responsive: no horizontal scroll at 375 px and 1280 px; cards stack on mobile.
- Accessibility: one h1; headings never skip levels; all images have meaningful alt text; text contrast >= 4.5:1; visible keyboard focus; everything reachable by Tab. The dialog traps focus, closes with Esc, and returns focus to the button that opened it. The expandable steps work with the keyboard.
- SEO and sharing: title, meta description, Open Graph tags (og:title, og:description, og:image).
- Performance: Lighthouse Performance >= 90 and Accessibility >= 95 on mobile (measured on the production build).
- CTA: primary CTA appears in the hero and the final section, and works. The DevFest registration link and the three social links work, open in a new tab with `rel="noopener noreferrer"`, and have accessible names (for example "GDG Davao on Facebook").
- Content: no lorem ipsum, no health claims, no imitation of a real business. Use the Google look as a visual theme only: no Google logo, name or product marks.
