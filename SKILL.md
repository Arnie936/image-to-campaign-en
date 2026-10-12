---
name: image-to-campaign
description: |
  Turn ONE product/brand image into a complete, identity-consistent English
  marketing funnel: a scroll-driven landing page, 3 Instagram Reels (9:16) with
  captions, and a styled blog article — all derived from a single approved Brand
  Brief so everything matches. Output is one campaign folder.
  Use this whenever the user uploads or points at a single product/brand image
  and wants marketing assets, a "campaign", a "funnel", "marketing from this
  image", "posts + videos + website", Instagram content plus a landing page, ads
  that lead to a sales page, or says "turn this image into ads/Reels/a landing
  page". Trigger even when the user names only one piece (e.g. "make Reels from
  this image") if the larger goal is a full campaign, and ESPECIALLY when they
  want all assets to look consistent / cohesive. This skill orchestrates the
  higgsfield-* skills (generate, product-photoshoot) for asset generation. NOT
  for a one-off single image/video with no funnel (use higgsfield-generate
  directly) or marketplace listing cards (use higgsfield-marketplace-cards).
argument-hint: "[image-path] [optional brand/product idea]"
allowed-tools: Bash, Read, Write, Edit, Glob, Grep
---

# Image → Campaign

Build a full English marketing funnel from one image. The whole point: **one
image in, a coherent funnel out** — Instagram Reels that hook attention, a blog
that builds trust and ranks, and a landing page that converts. Every asset
shares one visual and verbal identity, because they are all derived from a
single **Brand Brief** that you write and the user approves before any credits
are spent.

## Core principle: brief-first, single source of truth

Do NOT generate assets first and try to match them later. That always drifts.
Instead:

1. Write **one Brand Brief** from the image + a short interview. The brief fixes
   product identity, thesis line, palette (OKLCH tokens), typography, tone,
   scene, CTA, and the chosen Reel angles/style. It also contains every asset
   prompt, written out.
2. The user approves the brief at **one checkpoint**.
3. Every output — landing page, Reels, blog — reads its thesis, palette, fonts,
   tone, and prompts **from the brief**. Nothing re-derives identity on its own.

This is why the landing page, Reels, and blog end up looking like one campaign
instead of three unrelated AI artifacts.

## Locked defaults for this skill

- **Language: English.** All visible copy (site, captions, blog) is English.
  If the user writes in another language or asks for one, talk to them in their
  language and ask once which language the campaign copy should use.
- **Conversion goal: demo/concept.** There is no real shop yet, so every CTA is
  a clean placeholder (e.g. "Discover now"). Do not invent fake prices,
  checkout links, or reviews.
- **One approval checkpoint**, right after the brief. After approval, run
  autonomously to the end.
- **Landing page stays local** (a preview server). Deployment (Vercel) is a
  later step, only if the user asks.

## Step 0 — Bootstrap

Asset generation runs through the Higgsfield CLI (same engine as the
`higgsfield-generate` and `higgsfield-product-photoshoot` skills).

1. If `higgsfield` is not on `$PATH`, install it:
   `curl -fsSL https://raw.githubusercontent.com/higgsfield-ai/cli/main/install.sh | sh`
2. Run `higgsfield account status`. If it fails with `Session expired` /
   `Not authenticated`, ask the user to run `higgsfield auth login` and wait.
   If they don't have a Higgsfield account yet, point them to
   https://higgsfield.ai/s/mcp-arnold-oberleiter-ecZvus to sign up (an account
   with credits is required to generate any asset).

Confirm you actually have the input image (a local path). If the user only
described a product with no image, say so — this skill is built around a real
image. You can still proceed text-only, but fidelity drops; tell them that.

## Step 1 — Interview (max 2 questions)

Look at the image first and infer everything you can (what the product is, who
it is for, the mood). Ask only what you genuinely cannot tell. Keep it to the
two questions from the landing-page spec:

1. *What is the product/brand in one sentence, who is it for, and what feeling
   should it create?*
2. *Should I generate all image and video assets with Higgsfield, or are there
   existing assets/logo/colors I should use?*

Skip a question if the answer is already obvious from the image or the user's
message. Do not ask about price or sales destination — the CTA is a demo
placeholder by default.

## Step 2 — Write the Brand Brief

Follow `references/brand-brief.md`. Produce `brief.md` containing the identity
fields AND every asset prompt (5 site assets, 3 Reel prompts, 1 blog image).
Writing the prompts now — before spending anything — is what makes the
checkpoint meaningful.

## 🛑 CHECKPOINT — get approval before generating

Show the user, compactly:

- the thesis line, scene sentence, the 4 palette tokens, fonts, tone words, CTA
- the chosen scroll concept (one line of why)
- the 3 Reel angles + the chosen Reel style (cinematic vs UGC) and why
- the full list of asset prompts you are about to run

Then ask one thing: *"Does the brief work for you, or should I change anything
before I generate?"* Generation costs credits, so do not skip this. Apply edits,
then proceed. After this point, run autonomously.

## Step 3 — Build (after approval)

Build in this order — it is deliberate. The landing page is built first because
it locks the design system and produces the hero video, which the Reels reuse.

1. **Landing page** → `references/landing-page.md`. Generates the 5 site assets,
   assembles `website/index.html`, verifies in the browser.
2. **Reels** → `references/reels.md`. Three 9:16 Reels. Reuse/reframe the site's
   hero or middle video for the cinematic showcase angle to save credits;
   generate the other two. Write `reels/captions.md`.
3. **Blog** → `references/blog.md`. An English SEO article in `blog/blog.html`
   that reuses the same palette tokens and fonts, with one image (reuse a site
   still where possible) and a CTA back to the landing page.

## Step 4 — QA

- Landing page: run the full browser checklist in `references/landing-page.md`.
- Reels (optional but recommended): score each with the Virality Predictor
  (`higgsfield generate create brain_activity --video <reel> --wait`) and
  regenerate the weakest if a clearly better angle is obvious. Report the
  scores; do not silently sit on them.
- Confirm every asset that carries copy is in the campaign language, and that
  the palette and fonts are identical across site, Reels thumbnails, and blog.

## Step 5 — Deliver

Assemble the campaign folder (structure below) and write `README.md` from
`assets/campaign-readme-template.md`: what's inside, how to preview the site
locally, the 3 captions ready to paste, and the obvious next step (deploy +
swap the placeholder CTA for a real one).

Final message to the user (concise, in their language): the local site URL, the
thesis line, the 3 Reel angles with their files, where the captions and blog
are, and any limitation you hit (e.g. an asset you had to regenerate).

## Campaign folder structure

```
campaign-<slug>/
  brief.md                  # the approved single source of truth
  website/
    index.html
    assets/                 # hero.mp4, middle.mp4, g1.jpg, g2.jpg, g3.jpg
  reels/
    reel-1-hook.mp4
    reel-2-showcase.mp4
    reel-3-lifestyle.mp4
    captions.md             # per reel: hook text, caption, hashtags, CTA
  blog/
    blog.html
    assets/                 # blog image(s)
  README.md
```

## Consistency laws (apply to every generated asset)

Across the whole campaign, hold these constant — this is what makes it feel like
one brand and not a generated grab-bag:

- same product identity and shape
- same material language
- same lighting direction
- same color world (the brief's palette)
- same premium tone

Reject and regenerate any asset where the product identity changes, the shape
drifts, the material looks wrong, text gets baked into the image/video (AI text
rendering is unreliable — keep generated media clean and add real text in the
caption/editor), or it simply looks "AI-made". Consistency beats spectacle.

## Reference index

- `references/brand-brief.md` — how to derive the brief + the brief template and
  the full asset-prompt list (read this first, in Step 2)
- `references/landing-page.md` — the brief-aware, self-contained landing-page
  build with the browser QA checklist
- `references/reels.md` — the 3 Reel angles, cinematic-vs-UGC selection,
  generation commands, reframe reuse, and the captions format
- `references/blog.md` — the English SEO article spec and HTML templating
- `assets/brief-template.md`, `assets/blog-template.html`,
  `assets/campaign-readme-template.md` — fill-in templates
