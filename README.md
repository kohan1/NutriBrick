# NutriBrick

Landing page for NutriBrick — a Duplo-brick-sized food bite for kids. A Future
Anything student venture; the product is still a concept.

## Live site

https://kohan1.github.io/NutriBrick/

## How this is served

GitHub Pages, deployed straight from the `claude/nutribrick-github-pages-7nioc7`
branch at the repository root. There is no build step.

- `index.html` — the whole site. It is a self-extracting bundle: the page's
  markup, its React runtime and its webfonts all ship inside this one file as a
  manifest of base64 blobs, unpacked into the document on load.
- `.nojekyll` — turns off Jekyll processing so nothing is rewritten on the way
  out.

The only thing fetched over the network at runtime is `three.js` (used for the
rotating 3D brick in the hero), tried against esm.sh, jsDelivr and unpkg in
order. If all three are unreachable the hero falls back to a flat CSS brick and
the rest of the page is unaffected.

## Editing

`index.html` is generated output, not hand-authored source — the readable markup
lives JSON-encoded inside the `__bundler/template` script tag near the end of the
file. Regenerate and replace the whole file rather than editing it in place.
