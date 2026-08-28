# Shared graphics/i18n toolkit

The interactive-widget engine, bilingual EN/PL toggle, formula-tooltip
system, and SVG+slider diagram pattern discussed for this book now live in
a shared repo, not duplicated here:

**`C:\Users\barte\Documents\VSCODE\learning-materials`** — read
`docs/INTEGRATION.md` there before copying anything into this book's
`assets/`.

(An earlier version of this file, written before that shared repo existed,
described a one-off port from `renderman_guide`/`pxrsurface-guide` directly.
That content has been generalized and superseded by the shared repo above —
don't follow the old version if you find it in git history, follow
`learning-materials/docs/INTEGRATION.md` instead.)

## This book's own notes

- Currently Polish-only (`<html lang="pl">`), no i18n scaffolding at all —
  adopting the shared `i18n.js` means setting
  `data-i18n-storage="ldb-lang"` and `data-i18n-default="pl"` on `<html>`
  per the integration guide's contract (this book defaults to Polish, the
  opposite of `pxrsurface-guide`, which is exactly the case that shared
  file's config-driven design now handles cleanly).
- **Concrete pilot target**: `dodatki/dodatek-o-anizotropia-i-multiscatter-ggx.html`
  — currently a 38-line stub ("Status: W przygotowaniu"). Its declared
  subject (anisotropy, multiscatter GGX) is close to a direct physics match
  for two widgets already built and working in `pxrsurface-guide`:
  `spec.html`/`spec.js` (Beckmann vs GGX, live split-sphere + NDF plot) and
  `aniso.html`/`aniso.js` (specular rotation vs. shading-tangent direction,
  draggable tangent-field diagram). Port the widgets, rewrite the
  surrounding prose in this book's own voice — the source pages' prose is
  `pxrsurface-guide`'s own Arnold-vs-PxrSurface framing.
- Secondary candidates once the pilot works end to end:
  `rozdzialy/rozdzial-19-tkaniny-i-wlosy.html` (fabrics/hair → a cone-angle
  fuzz widget) and `rozdzialy/rozdzial-13-aistandardsurface-pxrsurface.html` /
  `rozdzialy/rozdzial-23-aov-debugging-arnold-vs-renderman.html` (both
  already do Arnold/RenderMan side-by-side comparison).
- This book's `.topnav`/`.topnav__brand` classes already match the shared
  convention — the `.lang-switch` markup from the integration guide drops
  straight in, no renaming needed.
