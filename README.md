# My Personal Blog

A small Quarto website for projects and personal writing.
The visual system uses locally hosted Source Sans 3 and Source Code Pro variable fonts.
Writing and Projects are separate content streams, with shared metadata-driven listing layouts.

## Local setup

Install [Pixi](https://pixi.sh/), then create the locked project environment:

```bash
pixi install
```

Preview the site locally:

```bash
pixi run preview
```

Render the complete site:

```bash
pixi run render
```

## Formatting

Format all Markdown, Quarto, Python, R, CSS, SCSS, and YAML source files:

```bash
pixi run format
```

Check formatting without changing files:

```bash
pixi run format-check
```

The aggregate commands use Panache for Markdown and Quarto, Ruff for Python, Air for R,
and Prettier for styles and YAML. Panache also passes Python and R code blocks inside
Quarto documents to their language-specific formatter. Focused `format-docs`,
`format-python`, `format-r`, and `format-styles` tasks are available when only one
source type needs formatting; matching `check-*` tasks provide non-mutating checks.

Pixi provides Quarto, standard Python 3.14, Jupyter, and the shared Python packages.
Quarto is the site generator; Jupyter is used only to execute embedded Python cells
during a Quarto render. The published `_site` output is static and does not require
Python or Jupyter at runtime.

The project uses `freeze: auto`, so Quarto can reuse computational output when inputs
have not changed. Run `pixi run quarto check jupyter` to verify the cell execution
environment.

## Write a new article

Create a folder in `posts/` containing an `index.qmd` file:

```text
posts/my-new-article/index.qmd
```

Use this minimum frontmatter:

```yaml
---
title: "Article title"
description: "A concise summary for listings and social metadata."
date: "2026-08-02"
categories: [Consumer Analytics, Python]
---
```

Articles containing executable Python cells should also select the Pixi environment's
Jupyter kernel:

```yaml
jupyter: python3
```

Short explanatory code should remain visible. Fold only longer setup or helper cells:

````markdown
```{python}
#| code-fold: true
#| code-summary: "Show setup code"

import pandas as pd
```
````

Writing includes documents from `posts/`. Project case studies remain in the separate
Projects section so an item is never duplicated between the two home-page listings.

The repository currently includes two published posts whose titles begin with
`Sample note:`. They contain clearly marked placeholder copy for testing article and
listing styles. Delete their folders once real articles replace them:

```text
posts/measuring-incrementality/
posts/reproducible-analysis-workflows/
```

## Add a project

Create a case-study folder in `projects/`:

```text
projects/my-project/index.qmd
```

Use standard project metadata:

```yaml
---
title: "Project title"
description: "The question, approach, and practical outcome in one sentence."
date: "2026-08-02"
categories: [Marketing Measurement, Python]
featured: true
---
```

Projects are sorted by date. `featured: true` also places a project in the featured
section on the home page. Listing fields deliberately exclude images, even when a
project contains charts.

## GitHub Pages

The workflow in `.github/workflows/publish.yml` installs the locked Pixi environment,
renders the site with Quarto through `pixi run render`, and publishes `_site` whenever
`main` is updated.

In the repository settings, select **GitHub Actions** as the Pages source before the
first deployment.
