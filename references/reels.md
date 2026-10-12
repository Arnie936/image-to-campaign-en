# Instagram Reels (3 × 9:16)

Three vertical Reels, one per angle locked in the brief. They are the top of the
funnel: their job is to stop the scroll and send people to the landing page. All
copy is English. Output to `campaign-<slug>/reels/`.

Format for all three: aspect ratio `9:16`, ~15s (8–15s is fine), 720p. Keep the
generated video clean — **no baked-in text.** On-screen hook text is added later
in the IG editor from the wording you provide in `captions.md` (AI text
rendering is unreliable and would break the premium feel).

## The 3 angles

| File | Angle | Intent |
|---|---|---|
| `reel-1-hook.mp4` | Hook / problem→solution | Open on tension or a scroll-stopper, resolve into the product |
| `reel-2-showcase.mp4` | Product showcase (cinematic) | Product as hero, clean motion — **reuse the site hero/middle video** |
| `reel-3-lifestyle.mp4` | Atmosphere / lifestyle | Product in its world, mood over message |

## Style path (from the brief's Reel decision)

### Cinematic product (no person) — default

Generate with Seedance, seeding from the product image or a site still so
identity holds:

```bash
higgsfield generate create seedance_2_0 \
  --prompt "<angle prompt from brief, same product identity + palette>" \
  --start-image <product-or-still> \
  --duration 12 --aspect_ratio 9:16 --resolution 720p --wait
```

If `seedance_2_0` does not expose `9:16` directly, generate at its native ratio
then reframe (see below).

### UGC presenter — when the brief picked it

Use Marketing Studio. Import the product once, then generate per angle:

```bash
# import product from the image (once)
higgsfield upload create <product.jpg>            # -> upload id
higgsfield marketing-studio products create --title "<name>" --image <upload_id>

# generate a UGC reel (per angle)
PRODUCT_IDS_JSON=$(mktemp); printf '["<product_id>"]' > "$PRODUCT_IDS_JSON"
higgsfield generate create marketing_studio_video \
  --prompt "<angle prompt from brief>" \
  --product_ids @"$PRODUCT_IDS_JSON" \
  --mode ugc --duration 15 --aspect_ratio 9:16 --resolution 720p \
  --generate-audio true --wait
```

For a consistent presenter across all three Reels, train a Soul Character once
via the `higgsfield-soul-id` skill and reuse it, or pass the same Marketing
Studio avatar. Note which you used in `captions.md`.

## Reuse the site video for the showcase (save credits)

The showcase angle should reuse the landing page's `hero.mp4` (or `middle.mp4`)
reframed to vertical instead of a fresh generation:

```bash
higgsfield generate workflow reframe \
  --video website/assets/hero.mp4 \
  --aspect-ratio 9:16 --resolution 720p --wait
```

Use the reframed result as `reel-2-showcase.mp4`. Only generate a fresh showcase
clip if the reframe crops out the product or looks weak.

## Optional polish

- A music bed can lift a cinematic Reel: `higgsfield generate create sonilo_music
  --prompt "<mood from brief>" --duration 15 --wait`, then note it for the editor
  (we deliver clean video + separate audio rather than hard-muxing).
- Quality gate: score finished Reels with the Virality Predictor
  (`higgsfield generate create brain_activity --video reels/reel-1-hook.mp4
  --wait`) and regenerate the weakest if a better angle is obvious.

## captions.md format

Write one block per Reel. The caption, hashtags, and CTA all use the brief's
tone and the same CTA wording as the landing page — this is the verbal thread
that ties the funnel together.

```markdown
## Reel 1 — Hook / problem→solution  (reel-1-hook.mp4)
**On-screen hook (add as text in the editor):** <3–6 words>
**Caption:** <1–3 sentences, brand tone>
**Hashtags:** #… #… #…  (5–10, mixed: broad + niche)
**CTA:** <brief CTA text> → link in bio
```

Repeat for Reel 2 and Reel 3.
