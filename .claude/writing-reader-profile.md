# Reader Profiles — HVTI graphics documentation

A menu of selectable audiences for the `ehrlinger-writing` harness. Write for
ONE persona at a time, not a blend. The active persona is chosen per task
(explicit choice → repo `CLAUDE.md` default → ask). The `hvti_graphics` recipes
book defaults to persona (a).

## (a) HVTI/CORR biostatistician — DEFAULT for the recipes book

The biostats team (Austin, Kelsey, Wendy) adopting the house plotting style.

- **Already knows:** R, ggplot2, survival analysis, the CORR datasets.
- **Wants from a recipe:** all three at once — runnable code to copy, a call on
  which plot to use, and the meaning of a specific argument. They open a recipe
  for any of the three, often in the same sitting.
- **Lands when:** the code runs as written, the argument is shown in context,
  the recipe says when to use the plot, and the figure comes with a reading
  guide.
- **Bounces when:** the recipe opens with a wall of code before saying what the
  plot is for, or shows a figure with no guide on how to read it.
- **Watch for:** the reader hand-rolling a plot in raw ggplot instead of using
  the `hvtiPlotR`/`ggRandomForests` constructor that already makes it. Second,
  drifting off house style by skipping the `hv_*` theme or the two-step S3
  workflow.

## (b) Clinical researcher / surgeon — figure consumer

Clinical researchers and surgeons do not read the book. They receive the
exported figure. Persona (a) is the one who, on their behalf, picks the right
plot and writes or says how to read it. So this is not a prose audience — it is
a constraint on persona (a)'s prose: when writing for the biostatistician,
remember the figure will be handed to a clinician who never saw the recipe. The
recipe should make the figure self-explanatory, so the reading guide carries
over to the person who only sees the plot.

## (c) External R user migrating from SAS — bilingual

Knows both the SAS workflow and R. Anchors: `%kaplan`, `plot.sas`,
PROC LIFETEST/PHREG, the Blackstone-Naftel-Turner additive hazard. The need is
not hand-holding through R; it is confirmation that the R output matches the
SAS original they already trust.

- **Already knows:** the SAS workflow AND R.
- **Wants from a recipe:** confirmation the R output matches the SAS original
  they trust.
- **Lands when:** the recipe ties the R function to the SAS macro it replaces
  and states that the numbers match.
- **Bounces when:** the R version is presented with no bridge to, or no
  reconciliation against, the SAS they know.
