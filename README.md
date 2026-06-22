# Curae

Marketing site for **Curae** — a New York events studio. *Events, with care.*

Live: <https://joincuraecollective.com>
Contact: [info@joincuraecollective.com](mailto:info@joincuraecollective.com)

## What this is

A single, self-contained static page. No framework, no bundler, no build step.
`index.html` carries the markup, the inlined CSS, and the inlined JavaScript.
The only external dependency is Google Fonts (Fraunces + Inter). Everything is
scroll-driven with plain DOM APIs (IntersectionObserver, `requestAnimationFrame`),
and degrades to a static, fully readable page under `prefers-reduced-motion`.

```
.
├── index.html        # the entire site
├── 404.html          # styled not-found page
├── og-image.png      # social share card (1200×630)
├── favicon.svg       # primary icon  (+ favicon-32.png, apple-touch-icon.png)
├── logos/            # client logos shown in the "We work with" grid
├── CNAME             # custom domain → joincuraecollective.com
├── robots.txt
├── sitemap.xml
└── .nojekyll         # tells GitHub Pages to skip Jekyll
```

## Local preview

No install needed. From the repo root:

```bash
python3 -m http.server 8000
```

Then open <http://localhost:8000>. Use a server (not a `file://` open) so the
relative `logos/` paths and the fonts resolve the same way they will in
production. Any equivalent works too, e.g. `npx serve`.

## Deploy (GitHub Pages)

This repo deploys with **zero build step**.

1. Push to GitHub.
2. Settings → Pages → Build and deployment → Source: **Deploy from a branch**.
3. Branch: `main`, folder: `/ (root)`. Save.

### Custom domain

The `CNAME` file points the site at `joincuraecollective.com`. With the custom
domain, also set it under Settings → Pages and add DNS records at your registrar:

- Four `A` records for the apex `@` → `185.199.108.153`, `185.199.109.153`,
  `185.199.110.153`, `185.199.111.153`
- (optional) a `CNAME` record for `www` → `<username>.github.io`

## Asset / logo notes

- **All paths are relative** (e.g. `logos/google.png`, never `/logos/...`), so the
  site works unchanged at both the apex domain and a `/<repo>` project-pages URL.
- The `.nojekyll` file is required so Pages serves the `logos/` directory verbatim.
- The grid shows the client **name** by default and swaps to the **logo image** on
  hover. Each `<img>` has an `onerror` fallback that hides a missing image and keeps
  showing the name, so a dropped file degrades gracefully.
- To add a client: drop a transparent PNG/SVG/WebP in `logos/` and add a `.logo`
  block in the `.logos` grid in `index.html`, mirroring the existing entries.
