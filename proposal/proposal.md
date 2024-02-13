Project proposal
================
Team name

``` r
library(tidyverse)
library(broom)
library(readr)
```

## 1. Introduction

## 2. Data

``` r
# bind_rows to combine data
# book1_100k <- read_csv("data/book1-100k.csv")
```

``` r
# bind_rows to combine data
# book1_100k <- read_csv("data/book1-100k.csv")
library(readr)

file_names <- list.files(path = "../data/archive")
length(file_names)
```

    ## [1] 30

``` r
library(plyr)
```

    ## ------------------------------------------------------------------------------

    ## You have loaded plyr after dplyr - this is likely to cause problems.
    ## If you need functions from both plyr and dplyr, please load plyr first, then dplyr:
    ## library(plyr); library(dplyr)

    ## ------------------------------------------------------------------------------

    ## 
    ## Attaching package: 'plyr'

    ## The following objects are masked from 'package:dplyr':
    ## 
    ##     arrange, count, desc, failwith, id, mutate, rename, summarise,
    ##     summarize

    ## The following object is masked from 'package:purrr':
    ## 
    ##     compact

``` r
dataset1 <- ldply(paste("../data/archive/", file_names[1:10], sep = ""), read_csv)
```

    ## Rows: 58292 Columns: 18

    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## chr (11): Name, RatingDist1, RatingDist4, RatingDistTotal, Publisher, Langua...
    ## dbl  (7): Id, pagesNumber, PublishMonth, PublishDay, CountsOfReview, Publish...
    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
    ## Rows: 39705 Columns: 20
    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## chr (12): Name, Authors, ISBN, Publisher, RatingDist5, RatingDist4, RatingDi...
    ## dbl  (8): Id, Rating, PublishYear, PublishMonth, PublishDay, CountsOfReview,...
    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
    ## Rows: 57046 Columns: 18
    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## chr (11): Authors, Publisher, Language, RatingDistTotal, RatingDist5, Rating...
    ## dbl  (7): pagesNumber, Rating, CountsOfReview, PublishDay, PublishMonth, Id,...
    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
    ## Rows: 41892 Columns: 20
    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## chr (12): Name, Authors, ISBN, Publisher, RatingDist5, RatingDist4, RatingDi...
    ## dbl  (8): Id, Rating, PublishYear, PublishMonth, PublishDay, CountsOfReview,...
    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
    ## Rows: 43622 Columns: 20
    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## chr (12): Name, Authors, ISBN, Publisher, RatingDist5, RatingDist4, RatingDi...
    ## dbl  (8): Id, Rating, PublishYear, PublishMonth, PublishDay, CountsOfReview,...
    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
    ## Rows: 38288 Columns: 20
    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## chr (12): Name, Authors, ISBN, Publisher, RatingDist5, RatingDist4, RatingDi...
    ## dbl  (8): Id, Rating, PublishYear, PublishMonth, PublishDay, CountsOfReview,...
    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
    ## Rows: 34759 Columns: 20
    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## chr (12): Name, Authors, ISBN, Publisher, RatingDist5, RatingDist4, RatingDi...
    ## dbl  (8): Id, Rating, PublishYear, PublishMonth, PublishDay, CountsOfReview,...
    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
    ## Rows: 33439 Columns: 20
    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## chr (12): Name, Authors, ISBN, Publisher, RatingDist5, RatingDist4, RatingDi...
    ## dbl  (8): Id, Rating, PublishYear, PublishMonth, PublishDay, CountsOfReview,...
    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
    ## Rows: 32986 Columns: 20
    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## chr (12): Name, Authors, ISBN, Publisher, RatingDist5, RatingDist4, RatingDi...
    ## dbl  (8): Id, Rating, PublishYear, PublishMonth, PublishDay, CountsOfReview,...
    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
    ## Rows: 32105 Columns: 19
    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## chr (12): Authors, Description, ISBN, Language, Name, Publisher, RatingDist1...
    ## dbl  (7): CountsOfReview, Id, PublishDay, PublishMonth, PublishYear, Rating,...
    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

``` r
#dataset2 <- ldply(paste("../data/archive/", file_names[11:23], sep = ""), read_csv)
#full_dataset <- bind_rows(dataset1, dataset2)
```

## 3. Ethics review

## 4. Data analysis plan
