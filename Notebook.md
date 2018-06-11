STAT545 Notebook
================

-   [1. Basic Working of RStudio](#basic-working-of-rstudio)
-   [2. dplyr functions](#dplyr-functions)

1. Basic Working of RStudio
---------------------------

`Date: 11/06/2018`

#### 1.1 The operator `<-`

The operator `<-` is recommended to use when coding. A shortcut to input the operator is **Alt+-**. RStudio automatically surrounds it with spaces.

#### 1.2 Keyboard shortcuts

Try **Alt+Shift+K** to see the list of shortcuts in RStudio.

#### 1.3 R chunk

-   insert a R chunk: **Ctrl+Alt+I**.
-   run a R chunk: placing the cursor inside it and pressing **Ctrl+Shift+Enter**.

#### 1.4 Clear Environment tab

`ls()` gives the whole stuff stored in the environment at the moment

``` r
ls()
#> [1] "autoloads"
```

Clear the workspace to ensure the code is re-runnable:

``` r
rm(list = ls())
```

#### 1.5 Dataframe

-   use the package `tidyverse`, which includes popular packages like `dplyr` and `ggplot2`.
-   matrix has a homogenous structure, which means we can't put character data into a numeric matrix.
-   `data()` gives the full list of the datasets of loaded packages

2. dplyr functions
------------------

#### 2.1 `mutate()` function

To get rid of a new variable by setting it to `NULL`.

``` r
mtcars %>% head(10) %>%
  mutate(tmp1 = wt * 10, tmp2 = qsec * 10, tmp1 = NULL)
#>     mpg cyl  disp  hp drat    wt  qsec vs am gear carb  tmp2
#> 1  21.0   6 160.0 110 3.90 2.620 16.46  0  1    4    4 164.6
#> 2  21.0   6 160.0 110 3.90 2.875 17.02  0  1    4    4 170.2
#> 3  22.8   4 108.0  93 3.85 2.320 18.61  1  1    4    1 186.1
#> 4  21.4   6 258.0 110 3.08 3.215 19.44  1  0    3    1 194.4
#> 5  18.7   8 360.0 175 3.15 3.440 17.02  0  0    3    2 170.2
#> 6  18.1   6 225.0 105 2.76 3.460 20.22  1  0    3    1 202.2
#> 7  14.3   8 360.0 245 3.21 3.570 15.84  0  0    3    4 158.4
#> 8  24.4   4 146.7  62 3.69 3.190 20.00  1  0    4    2 200.0
#> 9  22.8   4 140.8  95 3.92 3.150 22.90  1  0    4    2 229.0
#> 10 19.2   6 167.6 123 3.92 3.440 18.30  1  0    4    4 183.0
```

#### 2.2 `rename()` function

To chage column names by using `rename()`.

``` r
mtcars[, 1:5] %>% head(10) %>%
  rename(mpg.NEW = mpg,
         cyl.NEW = cyl,
         disp.NEW = disp)
#>                   mpg.NEW cyl.NEW disp.NEW  hp drat
#> Mazda RX4            21.0       6    160.0 110 3.90
#> Mazda RX4 Wag        21.0       6    160.0 110 3.90
#> Datsun 710           22.8       4    108.0  93 3.85
#> Hornet 4 Drive       21.4       6    258.0 110 3.08
#> Hornet Sportabout    18.7       8    360.0 175 3.15
#> Valiant              18.1       6    225.0 105 2.76
#> Duster 360           14.3       8    360.0 245 3.21
#> Merc 240D            24.4       4    146.7  62 3.69
#> Merc 230             22.8       4    140.8  95 3.92
#> Merc 280             19.2       6    167.6 123 3.92
```

-   `select()` function
    -   `select()` can change the name of columns request to keep.
    -   `everthing()` selects all columns.

``` r
mtcars[, 1:5] %>% head(10) %>%
  select(mpg.NEW = mpg, everything())
#>                   mpg.NEW cyl  disp  hp drat
#> Mazda RX4            21.0   6 160.0 110 3.90
#> Mazda RX4 Wag        21.0   6 160.0 110 3.90
#> Datsun 710           22.8   4 108.0  93 3.85
#> Hornet 4 Drive       21.4   6 258.0 110 3.08
#> Hornet Sportabout    18.7   8 360.0 175 3.15
#> Valiant              18.1   6 225.0 105 2.76
#> Duster 360           14.3   8 360.0 245 3.21
#> Merc 240D            24.4   4 146.7  62 3.69
#> Merc 230             22.8   4 140.8  95 3.92
#> Merc 280             19.2   6 167.6 123 3.92
```

-   `tally()` function
    -   A convenience function that knows to count rows.

``` r
mtcars %>% group_by(gear) %>%
  tally()
#> # A tibble: 3 x 2
#>    gear     n
#>   <dbl> <int>
#> 1     3    15
#> 2     4    12
#> 3     5     5

mtcars %>% count(gear)
#> # A tibble: 3 x 2
#>    gear     n
#>   <dbl> <int>
#> 1     3    15
#> 2     4    12
#> 3     5     5
```

Or
