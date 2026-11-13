# Co-brand Header Alignment

Use this reference whenever a card set carries a supplied logo, partner credit, creator byline, sponsor lockup, or another repeated header identity.

## Align Visible Artwork, Not The Image Canvas

Logo files often contain white or transparent padding. CSS aligns the full image rectangle, so an apparently correct `align-items: center` can still make the adjacent text look too high or too low.

Before layout:

1. Keep the original asset unchanged in `assets/`.
2. Inspect the visible-pixel or alpha bounding box.
3. If the canvas has accidental padding, create a tightly cropped derivative with only 0-2 px safe margin.
4. If the logo arrives on white, remove the background only when that matches the user's intent; preserve anti-aliased edges and keep the original file.
5. Size the cropped derivative by its visible artwork, not by the dimensions of the source canvas.

Do not compensate for padded assets with arbitrary `translateY`, negative margins, or page-specific nudges. Normalize the asset once, then reuse it on every page.

## Build One Lockup

Treat the logo and partner text as one component:

```css
.brand-lockup {
  display: inline-flex;
  align-items: center;
  gap: 24px;
  min-width: 0;
}
.brand-logo {
  display: block;
  width: auto;
  height: 56px;
}
.co-brand {
  font-family: var(--sans-zh);
  font-size: 26px;
  line-height: 1;
  font-weight: 700;
  white-space: nowrap;
}
```

- Match partner text to the wordmark's neutral colour, sans-serif character, and visual weight unless the brief explicitly defines another co-brand system.
- The `×`, slash, or divider belongs to the lockup and should share the same baseline and colour logic.
- Do not use the page accent colour for partner text merely to make it noticeable. Accent colour changes hierarchy and can make the lockup look pasted on.
- Set the gap from the visible end of the wordmark. Raw source padding must not influence the perceived spacing.

## Optical Alignment

Geometric centering is the starting point, not the final check.

- Compare the visual centre of the wordmark text with the centre of the partner text; do not align against the top of a taller icon.
- Compare cap height / Chinese character box, baseline, and stroke weight at 100% size.
- A 1-3 px optical correction is acceptable only after the logo asset has been tightly cropped.
- Keep the lockup vertically centred within the header rule and leave balanced space above and below.
- If the partner line wraps, the lockup is too wide: reduce the logo size, shorten the credit with user approval, or change the header structure.

## Multi-page QA

Render one header crop at 100% and inspect it before rendering the full set. Then check the contact sheet to confirm that every page reuses the same lockup, header height, divider position, and footer system.

The header fails if:

- logo and partner text appear on different visual baselines;
- the partner text uses a different visual language from the wordmark without a brand reason;
- spacing changes between pages;
- the lockup is technically centred but visibly sags because of transparent padding;
- the right-side metadata competes with or crowds the lockup.
