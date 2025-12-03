Mpox Project
================
Shayne Estill

``` r
library(janitor)
```

    ## 
    ## Attaching package: 'janitor'

    ## The following objects are masked from 'package:stats':
    ## 
    ##     chisq.test, fisher.test

``` r
library(rio)
library(lubridate)
```

    ## 
    ## Attaching package: 'lubridate'

    ## The following objects are masked from 'package:base':
    ## 
    ##     date, intersect, setdiff, union

``` r
library(skimr)
library(epikit)
library(gtsummary)
library(apyramid)
library(tidyverse)
```

    ## ── Attaching core tidyverse packages ──────────────────────── tidyverse 2.0.0 ──
    ## ✔ dplyr   1.1.4     ✔ readr   2.1.5
    ## ✔ forcats 1.0.1     ✔ stringr 1.5.2
    ## ✔ ggplot2 4.0.0     ✔ tibble  3.3.0
    ## ✔ purrr   1.1.0     ✔ tidyr   1.3.1

    ## ── Conflicts ────────────────────────────────────────── tidyverse_conflicts() ──
    ## ✖ dplyr::filter() masks stats::filter()
    ## ✖ dplyr::lag()    masks stats::lag()
    ## ℹ Use the conflicted package (<http://conflicted.r-lib.org/>) to force all conflicts to become errors

``` r
library(pacman)
library(readxl)
```

``` r
# Install remotes if you need to (so you can install a package from GitHub)
pacman::p_load("remotes")

# Use the install_github function from remotes to install appliedepidata
remotes::install_github("appliedepi/appliedepidata")
```

    ## Using GitHub PAT from the git credential store.

    ## Skipping install of 'appliedepidata' from a github remote, the SHA1 (ea38b977) has not changed since last install.
    ##   Use `force = TRUE` to force installation

``` r
# Save down the two mpox files using the save_data() function from appliedepidata
appliedepidata::save_data("mpox_linelist",
                        path = "data")
```

    ## ✔ File(s) successfully saved here: /Users/shayneestill/Desktop/Independent Data Analysis Projects/mpox_project/data

``` r
appliedepidata::save_data("mpox_aggregate_table",
                          path = "data")
```

    ## ✔ File(s) successfully saved here: /Users/shayneestill/Desktop/Independent Data Analysis Projects/mpox_project/data

Read the data into this file

``` r
mpox_table = read_csv(file = "./data/mpox_aggregate_table.csv")
```

    ## Rows: 101 Columns: 3
    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## chr  (1): Country
    ## dbl  (1): Cases
    ## date (1): DateRep
    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

``` r
mpox_linelist = read_excel("./data/mpox_linelist.xlsx")
```

Data exploration Tasks: Take a look at the different data frames and
determine:

- The number of columns and observations (e.g. their dimensions)
- The class of their columns and whether it matches its nature (e.g.,
  are “dates” considered “dates” by R?)
- If the contents of columns are clean and standardized in the mpox
  linelist (e.g. gender, clinical symptoms, outcome, hiv status and
  sexual orientation). Do you need to recode any of them?
- How unknown or missing data is categorized in these columns. Do these
  values need to be standardized?

``` r
mpox_table = 
    janitor::clean_names(mpox_table)

mpox_linelist = 
    janitor::clean_names(mpox_linelist)
```

The mpox_table dataset has 101 rows and 101 columns.

The mpox_linelist dataset has 2000 rows and 2000 columns.
