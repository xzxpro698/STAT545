STAT545 Notebook
================

-   [1. Basic Working of RStudio](#basic-working-of-rstudio)
-   [2. dplyr functions](#dplyr-functions)

1. Basic Working of RStudio
---------------------------

`Date: 11/06/2018`

-   **The assign operator `<-`**
    The operator `<-` is recommended to use when coding. A shortcut to input the operator is **Alt+-**. RStudio automatically surrounds it with spaces.

-   **Keyboard shortcuts**
    Try **Alt+Shift+K** to see the list of shortcuts in RStudio.

-   **R chunk**
    -   insert a R chunk: **Ctrl+Alt+I**.
    -   run a R chunk: placing the cursor inside it and pressing **Ctrl+Shift+Enter**.
-   **Clear Environment tab**
    `ls()` gives the whole stuff stored in the environment at the moment
    Clear the workspace to ensure the code is re-runnable:

``` r
ls()
#> [1] "autoloads"
rm(list = ls())
```

-   **Dataframe**
    -   use the package `tidyverse`, which includes popular packages like `dplyr` and `ggplot2`.
    -   matrix has a homogenous structure, which means we can't put character data into a numeric matrix.
    -   `data()` gives the full list of the datasets of loaded packages

2. dplyr functions
------------------

-   **`mutate()` function**
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

-   **`rename()` function **
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

-   **`select()` function**
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

-   **`tally()` function**
    -   A convenience function that knows to count rows.
    -   `count()` gives the same result.

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

-   **`summarise_at()` function**
    -   applies the summarise function(s) to multiple variables

``` r
mtcars %>%
  group_by(cyl) %>%
  summarise_at(vars(mpg, disp, hp), funs(mean, median))
#> # A tibble: 3 x 7
#>     cyl mpg_mean disp_mean hp_mean mpg_median disp_median hp_median
#>   <dbl>    <dbl>     <dbl>   <dbl>      <dbl>       <dbl>     <dbl>
#> 1     4     26.7      105.    82.6       26          108        91 
#> 2     6     19.7      183.   122.        19.7        168.      110 
#> 3     8     15.1      353.   209.        15.2        350.      192.
```

-   **`first()`, `last()`, `nth()`**
    Extract the first, last or nth value from a vector.
    It doesn't collapse the *n* rows for each group into one row, but compute within them.

``` r
mtcars[, 1:5] %>%
  group_by(cyl) %>%
  mutate(qsec.diff = disp - first(disp))
#> # A tibble: 32 x 6
#> # Groups:   cyl [3]
#>      mpg   cyl  disp    hp  drat qsec.diff
#>    <dbl> <dbl> <dbl> <dbl> <dbl>     <dbl>
#>  1  21       6  160    110  3.9       0   
#>  2  21       6  160    110  3.9       0   
#>  3  22.8     4  108     93  3.85      0   
#>  4  21.4     6  258    110  3.08     98   
#>  5  18.7     8  360    175  3.15      0   
#>  6  18.1     6  225    105  2.76     65   
#>  7  14.3     8  360    245  3.21      0   
#>  8  24.4     4  147.    62  3.69     38.7 
#>  9  22.8     4  141.    95  3.92     32.8 
#> 10  19.2     6  168.   123  3.92      7.60
#> # ... with 22 more rows
```

-   **`min_rank()` function**
    `min_rank()` is a windowed function, taking *n* inputs and giving back *n* outputs.
    Among the three methods, `min_rank()` is the one having the right result.

``` r
mtcars[, 1:5] %>%
  group_by(cyl) %>%
  filter(min_rank(hp) == 1)
#> # A tibble: 4 x 5
#> # Groups:   cyl [3]
#>     mpg   cyl  disp    hp  drat
#>   <dbl> <dbl> <dbl> <dbl> <dbl>
#> 1  18.1     6 225     105  2.76
#> 2  30.4     4  75.7    52  4.93
#> 3  15.5     8 318     150  2.76
#> 4  15.2     8 304     150  3.15

mtcars[, 1:5] %>%
  group_by(cyl) %>%
  filter(rank(hp) == 1)
#> # A tibble: 2 x 5
#> # Groups:   cyl [2]
#>     mpg   cyl  disp    hp  drat
#>   <dbl> <dbl> <dbl> <dbl> <dbl>
#> 1  18.1     6 225     105  2.76
#> 2  30.4     4  75.7    52  4.93

mtcars[, 1:5] %>%
  group_by(cyl) %>%
  filter(order(hp) == 1)
#> # A tibble: 3 x 5
#> # Groups:   cyl [3]
#>     mpg   cyl  disp    hp  drat
#>   <dbl> <dbl> <dbl> <dbl> <dbl>
#> 1  21       6  160    110  3.9 
#> 2  16.4     8  276.   180  3.07
#> 3  21.5     4  120.    97  3.7
```
