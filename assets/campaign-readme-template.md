# Campaign — <product/brand>

Generated entirely from one image. Everything shares one identity (see `brief.md`).

## Thesis line
<thesis line>

## Contents

| Asset | Path | Role in the funnel |
|---|---|---|
| Landing page | `website/index.html` | Conversion (demo CTA) |
| Reel 1 – Hook | `reels/reel-1-hook.mp4` | Attention |
| Reel 2 – Showcase | `reels/reel-2-showcase.mp4` | Desire |
| Reel 3 – Lifestyle | `reels/reel-3-lifestyle.mp4` | Context/trust |
| Captions | `reels/captions.md` | Post text + hashtags + CTA |
| Blog article | `blog/blog.html` | SEO / mid-funnel |

## Preview the landing page locally

```bash
cd website
python -m http.server 8000
# then open http://localhost:8000
```

## How to use the campaign

1. Post the Reels on Instagram. Add the hook text from `captions.md` as
   on-screen text in the IG editor, then paste the caption + hashtags.
2. Link in bio → landing page.
3. Publish the blog (e.g. on the later live domain); its CTA points to the
   landing page.

## Next steps (when the demo becomes real)

- Deploy the landing page (Vercel) and put the real URL into the Reels bio and
  the blog CTA.
- Replace the placeholder CTA with the real destination (shop, waitlist, form).
- Score the Reels with the Virality Predictor and regenerate the weakest one.

## Known limitations
<what was not fully solved>
