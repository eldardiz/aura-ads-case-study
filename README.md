# Aura Ads — case study page redesign

Speculative redesign of the Aura Ads case study template, built on the live Tonies® story.

**[View the mockup →](https://aura-ads-case-study.vercel.app)** (or open `index.html` locally)

Before: https://auraads.co/case-studies/tonies

---

## Why this exists

Ryan Walton (Founder & CEO, Aura Ads) asked for a rework of the case study pages. His words: they are CMS based so the marketing manager can fill them out, but the previous developer broke them into multiple CMS sections, which makes them very painful to update.

Reading the published HTML confirms it. One case study on the current site is roughly **52 fields**:

| Group | Fields |
|---|---|
| Name, industry, platforms, hero image | 4 |
| 3 stat blocks (value + label) | 6 |
| Quote: text, avatar, name, role | 4 |
| Rich text bodies (overview, challenge, approach, solution, results) | 5 |
| Fixed image slots | 3 |
| Approach: 5 × (title + body) | 10 |
| Video embeds | 12 (13 on HelloFresh) |
| Card fields for the listings | ~5 |
| Slug, SEO title, SEO description, OG image | ~4 |

Webflow caps a collection at 30 fields, so this cannot live in one collection. That is why it was split. It is a structural problem, not a tidiness one.

Unused slots do not disappear either: TUSHY ships an empty approach block, Gousto three blank video embeds, HelloFresh five empty bindings.

## The fix

The reference Ryan sent (bark.london, Aura's merger partner) is built as a **block stack**. Across five of their case studies: 6 to 12 blocks per page, 10 block types, different order every time, nothing empty. That is the architecture, not just the look.

This mockup rebuilds the Tonies page the same way. Nine blocks:

1. **Hero** — outcome headline, client mark, meta (industry, platforms)
2. **Stat strip** — 3 × value / label / context, over the hero image
3. **Quote** — optional, hides when empty (Tonies has no testimonial in the CMS, so it shows as a visible placeholder here)
4. **Video** — single featured creative
5. **Text** — label + heading + body, repeatable
6. **Numbered list** — the approach principles, any number of them
7. **Creative** — n assets + caption, repeatable, with its own aspect ratio per block
8. **Facts rail** — sticky: client, industry, platforms, services, results, about, CTA
9. **Related** — 4 items from the Case Studies collection

Open the page and hit **"Show CMS blocks"** (bottom left) to see each block outlined and labelled.

Layout follows [ramp.com/customers/hingham](https://ramp.com/customers/hingham): full-bleed hero with stats on the image, quote band, video, 755px story column beside a sticky facts rail, one dark band for the creative wall, results, related stories.

## What is real

- **Every number and every body paragraph** is lifted verbatim from the live Tonies page.
- **Brand tokens** come from Aura's own stylesheet: IntegralCF + PP Neue Montreal, orange `#e96110`, purple `#5c41f7`, lilac `#f2f0fe`, peach `#fef6f1`, teal `#00abaa`.
- **Imagery** is Aura's actual Tonies work: 11 Vimeo stills and 2 statics pulled from the live page.
- **Written for the mockup:** section headlines, the two creative captions, the placeholder quote (marked as a placeholder).

## Notes

- IntegralCF has no lowercase, so every heading renders caps. H2s dropped to 34px to compensate.
- Aspect ratio is per creative block here, not hard-coded into the template as it is on the current site.
- Fonts are included so the page renders on any machine. They are Aura's licensed families (Fontfabric, Pangram Pangram), included for review purposes only.

## Findings from the audit (sent to Ryan, Sept 2026)

1. The "Solution" nav link pointed at `/dev/solution` and 404'd sitewide. **Fixed by their team since.**
2. The 52-field structure above.
3. ~270 assets, including case study heroes, load from a different Webflow site's CDN (`6601a669…`, not the live `65fad326…`).
