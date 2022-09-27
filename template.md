Simple document
================

    ## ── Attaching packages ─────────────────────────────────────── tidyverse 1.3.2 ──
    ## ✔ ggplot2 3.3.6      ✔ purrr   0.3.4 
    ## ✔ tibble  3.1.8      ✔ dplyr   1.0.10
    ## ✔ tidyr   1.2.1      ✔ stringr 1.4.1 
    ## ✔ readr   2.1.2      ✔ forcats 0.5.2 
    ## ── Conflicts ────────────────────────────────────────── tidyverse_conflicts() ──
    ## ✖ dplyr::filter() masks stats::filter()
    ## ✖ dplyr::lag()    masks stats::lag()

I’m an R Markdown document!

\#data import CSV

import data using reader package

``` r
litters_df = read.csv("./data/FAS_litters.csv")
litters_df = janitor::clean_names(litters_df)

head(litters_df)
```

    ##   group litter_number gd0_weight gd18_weight gd_of_birth pups_born_alive
    ## 1  Con7           #85       19.7        34.7          20               3
    ## 2  Con7     #1/2/95/2       27.0        42.0          19               8
    ## 3  Con7 #5/5/3/83/3-3       26.0        41.4          19               6
    ## 4  Con7   #5/4/2/95/2       28.5        44.1          19               5
    ## 5  Con7   #4/2/95/3-3         NA          NA          20               6
    ## 6  Con7   #2/2/95/3-2         NA          NA          20               6
    ##   pups_dead_birth pups_survive
    ## 1               4            3
    ## 2               0            7
    ## 3               0            5
    ## 4               1            4
    ## 5               0            6
    ## 6               0            4

``` r
tail(litters_df)
```

    ##    group litter_number gd0_weight gd18_weight gd_of_birth pups_born_alive
    ## 44  Low8           #79       25.4        43.8          19               8
    ## 45  Low8          #100       20.0        39.2          20               8
    ## 46  Low8         #4/84       21.8        35.2          20               4
    ## 47  Low8          #108       25.6        47.5          20               8
    ## 48  Low8           #99       23.5        39.0          20               6
    ## 49  Low8          #110       25.5        42.7          20               7
    ##    pups_dead_birth pups_survive
    ## 44               0            7
    ## 45               0            7
    ## 46               0            4
    ## 47               0            7
    ## 48               0            5
    ## 49               0            6

``` r
view(litters_df)
skimr::skim(litters_df)
read_csv("./data/FAS_litters.csv", na = c(".","NA"), skip = 2)
```

“read_csv” functions

# need to read into excel spreadsheet

``` r
read_excel("./data/mlb11.xlsx")
```

    ## # A tibble: 30 × 12
    ##    team         runs at_bats  hits homer…¹ bat_avg strik…² stole…³  wins new_o…⁴
    ##    <chr>       <dbl>   <dbl> <dbl>   <dbl>   <dbl>   <dbl>   <dbl> <dbl>   <dbl>
    ##  1 Texas Rang…   855    5659  1599     210   0.283     930     143    96   0.34 
    ##  2 Boston Red…   875    5710  1600     203   0.28     1108     102    90   0.349
    ##  3 Detroit Ti…   787    5563  1540     169   0.277    1143      49    95   0.34 
    ##  4 Kansas Cit…   730    5672  1560     129   0.275    1006     153    71   0.329
    ##  5 St. Louis …   762    5532  1513     162   0.273     978      57    90   0.341
    ##  6 New York M…   718    5600  1477     108   0.264    1085     130    77   0.335
    ##  7 New York Y…   867    5518  1452     222   0.263    1138     147    97   0.343
    ##  8 Milwaukee …   721    5447  1422     185   0.261    1083      94    96   0.325
    ##  9 Colorado R…   735    5544  1429     163   0.258    1201     118    73   0.329
    ## 10 Houston As…   615    5598  1442      95   0.258    1164     118    56   0.311
    ## # … with 20 more rows, 2 more variables: new_slug <dbl>, new_obs <dbl>, and
    ## #   abbreviated variable names ¹​homeruns, ²​strikeouts, ³​stolen_bases,
    ## #   ⁴​new_onbase

``` r
lr_words_df = 
  read_excel(
    "./data/LotR_Words.xlsx",
    range = "B2:D6"
  )
```

    ## New names:
    ## • `` -> `...2`
    ## • `` -> `...3`

# read SAS dataset

``` r
pulse_data = read_sas("./data/public_pulse_data.sas7bdat")
```

\#data export

``` r
write_csv(lr_words_df, file = "./data/lr_words_df.csv")
```

# data minipulation with dplyr

``` r
options(tibble.print_min = 3)

litters_data = read_csv("./data/FAS_litters.csv",
  col_types = "ccddiiii")
litters_data = janitor::clean_names(litters_data)

pups_data = read_csv("./data/FAS_pups.csv",
  col_types = "ciiiii")
pups_data = janitor::clean_names(pups_data)
```

# select function

``` r
#select the variables you want:
select(litters_data, group, litter_number, gd0_weight, pups_born_alive)
```

    ## # A tibble: 49 × 4
    ##   group litter_number gd0_weight pups_born_alive
    ##   <chr> <chr>              <dbl>           <int>
    ## 1 Con7  #85                 19.7               3
    ## 2 Con7  #1/2/95/2           27                 8
    ## 3 Con7  #5/5/3/83/3-3       26                 6
    ## # … with 46 more rows

``` r
#specify a range of columns to keep
select(litters_data,group:gd_of_birth)
```

    ## # A tibble: 49 × 5
    ##   group litter_number gd0_weight gd18_weight gd_of_birth
    ##   <chr> <chr>              <dbl>       <dbl>       <int>
    ## 1 Con7  #85                 19.7        34.7          20
    ## 2 Con7  #1/2/95/2           27          42            19
    ## 3 Con7  #5/5/3/83/3-3       26          41.4          19
    ## # … with 46 more rows
