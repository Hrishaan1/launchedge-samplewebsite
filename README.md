# LaunchEdge — Sample Landing Page

This repository contains a single-file, responsive SaaS landing page for "LaunchEdge" built with Tailwind CSS (CDN), Google Fonts, and vanilla JavaScript. It's a small sample project intended to demonstrate a modern landing page layout with accessible mobile navigation, animated cards, and simple interactions.

## Project structure

- `index.html` — the entire site (HTML, CSS, and JS) in one file for simplicity.

## Features

- Responsive, single-page layout
- Tailwind CSS via CDN with a small inline Tailwind config
- Google Fonts (Poppins)
- Accessible mobile menu with ARIA attributes and click-outside handling
- Sticky header with subtle backdrop blur
- Animated gradient hero background and floating decorations
- Centralized `.card` component with hover lift and neutral shadows
- IntersectionObserver-driven fade-in animations

## Quick start

1. Open `index.html` in your browser (double-click or open it from a file server).

2. For local development with live reload (optional), you can use a simple static server. If you have Python installed:

```bash
# Python 3.x
python3 -m http.server 8000
# then open http://localhost:8000 in your browser
```

Or use Node's `http-server`:

```bash
npm install -g http-server
http-server -p 8000
```

## Development notes

- The site uses the Tailwind CDN (`https://cdn.tailwindcss.com`) with a small inline `tailwind.config` object defined at the top of `index.html`.
- All custom styles and scripts are embedded in `index.html` for easy sharing.

### Debugging the card hover "snapping" issue

A debugging helper was temporarily added to `index.html` to log computed transforms and bounding rectangles for `.card` elements when hovered. If you're troubleshooting hover snapping:

1. Open DevTools → Console.
2. Hover the card that snaps and inspect the `card-hover-debug` logs.
3. The log shows the card's computed `transform`, `transition`, `box-shadow`, and `rect` snapshots before and after hover.

If you find an ancestor with a non-`none` transform in the logs, that ancestor may be causing the snapping. You can either remove the ancestor's transform, or isolate the card with CSS (`isolation: isolate;` or `transform: translateZ(0);`) to create a new stacking context. The project already applies `isolation: isolate` to `.card` to mitigate this.

### Removing the debug helper

If you want the debug helper removed (it is currently present), open `index.html` and delete the 
```js
// --- DEBUG: enhanced hover logging for .card elements ---
```
block near the end of the file.

## Accessibility

- Mobile menu toggles `aria-expanded` and `aria-hidden` to improve screen reader behavior.
- Buttons and links use clear focus states via Tailwind utility classes.

## Tests

This is a static HTML demo; there are no unit tests included. For small visual checks you can use Playwright or Puppeteer to script hovering each `.card` and taking screenshots.

## Next steps / Suggestions

- Extract styles and JS into separate files for maintainability and easier toolchain integration.
- Add visual regression tests (Playwright/Percy) to catch hover/animation regressions.
- Replace Tailwind CDN with a build setup (PostCSS, Tailwind CLI) for production.

## License

This project is provided as-is for demo purposes.
