# Contributor guide

We welcome contributions to this repository in the form of bug
reports, feature requests, and pull requests.. Please read through and
follow the guidelines detailed below.

# Development environment

For local development of slide material you will need the following
prerequisites:

- Quarto
- pixi
- R packages listed in `pixi.toml` (install with `pixi update`)

## Quarto extensions

You also need to install the Quarto extensions `fontawesome` and
`nbis-course-quarto`:

```
quarto add quarto-ext/fontawesome
quarto add percyfal/nbis-course-quarto
```

## pre-commit

It is recommended that you setup `pre-commit` for linting and for
preventing the mistaken addition of large files, among other things.
Run

```
pixi run pre-commit
```

to initialize `pre-commit` hooks.

# Running Quarto

Activate the `pixi` environment with `pixi shell` and run

```
quarto preview
```

to preview pages, and

```
quarto render
```

to render.

# Images

You can add images to the `img` directory. Make sure to compress files
as much as you can so as not to bloat the repository. For example, to
compress `png` files you can run

```
pngquant -q 10 --output filename.png filename.png -f
```

and for `jpg` files

```
jpegoptim --size 100k --force -o filename.jpg
```

You can adjust the parameters in case you think the quality becomes
too poor. The colors can at times become less clear and crisp, but
that is a small price to pay for reduction in size.

# Presentation material

## Slide structure

Some recommendations on how to structure the slides. Sections are at
level 1, slides are at level 2.

### Fenced divs

Use fenced divs wherever possible for grouping content:

```
## Slide

:::{}

- item 1
- item 2

:::
```

### Columns

Use `.columns` div for multi-column content.

```
## Slide

:::: {.columns}

::: {.column width="50%"}

:::

::: {.column width="50%"}

:::

::::
```

### Citations

Wherever possible, use the custom `.flushright` div to flush citations
to the right.

```
## Slide

::: {.flushright}

@citation-key

:::
```

### Notes

The use of notes is encouraged for links, background information and
more. Notes will show up in presenter view, but can also be a resource
should we convert slides into an article.

```
## Slide

::: {.notes}

Links to URLs, data provenance, ...

:::
```

### R code blocks

Use fenced div with `r` tag for R code blocks:

````
## Slide

```{r }
#| label: my-label
#| echo: false
#| eval: true
#| out-width: 100%

## R code here to generate plot / table
```
````

### TikZ figures

The [TikZ](https://tikz.dev/) package can be used to make more complex
diagrams and illustrations. Make sure to set `cache: true`.

````
## Slide

```{r, engine="tikz", fig.ext="svg"}
#| label: tikz-label
#| echo: false
#| eval: true
#| cache: true
#| out-width: 800px
#| out-height: 550px
#| fig-align: center
\begin{tikzpicture}[>=latex]
%% TikZ code here
\end{tikzpicture}
```
````
