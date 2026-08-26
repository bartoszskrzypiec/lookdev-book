# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project overview

"Lookdev dla Artystów Technicznych" — a Polish-language static HTML book teaching look development
for production renderers (Arnold, RenderMan) to technical artists. It goes deep on the mathematical
foundations of color grading (gamma, grade, offset, ASC CDL, saturation matrices, ...) and treats
that as one of several equally-weighted pillars alongside practical material authoring (dielectrics,
metals, SSS, hair, cloth, layered materials) and lookdev lighting/review (HDRI rigs, turntables,
calibrated viewing environments). 24 numbered main chapters (rozdziały) build linearly on each
other; 23 lettered appendices (dodatki A–W) go deeper into specific topics (full derivations,
renderer-specific parameter references); one computational companion (pomocnik) walks through
grading math by hand. Live at https://bartoszskrzypiec.github.io/lookdev-book/ (once the GitHub
repo + Pages are set up — not yet done as of the initial commit).

This is a living project, not a one-shot publication — chapters and appendices get revisited,
deepened, and rewritten over time, exactly like its two sibling books. Don't build rigid generated
structures (e.g. auto-generated index files) that would need manual rebuilding on every content
change. The initial commit's full scaffold (index.html + every rozdział/dodatek as a stub) *was*
produced by a one-off Python script — that script is not part of this repo (it lived in a scratch
directory) and must not be recreated as a standing build step.

## Sibling projects — read before writing color/lookdev content

This book is the third in a trilogy and is deliberately **not self-contained on topics the
siblings already cover in depth**:

- [raytracing-book](https://bartoszskrzypiec.github.io/raytracing-book/) — ray tracing math.
  Dodatek E (gamma/tone mapping, shallow — this book is the deeper treatment), Dodatki L–O (full
  ACES series: interchange problem, AP0/AP1, RRT/ODT, 1.0 vs 2.0), Dodatki AG–AI ("Lookdev w
  praktyce": SSS, displacement/subdivision, MaterialX/OSL), Dodatki AJ–AL (LPE/AOV, cryptomatte,
  light linking), Dodatek A (PBR/BRDF variants), Dodatek H (dispersion), Dodatek AB (measured
  BRDF), Dodatek AC (layered materials), Dodatek AA (triplanar), Dodatek AM (spectral rendering).
- [pipeline-book](https://bartoszskrzypiec.github.io/pipeline-book/) — production pipeline.
  Rozdział 12 + Dodatek D (OCIO/ACES config architecture — the engineering side, not artist-facing
  grading).

**Rule**: this book stands on its own to read, but wherever a topic already has a deeper derivation
in a sibling book, link to it instead of repeating it — and vice versa. Cross-book links must be
**absolute URLs** (`https://bartoszskrzypiec.github.io/raytracing-book/...`), never relative paths,
since these are separate repos/sites. Don't add backlinks *from* raytracing-book/pipeline-book
*into* this book until the target page here has real content — a backlink to a stub is worse than
no backlink.

## No build system

Pure static HTML/CSS with inline SVG diagrams — no npm, no package.json, no bundler, no test
suite, no linter. To "run" the site, open any `.html` file directly in a browser, or serve the
repo root with any static file server. Deploy via GitHub Pages (Settings → Pages → Deploy from
branch → `main` / `/(root)`) once the GitHub repo exists.

## Structure

```
index.html                                — table of contents (spis treści), root only
rozdzialy/rozdzial-NN-slug.html           — 24 main chapters, NN zero-padded 01–24
dodatki/dodatek-x-slug.html               — 23 lettered appendices, x = a–w, in six thematic
                                            blocks (see index.html part-labels): matematyka koloru
                                            w głębi (A–F), ACES i zarządzanie kolorem (G–J), Arnold
                                            i RenderMan w głębi (K–N), materiały w głębi (O–Q),
                                            detal i geometria (R–T), warsztat i review (U–W)
matematyka/podstawy-matematyczne.html     — "Zanim zaczniesz" primer: powers/exponents (gamma),
                                            logarithms (log encodings), 3×3 matrices and RGB
                                            vectors (color space conversion), linear interpolation
                                            (LUTs). The one content page outside
                                            rozdzialy/dodatki/pomocnik — any repo-wide script must
                                            glob it explicitly.
pomocnik/pomocnik-obliczeniowy-tom-1.html — computational companion: sRGB→linear by hand, build the
                                            sRGB→ACEScg matrix step by step, implement ASC CDL and
                                            compare against a Grade node. Covers R.3–10.
assets/style.css                          — single shared stylesheet (dark theme), copied from
                                            raytracing-book and evolving independently from here
assets/interactive.js                     — formula modals + `.vec[data-tip]` tooltips, copied
                                            as-is; not yet used by any page in this book
```

Every page links `assets/style.css` plus keeps its own Google Fonts `<link>` inline, exactly like
raytracing-book and pipeline-book.

## Visual system — reused, revocabularied

Same CSS mechanics as both sibling books (`.viewport-readout`, `.panel`, `.eyebrow`,
`.diagram-frame`, `.site-nav`, `.formula`, colors `--amber/--cyan/--violet/--raster`). No KaTeX/
MathJax — formulas are plain unicode in `.formula` blocks (e.g. `V_sRGB ≈ V_linear^(1/2,2)`), matrix
algebra included; this was a deliberate choice to stay visually consistent with the trilogy over
introducing real math typesetting. Only the *vocabulary* inside components changes to fit lookdev:

- `.viewport-readout` (top HUD bar) → lookdev/color context, e.g. `SPACE · linear vs sRGB`,
  `DECODE · ^(1/2.2)`, or for a rozdział: `ROZDZIAŁ · NN/24` `CZĘŚĆ · <roman>` `STATUS · ...`; for a
  dodatek: `DODATEK · <letter>` `EXT OF · R.N` `STATUS · ...`.
- `.eyebrow` "Rozdział N / X" → X is a short (1–3 word) part tag, not the full part label (see
  PARTS in the generator script's logic, still readable from any already-written chapter's
  `.eyebrow`).
- `.diagram-hud` → names that read like a color pipeline's own instrumentation:
  "Linear.vs.gamma", "Tone.mapping.curves", "GGX.lobe" — pattern from raytracing-book's Dodatek E.
- Inline SVG diagrams: transfer function curves, chromaticity diagrams, BRDF lobes, shader graphs,
  turntable/HDRI diagrams — instead of ray-bounce diagrams.
- Color tokens (`--amber/--cyan/--violet/--raster`) stay as accents.
- `.table-frame` / `.data-table` is a genuinely new component, not inherited from either sibling
  book (neither has a styled `<table>`) — added while writing Rozdział 4 because this book needs
  real comparison tables (color space primaries, Arnold↔RenderMan parameters) more than either
  sibling did. Styled to match the existing dark theme (`var(--border)`, `var(--mono)` headers).
  Reuse it rather than inventing another table style or falling back to unstyled `<table>`.

## Content authoring rules

- **Never rename/reletter dodatki (A–W) without asking**, even if the ordering looks imperfect.
  Renumbering breaks prose cross-references ("Dodatek H", "Rozdział 6", …) scattered by name across
  *other* files — a much bigger, riskier change than it first appears.
- **Every dodatek's `.viewport-readout`** carries an `EXT OF` token naming which rozdział it
  extends — this is the source of truth for cross-linking, don't infer relationships from titles
  alone.
- **Formulas must define their symbols.** When a `.formula` introduces a variable, explain what it
  means — either inline via `<strong>` in the surrounding prose or in the formula's `.sub` span.
  Same rule for renderer-specific parameter names (`aiStandardSurface.base`, `PxrSurface.diffuseGain`,
  …) the first time they appear on a page.
- **File names and in-text numbering are decoupled.** Renaming a file must never change prose
  references like "Rozdział 6" or "Dodatek H" inside content — those describe the book's structure,
  not the file on disk.
- **Stub → real chapter**: when writing a stub's real content, replace the `.panel.practice`
  "status" block entirely (don't leave "W przygotowaniu" language anywhere), keep the existing
  `.site-nav` as-is unless the structure itself changes, and keep the hook sentence in `index.html`
  and the chapter's own `.subtitle` in sync if it's reworded.
- **Arnold and RenderMan in parallel**: per-topic content (Część V–VI especially) should show both
  renderers' actual node/parameter names side by side (tables are fine), not just one with the
  other as a footnote — this was an explicit scope decision, not a default to drift away from.

## Navigation system

Multiple hand-authored layers, no generation script — each is added deliberately per page, not
mechanically to every page:

- **`.site-nav`**: rozdziały get `Spis treści` + `← Poprzedni` / `Następny →` in chapter order
  (first/last chapter omit the missing side); dodatki and the primer/pomocnik get `← Spis treści`
  only, plus (once a dodatek has real content) an `↑` link up to the rozdział named in its `EXT OF`.
- **`.deeper`** block: an "Idź głębiej" list of dodatki that extend *this* page, built from the
  reverse of the `EXT OF` mapping — add only once a page has real prose with a natural anchor point
  (not yet present anywhere; all pages are still stubs as of the initial commit).
- **`.inline-deeper`** chips: small pill-style links after the specific paragraph that introduces a
  topic covered more deeply elsewhere — same rule, add only where content already exists.

## Git workflow

Commit and push right after making a change in this repo, without asking for confirmation each
time, once a GitHub remote exists — same established preference as the two sibling repos. Still use
judgment for anything unusually large or risky, and never force-push or rewrite history without
asking. Commit messages in this repo avoid Polish diacritics (ASCII-safe) to sidestep Windows
console/heredoc encoding issues — page *content* always uses full, correct Polish diacritics
regardless. The GitHub repo (`bartoszskrzypiec/lookdev-book`) and Pages deployment do not exist yet
as of the initial commit — creating them and pushing is a separate, explicitly-confirmed step, not
something to do automatically just because a local commit exists.
