# Meridian Bay: design notes (Part A)

Style: Warm Editorial (taste file), with #0052DF as the single accent. Calm, premium, photographic.

## Palette tokens
| Token | Hex | Use |
|---|---|---|
| blue | #0052DF | Primary buttons, links, eyebrow, icons, focus ring (6.4:1 on white) |
| blue-hover | #0045BD | Primary hover |
| blue-wash | #EAF1FD | Icon tiles, ticks, avatars |
| navy | #0B1F4D | Headlines, process panel, form section, footer |
| body | #3B4763 | Body copy (9.3:1 on paper) |
| muted | #5F6A82 | Labels, captions (5.4:1 on paper) |
| context | #8590A8 | First clause of H1 only, large text (3.2:1, AA large) |
| paper | #FAF8F4 | Page background (warm off-white) |
| paper-2 | #F3F0EA | Testimonials band |
| line | #E6E1D8 | Hairlines, card borders |
| sky | #E4ECF8 | Horizon tint at the bottom of the hero |

## Type
- Display: **Newsreader** 500 (opsz axis), normal tracking (-0.01em max). H1 78 / 40 px, H2 52 / 34 px, trust figures 40 / 30 px, quotes italic 500 at 23–28 px.
- Text: **Geist** 400 / 500 / 600. Body 17 px (16 mobile), card titles 600 19 px, labels 600 14.5 px.
- Serif is used once per section, large; never for paragraphs (avoids the "looks like AI" hate entry).
- Final build: self-host both as WOFF2 subsets, `font-display: swap`, preload Newsreader 500 only.

## Spacing / radius
- 4-based scale: 8, 12, 16, 20, 24, 28, 40, 56, 64, 88, 128.
- Section padding 128 px desktop, 88 px mobile. Container 1200 px, gutters 40 / 32 / 20.
- Radius: inputs 12, cards 24, dark panel 32 (24 mobile), buttons 12.

## Components
- **Hero**: pill eyebrow, two-tone H1 (grey question, navy answer), ticks, primary + outline WhatsApp button. Skyline image slot below, masked to fade upward.
- **Trust bar**: one frosted-glass strip overlapping the skyline (the only glass on the page, because it sits over imagery).
- **Problem cards**: buttons. Clicking scrolls to the form and preselects Tenant / Landlord.
- **Process**: navy inset panel, dashed connector between numbered steps.
- **Testimonials**: accent bar beside each quote, first quote larger.
- **FAQ**: native `<details>`, first open, sticky H2 on desktop.
- **Form**: white card on navy; native validation; `action="#"`.
- **Sticky CTA (mobile only)**: appears after the hero CTA leaves view, hides as the form arrives.
- Scroll reveal on section heads and card groups; off under reduced motion; hero never gated.

## Collapse to 375 px
1. Header: logo stacks "Meridian Bay / Legal Consultants"; outline button stays (44 px).
2. Hero: 40 px H1, ticks stack left-aligned, buttons full width. Primary CTA above the fold at 375×812.
3. Trust: 4 columns → 2×2 glass grid.
4. Problems: 4 → 2 (tablet) → 1 column, icon left of title.
5. Process: 3 columns → vertical timeline (≤860 px).
6. Testimonials: 3 → featured + 2 (tablet) → 1.
7. FAQ: two columns → stacked.
8. Form: two columns → stacked; name/WhatsApp row → single column.
9. Footer: stacked, extra bottom padding for the sticky button.

## Image slot
Daytime Marina/JLT skyline, near-white sky, cool haze, skyline in the bottom quarter. ~2400×760, AVIF/WebP under ~120 KB, `object-position: center bottom`, keep the CSS mask. Not the LCP element (the H1 is).
