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
- **Update, 2026-08-28: the first widget is live**, in
  `rozdzialy/rozdzial-14-dielektryki-i-metale.html` (Dielektryki i metale)
  rather than the appendix originally flagged below — that chapter's own
  "Metalness kontra Face/Edge Color" section had zero diagrams and was a
  near-direct port of `pxrsurface-guide`'s `guide.html`/`guide.js`
  split-sphere metalness widget (`#viz-metalness`), so it went first.
  `assets/viz.js`, `assets/i18n.js` (a hard dependency of `viz.js` even
  though this book has no language switch — it no-ops without a
  `[data-set-lang]` element) and `assets/widgets.css` were copied in from
  `learning-materials` unmodified. **Two CSS aliases were missing from
  `docs/INTEGRATION.md`'s worked example** and had to be added by hand to
  make `.viz`'s own background/radius render correctly:
  `--bg-elevated: var(--bg-panel)` and `--radius: 10px` — the doc's example
  only listed the 6 tokens `viz.js`'s *JS* `theme()` reads, not the extra 2
  that `widgets.css` itself needs. Fixed in `learning-materials` now (see
  its `CHANGELOG.md`), so a fresh copy of `docs/INTEGRATION.md` no longer
  has the gap.
- **Original pilot target, still open**:
  `dodatki/dodatek-o-anizotropia-i-multiscatter-ggx.html` — still a 38-line
  stub ("Status: W przygotowaniu"). Its declared subject (anisotropy,
  multiscatter GGX) is close to a direct physics match for
  `pxrsurface-guide`'s `aniso.html`/`aniso.js` (specular rotation vs.
  shading-tangent direction, draggable tangent-field diagram) — a plane
  primitive (not yet in `viz.js`) would show anisotropic grain direction
  more clearly than a sphere, but the sphere-only port is still a
  reasonable first pass.
- Secondary candidates once the pilot works end to end:
  `rozdzialy/rozdzial-19-tkaniny-i-wlosy.html` (fabrics/hair → a cone-angle
  fuzz widget) and `rozdzialy/rozdzial-13-aistandardsurface-pxrsurface.html` /
  `rozdzialy/rozdzial-23-aov-debugging-arnold-vs-renderman.html` (both
  already do Arnold/RenderMan side-by-side comparison).
- This book's `.topnav`/`.topnav__brand` classes already match the shared
  convention — the `.lang-switch` markup from the integration guide drops
  straight in, no renaming needed.
