# The Second Heavy-Ball Riddle — research notes

Open **[index.html](index.html)** for the offline blog, or **[heavyball-notes.pdf](heavyball-notes.pdf)** for the print edition. The full mathematical content is in English.

The document explains the exact separation witness, proves exclusion of all finite cycles, gives the full uniform global convergence proof, and discusses the stronger common two-point record obstruction. All three figures are original and reproducible. Arithmetic details are expandable in the HTML and fully visible in the PDF.

The September 10 revision uses white-background vector figures with mathematical typography, inspired by Figures 7 and 8 of the original riddle paper. It adds the HB vector decomposition, an early-trajectory inset, named lemmas, and expanded derivations for Fourier diagonalization, Bernstein coefficients, summation, causal continuation, and the energy-to-rate estimate.

## Files

- `notes.md`: editable mathematical source.
- `index.html`: self-contained HTML, including math fonts and figures; no network access required for reading.
- `heavyball-notes.pdf`: A4 edition with print typography, expanded details, page numbers, and bookmarks.
- `checks/`: exact arithmetic checkers; Python standard library only.
- `evidence/`: immutable copies of the underlying proofs, reviews, and target-specific verdicts.
- `assets/`: original SVG/PDF/PNG figures, numerical illustration data, and embedded body fonts.
- `scripts/`: figure generation, HTML build, browser checks, and PDF export.
- `validation/`: saved check outputs and layout inspection images.

The figures' floating-point computations illustrate the mathematics. The exact finite checks and analytical proofs have separate roles. No Lean kernel-checked formalization is claimed.

## Rebuild

Verify the finite mathematics:

```bash
python -B checks/verify_submission.py
```

Generate figures with NumPy and Matplotlib installed:

```bash
python scripts/make_figures.py
```

Build the HTML with Node.js:

```bash
npm install
npm run build
```

In the original workspace the builder can also use the existing KaTeX and markdown-it installation under `/root/SGD/OptBound`. Outside that workspace, install this directory's dependencies with the command above. Body fonts are bundled; their license is in `assets/fonts/LICENSE.txt`.

Export and verify the PDF with Playwright and Poppler utilities installed:

```bash
python -m playwright install chromium
python scripts/export_and_check.py
```

Refresh the archive and its SHA-256 manifest after a successful export (Pillow required):

```bash
python scripts/package_edition.py
```

The HTML and PDF derive from the same Markdown source. The exporter checks desktop/mobile document overflow, math rendering, offline resources, links, detail expansion, and expected PDF content. Source and evidence links in the PDF are rendered as text; the companion files are available in the full bundle. Public literature links remain clickable.

## Scope and provenance

The source snapshot is the Heavy-Ball campaign of September 9, 2026. Theorem A and Theorem B correspond to distinct proved targets; the stronger record obstruction has its own review. Historical source files are preserved verbatim, including pre-verification wording superseded by later decisions. See `evidence/verdicts.json` and `evidence/snapshot.json`.

These notes make no claim of exhaustive parameter classification, a sharp convergence rate, completed formalization, or established publication priority. No author affiliation or external endorsement is implied.
