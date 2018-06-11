STAT545 Notebook
================

-   [1. Basic Working of RStudio](#basic-working-of-rstudio)

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
