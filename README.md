
<!-- README.md is generated from README.Rmd. Please edit that file -->

# explore-quarto-directories

<!-- badges: start -->
<!-- badges: end -->

The goal of explore-quarto-directories is to demonstrate how quarto
looks for files.

Directory structure is as follows:

``` r
fs::dir_tree(recurse = 2)
#> .
#> ├── README.Rmd
#> ├── README.md
#> ├── explore-quarto-directories.Rproj
#> ├── first
#> │   ├── diamonds.csv
#> │   ├── first.html
#> │   ├── first.html.md
#> │   ├── first.qmd
#> │   └── second
#> │       ├── second.html
#> │       ├── second.html.md
#> │       ├── second.qmd
#> │       └── storms.csv
#> ├── penguins.csv
#> ├── top.html
#> ├── top.html.md
#> └── top.qmd
```
