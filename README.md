# HVTI ggplot graphics recipes

[![Publish](https://github.com/ehrlinger/hvti_graphics/actions/workflows/publish.yml/badge.svg)](https://github.com/ehrlinger/hvti_graphics/actions/workflows/publish.yml)
[![Site](https://img.shields.io/badge/read-ehrlinger.github.io%2Fhvti__graphics-1f6feb)](https://ehrlinger.github.io/hvti_graphics/)
[![Version](https://img.shields.io/badge/edition-1.0.0-blue)](https://github.com/ehrlinger/hvti_graphics/releases)
[![License: CC BY 4.0](https://img.shields.io/badge/license-CC%20BY%204.0-lightgrey)](https://creativecommons.org/licenses/by/4.0/)

A working catalog of the figures we draw for CORR manuscripts and
presentations — Kaplan-Meier curves, propensity-balance plots, spaghetti plots,
CONSORT diagrams, random-forest visualizations — each paired with the code that
produces it. The aim is the one we hold for all of this team's tooling: start
from a working recipe, not a blank script.

**Read it here:** <https://ehrlinger.github.io/hvti_graphics/>

This is the **1.0.0** edition: the full figure catalog, the random-forest and
varPro recipes, and every chapter on the current `hvti*` package APIs.

## Who it's for

The HVTI/CORR biostatistics team and anyone building publication figures on our
stack. It assumes you know R, `ggplot2`, and the clinical questions; it does not
assume you remember which constructor draws a stratified hazard plot or how to
overlay a population life table.

## Two ideas run through the book

- **A figure is built in two steps.** A constructor (`hv_survival()`,
  `gg_varpro()`, …) prepares and validates the data, then `plot()` hands you a
  bare ggplot you finish with the usual `+`. The recipes lean on this so styling
  stays in your hands.
- **Every example stands on its own.** Each chunk generates its own sample data,
  so you can copy it, run it, and see the figure before you point it at your own
  analysis.

## The packages underneath

The recipes are built on the `hvti*` packages we maintain — chiefly
[hvtiPlotR](https://github.com/ehrlinger/hvtiPlotR) (themes and plot
constructors) — together with
[ggRandomForests](https://github.com/ehrlinger/ggRandomForests) for forest and
varPro graphics and
[TemporalHazard](https://github.com/ehrlinger/temporal_hazard) for
additive-hazard models, with `ggplot2` underneath. Where a package gives you a
helper we use it; where it does not (a plain density or box plot), we fall back
to bare `ggplot2` and style it to match.

## Building it locally

The book is a [Quarto](https://quarto.org) book.

```bash
quarto render                          # full book (HTML + PDF)
quarto render --to html                # HTML only
quarto render survival.qmd --to html   # a single chapter
```

Rendering reuses Quarto's committed `_freeze/` cache, so a normal render does not
re-run R. When you change a chapter's code, re-render it locally and commit the
updated `_freeze/` so the change reaches the site.

## How the site is published

A push to `main` triggers [`.github/workflows/publish.yml`](.github/workflows/publish.yml),
which renders the HTML from the frozen results and deploys `_book/` to the
`gh-pages` branch. CI never runs R — the book depends on local-source packages it
cannot install — so the published figures are only as current as the committed
`_freeze/`. The PDF is built locally; CI does HTML only.

## License

The text and figures are released under
[Creative Commons Attribution 4.0 International](https://creativecommons.org/licenses/by/4.0/)
(CC BY 4.0); see [`LICENSE`](LICENSE). Copyright 2025, John Ehrlinger.
