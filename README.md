# Worldinmarketing

A reproducible personal blog built with [Quarto](https://quarto.org/),
featuring two computational posts (one in R, one in Python) that analyze
the Palmer Penguins dataset.

## Prerequisites

Install the following before building this site. Versions used during development are listed; newer versions should also work.

- [Quarto](https://quarto.org/docs/get-started/) (version 1.5 or later)
- [uv](https://docs.astral.sh/uv/getting-started/installation/) (Python package/environment manager)
- [R](https://cran.r-project.org/) (version 4.6.1)

`renv` (the R environment manager) does not need to be installed manually. It bootstraps itself automatically the first time R is run in this project.

## Build instructions

Clone the repository:

```bash
git clone git@github.com:maryamh0sseini/maryamh0sseini.github.io.git
cd maryamh0sseini.github.io
```

Set up the Python environment (this reads `pyproject.toml` and `uv.lock` and creates a local `.venv`):

```bash
uv sync
```

Set up the R environment. Open R **from the top level of this repository**
(for example, by opening `Worldinmarketing.Rproj` in RStudio or Positron,
which ensures R starts in the right folder), then run:

```r
renv::restore()
```

This installs the exact package versions recorded in `renv.lock` into a project-local R library.
Render the site. From the top level, in a terminal:

```bash
uv run quarto render
```

Running with `uv run` ensures Quarto uses this project's Python virtual environment. Running `quarto render` from the top level (rather than from inside `posts/`) ensures R reads `.Rprofile` and activates `renv`.

## Viewing the built site

The rendered site is written to the `docs/` folder. Open `docs/index.html` in a browser to view it locally:

```bash
start docs/index.html
```

(On macOS/Linux, use `open docs/index.html` instead of `start`.)

The live version of this site is published at:
https://maryamh0sseini.github.io

## About the posts

Two computational posts live under `posts/`:

- `posts/penguins-r/index.qmd` — written in R, analyzing penguin body size by species.
- `posts/penguins-py/index.qmd` — written in Python, analyzing penguin bill shape by island.

Both posts use the **Palmer Penguins** dataset, available via the
[`palmerpenguins`](https://allisonhorst.github.io/palmerpenguins/) R package and the `palmerpenguins` Python package. Data were collected and made available by Dr. Kristen Gorman and the Palmer Station, Antarctica LTER, and are released under a CC0 license.

The dataset is loaded directly from these packages at render time. It is not committed as a separate data file, and no network access is required to load it, since the packages bundle the data locally.

## Environment files

This project pins one environment per language, at the top level of the repository:

- **Python**: `pyproject.toml`, `uv.lock`, `.python-version`
- **R**: `renv.lock`, `.Rprofile`, `renv/`

Both must be committed to version control (with the exception of `renv/library`, which `renv`'s own `.gitignore` keeps untracked).