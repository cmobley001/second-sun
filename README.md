# Second Sun

A one-page storefront for **Second Sun**, a fictional vintage clothing shop in Chico, California. Built with [Astro 5](https://astro.build) from a Figma design. This is a concept project: the copy, address, opening hours and customer quotes are placeholders.

## Getting started

```bash
npm install
npm run dev      # http://localhost:4321
npm run build    # static build to ./dist
npm run preview  # serve the build
```

Requires Node 18.20+ (developed on Node 25).

## Design source (Figma)

[design-1 on Figma](https://www.figma.com/design/SgKQO5cAPK4Y7hVcRyApc5/design-1)

The file has these top-level frames:

| Frame | Node ID | Purpose |
| --- | --- | --- |
| Design Foundations | `4:2` | Color, type, spacing and radius tokens |
| Second Sun — Chico vintage storefront | `21:2` | Desktop page, 1440px |
| Second Sun — Mobile · 390px | `22:5` | Mobile page, 390px |
| Mobile nav — closed | `30:8` | Updated mobile nav, closed state |
| Mobile nav — open (Menu) | `30:33` | Updated mobile nav, menu open |

The two mobile nav frames were added after the original mobile design. The original mobile frame still shows the earlier wrapped-link nav. The site follows the newer Menu version: a 64px bar with the logo, a compact "Come on by" button and a "Menu" toggle. It stays one height no matter how many links are added.

## Project structure

```
src/
  assets/
    images/        Photos from the design (hero, collections, community)
    icons/         Map marker and social icons (SVG)
  components/      One file per page section
    Header.astro   Announcement bar, nav, mobile Menu toggle
    Hero.astro
    Ribbon.astro   Sage manifesto strip
    Story.astro
    Collections.astro
    Gallery.astro
    Stories.astro  Customer quotes
    Visit.astro    Address, hours, illustrative CSS map
    InnerCircle.astro  Newsletter sign-up (sample form)
    Footer.astro
  layouts/Layout.astro   Document shell and Google Fonts
  pages/index.astro      Assembles the sections
  styles/global.css      Design tokens and shared classes
```

## Design tokens

Tokens from the Figma variables live as CSS custom properties in `src/styles/global.css`, using the same names as in Figma: `--color-bg-page`, `--color-text-primary`, `--spacing-lg`, `--radius-sm` and so on. Shared type and button classes (`.label`, `.nav-link`, `.display`, `.h1`, `.h3`, `.body-lg`, `.btn--primary`, `.btn--outline`) map to the Figma text styles.

Fonts are [Fraunces](https://fonts.google.com/specimen/Fraunces) (headings) and [DM Sans](https://fonts.google.com/specimen/DM+Sans) (body), loaded from Google Fonts.

## Responsive behavior

Components use scoped styles with these breakpoints:

- **1100px and below:** the nav tagline hides and the Visit section stacks.
- **900px and below:** most two-column sections stack.
- **767px and below:** mobile layout, with the Menu toggle replacing the inline nav links.

## Placeholder content to replace

- Address, hours and parking notes in `Visit.astro`
- Customer quotes in `Stories.astro`
- `hello@secondsun.example` and the social links in `Footer.astro`
- The newsletter form in `InnerCircle.astro` only shows a thank-you message and sends nothing
- The map in `Visit.astro` is an illustrative CSS drawing, not a real map. "Get Directions" links to a Google Maps search.
