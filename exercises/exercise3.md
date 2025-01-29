Exercise 3
================

## Load the data

Let’s start by loading the project data file and looking at its
structure.

``` r
## load the data
app_data_raw <- read_feather(paste0(data_path,"app_data_starter_coded.feather")) 

## show the top 10 rows
app_data_raw
```

    ## # A tibble: 2,018,477 × 8
    ##    application_number examiner_id    au app_last_action_date app_disposal_type
    ##    <chr>                    <dbl> <dbl> <chr>                <chr>            
    ##  1 08284457                 96082  1764 30jan2003 00:00:00   ISS              
    ##  2 08413193                 87678  1764 27sep2010 00:00:00   ISS              
    ##  3 08531853                 63213  1752 30mar2009 00:00:00   ISS              
    ##  4 08637752                 73788  1648 07sep2009 00:00:00   ISS              
    ##  5 08682726                 77294  1762 19apr2001 00:00:00   ABN              
    ##  6 08687412                 68606  1734 16jul2001 00:00:00   ISS              
    ##  7 08716371                 89557  1627 15may2017 00:00:00   PEND             
    ##  8 08765941                 97543  1645 03apr2002 00:00:00   ABN              
    ##  9 08776818                 98714  1637 27nov2002 00:00:00   ABN              
    ## 10 08809677                 65530  1723 23mar2009 00:00:00   ISS              
    ## # ℹ 2,018,467 more rows
    ## # ℹ 3 more variables: gender <chr>, race <chr>, examiner_earliest_date <date>

## Prepare the monthly aggregated panel

We will now aggregate the data on the monthly basis. Specifically, we
need to follow these steps:

### First, examiner-level features

Start with creating a copy of the raw data to calculate these:

1.  Extract `year` and `month` from the `app_last_action` field
2.  Group data by `year`, `month` and `examiner_id`
3.  Summarize by the groups, to create the panel data, which will have
    these variables:
    - total number of applications processed
    - examiner tenure in days since hire date (approximated with
      `examiner_earliest_date`)
    - examiner’s art unit number in that month
    - total number of applications with patents issued
      (`app_disposal_type == "ISS"`)
    - total number of applications that were abandoned after a rejection
      (`app_disposal_type == "ABN"`)
    - total number of applications with final decision still pending
      (`app_disposal_type == "PEND"`)
    - also keep gender and race variables, though they don’t change
      within examiner

``` r
## your code here
```

### Calculate art-unit-level features

Create another copy of the raw data, but aggregate it on a different
level

1.  Extract year and month fields again,
2.  Group data by year, month, and art unit number
3.  Summarize to create these variables
    - number of examiners in that art unit in that month
    - number of minority-race (non-white) examiners
    - number of women
    - number of applications processed in that month

``` r
## your code here
```

### Join the art unit characteristics to the examiner monthly data

Join the second generated dataset to the first one using `left_join()`
command in `dplyr` package, and calculate additional variables:

- extract TC number from `au` into a `tc` variable. Remember that it’s
  indicated by the first two digits, so an art unit 1652 is located in
  Technology Center 1600

- extract workgroup (WG) number from art unit, using the first 3 digits
  of the art unit. So, an art unit 1652 is part of the workgroup `wg`
  1650

``` r
## your code here
```

## Estimate, using linear regressions, what factors predict productivity

Using the resulting monthly dataset, estimate what factors in the data
are associated with higher/lower number of applications processed by any
given examiner in any given month.

``` r
## your code here
```
