# Landing page (brief-aware)

This is the self-contained landing-page spec for the campaign — a brief-aware
build of a scroll-driven premium product page. Key rule: **do not re-derive
identity here.** The
thesis line, scene sentence, palette tokens, typography, tone, CTA, scroll
concept, and the 5 asset prompts already exist in `brief.md`. Read them and
build. Output goes to `campaign-<slug>/website/`.

Build the page, generate the assets, verify in the browser, iterate until it
ships. Do not stop after planning. The page must feel like a premium product
page, not an AI template — if someone could glance at it and say "AI made that",
it failed.

## Section order (exact)

1. Hero with `hero.mp4` full-bleed
2. Thesis line (from brief)
3. Two feature pairs using `g1.jpg` and `g2.jpg`
4. Gallery band: image / `middle.mp4` / image
5. Three numbered detail rows
6. CTA (the brief's demo placeholder)
7. Animated footer

## Files

- one `website/index.html`
- one `website/assets/` folder
- clean HTML/CSS/JS, no build step unless absolutely necessary
- smooth inertia scrolling (Lenis or a lightweight equivalent)
- scroll-triggered reveals (GSAP ScrollTrigger or a lightweight equivalent)
- hero that moves before the first scroll
- responsive: desktop, tablet, mobile

## Assets

Generate exactly the 5 assets defined in the brief — **2 videos + 3 images,
each used exactly once.** Use the higgsfield CLI; pass the product image as the
visual reference so identity holds.

- Vertical product stills (`g1`, `g2`, `g3`): prefer the
  `higgsfield-product-photoshoot` skill (`product-photoshoot create`) — its
  enhancer is built for brand product visuals. Map: `g1` → `lifestyle_scene`,
  `g2` → `product_shot` or `conceptual_product` (macro/detail), `g3` →
  `moodboard_pin` or `hero_banner`. Pass `--image <product>` and `--aspect_ratio`
  to a vertical ratio (`3:4`/`4:5`/`9:16`), `--resolution 2k`.
- Videos (`hero.mp4`, `middle.mp4`): `higgsfield generate create seedance_2_0
  --prompt "..." --start-image <product-or-still> --duration 8 --aspect_ratio
  16:9 --wait`. Lock camera motion to the scroll axis: no drift, no random zoom,
  constant velocity. The two videos must feel like siblings — change only motion
  or framing.

Inspect each asset before wiring it in. Reject and regenerate per the
consistency laws in SKILL.md (identity drift, wrong material, baked-in text,
broken details, off-palette, obviously AI). Only wire assets into `index.html`
after they pass.

## Copy (English, from the brief's tone)

Write directly into `index.html`: one eyebrow, one lede, the thesis line, three
captions (3–5 words, one accent word each), two feature blocks (heading + two
sentences), three numbered detail rows, one CTA line. Headlines short, specific
beats generic, no jargon, no spec-sheet dumping, no em dashes, no intro line
that repeats the title. Every claim concrete enough to be falsifiable.

## Hard visual bans

No generic gradient text, no glassmorphism, no identical card grids, no huge
fake hero metrics, no SaaS clichés, no blurry AI blobs, no random neon, no
stock-photo emptiness, no meaningless icons, no placeholder-looking sections.
One committed accent. Hero text sits on a soft dark halo so it never washes out.

## Browser QA (mandatory)

Start a local server, open the site, and check at desktop, tablet, and mobile
widths:

- loads with no console errors; all assets load
- hero moves before the first scroll; scrolling is smooth; reveals fire
- no layout overlap, no clipped text, no broken mobile layout
- no visible placeholder text, no missing images, no reused asset
- exactly 2 videos + 3 images, each once
- CTA visible and clear; text readable; contrast acceptable
- does not feel like a generic AI template

Fix and retest until it passes. Record pass/fail in the final report.

This reference is fully self-contained: same premium standards as a standalone
scroll-page brief, but identity comes from `brief.md`, copy is English, and the
CTA is the demo placeholder. No external spec file is required.
