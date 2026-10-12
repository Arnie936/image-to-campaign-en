# Blog article (English, SEO, on-brand)

The blog is the mid-funnel piece: it builds trust and can rank in search, then
points to the landing page. It must look like it belongs to the same brand, so
it reuses the brief's palette tokens and fonts rather than inventing a new look.
Output to `campaign-<slug>/blog/blog.html`.

## Spec

- **Language:** English (or the campaign language set in the brief).
- **Length:** ~600–900 words. Long enough to be useful, not padded.
- **Topic:** derive from the thesis line — a question or need the target audience
  actually searches for, that the product answers. Not "About our product".
- **Voice:** the brief's tone. Specific, concrete, falsifiable claims; no fluff,
  no keyword stuffing, no em dashes.
- **Structure:**
  - one `<h1>` (the article title, distinct from the thesis line but related)
  - a short lead paragraph that frames the problem
  - 3–4 `<h2>` sections with real substance
  - a closing section that turns into the CTA back to the landing page
- **Image:** one lead image. Prefer reusing a site still (`g1`/`g3`) reframed to
  a wide ratio over a fresh generation; only generate a new 16:9/3:2 image if the
  article needs one the site does not have. Save it under `blog/assets/`.
- **Internal link:** the CTA links to `../website/index.html` (relative), using
  the brief's CTA wording. When the site is later deployed, this becomes the live
  URL.
- **SEO basics:** a `<title>` and `<meta name="description">` in English, one
  clear `<h1>`, descriptive `alt` text on the image, semantic headings.

## Templating

Use `assets/blog-template.html`. Replace the placeholders from `brief.md`:

| Placeholder | Source |
|---|---|
| `{{BG}}` `{{INK}}` `{{MUTED}}` `{{ACCENT}}` | the brief's 4 OKLCH palette tokens |
| `{{DISPLAY_FONT}}` `{{BODY_FONT}}` | the brief's fonts (with a Google Fonts `<link>`) |
| `{{TITLE}}` | article `<h1>` / `<title>` |
| `{{META_DESCRIPTION}}` | English SEO description, ~150 chars |
| `{{HERO_IMG}}` `{{HERO_ALT}}` | lead image path + English alt text |
| `{{CONTENT}}` | the article body as semantic HTML (`<p>`, `<h2>`, …) |
| `{{CTA_TEXT}}` | the brief's CTA placeholder |
| `{{LANDING_URL}}` | `../website/index.html` |

Because the tokens and fonts come from the same brief, the blog and the landing
page render as one visual system automatically. Verify the page opens cleanly in
the browser (fonts load, image shows, CTA links correctly, readable on mobile
width) before considering it done.
