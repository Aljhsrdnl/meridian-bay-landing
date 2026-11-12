# Meridian Bay Legal Consultants — landing page

A one-page, responsive landing page for **Meridian Bay Legal Consultants**, a rental-dispute law firm in Dubai that represents tenants and landlords at the Rental Dispute Settlement Centre. The page has one goal: get a stressed visitor (usually on a phone, arriving from an ad) to request a free case review through the form or WhatsApp.

Built as **Part A of the PremiumPages Web Designer-Developer test task**. The page copy follows the brief word for word and in the order the brief gives it.

> **The firm is fictional.** Meridian Bay Legal Consultants is not a real company. The page says so in the footer, and the WhatsApp number (`+971 50 000 0000`) is a placeholder. The form doesn't send data anywhere (`action="#"`).

## Stack

- Plain HTML, CSS and vanilla JavaScript in a single `index.html`, with no frameworks, build step or dependencies.
- Font: [Mona Sans](https://github.com/github/mona-sans) (SIL Open Font License 1.1, weights 400/500/600), self-hosted as one variable WOFF2 (Google Fonts' latin subset) in `site/assets/fonts/` with its licence (`OFL.txt`). No third-party font requests.
- Icons: [Phosphor](https://phosphoricons.com) (MIT), inlined as an SVG sprite.
- Images: WebP at several widths, served with `srcset`/`sizes`.
- Photos (day and night Dubai skyline, How it works cards): free stock from Unsplash / Pexels, cropped and converted to WebP.
  - How it works card 3: Vitaly Gariev on Unsplash.
- Situation icons (glass document, calendar, key, trend arrow): AI-generated for this project, used as illustrations (the brief allows icons and illustrations).

The page works without JavaScript. All content is visible, the form uses native validation, and "I am a" falls back to a native `<select>`. JavaScript adds smooth scroll-to-form, the How-it-works carousel controls, the custom dropdown, the validation styling and the sticky mobile button.

## Folder layout

```
meridian-bay-landing/
├── site/                  # the deployable website (deploy this folder)
│   ├── index.html         # the page: HTML + inline CSS + inline JS + JSON-LD structured data
│   ├── robots.txt         # allows all crawlers, AI crawlers listed by name; points to the sitemap
│   ├── sitemap.xml        # the one URL
│   ├── llms.txt           # plain-text summary for AI assistants (optional convention)
│   └── assets/            # WebP images, the OG share image, the favicon set, fonts/ (Mona Sans + OFL.txt)
├── design/                # design sources: approved mockup, notes, original photos, illustrations
└── README.md
```

## Run locally

Any static file server works. Serve the `site/` folder:

```bash
cd site
python3 -m http.server 8080
# then open http://localhost:8080
```

or `npx serve site`.

Opening `index.html` straight from disk (`file://`) mostly works too, but use a server to test how it really behaves.

## Deploy

Deploy **only the `site/` folder**; it holds everything the page needs.

**Vercel**
- Dashboard: import the repo, set *Root Directory* to `site`, Framework preset *Other*, no build command.
- CLI: `npx vercel deploy site --prod`

**Netlify**
- Dashboard: import the repo, set *Base directory* / *Publish directory* to `site`, leave the build command empty.
- Drag and drop: drop the `site/` folder onto app.netlify.com/drop.
- CLI: `npx netlify deploy --dir=site --prod`

**GitHub Pages**
- Pages can only serve from the repo root or `/docs`. Either use a GitHub Actions workflow (*Settings → Pages → Source: GitHub Actions*, using the "Static HTML" starter with `path: site`), or copy the contents of `site/` to a `gh-pages` branch root and publish that branch.

All three hosts serve the files with gzip/brotli compression and HTTPS, which the PageSpeed score relies on.

## Replace before deploy

The live URL isn't known yet, so every absolute URL uses the placeholder origin **`https://meridian-bay.example`** (`.example` is a reserved domain, so it can never resolve to someone else's site). Replace it with the real origin, **without a trailing slash**, in one find-and-replace across `site/`:

```bash
# from the repo root; example origin shown, use yours (macOS sed; on Linux drop the '')
grep -rl 'https://meridian-bay.example' site | xargs sed -i '' 's#https://meridian-bay\.example#https://meridian-bay.vercel.app#g'
grep -rn 'meridian-bay.example' site   # must print nothing
```

Where it appears (29 occurrences, all in `site/`):

| File | What |
| --- | --- |
| `site/index.html` (`<head>`) | `<link rel="canonical">`, `og:url`, `og:image`, and every `@id` / `url` in the JSON-LD block (26 in total) |
| `site/robots.txt` | the `Sitemap:` line |
| `site/sitemap.xml` | `<loc>` (also update `<lastmod>` if the page changes) |
| `site/llms.txt` | the canonical page link |

Notes:
- If the page is served from a sub-path (a GitHub Pages *project* site such as `https://user.github.io/repo/`), use the full base including the path (`https://user.github.io/repo`). Crawlers only read `robots.txt` at the host root, so on a project site it is ignored; submit `sitemap.xml` in Google Search Console instead.
- After deploy, check the share preview (e.g. opengraph.xyz or a WhatsApp message to yourself) and run Google's Rich Results Test and the Schema.org validator on the live URL.

## Checks before submitting

- Copy matches the brief word for word.
- Layout at 375 px, 768 px and 1440 px, with no horizontal scroll.
- PageSpeed Insights (mobile) at 85 or above on the live URL.
