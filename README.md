## Contributing

### New chapters

Create new Quarto documents (.qmd) for new chapters using the [tidy.qmd](tidy.qmd) chapter as a template. Label top-level headings with section labels (e.g., `# Basics {#sec-tidy}`) and refer to them in other sections of the book with a cross-reference (e.g., `see xx and yy in [Chapter -@sec-tidy]`). Include these quarto filenames as `chapters` under the relevant `part` (see the [_quarto.yml](_quarto.yml)) for examples.

Create new appendices the same way as new chapters, but include them as `appendices` in the [_quarto.yml](_quarto.yml).

Unnumbered chapters, such as [index.qmd](index.qmd) are achieved with `# Preface {.unnumbered}`.

### Exercises

Using the [tidy.qmd](tidy.qmd) chapter as a template, set the exercise counter at the top to 1:

    ```{r}
    #| echo: false
    options(digits=3)
    options(max.print=200)
    .ex <- 1
    ```

Exercises are called out inline using the [callout box syntax](https://quarto.org/docs/authoring/callouts.html). The inline R code prints the exercise number, then increments the exercise counter for the next exercise in that chapter. 


    ::: {.callout-note}
    
    # Exercise `r .ex``r .ex=.ex+1`
    
    What are the values after each statement in the following?
    
    ```{r ex1}
    mass <- 50              # mass?
    age  <- 30              # age?
    mass <- mass * 2        # mass?
    age  <- age - 10        # age?
    mass_index <- mass/age  # massIndex?
    ```
    
    :::

### Building and deploying

Render the book using the "Render Book" button in the RStudio build pane, or using the keyboard shortcut Cmd-Shift-B. The compiled book will be placed in the [_book](_book) directory by default. This directory is ignored by git. Open the `_book/index.html` to preview.

To publish to GitHub Pages, follow the directions [here](https://quarto.org/docs/publishing/github-pages.html). 

First, make sure all your changes are committed on the main branch, then set up an orphan `gh-pages` branch.

```sh
git checkout --orphan gh-pages
git reset --hard # make sure all changes are committed before running this!
git commit --allow-empty -m "Initialising gh-pages branch"
git push origin gh-pages
```

Then go into the repository settings and make sure GitHub Pages is served from a branch (`gh-pages`) from root `/`. Make sure `_book` is in your `.gitignore`.

Then, publish:

```
quarto publish gh-pages
```
