# CLAUDE.md

Second Sun: a one-page Astro 5 storefront for a fictional vintage shop, built from Figma. See `README.md` for setup and structure.

## Commands

- `npm run dev`: dev server (port 4321, or the next free one)
- `npm run build`: static build; run this before finishing a change
- No test suite or linter. Verify visually in a browser at 1440px and 390px.

## Figma

- File key: `SgKQO5cAPK4Y7hVcRyApc5` (https://www.figma.com/design/SgKQO5cAPK4Y7hVcRyApc5/design-1)
- Frames: Foundations `4:2`, Desktop `21:2`, Mobile `22:5`, Mobile nav closed `30:8`, Mobile nav open `30:33`
- To implement or update a section, use the Figma MCP `get_design_context` on that section's node, with a screenshot. Adapt the output to Astro and plain CSS. Never paste React or Tailwind output, and never install Tailwind.
- Download image and SVG assets locally into `src/assets/`. Never reference temporary Figma asset URLs.
- Figma variables are bound to the design. When Figma changes, update the matching CSS variable in `src/styles/global.css` rather than hardcoding values in components.
- The original mobile frame (`22:5`) still has the old wrapped-link nav. The site intentionally follows frames `30:8` and `30:33` instead. Do not revert the mobile nav to wrapped links.

## Conventions

- One section per component in `src/components/`, composed in `src/pages/index.astro`.
- Styles are scoped in each component's `<style>`. Shared pieces live in `global.css`: tokens (`--color-*`, `--spacing-*`, `--radius-*`), type classes (`.label`, `.nav-link`, `.display`, `.h1`, `.h3`, `.body-lg`, `.body-sm`), and buttons (`.btn`, `.btn--primary`, `.btn--outline`).
- Use the token variables, not hex values or magic numbers, where a token exists.
- Breakpoints are 1100px, 900px and 767px (max-width). Layouts are fluid CSS grid or flex inside the `.wrap` container (1312px content width plus gutter), not absolute positioning.
- Photos use Astro's `<Image>` from `astro:assets`. Icons are SVG files imported from `src/assets/icons/` and used with `<img>`.
- All copy, address, hours, quotes and emails are placeholders. Keep them clearly fictional (`.example` domain).

## Mobile nav (Header.astro)

At 767px and below: a 64px bar with the wordmark, a compact "Come on by" button and a "Menu" toggle. The toggle opens a full-width dropdown with large Fraunces links. It closes on link tap, the CTA, Escape, outside tap, and resize to desktop. Background scroll is locked while it is open. The toggle has `aria-expanded` and `aria-controls`. To add a nav link, add an entry to the `links` array at the top of the file. The bar height stays the same.

## Gotchas

- Downloaded images are JPEGs. Keep the `.jpg` extension even if Figma serves them as `.png`.
- `<Image>` adds `width` and `height` attributes. The global `img { height: auto }` rule keeps `aspect-ratio` working, and `.hero__photo img` overrides it with `height: 100%`.
- Use `box-sizing: border-box` (set globally). A `.wrap` element with `content-box` overflows the page.
- On macOS, `sed -i` needs an empty-string argument. Prefer the Edit tool.
- If the dev server serves stale CSS after edits, stop it, delete `node_modules/.vite` and `.astro`, and restart. Check that no old server is still holding port 4321.
- `.claude/launch.json` defines the dev server for the Claude desktop app preview. Keep it.
