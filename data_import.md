Data Import
================

Option command i opens the code chunk

Put all the packages haven reads SAS

``` r
library(tidyverse)
```

    ## ── Attaching core tidyverse packages ──────────────────────── tidyverse 2.0.0 ──
    ## ✔ dplyr     1.1.4     ✔ readr     2.1.6
    ## ✔ forcats   1.0.1     ✔ stringr   1.6.0
    ## ✔ ggplot2   4.0.1     ✔ tibble    3.3.0
    ## ✔ lubridate 1.9.4     ✔ tidyr     1.3.1
    ## ✔ purrr     1.2.0     
    ## ── Conflicts ────────────────────────────────────────── tidyverse_conflicts() ──
    ## ✖ dplyr::filter() masks stats::filter()
    ## ✖ dplyr::lag()    masks stats::lag()
    ## ℹ Use the conflicted package (<http://conflicted.r-lib.org/>) to force all conflicts to become errors

``` r
library(readxl)
library(haven)
```

## Read in some data

Read in the litters dataset. Janitor cleans up the names - converts to
lowercase, replaces spaces and puncts w \_, removes special characters,
makes names syntactically

``` r
litters_df = read_csv("./data/FAS_litters.csv")
```

    ## Rows: 49 Columns: 8
    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## chr (4): Group, Litter Number, GD0 weight, GD18 weight
    ## dbl (4): GD of Birth, Pups born alive, Pups dead @ birth, Pups survive
    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

``` r
litters_df = janitor::clean_names(litters_df)
```

## Take a look at the data

Printing in the console

``` r
litters_df
```

    ## # A tibble: 49 × 8
    ##    group litter_number   gd0_weight gd18_weight gd_of_birth pups_born_alive
    ##    <chr> <chr>           <chr>      <chr>             <dbl>           <dbl>
    ##  1 Con7  #85             19.7       34.7                 20               3
    ##  2 Con7  #1/2/95/2       27         42                   19               8
    ##  3 Con7  #5/5/3/83/3-3   26         41.4                 19               6
    ##  4 Con7  #5/4/2/95/2     28.5       44.1                 19               5
    ##  5 Con7  #4/2/95/3-3     <NA>       <NA>                 20               6
    ##  6 Con7  #2/2/95/3-2     <NA>       <NA>                 20               6
    ##  7 Con7  #1/5/3/83/3-3/2 <NA>       <NA>                 20               9
    ##  8 Con8  #3/83/3-3       <NA>       <NA>                 20               9
    ##  9 Con8  #2/95/3         <NA>       <NA>                 20               8
    ## 10 Con8  #3/5/2/2/95     28.5       <NA>                 20               8
    ## # ℹ 39 more rows
    ## # ℹ 2 more variables: pups_dead_birth <dbl>, pups_survive <dbl>

Gives the first 6 rows

``` r
head(litters_df)
```

    ## # A tibble: 6 × 8
    ##   group litter_number gd0_weight gd18_weight gd_of_birth pups_born_alive
    ##   <chr> <chr>         <chr>      <chr>             <dbl>           <dbl>
    ## 1 Con7  #85           19.7       34.7                 20               3
    ## 2 Con7  #1/2/95/2     27         42                   19               8
    ## 3 Con7  #5/5/3/83/3-3 26         41.4                 19               6
    ## 4 Con7  #5/4/2/95/2   28.5       44.1                 19               5
    ## 5 Con7  #4/2/95/3-3   <NA>       <NA>                 20               6
    ## 6 Con7  #2/2/95/3-2   <NA>       <NA>                 20               6
    ## # ℹ 2 more variables: pups_dead_birth <dbl>, pups_survive <dbl>

Last few rows

``` r
tail(litters_df)
```

    ## # A tibble: 6 × 8
    ##   group litter_number gd0_weight gd18_weight gd_of_birth pups_born_alive
    ##   <chr> <chr>         <chr>      <chr>             <dbl>           <dbl>
    ## 1 Low8  #79           25.4       43.8                 19               8
    ## 2 Low8  #100          20         39.2                 20               8
    ## 3 Low8  #4/84         21.8       35.2                 20               4
    ## 4 Low8  #108          25.6       47.5                 20               8
    ## 5 Low8  #99           23.5       39                   20               6
    ## 6 Low8  #110          25.5       42.7                 20               7
    ## # ℹ 2 more variables: pups_dead_birth <dbl>, pups_survive <dbl>

Skim is the only function in the skimr package, not downloading all of
skimr

``` r
skimr::skim(litters_df)
```

|                                                  |            |
|:-------------------------------------------------|:-----------|
| Name                                             | litters_df |
| Number of rows                                   | 49         |
| Number of columns                                | 8          |
| \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_   |            |
| Column type frequency:                           |            |
| character                                        | 4          |
| numeric                                          | 4          |
| \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_ |            |
| Group variables                                  | None       |

Data summary

**Variable type: character**

| skim_variable | n_missing | complete_rate | min | max | empty | n_unique | whitespace |
|:--------------|----------:|--------------:|----:|----:|------:|---------:|-----------:|
| group         |         0 |          1.00 |   4 |   4 |     0 |        6 |          0 |
| litter_number |         0 |          1.00 |   3 |  15 |     0 |       49 |          0 |
| gd0_weight    |        13 |          0.73 |   1 |   4 |     0 |       26 |          0 |
| gd18_weight   |        15 |          0.69 |   1 |   4 |     0 |       31 |          0 |

**Variable type: numeric**

| skim_variable   | n_missing | complete_rate |  mean |   sd |  p0 | p25 | p50 | p75 | p100 | hist  |
|:----------------|----------:|--------------:|------:|-----:|----:|----:|----:|----:|-----:|:------|
| gd_of_birth     |         0 |             1 | 19.65 | 0.48 |  19 |  19 |  20 |  20 |   20 | ▅▁▁▁▇ |
| pups_born_alive |         0 |             1 |  7.35 | 1.76 |   3 |   6 |   8 |   8 |   11 | ▁▃▂▇▁ |
| pups_dead_birth |         0 |             1 |  0.33 | 0.75 |   0 |   0 |   0 |   0 |    4 | ▇▂▁▁▁ |
| pups_survive    |         0 |             1 |  6.41 | 2.05 |   1 |   5 |   7 |   8 |    9 | ▁▃▂▇▇ |

Put View(litters_df) shows the full dataset, but don’t put this in RMD
only in the console!

Character variable- mix of letters and numbers double- particular kind
of number, missing variables coded as NA

Can type in ?read_csv to look at the help function

## Options to read_csv

``` r
litters_df = read_csv("./data/FAS_litters.csv", skip = 10, col_names = FALSE)
```

    ## Rows: 40 Columns: 8
    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## chr (4): X1, X2, X3, X4
    ## dbl (4): X5, X6, X7, X8
    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

all of these are missing na

``` r
litters_df = read_csv("./data/FAS_litters.csv", na = c("", "NA", ".", 999))
```

    ## Rows: 49 Columns: 8
    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## chr (2): Group, Litter Number
    ## dbl (6): GD0 weight, GD18 weight, GD of Birth, Pups born alive, Pups dead @ ...
    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

``` r
litters_df = read_csv("./data/FAS_litters.csv")
```

    ## Rows: 49 Columns: 8
    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## chr (4): Group, Litter Number, GD0 weight, GD18 weight
    ## dbl (4): GD of Birth, Pups born alive, Pups dead @ birth, Pups survive
    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

checkout `read_csv()` for more information

## Other formats EXCEL

Read in an excel file

``` r
mlb_df = read_excel("./data/mlb11.xlsx")
mlb_df
```

    ## # A tibble: 30 × 12
    ##    team        runs at_bats  hits homeruns bat_avg strikeouts stolen_bases  wins
    ##    <chr>      <dbl>   <dbl> <dbl>    <dbl>   <dbl>      <dbl>        <dbl> <dbl>
    ##  1 Texas Ran…   855    5659  1599      210   0.283        930          143    96
    ##  2 Boston Re…   875    5710  1600      203   0.28        1108          102    90
    ##  3 Detroit T…   787    5563  1540      169   0.277       1143           49    95
    ##  4 Kansas Ci…   730    5672  1560      129   0.275       1006          153    71
    ##  5 St. Louis…   762    5532  1513      162   0.273        978           57    90
    ##  6 New York …   718    5600  1477      108   0.264       1085          130    77
    ##  7 New York …   867    5518  1452      222   0.263       1138          147    97
    ##  8 Milwaukee…   721    5447  1422      185   0.261       1083           94    96
    ##  9 Colorado …   735    5544  1429      163   0.258       1201          118    73
    ## 10 Houston A…   615    5598  1442       95   0.258       1164          118    56
    ## # ℹ 20 more rows
    ## # ℹ 3 more variables: new_onbase <dbl>, new_slug <dbl>, new_obs <dbl>

View shows the whole data file ?read_excel- specific

# Read in SAS

``` r
pulse_df = read_sas("./data/public_pulse_data.sas7bdat")
```

# read in STATA.dta

read_dta

## read in SPSS

read_sav
