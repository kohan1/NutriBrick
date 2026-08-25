# NutriBrick

Landing page for NutriBrick — a Duplo-brick-sized food bite for kids. A Future
Anything student venture; the product is still a concept.

## Live site

https://kohan1.github.io/NutriBrick/

## How this is served

GitHub Pages, via the workflow in `.github/workflows/pages.yml`. It publishes
`index.html` on every push to `claude/nutribrick-github-pages-7nioc7`. There is
no build step — the workflow just stages the file and uploads it.

- `index.html` — the whole site. It is a self-extracting bundle: the page's
  markup, its React runtime, three.js and its webfonts all ship inside this one
  file as a manifest of base64 blobs, unpacked into the document on load.
- `og.png` — the 1200x630 social card referenced by the Open Graph tags.
- `.nojekyll` — turns off Jekyll processing so nothing is rewritten on the way
  out.

The page makes **no external requests at all**. `three.js` (which renders the
rotating 3D bricks) used to load from a CDN at runtime, so on any network that
blocked esm.sh, jsDelivr and unpkg the hero fell back to a flat CSS brick —
directly beside the words "studs that actually interlock". It is now bundled in:
`three.module.js` and `RoundedBoxGeometry.js` are concatenated into one ES module,
gzipped into the manifest, and imported from a blob URL. Verified by loading the
page with every external host blocked; all three canvases still render.

`og.png` is the link-preview card, built from the page's own 3D brick render.

## Editing

`index.html` is generated output, not hand-authored source — the readable markup
lives JSON-encoded inside the `__bundler/template` script tag near the end of the
file. Do not edit it in place; regenerate it and replace the whole file.

The source it was generated from is kept in `src/` for reference:

- `NutriBrick.dc.html` — the design-canvas document
- `NutriBrick-standalone-src.html` — the same page as readable standalone markup
- `_ds/organic-…/` — the "Organic" design system (tokens, component CSS); see
  its `readme.md`
- `support.js` — canvas runtime the standalone source loads

Nothing in `src/` is served; only `index.html` is published.
