# Accessible LaTeX Handout Template

[![Build PDFs](https://github.com/YOUR-USERNAME/YOUR-REPO/actions/workflows/build-pdf.yml/badge.svg)](https://github.com/YOUR-USERNAME/YOUR-REPO/actions/workflows/build-pdf.yml)

A LaTeX template for math course handouts that produces accessible PDFs. The output is a tagged PDF/UA-2 document with math encoded as MathML, so screen readers and other assistive technologies can read headings, lists, tables, figures, and equations correctly.

**[Download the latest sample PDF](https://github.com/YOUR-USERNAME/YOUR-REPO/releases/latest/download/accessible-handout-template.pdf)** · **[See all releases](https://github.com/YOUR-USERNAME/YOUR-REPO/releases)**

## What the template provides

- PDF/UA-2 tagging, with the document language and title set in the PDF metadata
- Equations tagged as MathML, both inline and displayed
- Placeholder sections and subsections, a definition, a theorem with proof, an example, and an exercises list
- A table with its header row tagged for screen readers
- A figure with alt text
- 12pt text, one-inch margins, and high-contrast link colors
- Comments marked `[A11Y]` on every line that matters for accessibility, explaining why it's there

## Requirements

- **LuaLaTeX.** The MathML tagging only works with LuaLaTeX; pdfLaTeX and XeLaTeX won't produce it.
- **TeX Live 2025 or newer.** Older distributions don't include the tagging features the template relies on.

## Getting started

### In Overleaf

1. Download the source code zip from the [latest release](https://github.com/YOUR-USERNAME/YOUR-REPO/releases/latest).
2. In Overleaf, choose **New Project → Upload Project** and select the zip.
3. Open **Menu** in the project and set **Compiler** to **LuaLaTeX** and **TeX Live version** to 2025 or newer.
4. Recompile.

### On your own computer

Download or clone this repository, then compile with:

```bash
latexmk -lualatex accessible-handout-template.tex
```

## Customizing the template

1. **Fill in the handout details.** Near the top of the file, the `EDIT THESE` block sets the title, author, course, and date. These values are used for both the visible title and the PDF metadata, so they always match.
2. **Set the language.** If the handout isn't in US English, change `lang` in the `\DocumentMetadata` block (for example, `en-GB`, `es`, or `fr`).
3. **Replace the placeholder content** with your own sections, text, equations, tables, and figures.
4. **Keep the `[A11Y]` lines.** Each one is explained by a comment in the file.

### Accessibility checklist

When adding your own content:

- Use `\section` and `\subsection` for headings instead of bold text or manual formatting, so the document has a navigable structure.
- Put all math in math mode, including single variables in running text and table headers: write `\(a\)`, not `a`.
- State the problem and define notation before using it. A screen-reader user can't glance around the page for context.
- Give every image alt text with `\includegraphics[alt={...}]{file}`. Describe what the reader should take away from the image, not just what it is.
- Introduce every table and figure in the text, and give each a caption that says what it shows.
- Keep tables simple: one header row, no merged cells, and narrow enough to fit the page. If a table has more than one header row, update `table/header-rows`.
- Refer to equations, tables, and figures with `\eqref` and `\ref`, so readers get working links.

## Checking accessibility

A PDF that compiles is not necessarily accessible. Before sharing a handout:

1. **Confirm the PDF is tagged.** In Acrobat Reader, open **File → Properties** and check that **Tagged PDF** says Yes.
2. **Validate it.** Run the PDF through [veraPDF](https://verapdf.org/) using the PDF/UA-2 profile. For files in this repository, this happens automatically on every commit (see [Automated builds](#automated-builds)); if you're working on your own copy elsewhere, run veraPDF yourself.
3. **Listen to it.** If you can, read it with a screen reader. Support for MathML in PDFs varies between PDF viewers and screen readers, so a file that passes validation can still read poorly in some combinations.

## Automated builds

A GitHub Actions workflow (`.github/workflows/build-pdf.yml`) compiles every top-level `.tex` file that contains `\documentclass`, then checks each PDF against PDF/UA-2 with [veraPDF](https://verapdf.org/):

- **On every commit to any branch,** it builds and validates the PDFs. Open the run in the **Actions** tab and look under **Artifacts** for the PDFs (`handout-pdfs`) and the validation reports (`verapdf-reports`).
- **When a release is published,** it does the same, then attaches the PDFs to the release. PDFs are attached only if every document built and passed veraPDF, so a non-conforming handout can't ship in a release.

If a build fails, the workflow uploads the LaTeX log (`latex-log`) so the error can be found.

### Reading the veraPDF reports

The `verapdf-reports` artifact contains two reports for each PDF. Open the `.html` report in a browser: it lists each rule that failed, with a description. The `.xml` report is the machine-readable version the workflow uses to decide pass or fail.

A failed check doesn't always mean a problem with your content. LaTeX's tagging support for some packages is still maturing, so a few failures may come from the tagging code itself. If you're unsure, [open an issue](https://github.com/YOUR-USERNAME/YOUR-REPO/issues) and include the HTML report.

## Versioning

This project uses [semantic versioning](https://semver.org/), with tags like `v1.2.0`:

- The **last number** changes for fixes and small tweaks.
- The **middle number** changes for additions that don't break existing handouts.
- The **first number** changes when an update could break handouts built on an earlier version.

The version and date also appear in the header comment of the template, and each release is described in [CHANGELOG.md](CHANGELOG.md).

## Repository contents

| File | Purpose |
| --- | --- |
| `accessible-handout-template.tex` | The handout template |
| `.github/workflows/build-pdf.yml` | Builds the PDFs and attaches them to releases |
| `CHANGELOG.md` | What changed in each version |
| `README.md` | This file |

## Feedback and contributions

Questions, problems, and suggestions are welcome. Please [open an issue](https://github.com/YOUR-USERNAME/YOUR-REPO/issues) describing what you found, including the template version and, for build problems, the error from the LaTeX log.

## Authors

Caroline Larsen and Andrew Ruether

## License

Add your chosen license here, for example [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/) or [MIT](https://opensource.org/license/mit). Also add a matching `LICENSE` file to the repository, so others know how they may use and adapt the template.
