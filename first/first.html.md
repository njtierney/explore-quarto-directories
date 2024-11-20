---
title: first level
format: 
  html:
    keep-md: true
    embed-resources: true
---




Exploring how we read in data in Quarto



::: {.cell}

```{.r .cell-code}
library(tidyverse)
```

::: {.cell-output .cell-output-stderr}

```
── Attaching core tidyverse packages ──────────────────────── tidyverse 2.0.0 ──
✔ dplyr     1.1.4     ✔ readr     2.1.5
✔ forcats   1.0.0     ✔ stringr   1.5.1
✔ ggplot2   3.5.1     ✔ tibble    3.2.1
✔ lubridate 1.9.3     ✔ tidyr     1.3.1
✔ purrr     1.0.2     
── Conflicts ────────────────────────────────────────── tidyverse_conflicts() ──
✖ dplyr::filter() masks stats::filter()
✖ dplyr::lag()    masks stats::lag()
ℹ Use the conflicted package (<http://conflicted.r-lib.org/>) to force all conflicts to become errors
```


:::
:::



# Where does this quarto doc think we are?



::: {.cell}

```{.r .cell-code}
getwd()
```

::: {.cell-output .cell-output-stdout}

```
[1] "/Users/nick/github/njtierney/explore-quarto-directories/first"
```


:::
:::




Here's a file tree



::: {.cell}

```{.r .cell-code}
fs::dir_tree(recurse = 2)
```

::: {.cell-output .cell-output-stdout}

```
.
├── diamonds.csv
├── first.html
├── first.html.md
├── first.qmd
├── first.rmarkdown
├── first_files
│   └── libs
│       ├── bootstrap
│       ├── clipboard
│       └── quarto-html
└── second
    ├── second.html
    ├── second.html.md
    ├── second.qmd
    ├── second_files
    │   └── libs
    └── storms.csv
```


:::
:::



# Writing files out from the root RStudio project



::: {.cell}

```{.r .cell-code}
penguins_csv <- read_csv("penguins.csv")
```

::: {.cell-output .cell-output-error}

```
Error: 'penguins.csv' does not exist in current working directory ('/Users/nick/github/njtierney/explore-quarto-directories/first').
```


:::

```{.r .cell-code}
penguins_csv
```

::: {.cell-output .cell-output-error}

```
Error: object 'penguins_csv' not found
```


:::
:::

::: {.cell}

```{.r .cell-code}
diamonds_csv <- read_csv("first/diamonds.csv")
```

::: {.cell-output .cell-output-error}

```
Error: 'first/diamonds.csv' does not exist in current working directory ('/Users/nick/github/njtierney/explore-quarto-directories/first').
```


:::

```{.r .cell-code}
diamonds_csv
```

::: {.cell-output .cell-output-error}

```
Error: object 'diamonds_csv' not found
```


:::
:::

::: {.cell}

```{.r .cell-code}
storms_csv <- read_csv("first/second/storms.csv")
```

::: {.cell-output .cell-output-error}

```
Error: 'first/second/storms.csv' does not exist in current working directory ('/Users/nick/github/njtierney/explore-quarto-directories/first').
```


:::

```{.r .cell-code}
storms_csv
```

::: {.cell-output .cell-output-error}

```
Error: object 'storms_csv' not found
```


:::
:::



# Referring to each file relative to where we are based



::: {.cell}

```{.r .cell-code}
read_csv("../penguins.csv")
```

::: {.cell-output .cell-output-stderr}

```
Rows: 344 Columns: 8
── Column specification ────────────────────────────────────────────────────────
Delimiter: ","
chr (3): species, island, sex
dbl (5): bill_length_mm, bill_depth_mm, flipper_length_mm, body_mass_g, year

ℹ Use `spec()` to retrieve the full column specification for this data.
ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
```


:::

::: {.cell-output .cell-output-stdout}

```
# A tibble: 344 × 8
   species island    bill_length_mm bill_depth_mm flipper_length_mm body_mass_g
   <chr>   <chr>              <dbl>         <dbl>             <dbl>       <dbl>
 1 Adelie  Torgersen           39.1          18.7               181        3750
 2 Adelie  Torgersen           39.5          17.4               186        3800
 3 Adelie  Torgersen           40.3          18                 195        3250
 4 Adelie  Torgersen           NA            NA                  NA          NA
 5 Adelie  Torgersen           36.7          19.3               193        3450
 6 Adelie  Torgersen           39.3          20.6               190        3650
 7 Adelie  Torgersen           38.9          17.8               181        3625
 8 Adelie  Torgersen           39.2          19.6               195        4675
 9 Adelie  Torgersen           34.1          18.1               193        3475
10 Adelie  Torgersen           42            20.2               190        4250
# ℹ 334 more rows
# ℹ 2 more variables: sex <chr>, year <dbl>
```


:::

```{.r .cell-code}
read_csv("diamonds.csv")
```

::: {.cell-output .cell-output-stderr}

```
Rows: 53940 Columns: 10
── Column specification ────────────────────────────────────────────────────────
Delimiter: ","
chr (3): cut, color, clarity
dbl (7): carat, depth, table, price, x, y, z

ℹ Use `spec()` to retrieve the full column specification for this data.
ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
```


:::

::: {.cell-output .cell-output-stdout}

```
# A tibble: 53,940 × 10
   carat cut       color clarity depth table price     x     y     z
   <dbl> <chr>     <chr> <chr>   <dbl> <dbl> <dbl> <dbl> <dbl> <dbl>
 1  0.23 Ideal     E     SI2      61.5    55   326  3.95  3.98  2.43
 2  0.21 Premium   E     SI1      59.8    61   326  3.89  3.84  2.31
 3  0.23 Good      E     VS1      56.9    65   327  4.05  4.07  2.31
 4  0.29 Premium   I     VS2      62.4    58   334  4.2   4.23  2.63
 5  0.31 Good      J     SI2      63.3    58   335  4.34  4.35  2.75
 6  0.24 Very Good J     VVS2     62.8    57   336  3.94  3.96  2.48
 7  0.24 Very Good I     VVS1     62.3    57   336  3.95  3.98  2.47
 8  0.26 Very Good H     SI1      61.9    55   337  4.07  4.11  2.53
 9  0.22 Fair      E     VS2      65.1    61   337  3.87  3.78  2.49
10  0.23 Very Good H     VS1      59.4    61   338  4     4.05  2.39
# ℹ 53,930 more rows
```


:::

```{.r .cell-code}
read_csv("second/storms.csv")
```

::: {.cell-output .cell-output-stderr}

```
Rows: 19537 Columns: 13
── Column specification ────────────────────────────────────────────────────────
Delimiter: ","
chr  (2): name, status
dbl (11): year, month, day, hour, lat, long, category, wind, pressure, tropi...

ℹ Use `spec()` to retrieve the full column specification for this data.
ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
```


:::

::: {.cell-output .cell-output-stdout}

```
# A tibble: 19,537 × 13
   name   year month   day  hour   lat  long status      category  wind pressure
   <chr> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <chr>          <dbl> <dbl>    <dbl>
 1 Amy    1975     6    27     0  27.5 -79   tropical d…       NA    25     1013
 2 Amy    1975     6    27     6  28.5 -79   tropical d…       NA    25     1013
 3 Amy    1975     6    27    12  29.5 -79   tropical d…       NA    25     1013
 4 Amy    1975     6    27    18  30.5 -79   tropical d…       NA    25     1013
 5 Amy    1975     6    28     0  31.5 -78.8 tropical d…       NA    25     1012
 6 Amy    1975     6    28     6  32.4 -78.7 tropical d…       NA    25     1012
 7 Amy    1975     6    28    12  33.3 -78   tropical d…       NA    25     1011
 8 Amy    1975     6    28    18  34   -77   tropical d…       NA    30     1006
 9 Amy    1975     6    29     0  34.4 -75.8 tropical s…       NA    35     1004
10 Amy    1975     6    29     6  34   -74.8 tropical s…       NA    40     1002
# ℹ 19,527 more rows
# ℹ 2 more variables: tropicalstorm_force_diameter <dbl>,
#   hurricane_force_diameter <dbl>
```


:::
:::



# Using here:



::: {.cell}

```{.r .cell-code}
library(here)
```

::: {.cell-output .cell-output-stderr}

```
here() starts at /Users/nick/github/njtierney/explore-quarto-directories
```


:::
:::

::: {.cell}

```{.r .cell-code}
read_csv(here("penguins.csv"))
```

::: {.cell-output .cell-output-stderr}

```
Rows: 344 Columns: 8
── Column specification ────────────────────────────────────────────────────────
Delimiter: ","
chr (3): species, island, sex
dbl (5): bill_length_mm, bill_depth_mm, flipper_length_mm, body_mass_g, year

ℹ Use `spec()` to retrieve the full column specification for this data.
ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
```


:::

::: {.cell-output .cell-output-stdout}

```
# A tibble: 344 × 8
   species island    bill_length_mm bill_depth_mm flipper_length_mm body_mass_g
   <chr>   <chr>              <dbl>         <dbl>             <dbl>       <dbl>
 1 Adelie  Torgersen           39.1          18.7               181        3750
 2 Adelie  Torgersen           39.5          17.4               186        3800
 3 Adelie  Torgersen           40.3          18                 195        3250
 4 Adelie  Torgersen           NA            NA                  NA          NA
 5 Adelie  Torgersen           36.7          19.3               193        3450
 6 Adelie  Torgersen           39.3          20.6               190        3650
 7 Adelie  Torgersen           38.9          17.8               181        3625
 8 Adelie  Torgersen           39.2          19.6               195        4675
 9 Adelie  Torgersen           34.1          18.1               193        3475
10 Adelie  Torgersen           42            20.2               190        4250
# ℹ 334 more rows
# ℹ 2 more variables: sex <chr>, year <dbl>
```


:::

```{.r .cell-code}
read_csv(here("first/diamonds.csv"))
```

::: {.cell-output .cell-output-stderr}

```
Rows: 53940 Columns: 10
── Column specification ────────────────────────────────────────────────────────
Delimiter: ","
chr (3): cut, color, clarity
dbl (7): carat, depth, table, price, x, y, z

ℹ Use `spec()` to retrieve the full column specification for this data.
ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
```


:::

::: {.cell-output .cell-output-stdout}

```
# A tibble: 53,940 × 10
   carat cut       color clarity depth table price     x     y     z
   <dbl> <chr>     <chr> <chr>   <dbl> <dbl> <dbl> <dbl> <dbl> <dbl>
 1  0.23 Ideal     E     SI2      61.5    55   326  3.95  3.98  2.43
 2  0.21 Premium   E     SI1      59.8    61   326  3.89  3.84  2.31
 3  0.23 Good      E     VS1      56.9    65   327  4.05  4.07  2.31
 4  0.29 Premium   I     VS2      62.4    58   334  4.2   4.23  2.63
 5  0.31 Good      J     SI2      63.3    58   335  4.34  4.35  2.75
 6  0.24 Very Good J     VVS2     62.8    57   336  3.94  3.96  2.48
 7  0.24 Very Good I     VVS1     62.3    57   336  3.95  3.98  2.47
 8  0.26 Very Good H     SI1      61.9    55   337  4.07  4.11  2.53
 9  0.22 Fair      E     VS2      65.1    61   337  3.87  3.78  2.49
10  0.23 Very Good H     VS1      59.4    61   338  4     4.05  2.39
# ℹ 53,930 more rows
```


:::

```{.r .cell-code}
read_csv(here("first/second/storms.csv"))
```

::: {.cell-output .cell-output-stderr}

```
Rows: 19537 Columns: 13
── Column specification ────────────────────────────────────────────────────────
Delimiter: ","
chr  (2): name, status
dbl (11): year, month, day, hour, lat, long, category, wind, pressure, tropi...

ℹ Use `spec()` to retrieve the full column specification for this data.
ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
```


:::

::: {.cell-output .cell-output-stdout}

```
# A tibble: 19,537 × 13
   name   year month   day  hour   lat  long status      category  wind pressure
   <chr> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <chr>          <dbl> <dbl>    <dbl>
 1 Amy    1975     6    27     0  27.5 -79   tropical d…       NA    25     1013
 2 Amy    1975     6    27     6  28.5 -79   tropical d…       NA    25     1013
 3 Amy    1975     6    27    12  29.5 -79   tropical d…       NA    25     1013
 4 Amy    1975     6    27    18  30.5 -79   tropical d…       NA    25     1013
 5 Amy    1975     6    28     0  31.5 -78.8 tropical d…       NA    25     1012
 6 Amy    1975     6    28     6  32.4 -78.7 tropical d…       NA    25     1012
 7 Amy    1975     6    28    12  33.3 -78   tropical d…       NA    25     1011
 8 Amy    1975     6    28    18  34   -77   tropical d…       NA    30     1006
 9 Amy    1975     6    29     0  34.4 -75.8 tropical s…       NA    35     1004
10 Amy    1975     6    29     6  34   -74.8 tropical s…       NA    40     1002
# ℹ 19,527 more rows
# ℹ 2 more variables: tropicalstorm_force_diameter <dbl>,
#   hurricane_force_diameter <dbl>
```


:::
:::
