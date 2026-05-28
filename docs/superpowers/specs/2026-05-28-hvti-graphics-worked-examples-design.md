# HVTI graphics recipes — worked examples design

Date: 2026-05-28
Status: approved (pending spec review)

## Goal

Fill the stub chapters of the Quarto book *HVTI ggplot graphics recipes*
(`hvti_graphics`) with self-contained, rendered worked examples built on the
`hvtiPlotR` package (v2.3.1, installed). Every plot listed in the book outline
gets at least one worked example; gaps the package does not cover are filled
with base-ggplot recipes styled to match.

## Source material

`hvtiPlotR`'s vignettes already contain rendered worked examples for ~20
functions:

- `vignettes/plot-functions.qmd` — constructor → `plot()` examples for every
  `hv_*` family, using exported `sample_*()` data generators.
- `vignettes/plot-decorators.qmd` — themes, colour scales, labels/annotations,
  legend positioning, multi-panel patchwork, and saving (PDF/PPT).

These are the raw material. We adapt and condense them into the book's chapter
structure rather than inventing examples.

## The example pattern

Every plot example follows the package's two-step workflow, fully reproducible
via bundled generators so the book renders end-to-end:

```r
dat <- sample_*(...)               # bundled generator, reproducible
obj <- hv_*(dat, ...)              # constructor → S3 object of class hv_data
p   <- plot(obj, ...)              # bare ggplot: no scales/labels/theme
p + scale_*() + labs() + theme_hv_*()   # decorate with + operator
```

Each chapter begins with a shared, hidden setup chunk:

```r
#| include: false
knitr::opts_chunk$set(echo = TRUE, message = FALSE, warning = FALSE)
library(hvtiPlotR)
library(ggplot2)
```

Theme functions use the `theme_hv_*()` aliases (`theme_hv_manuscript`,
`theme_hv_poster`, `theme_hv_ppt`, `theme_hv_ppt_dark`,
`theme_hv_ppt_light`) — both `theme_hv_*` and `hv_theme_*` are exported.

Gap chapters (no hvtiPlotR helper) use base ggplot2 geoms styled with
`theme_hv_manuscript()` so they sit visually alongside the package plots.

## Chapter plan

Hybrid structure: keep the existing outline, add focused new chapters for
function families that do not fit a generic plot type. New files marked **new**.

### Figures part

| File | Functions / content |
|---|---|
| `scatter.qmd` | `hv_eda` — continuous scatter + LOESS |
| `survival.qmd` | `hv_survival` — KM curve, cumulative hazard, log-log, integrated life table |
| `hazard.qmd` **new** | `hazard_plot` family (survival/hazard/cumhaz/stratified/life overlay), `hv_nonparametric` curve, `hv_ordinal` |
| `nnt.qmd` **new** | `nnt_plot`, `survival_difference_plot` |
| `histograms.qmd` | `hv_mirror_hist` (binary + IPTW), `hv_stacked` (count + proportion) |
| `density.qmd` | base `geom_density` (gap) |
| `bar.qmd` | `hv_eda` count/percentage barplots, `hv_longitudinal` |
| `boxplots.qmd` | base `geom_boxplot` (gap) |
| `upset.qmd` | `hv_upset` (keeps existing Venn intro prose) |
| `spaghetti.qmd` | `hv_spaghetti`, `hv_trends` |
| `postagestamp.qmd` | base `facet_wrap` small multiples (gap) |
| `specialty.qmd` | part intro prose |
| `consort.qmd` **new** | `hv_consort` patient-flow (tracker workflow) |
| `sankey.qmd` **new** | `hv_alluvial`, `hv_sankey` cluster-stability |
| `balance.qmd` **new** | `hv_balance` covariate balance, `hv_followup` goodness-of-followup |
| `combination.qmd` | patchwork multi-panel composites |

### Tables part

| File | Content |
|---|---|
| `qt_tables.qmd` | Publication-quality `gt` tables — a summary/"table 1" style table built from `sample_*()` data, following the rich-iannone gt-effective-display-tables guidance already linked in the stub. |
| `figure_tables.qmd` | Tables that pair with figures: numbers-at-risk table from `hv_survival`, and the numeric table panel from `hv_longitudinal`. API for the risk/report table verified against the package during implementation. |

### Formatting part (adapted from `plot-decorators.qmd`)

| File | Content |
|---|---|
| `annotation.qmd` | `make_footnote` draft/publication footnotes, `labs()`, `annotate()`, `coord_cartesian()` |
| `themes.qmd` | `theme_hv_manuscript`, `theme_hv_poster`, `theme_hv_ppt`, `theme_hv_ppt_dark` |
| `colors.qmd` | manual colours, ColorBrewer palettes, suppressing legends |
| `legends.qmd` | legend positioning (inside/outside panel), text/key size |

### Publications part

| File | Content |
|---|---|
| `manuscripts.qmd` | manuscript PDF save with `hv_ggsave_dims` + `theme_hv_manuscript`; PowerPoint export (officer/rvg) |
| `researchday.qmd` | poster sizing with `theme_hv_poster` + PDF save |

## Files touched

- New chapter files: `hazard.qmd`, `nnt.qmd`, `consort.qmd`, `sankey.qmd`,
  `balance.qmd` (5 new).
- Edited chapter files: scatter, survival, histograms, density, bar, boxplots,
  upset, spaghetti, postagestamp, specialty, combination, qt_tables,
  figure_tables, annotation, themes, colors, legends, manuscripts, researchday.
- `_quarto.yml`: register the 5 new chapters in the correct parts.

## Success criteria

1. `quarto render` completes without error and produces HTML for every chapter.
2. Every `hv_*` function family in the chapter plan has at least one rendered
   worked example.
3. Each example is self-contained: data via `sample_*()` (or base R), no
   external files, no PHI.
4. Gap chapters (density, boxplots, postage-stamp) render base-ggplot examples
   styled with a `theme_hv_*` theme.
5. New chapters appear in the book navigation via `_quarto.yml`.

## Out of scope

- New functionality in `hvtiPlotR` itself.
- Reorganizing the existing part structure beyond adding the listed chapters.
- The `gt` table content beyond representative examples (not an exhaustive gt tutorial).

## Verification

`quarto render` from the repo root; inspect `_book/` HTML for each chapter.
Per repo workflow: all changes land on branch `feat/plot-recipes` via PR; the
user merges.
