Project title
================
by Team name

## Summary

Write-up of your project and findings go here. Think of this as the text
of your presentation. The length should be roughly 5 minutes when read
out loud. Although pacing varies, a 5-minute speech is roughly 750
words. To use the word count addin, select the text you want to count
the words of (probably this is the Summary section of this document, go
to Addins, and select the `Word count` addin). This addin counts words
using two different algorithms, but the results should be similar and as
long as you’re in the ballpark of 750 words, you’re good! The addin will
ignore code chunks and only count the words in prose.

You can also load your data here and present any analysis results /
plots, but I strongly urge you to keep that to a minimum (maybe only the
most important graphic, if you have one you can choose). And make sure
to hide your code with `echo = FALSE` unless the point you are trying to
make is about the code itself. Your results with proper output and
graphics go in your presentation, this space is for a brief summary of
your project.

## Presentation

Our presentation can be found [here](presentation/presentation.html).

## Data

Include a citation for your data here. See
<http://libraryguides.vu.edu.au/c.php?g=386501&p=4347840> for guidance
on proper citation for datasets. If you got your data off the web, make
sure to note the retrieval date.

## References

List any references here. You should, at a minimum, list your data
source.

# Joining Datasets

``` r
library(tidyverse)
```

    ## ── Attaching core tidyverse packages ──────────────────────── tidyverse 2.0.0 ──
    ## ✔ dplyr     1.1.4     ✔ readr     2.1.5
    ## ✔ forcats   1.0.0     ✔ stringr   1.5.1
    ## ✔ ggplot2   3.4.4     ✔ tibble    3.2.1
    ## ✔ lubridate 1.9.3     ✔ tidyr     1.3.1
    ## ✔ purrr     1.0.2     
    ## ── Conflicts ────────────────────────────────────────── tidyverse_conflicts() ──
    ## ✖ dplyr::filter() masks stats::filter()
    ## ✖ dplyr::lag()    masks stats::lag()
    ## ℹ Use the conflicted package (<http://conflicted.r-lib.org/>) to force all conflicts to become errors

``` r
library(tibble)
library(readxl)
```

``` r
Queer_Books_Database_1_ <- read_excel("data/Queer Books Database.xlsx", 
    sheet = "Fiction Database")
```

    ## New names:
    ## • `Time` -> `Time...32`
    ## • `Setting` -> `Setting...33`
    ## • `` -> `...36`
    ## • `Time` -> `Time...40`
    ## • `Setting` -> `Setting...41`

``` r
Queer_Books_Database <- read_excel("data/Queer Books Database.xlsx", 
    sheet = "Non-Fiction Database")
```

    ## New names:
    ## • `Faith` -> `Faith...22`
    ## • `` -> `...27`
    ## • `Faith` -> `Faith...30`

``` r
Queer_Books_Name_ <- read_excel("data/Queer_Books_Name .xlsx")
goodreads_top100_from1980to2023_v2_1_ <- read_csv("data/goodreads_top100_from1980to2023_v2 (1).csv")
```

    ## New names:
    ## Rows: 4400 Columns: 12
    ## ── Column specification
    ## ──────────────────────────────────────────────────────── Delimiter: "," chr
    ## (9): Book, Series, Release number, Author, Description, Format, Genres, ... dbl
    ## (3): ...1, Num Pages, Number of voters
    ## ℹ Use `spec()` to retrieve the full column specification for this data. ℹ
    ## Specify the column types or set `show_col_types = FALSE` to quiet this message.
    ## • `` -> `...1`

``` r
book1_100k <- read_csv("data/book1-100k.csv")
```

    ## Rows: 58292 Columns: 18
    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## chr (11): Name, RatingDist1, RatingDist4, RatingDistTotal, Publisher, Langua...
    ## dbl  (7): Id, pagesNumber, PublishMonth, PublishDay, CountsOfReview, Publish...
    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

``` r
fiction <- data_frame(Queer_Books_Database_1_)
```

    ## Warning: `data_frame()` was deprecated in tibble 1.1.0.
    ## ℹ Please use `tibble()` instead.
    ## This warning is displayed once every 8 hours.
    ## Call `lifecycle::last_lifecycle_warnings()` to see where this warning was
    ## generated.

``` r
Non_fiction_book <- data_frame(Queer_Books_Database)
```

# Joining Datasets

``` r
Queer_Goodread <- Queer_Books_Name_ %>% 
  left_join(goodreads_top100_from1980to2023_v2_1_, by = c("Title" = "Book"))
```

``` r
Queer_Fiction <- Queer_Books_Name_ %>% 
  left_join(fiction, by = "Title")
```

``` r
Queer_nonfiction <- Queer_Books_Name_ %>% 
  left_join(Non_fiction_book, by = "Title")
```

``` r
Queer_all <- Queer_Goodread %>% 
  inner_join(Queer_Fiction, by = "Title") %>% 
  inner_join(Queer_nonfiction, by = "Title")
```

``` r
Queer_Book1 <- Queer_Books_Name_ %>% 
  left_join(book1_100k, by = c("Title" = "Name"))
```
