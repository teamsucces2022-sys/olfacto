# OLEFACTO — Landing Page

A premium, production-ready e-commerce landing page for the OLEFACTO fragrance brand.
Plain HTML/CSS/JavaScript — no build step, no framework, no dependencies to install.
Open `index.html` in a browser and it works.

---

## ⚠️ Before you launch — please read

1. **Bottle label mismatch.** Your brief names the brand "OLEFACTO," but the physical
   bottle label in the photo you uploaded reads **"OLFACTO"** (no middle "E"). All text
   on this site uses **OLEFACTO** per your written brand name. The bottle photo itself
   is used unedited, exactly as instructed — so right now the headline says OLEFACTO
   while the actual bottle in the hero image says OLFACTO. Double-check which spelling
   is correct and relabel the bottle (or update the site copy) before launch — worth
   fixing before this goes in front of customers.

2. **Every fragrance name, description, note, price, badge, and review in this build
   is placeholder content**, exactly as requested. Nothing here should be treated as
   real product or customer data. See "Editing content" below for where to change it.

3. **All 40 product photos are currently the same real bottle photo you uploaded**,
   copied into each placeholder slot so the collection preview looks cohesive rather
   than empty. Replace each with a real photo before launch (see below) — it's a
   one-file swap per fragrance, nothing else needs to change.

---

## Project structure

```
olefacto/
├── index.html              All page markup and content sections
├── css/
│   └── style.css           All styling, design tokens, responsive rules
├── js/
│   ├── products-data.js    ★ THE ONLY FILE YOU NEED FOR PRODUCTS & REVIEWS
│   └── main.js              Rendering + interactivity (filter, FAQ, nav, etc.)
├── images/
│   ├── hero/                Main hero bottle photo + social-share image
│   ├── icons/                Favicon assets
│   ├── men/01.jpg – 20.jpg   One image per men's fragrance
│   └── women/01.jpg – 20.jpg One image per women's fragrance
└── favicon.ico
```

---

## Editing content

### Add, remove, or edit a fragrance
Open **`js/products-data.js`**. Every fragrance is one object in the `PRODUCTS` array:

```js
{
  id: 1,
  name: "Men's Fragrance 01",
  gender: "men",                 // "men" or "women" — drives the filter
  image: "images/men/01.jpg",
  price: "249 MAD",
  oldPrice: "349 MAD",           // set to "" to hide the strikethrough price
  discount: "-29%",              // set to "" to hide the badge
  description: "...",
  topNotes: "Bergamot, Pink Pepper",
  heartNotes: "Rose, Cinnamon",
  baseNotes: "Musk, Tonka Bean",
  badge: "Bestseller",           // "Bestseller" / "New" / "Limited Edition" / ""
  availability: "in-stock"
}
```

Edit any field directly, duplicate an object to add a fragrance, or delete one to
remove it. **You never need to touch `index.html` or any CSS** — the grid, the
filter, and the "Discover Your Signature Scent" offer picks (which auto-pull your
`Bestseller`-badged products) all render from this one array.

### Replace a product photo
Overwrite the file at the path in that product's `image` field — e.g. drop a new
photo in as `images/men/03.jpg`, same filename, same folder. Nothing else to update.

**Recommended source images:** portrait orientation, roughly 1000×1300px or larger,
JPEG. Keep the same aspect ratio (3:4) across all products so the grid stays aligned.

### Edit customer reviews
Also in `js/products-data.js`, below `PRODUCTS`, is a `REVIEWS` array — same idea,
one object per review (`name`, `location`, `rating` 1–5, `text`). These are sample
placeholders — replace with real feedback once you have it, and please don't mark
placeholder reviews as "verified" if you keep any of these live.

### Edit everything else (hero copy, Why Olefacto, FAQ, footer, etc.)
This text lives directly in `index.html` since it changes far less often than the
product catalogue — search for the section by its `<!-- ============ NAME ============ -->`
comment and edit the text in place.

---

## Design system

- **Colors** — all defined once as CSS variables at the top of `css/style.css`
  (`:root { --ink, --gold, --cream, --stone, ... }`). Change a value there and it
  updates everywhere.
- **Fonts** — Bodoni Moda (headlines) + Jost (body/UI), loaded from Google Fonts.
  This means **an internet connection is required** for the intended typefaces to
  load; without one, browsers fall back to a standard serif/sans-serif automatically,
  so the page still works, just not with the exact intended type. To make the site
  fully self-contained/offline-capable later, download the two font files and
  self-host them instead of using the Google Fonts `<link>` tags in `index.html`.
- **Signature motif** — the thin gold wave/line graphic (in the hero, and faintly
  behind the final call-to-action) is drawn from the swirl mark already engraved on
  your bottle label, so the digital design ties back to the physical product rather
  than being a generic decoration.

---

## Previewing locally

Just open `index.html` in any browser — no server required. If your browser blocks
local file access for any reason, run a tiny local server from this folder instead:

```
python3 -m http.server 8000
```
then visit `http://localhost:8000`.

## Deploying

This is a static site — it works on any static host. Drag-and-drop the whole
`olefacto` folder onto **Netlify** or **Vercel**, or push it to a repo and enable
**GitHub Pages**. No build command, no environment variables, nothing to configure.

Before going live:
- Update `<link rel="canonical">` and the `og:url` / `og:image` meta tags in
  `index.html`'s `<head>` with your real domain.
- Wire the "Shop Now" buttons (`data-product-id` in `js/main.js`, function
  `initProductCtas`) and the newsletter form (`initNewsletter`) to your real
  cart/checkout and email provider — both currently have clearly-marked placeholder
  behavior (console log / on-page thank-you message) so nothing breaks, but nothing
  is actually wired to a backend yet.
- Fill in the FAQ's support contact details and the footer's social links (currently `#`).

---

## Notes on SEO

The product grid is rendered client-side from `products-data.js` so that you can
manage all 40 fragrances from one place without touching markup. Modern search
engines generally index JavaScript-rendered content fine, and all core SEO
fundamentals are in place (semantic HTML, meta description, Open Graph/Twitter
tags, JSON-LD Organization + FAQPage structured data, descriptive alt text, proper
heading hierarchy). If deep per-fragrance search ranking becomes a priority later
(e.g. a dedicated page per product), that's a bigger step — a static site generator
would be the natural next move, and is a separate project from this landing page.
