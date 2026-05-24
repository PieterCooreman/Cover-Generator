# Cover Generator

A single-file, client-side web app that generates beautiful covers for blogs, social media, presentations, and more. Built with vanilla JavaScript and Bootstrap 5 — no build step, no backend, no API keys.

## Features

### Cover composition
- **Title**, **subtitle**, **paragraph**, and up to **3 buttons** — every element is optional and individually toggleable
- **Inline WYSIWYG editing**: click any text on the cover to edit it directly. A floating Bootstrap-styled toolbar offers bold, italic, underline, text color, alignment, and clear-formatting
- **Per-button URL** field: buttons in the HTML export point to real destinations
- Three distinct button styles applied automatically by position: primary (solid), outline, and ghost/glass (semi-transparent)

### Backgrounds
- **Picsum** — random high-resolution photos from Lorem Picsum, with a "Re-roll image" button
- **Solid color** — color picker
- **Gradient** — harmonized two-color linear gradient with random angle
- **Upload** — use your own image from disk

### Smart color palette
- Automatic palette extraction from any background image using ColorThief
- Text color picked to maintain WCAG contrast against the **effective** background (image + overlay)
- Primary button color picked from the palette by saturation × readability score
- Guarantee: never white text on a white overlay, never black text on a black overlay

### Overlay controls
- **Color picker** with **auto** mode that flips between dark and light based on image luminance
- **Opacity slider** (0–100%)
- Only appears for image-based backgrounds

### Typography
- 41 hand-curated Google Display fonts, listed alphabetically
- Includes everything from elegant serifs (Playfair Display, Cormorant Garamond) to bold sans (Bebas Neue, Anton), playful scripts (Lobster, Pacifico), and decorative western fonts (Rye, Sancreek, Smokum)
- Fonts load dynamically via `<link>` injection — only what you use, when you use it

### Layouts
- **Center** — everything centered
- **Left** — left-aligned (default editorial style)
- **Right** — right-aligned
- **Bottom** — anchored to the bottom-left (great for hero sections)
- **Split** — text on left half, image breathing on the right

### Orientation
- **Landscape** (1920×1080, 16:9)
- **Portrait** (1080×1920, 9:16)
- Typography, padding, and layout adapt automatically to the chosen orientation

### Randomize
Press **Space** (or click the Randomize button) to instantly generate a new cover. Distribution:
- 50% image background
- 25% solid color
- 25% gradient

Plus a fresh random font and layout each time.

### Lock toggles
🔒 icons next to **Background**, **Font**, **Palette**, and **Layout** sections let you pin individual aspects so they survive subsequent randomizations. Iterate on a font you love while shuffling everything else.

### Export

| Option | Description |
|---|---|
| **Open in new tab** | Full-page preview at 100% scale |
| **Download HTML (CMS snippet)** | Self-contained, scoped HTML+CSS snippet for pasting into WordPress Custom HTML blocks, Drupal, Squarespace, etc. Uses container query units (`cqw`) to scale fluidly. No `<html>`/`<head>`/`<body>` tags, no JS required |
| **Copy HTML to clipboard** | Same snippet, straight to clipboard |
| **Download PNG (1920×1080)** | Pixel-perfect PNG at native resolution (or 1080×1920 in portrait mode), rendered via html2canvas |

### Quality-of-life
- **localStorage persistence** — your work survives a refresh
- **Toast notifications** for every action
- **Reset all** button to start fresh
- **Mobile-friendly** sidebar collapses into an off-canvas drawer below 992px

## Tech stack

- **Bootstrap 5.3** — UI framework
- **Bootstrap Icons 1.11** — iconography
- **ColorThief 2.4** — palette extraction
- **html2canvas 1.4** — PNG rendering
- **Google Fonts** — display typography
- **Vanilla JavaScript** — no framework, no build step

All dependencies load from public CDNs. No npm, no bundler, no Node required.

## Project structure

```
covergenerator/
├── index.html       # Entire application (HTML + inline CSS + inline JS)
├── README.md        # This file
└── CLAUDE.md        # Coding guidelines used during development
```

The entire app is one HTML file. That's the design constraint.

## How to run

### Option 1: Local HTTP server (recommended)

`file://` URLs block CORS image fetches (Picsum) and may cause issues with PNG export. Use any static server:

```powershell
# From the project directory
python -m http.server 8000
```

Then open <http://localhost:8000> in your browser.

Alternatives:
- `npx serve`
- `npx http-server`
- VS Code Live Server extension

### Option 2: GitHub Pages

1. Push the repo to GitHub
2. Settings → Pages → enable Pages from the `main` branch
3. Visit the published URL

No build configuration needed — it's just a single HTML file.

### Option 3: Any static host

Drop `index.html` into Netlify, Vercel, Cloudflare Pages, S3, or any web server. Done.

## Keyboard shortcuts

| Key | Action |
|---|---|
| `Space` | Randomize (when not editing text) |

## Editing text

- **Single-click** any text element on the cover to enter edit mode
- A floating toolbar appears when you select text — apply formatting
- **Enter** inserts a line break (not a new paragraph)
- **Click outside** the text element to commit
- For buttons: edit text inline; URL is set via the sidebar input

## Browser support

- Chrome / Edge 105+ (container query units required for CMS snippet)
- Firefox 110+
- Safari 16+

The app itself works in older browsers too; only the CMS snippet's `cqw`-based scaling requires recent versions.

## Customization

All knobs live in three places at the top of the `<script>` block in `index.html`:

```js
const FONT_LIST = [...]      // Add/remove Google Fonts
const DEFAULT_TITLE = '...'  // Default placeholder text
const LAYOUTS = [...]        // Layout options
```

CSS variables and selectors are centralized at the top of the `<style>` block — adjust padding, font sizes, max-widths, gaps, etc. without touching JS.

## Privacy

Everything runs in your browser. No server, no analytics, no telemetry. Uploaded images never leave your machine. State is saved only to your browser's `localStorage`.

## License

MIT — do whatever you want.
