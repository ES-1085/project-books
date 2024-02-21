Project proposal
================
Team name

``` r
library(tidyverse)
library(broom)
library(readr)
library(stringr)
library(readxl)
library(dplyr)
```

## 1. Introduction

General Research Question:

## 2. Data

``` r
queer_books_data <- read_excel("../data/queer-books_all.xlsx")
```

Codebook

id: Book number

Title: Book title

Author: Book author

Author l-f: Book author last name and then first name

Additional authors: Additional author beside the first author

ISBN: Book identifier number

ISBN 13: Book identifier number with 13-digits long

Average Rating: Book average rating

Num Rating: Total number of rating

Publisher: Book publisher

Binding: Book binding type

Number of Pages: Number of pages of the book

Year Published: Book’s year published (first and/or latest publication)

Original Publication Year: First publication year

Exclusive sheft:

``` r
glimpse(queer_books_data)
```

    ## Rows: 500
    ## Columns: 15
    ## $ id                          <dbl> 58155951, 61780641, 28165393, 34376899, 58…
    ## $ Title                       <chr> "The Farthest Place", "A Tearful Dozen", "…
    ## $ Author                      <chr> "E. Barnes", "Kieran Frank", "Alex Kost", …
    ## $ `Author l-f`                <chr> "Barnes, E.", "Frank, Kieran", "Kost, Alex…
    ## $ `Additional Authors`        <chr> NA, NA, NA, NA, NA, "Sara Parker", NA, NA,…
    ## $ ISBN                        <chr> NA, NA, NA, NA, NA, "6.92545069E8", NA, "1…
    ## $ ISBN13                      <dbl> NA, NA, NA, NA, NA, 9.780693e+12, NA, 9.78…
    ## $ `Average Rating`            <dbl> 4.33, 4.33, 4.00, 4.00, 3.33, 4.43, 4.30, …
    ## $ `Num Ratings`               <dbl> 3, 3, 4, 5, 6, 7, 10, 10, 11, 13, 15, 15, …
    ## $ Publisher                   <chr> NA, "JMS Books LLC", NA, "Amazon Digital S…
    ## $ Binding                     <chr> "Kindle Edition", "Kindle Edition", "ebook…
    ## $ `Number of Pages`           <dbl> 218, 38, NA, 385, NA, 38, 261, 284, NA, 26…
    ## $ `Year Published`            <dbl> 2021, 2022, 2016, 2017, 2021, 2015, 2020, …
    ## $ `Original Publication Year` <dbl> NA, 2022, NA, 2017, NA, NA, NA, 2016, 2023…
    ## $ `Exclusive Shelf`           <chr> "queer-books_all", "queer-books_all", "que…

## 3. Ethics review

## 4. Data analysis plan
