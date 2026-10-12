# Brand Brief — the single source of truth

The brief is the most important artifact in this skill. Every downstream output
reads from it, so spend real effort here. Derive each field from the image plus
the two interview answers. Write it to `campaign-<slug>/brief.md` using the
template in `assets/brief-template.md`.

A good brief is specific and falsifiable, not marketing fluff. "Two-thirds less
acid" beats "smooth and delicious". The same rule applies to every field below.

## Identity fields

1. **Product identity** — what the product literally is: category, material,
   shape, distinctive features, brand/product name. This is the anchor for visual
   consistency; describe it concretely enough that every asset prompt can repeat
   it verbatim.
2. **Audience & feeling** — who it is for and the single emotion the campaign
   should create. One sentence.
3. **Thesis line** — the one line the entire campaign serves. Short, specific,
   memorable, not generic. English. This is the spine: the landing-page hero, the
   strongest Reel hook, and the blog title all flow from it.
4. **Scene sentence** — who is using this product, where, and in what light.
   This sentence decides whether the palette is dark or light and seeds every
   asset's environment, so write it before the palette.
5. **Palette (OKLCH)** — exactly four tokens: `bg`, `ink`, `muted`, `accent`.
   Build them from the scene, not from the category. Rules: OKLCH only; never
   pure `#000` or `#fff`; tint every neutral slightly toward the brand hue;
   exactly one saturated accent, everything else quiet; reduce chroma as
   lightness approaches 0 or 1 so it never goes garish.
6. **Typography** — one display face for headings, one clean body face. Readable
   first, stylish second. Name real web-available fonts (e.g. Google Fonts) so
   the landing page and blog can load them identically.
7. **Tone** — three voice adjectives plus a one-line do/don't. Drives the
   copy in all three outputs so the writing voice is consistent.
8. **CTA text** — an English demo placeholder (e.g. "Discover now",
   "Learn more"). Used identically as the final action on the site, at the end
   of the blog, and in every Reel caption. One destination, one wording.
9. **Scroll concept** — pick exactly one from the landing-page spec (A Ambient
   Loop, B Scroll Scrub, C Cursor Spotlight, D Horizontal Pan, E Exploded View,
   F Push Through, G Scrollytelling). Choose by what scrolling *means* for this
   product, and note the hero motion so `hero.mp4` is generated to match.

## Reel decision (resolve "style per image" here)

This is where the "decide the Reel style after seeing the image" choice gets
locked. Inspect the product and pick:

- **Cinematic product (no person)** — pure product motion via Seedance. Default
  for premium, design-led, or abstract products, and the safest match for the
  landing-page look. Prefer this unless a person clearly adds value.
- **UGC presenter** — a talking person via Marketing Studio. Choose when the
  product is used/worn/demonstrated by a person and a relatable testimonial sells
  it better (beauty, food, apparel, gadgets-in-hand).

State which you picked and one sentence why. If you pick UGC and want the same
face across all three Reels, note that the Reels step can train a Soul Character
(`higgsfield-soul-id`) once and reuse it.

Then fix the **3 Reel angles** (these are the locked default — adjust only with a
reason):

- **Reel 1 — Hook / problem→solution**: opens on tension or a scroll-stopping
  visual, resolves into the product.
- **Reel 2 — Product showcase (cinematic)**: the product as the hero, clean
  motion. This one reuses the site's hero/middle video via `reframe`.
- **Reel 3 — Atmosphere / lifestyle**: the product in its scene/world, mood over
  message.

## Asset-prompt list (write all of these in the brief)

Write every prompt now so the checkpoint shows exactly what will be generated.
All prompts must repeat the same product identity, material, lighting, and
palette language from the fields above. No text inside any image or video.

**Site assets (5)** — consumed by the landing page:

- `hero.mp4` — full-bleed hero video, moves before the first scroll, establishes
  the mood, motion matches the scroll concept.
- `middle.mp4` — a sibling of the hero, different motion/angle, same world.
- `g1.jpg` — vertical context shot: product in its scene.
- `g2.jpg` — vertical extreme macro: material/texture/detail.
- `g3.jpg` — vertical hero still: premium campaign image.

**Reel prompts (3)** — one per angle above, 9:16. For the showcase angle, note
"reuse `hero.mp4`/`middle.mp4` via reframe" instead of a fresh prompt unless the
reframe result is weak.

**Blog image (1)** — a 16:9 or 3:2 lead image. Prefer reusing a site still
(reframed) over a new generation; only write a fresh prompt if the blog needs a
wide image the site does not have.

## Checkpoint output

After writing `brief.md`, present the compact summary described in SKILL.md
(thesis, scene, palette, fonts, tone, CTA, scroll concept, Reel angles+style,
and the full prompt list) and ask for approval before generating anything.
