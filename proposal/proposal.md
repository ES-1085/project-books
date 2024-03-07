Queer Lit Sample Project Proposal
================
Asy Xaytouthor & Kandi Grey

``` r
library(tidyverse)
library(broom)
library(readr)
library(stringr)
library(readxl)
library(dplyr)
library(hexbin)
library(visdat)
library(naniar)
library(UpSetR)
library(ggplot2)
library(hrbrthemes)
library(tidyr)
library(viridis)
library(ggridges)
```

## 1. Introduction

General Research Question: Examining the correlation between the number
of Reviews a book receives and the Rating. Understanding a possible
evolution of queer literature from the 1970s - 2024.

Examining the general relation between reviews and rating from the
Goodreads rating system. The data has been formulated from Goodreads
lists and can be found here:

Queer_books-data -
<https://docs.google.com/spreadsheets/d/11cubO21f_MJb85e4IrpsaNH9Sm4-6B8-kL2CnUNGGdE/edit>  
Kandi Grey Queer Lit Shelf -
<https://www.goodreads.com/review/list/59261401-kandi-grey?shelf=queer-books_all>

The variables include id (Id number of book from), Title, Author (Last
name, First name), Additional Authors, ISBN, ISBN13, Average Rating ( 1-
5), Num Rating (Number of Ratings), Publisher, Binding (Paperback,
Hardcover, eBook, ect), Number of Pages, Year Published, Original
Publication Year, Exclusive Shelf (File name). 500 observations have
been recorded. Goodreads is a site and a tool used by people to
categorise books they have written and read. Goodreads has different
ways to help users categorise books; I created a ‘bookshelf’ to collect
books from Lists that other Goodreads users supplied. I collected the
top 500 from several Queer Literature lists to create the dataset we are
using. Using this data, we can examine the correlation between the
Average Rating and the Number of Reviews received, if the Binding method
is related to the year published, if there is a common publisher for
Queer literature. Possible Further Study: Examining the relation to
genre within Queer Literature. The differences across the queer
spectrum.

Vocabulary Definitions: Queer: does not fall under the
heterosexual/romantic spectrum, i.e. falls under the LGBTQIA+ spectrum
Queer Literature Definition: literature either written by an author that
identifies as queer, the themes of the book itself are queer related,
either through character, theme, topic ect.

## 2. Data

``` r
queer_books_data <- read_excel("../data/queer-books_data.xlsx")
book_genre <- read_excel("../data/data_genre (1).xlsx")
```

Codebook

id: Book number

title: Book title

author: Book author

author l-f: Book author last name and then first name

additional_authors: Additional author beside the first author

ISBN: Book identifier number

ISBN_13: Book identifier number with 13-digits long

average_rating: Book average rating

num_rating: Total number of rating

publisher: Book publisher

binding: Book binding type

number_of_pages: Number of pages of the book

year_published: Book’s year published (first and/or latest publication)

original_publication_year: First publication year

exclusive-shelf:file name

Genre Explanations: aromantic: book containing aromantic themes,
characters, relationships

asexual: book containing asexual and a-spectrum (demi-sexual,
gray-sexual ect) themes, characters, relationships

bisexual: book containing bisexual themes, characters, relationships

dystopian: books including one of the following: dystopian, futuristic,
science-fiction, speculative fiction, alien

fantasy: books including the following: fantasy, High-Fantasy,
Science-Fiction Fantasy, Magic, Paranormal, Urban Fantasy, Supernatural

fiction: books that didn’t contain any of the other genres, including
Historical Fiction, poetry, short stories, Contemporary, Anthologies,
Fiction Essays, Graphic Novels

gay: books including themes of homosexuality pertaining to male and male
relationships, characters identifying as gay

horror: books including one of the following genres: Horror, Paranormal,
Dark Fantasy, Supernatural, thriller, Gothic

intersexual: books containing intersexual themes, characters,
relationships

lesbian: books including themes of homosexuality pertaining to female
and female relationships, characters identifying as lesbian

mystery-thriller: books including one of the following genres: mystery,
thriller, crime, investigation, detective

non-binary: books that don’t fall within the gender binary of just male
or female, and includes themes of:queer, genderfluid, trans,
intersexual, agender, involves characters who identify as non-binary,
could also invlove themes of gender discussion and gender exploration

non-fiction: books that are not fictional

polyamourous: books containing polyamoruous themes, characters,
relationships

queer: books that are categorized generally, include multiple facets of
queerness, and are hard to define into a singular generalisation already
considered in the other genres

queer-platonic: books containing relationships that are not strictly
sexual or romantic

religion: books containing religious themes, characters including
Christianity, Buddhism, Muslim, Hindi or containing religious themes:
demons, angels, deities, gods, old-religions, balasura,

romance: books that include romance

trans: books containing transgender and transexual themes, characters,
relationships, discussions

``` r
glimpse(queer_books_data)
```

    ## Rows: 500
    ## Columns: 15
    ## $ id                        <dbl> 19351, 96986, 48037, 5297, 323455, 53064, 53…
    ## $ title                     <chr> "The Epic of Gilgamesh", "Plato Symposium (H…
    ## $ author                    <chr> "Anonymous", "Plato", "J. Sheridan Le Fanu",…
    ## $ `author_ l-f`             <chr> "Anonymous, Anonymous", "Plato, Plato", "Fan…
    ## $ additional_authors        <chr> "N.K. Sandars, John Maier, Herbert Mason, Jo…
    ## $ ISBN                      <chr> "1.41026286E8", "8.7220076E8", "8.09510839E8…
    ## $ ISBN_13                   <dbl> 9.780141e+12, 9.780872e+12, 9.780810e+12, NA…
    ## $ average_rating            <dbl> 3.72, 4.08, 3.85, 4.12, 4.22, 3.90, 3.70, 3.…
    ## $ num_ratings               <dbl> 94267, 70111, 109904, 1510379, 20296, 16738,…
    ## $ publisher                 <chr> "Penguin Books Limited", "Hackett Publishing…
    ## $ binding                   <chr> "Paperback", "Paperback", "Paperback", "Pape…
    ## $ number_of_pages           <dbl> 120, 109, 108, 272, 188, 384, 142, 194, 336,…
    ## $ year_published            <dbl> 2006, 1989, 2000, 2004, 1993, 1999, 2005, 20…
    ## $ original_publication_year <dbl> -1200, -380, 1872, 1890, 1897, 1911, 1912, 1…
    ## $ exclusive_shelf           <chr> "queer-books_all", "queer-books_all", "queer…

## 3. Ethics review

Limitations: The data is subjective, as it comes from Kandi’s personal
Goodreads profile and contains personal bias. It also a selection of 500
books from different queer book lists provided on Goodreads, which
contains human bias for literature. The Goodreads system has a voting
and review system that relies on human interaction, and therefore human
subjectivity. The lack of information generated to fully comprehend the
data is also limited in that there are variables not included within the
data collected e.g. Country of origin, languages published in, gender of
author - which would be significant to include when discussing the point
of representation within literature. The are also limitations within the
form of data collected: literature. The variables do not include a
labeling system for Adult, New Adult, Young Adult, or Children. The
genres given are broad sense of what the books contains and not
specifics e.g. the label Fantasy includes Sci-fi and High Fantasy which
don’t share many common literary aspects other than both being Fantasy.

Positive Effects: There is a lack of presented queer data regarding
literature and this data would be a stepping point for future projects
to understand how representation is important within communities - the
data covers a spectrum of queer representation but it only a sample.
Some of the queer identities include: asexuality, aromantic, gay,
lesbian, trans and more. The positive effect of this is the initiative
to start, to foster curiosity and awareness of these subjects. If this
project to were be expanded using full Goodreads lists (or attempting to
categorical analyse every book ever uploaded) rather than a sample from
Kandi’s personal profile, the impact would be useful in understanding
the trends within literature over time, if there has been an increase,
speculation on the relationship between queer authors and the works that
they write, and the links to a more international community.

Negative Effects: As the data is taken from a personal account, the
negative repercussions (if there are any) would fall directly on Kandi
due to personal connection. There is a possibility for
misinterpretations within the real world due to the limitations placed
on the data mentioned above.

Minimizing Negative Impacts: Through communicating clearly what the data
includes and does not include, how the personal bias affects the data
collected, hopefully the points of misinterpretations and
misconstructions can be minimized. This project is supposed to represent
the possibilities of analysis that can be done within the literary world
from a queer perspective, and the specifics within queer literature.

## 4. Data analysis plan

#### Correlation of average rating and number of rating

``` r
queer_books_data %>% 
  ggplot(aes( x = num_ratings, y = average_rating)) +
  geom_hex() +
  scale_fill_viridis_b("Number of Books") +
  labs( title = "Correlation of average rating and number of rating",
        subtitle = "Goodread data from 1974 - 2024",
        x = "Number of rating",
        y = "Average rating")
```

<img src="proposal_files/figure-gfm/correlation-rating-numrating-1.png" alt="Point Hexagon graph showing the correlation between the average rating of a selection of 500 books to the number of ratings receieved, the average rating being between 3 - 4.5, and number of ratings going from 1, through to 3e+06 (3 mil/3000,000). The highest rating received with the most number of ratings was 3.9 and 4.1. Dataset only includes 500 observations"  />

``` r
ggsave(filename = "rating_review_correlation.png", width = 10, height = 8)
```

``` r
queer_books_data %>% 
  ggplot(aes( x = num_ratings, y = average_rating)) +
  geom_hex() +
  scale_fill_viridis_b() +
  labs( title = "Correlation of average rating and number of rating",
        subtitle = "Goodread data from 1974 - 2024",
        x = "Number of rating",
        y = "Average rating")+
  xlim(0, 1e+06)
```

    ## Warning: Removed 8 rows containing non-finite outside the scale range
    ## (`stat_binhex()`).

    ## Warning: Removed 17 rows containing missing values or values outside the scale range
    ## (`geom_hex()`).

<img src="proposal_files/figure-gfm/correlation-rating-numrating-below-1mil-1.png" alt="Point Hexagon graph showing the correlation between the average rating of a selection of 500 books to the number of ratings receieved, the average rating being between 3 - 4.5, and number of ratings going from 1, through to 1000000 (1 mil). The highest rating received with the most number of ratings was 3.5 and 4. Dataset only includes 500 observations"  />

``` r
ggsave(filename = "rating_review_correlation-below-1mil.png", width = 10, height = 8)
```

    ## Warning: Removed 8 rows containing non-finite outside the scale range (`stat_binhex()`).
    ## Removed 17 rows containing missing values or values outside the scale range
    ## (`geom_hex()`).

``` r
#Won't be using this graph in the presentation - is there for clarification if necessary
```

#### Check correlation of top rating and number of rating

check whether the high average rating has high number of rating.
Checked: there is no overlap between the average rating and the number
of rating.

``` r
Top_ten_ave <- queer_books_data %>% 
  select(title, average_rating, num_ratings) %>% 
  arrange(desc(average_rating)) %>% 
  slice(1:10)

bottom_ten_ave <- queer_books_data %>% 
  select(title, average_rating, num_ratings) %>% 
  arrange((average_rating)) %>% 
  slice(1:10)

Top_ten_num <- queer_books_data %>% 
  select(title, num_ratings) %>% 
  arrange(desc(num_ratings)) %>% 
  slice(1:10)

top_bottom_ten <- bind_rows(Top_ten_ave, bottom_ten_ave)

# write_csv(top_bottom_ten, file = "top_bottom_ten.csv")
```

#### Compare low and high average rating

``` r
top_bottom_ten <- top_bottom_ten %>% 
  mutate(high_and_low = case_when(title %in% c("The Seemingly Impossible Love Life of Amanda Dean", "No FREE Attention: How Women use The Possibility of Sex to Manipulate Naïve and Lustful Men", "To a Darker Shore", "Nonbinary", "The Midnight Strider (The Chronomancer Chronicles, #2)", "Thirteenth", "The Blue Codex (The Blue Codex, #1)", "Earthflown", "Heartstopper: Volume Four (Heartstopper, #4)", "Crooked Kingdom (Six of Crows, #2)")~"high", title %in% c("The Loveless Princess", "This Song Is (Not) for You", "We Awaken", "Ace of Hearts", "That Inevitable Victorian Thing", "In My Dreams (Aces in Love #1)", "The Once and Future Queen, Vol. 1: Opening Moves", "Before I Let Go", "Overleveled, Underloved", "Coffee Cake (Coffee Cake, #1)")~"low"))
  
top_bottom_ten %>%   
  ggplot(aes(y = average_rating, x = num_ratings, group = high_and_low, color = high_and_low))+
  geom_point() +
  scale_color_manual(values = c("#660066", "#ffcc00")) +
  theme_ipsum() +
  labs(title = "Correlation between Average Rating and Number of Review",
       subtitle = "Comparison of Top and Bottom Average Ratings",
       x = "Average Rating", y = "Number of Reviews",
       color = "Rating group")
```

<img src="proposal_files/figure-gfm/visualise-low-high-rating-1.png" alt="Scatterplot showing correlation between average rating and number of reviews for the top and bottom average rating from the Queer Lit Sample data frame. The graph has 20 points, with the highest rating being 5 and the lowest 2.8. It shows little correlation between the amount of reviews and rating as most of the points are ont the lower end of the nymber of reviews with two exceptions being higher than 300,000 reviews."  />

``` r
ggsave(filename = "top-bottom-correlation.png", width = 10, height = 6)
```

``` r
top_bottom_ten %>%   
  ggplot(aes(y = average_rating, x = num_ratings, group = high_and_low, color = high_and_low))+
  geom_point() +
  scale_color_manual(values = c("#660066", "#ffcc00")) +
  theme_ipsum() +
  xlim(0,1000) +
   labs(title = "Correlation between Average Rating and Number of Review",
       subtitle = "Comparison of Top and Bottom Average Ratings",
       x = "Average Rating", y = "Number of Reviews",
       color = "Rating group")
```

    ## Warning: Removed 4 rows containing missing values or values outside the scale range
    ## (`geom_point()`).

<img src="proposal_files/figure-gfm/zoom-in-visualise-low-high-rating-1.png" alt="Scatterplot showing correlation between average rating and number of reviews for the top and bottom average rating from the Queer Lit Sample data frame. The graph has 16 points, with the highest rating being 5 and the lowest 2.8. Is focused on books that recieved less than 1000 reviews. Both the highest rate and lowest rated recieved less than 100 reviews."  />

``` r
ggsave(filename = "top-bottom-correlation-below-1000reviews.png", width = 10, height = 6)
```

    ## Warning: Removed 4 rows containing missing values or values outside the scale range
    ## (`geom_point()`).

``` r
Top_ten_ave %>% 
  left_join(Top_ten_num, by = "title")
```

    ## # A tibble: 10 × 4
    ##    title                              average_rating num_ratings.x num_ratings.y
    ##    <chr>                                       <dbl>         <dbl>         <dbl>
    ##  1 The Seemingly Impossible Love Lif…           5               16            NA
    ##  2 No FREE Attention: How Women use …           4.91           257            NA
    ##  3 To a Darker Shore                            4.79            19            NA
    ##  4 Nonbinary                                    4.78            51            NA
    ##  5 The Midnight Strider (The Chronom…           4.76            17            NA
    ##  6 Thirteenth                                   4.74            53            NA
    ##  7 The Blue Codex (The Blue Codex, #…           4.7             10            NA
    ##  8 Earthflown                                   4.65           172            NA
    ##  9 Heartstopper: Volume Four (Hearts…           4.61        369882            NA
    ## 10 Crooked Kingdom (Six of Crows, #2)           4.6         625376            NA

#### Mutate year to decade

``` r
queer_books_data <- queer_books_data %>% 
  mutate(year_by_decade = case_when(year_published %in% c("1970","1971", "1972", "1973", "1974","1975", "1976", "1977", "1978", "1979") ~ "1970s",
                                    year_published %in% c("1980","1981", "1982","1983","1984","1985","1986","1987","1988","1989") ~ "1980s",
                                    year_published %in% c("1990","1991","1992","1993","1994","1995","1996","1997","1998","1999") ~ "1990s",
                                    year_published %in% c("2000","2001","2002","2003","2004","2005","2006","2007","2008","2009") ~ "2000s",
                                    year_published %in% c("2010","2011","2012","2013","2014","2015","2016","2017","2018","2019") ~ "2010s",
                                    year_published %in% c("2020","2021","2022","2023","2024") ~ "2020s"))
```

``` r
queer_books_data <- queer_books_data %>% 
  mutate(originalyear_by_decade = case_when(original_publication_year %in% c("1897","1890", "1872","-380","-1200") ~ "<1900s",
                                            original_publication_year %in% c("1910","1911", "1912","1913","1914","1915","1916","1917","1918","1919") ~ "1910s",
                                            original_publication_year %in% c("1920","1921", "1922","1923","1924","1925","1926","1927","1928","1929") ~ "1920s",
                                            original_publication_year %in% c("1930","1931", "1932","1933","1934","1935","1936","1937","1938","1939") ~ "1930s",
                                            original_publication_year %in% c("1940","1941", "1942","1943","1944","1945","1946","1947","1948","1949") ~ "1940s",
                                            original_publication_year %in% c("1950","1951", "1952","1953","1954","1955","1956","1957","1958","1959") ~ "1950s",
                                            original_publication_year %in% c("1960","1961", "1962","1963","1964","1965","1966","1967","1968","1969") ~ "1960s",
                                            original_publication_year %in% c("1970","1971", "1972", "1973", "1974","1975", "1976", "1977", "1978", "1979") ~ "1970s",
                                    original_publication_year %in% c("1980","1981", "1982","1983","1984","1985","1986","1987","1988","1989") ~ "1980s",
                                    original_publication_year %in% c("1990","1991","1992","1993","1994","1995","1996","1997","1998","1999") ~ "1990s",
                                    original_publication_year %in% c("2000","2001","2002","2003","2004","2005","2006","2007","2008","2009") ~ "2000s",
                                    original_publication_year %in% c("2010","2011","2012","2013","2014","2015","2016","2017","2018","2019") ~ "2010s",
                                    original_publication_year %in% c("2020","2021","2022","2023","2024") ~ "2020s"))
```

#### Visualise second and original publication by decade

``` r
queer_books_data %>% 
  ggplot(aes( x = year_by_decade)) +
  geom_bar()+
  labs(title = "Rate of Publication",
       subtitle = "by Decade",
    x = "Publication Decade",
    y = "Number of Books")
```

<img src="proposal_files/figure-gfm/decade-published-graph-1.png" alt="Bar graph showing the number of books published by decade from the 70s, to the 2020s. The order of number of queer books published from lowest to highest: 1970s, NA, 1980s, 1990s, 2020s, 2000s, and 2010s has the highest number of books. Dataset only contains 500 books."  />

``` r
#Won't be using this graph in presentation
```

``` r
queer_books_data %>% 
  ggplot(aes( x = originalyear_by_decade, fill = average_rating)) +
  geom_bar()+
  labs(title = "Original Year of Publication",
       subtitle = "by Decade",
       x = "Original Publication Decade",
       y = "Number of Books")
```

    ## Warning: The following aesthetics were dropped during statistical transformation: fill.
    ## ℹ This can happen when ggplot fails to infer the correct grouping structure in
    ##   the data.
    ## ℹ Did you forget to specify a `group` aesthetic or to convert a numerical
    ##   variable into a factor?

<img src="proposal_files/figure-gfm/first-published-gragh-1.png" alt="Bar graph showing the number of books and the decade they were originally published in from pre 1900s - 2020s, including NA. The order of number of queer books published from lowest to highest: 1930s, 1940s, 1910s, 1920s, &lt;1900s, 1950s/1960s, 1970s, 1980s, NA, 1990s, 2020s, 2000s, and 2010s has the highest. Dataset only contains 500 books."  />

``` r
#Won't be using this graph in the presentation
```

#### Visualise the change of binding’s types by decade

``` r
queer_books_data %>%
  ggplot(aes( x = year_by_decade, fill = binding)) +
  geom_bar(alpha = 0.7) +
  scale_fill_viridis_d("Binding Format") +
  labs(title = "Binding Format Frequency",
       subtitle = "by Decade",
       x = "Decade of Publication", y = "Number of Books") 
```

<img src="proposal_files/figure-gfm/change-binding-dacade-1.png" alt="Bar graph showing the number of books published by decade from the 70s, to the 2020s. The order of number of queer books published from lowest to highest: 1970s, NA, 1980s, 1990s, 2020s, 2000s, and 2010s has the highest number of books. Bar graph color-coded by types of book binding: ARC, Audio CD, ebook, hardcover, Kindle edition, Kindle edition with audio, Mas market paperback, MP3 CD, Paperback,  Dataset only contains 500 books."  />

``` r
ggsave(filename = "binding-format-decade.png", width = 12, height = 8)

#Won't be using this graph in the presentation
```

``` r
queer_books_data %>%
  ggplot(aes( x = originalyear_by_decade, fill = binding)) +
  geom_bar(alpha = 0.7) +
  scale_fill_viridis_d("Binding Format") +
  labs(title = "Binding Format Frequency",
       subtitle = "by Decade",
       x = "Decade of Publication", y = "Number of Books") 
```

<img src="proposal_files/figure-gfm/binding-frequency-orignal-decade-1.png" alt="Bar graph showing the number of books orignally published by decade from pre 1900s (&lt;1900) to the 2020s, including NA. The order of number of queer books published from lowest to highest: 1930s, 1940s, 1910s, 1920s, &lt;1900s, 1950s/1960s, 1970s, 1980s, NA, 1990s, 2020s, 2000s, and 2010s has the highest. Bar graph color-coded by types of book binding: ARC (Advanced Reader Copy), Audio CD, ebook, hardcover, Kindle edition, Kindle edition with audio, Mass-market paperback, MP3 CD, Paperback. Pre 1900s - 1970s only has Paperback and Hardcover, variety of binding format increases as decades progress. NA includes Paperback, Kindle, ebook and ARC. Dataset only contains 500 books."  />

``` r
ggsave(filename = "binding_format_original_decade.png", width = 12, height = 8)
```

#### Visualise the change of binding formats by year

``` r
queer_books_data %>%
  ggplot(aes( x = year_published, fill = binding)) +
  geom_bar(alpha = 0.7) +
  scale_fill_viridis_d()+
  labs(title = "Binding Format Frequency",
       subtitle = "by Year of Publication",
       x = "Publication Year",
       y = "Number of Books")
```

    ## Warning: Removed 2 rows containing non-finite outside the scale range
    ## (`stat_count()`).

<img src="proposal_files/figure-gfm/change-binding-years-1.png" alt="Bar graph showing number of books published per year and color-filled by binding format. The highest number of books was published in 2016, also has the widest variety of binding formats. Variety of binding formats increases across the graph"  />

``` r
ggsave(filename = "binding-format-by-year.png", width = 12, height = 8)
```

    ## Warning: Removed 2 rows containing non-finite outside the scale range
    ## (`stat_count()`).

#### Filter book that got republished

``` r
republished_book <- queer_books_data %>% 
  filter(year_published != original_publication_year)

#ggplot(data = republished_book,
 #      mapping = aes( x = year_published, y = original_published)) +
  #geom_point() ##what would be a good geom to visualize this data. 
```

#### Check top publishers

Look at which publisher has more number of book published.

``` r
queer_books_data %>% 
  count(publisher) %>% 
  arrange(desc(n))
```

    ## # A tibble: 285 × 2
    ##    publisher                                       n
    ##    <chr>                                       <int>
    ##  1 <NA>                                           39
    ##  2 Less Than Three Press                          14
    ##  3 Vintage                                        12
    ##  4 Dreamspinner Press                             10
    ##  5 Little, Brown Books for Young Readers           8
    ##  6 CreateSpace Independent Publishing Platform     7
    ##  7 DAW                                             7
    ##  8 Spectra                                         7
    ##  9 Tor Books                                       7
    ## 10 Ace                                             6
    ## # ℹ 275 more rows

#### Merge genre to primary dataset

Try to make a similar graph for all the genre

``` r
book_genre <- book_genre %>% 
  select("title", "genre_1", "genre_2", "genre_3", "genre_4", "genre_5", "genre_6", "genre_7", "genre_8")


queer_books_genre <- queer_books_data %>% 
  left_join(book_genre, by = c("title" = "title"))
```

    ## Warning in left_join(., book_genre, by = c(title = "title")): Detected an unexpected many-to-many relationship between `x` and `y`.
    ## ℹ Row 248 of `x` matches multiple rows in `y`.
    ## ℹ Row 33 of `y` matches multiple rows in `x`.
    ## ℹ If a many-to-many relationship is expected, set `relationship =
    ##   "many-to-many"` to silence this warning.

``` r
queer_books_genre %>% 
  ggplot(aes(x = fct_rev(fct_infreq(genre_1)), fill = binding)) +
  geom_bar(alpha=0.7) +
  coord_flip() +
  scale_fill_viridis_d("Binding Format") +
  labs( title = "Number of Books per Genre",
        subtitle = "by Binding Format",
        x = "Genre Type", y = "Number of Books")
```

<img src="proposal_files/figure-gfm/book-genre-join-1.png" alt="Bar graph of number of books per genre. Highest number of books is in the fantasy genre, 2nd highest is gay, and then asexual. The lowest is in intersexual, then religion and non-binary. Books are color-coordinated by binding format and there is an even spread of binding format variety across the genres. Dataset only has 500 observations."  />

``` r
ggsave(filename = "books-per-genre-binding-format.png", width = 12, height = 8)
```

#### Categorise the average rating

``` r
queer_books_genre <- queer_books_genre %>% 
  mutate(rating_categories = case_when(str_starts(average_rating, pattern = "2")~"2",
                                       str_starts(average_rating, pattern = "3")~"3",
                                       str_starts(average_rating, pattern = "4")~"4",
                                       str_starts(average_rating, pattern = "5")~"5"))
```

#### Compare the books’ rating of the top publishers

Look at the books’ title published by the top five of most frequent
publishers. Then look at the correlation of these books’ average ratings
and number of ratting.

``` r
Books_and_publishers <- queer_books_genre %>% 
  filter(publisher %in% c("Less Than Three Press", "Vintage", "Dreamspinner Press", "Little, Brown Books for Young Readers", "CreateSpace Independent Publishing Platform", "DAW", "Spectra", "Tor Books", "NA")) 

ggplot(data = Books_and_publishers,
       mapping = aes( y = fct_rev(fct_infreq(publisher)), fill = "rating_categories")) +
  geom_bar() +
  scale_fill_viridis_d() +
  labs(title = "Top Eight Publishers",
       x = "Number of Books", y = NULL) +
  guides(fill = "none")
```

<img src="proposal_files/figure-gfm/books-of-publisher-sum-1.png" alt="Horizontal Bar Graph showing the number of books per the top 8 publishing companies. The highest number of books per publisher is Less Than Three Press with 19 books, the lowest is Tor Books with 7."  />

``` r
ggsave(filename = "top-publishers.png", width = 10, height = 8)

#Won't be using this in presentation
```

#### Check missing data

``` r
vis_miss(queer_books_genre)
```

![](proposal_files/figure-gfm/missing-data-1.png)<!-- -->

``` r
ggsave(filename = "missing-data-all.png", width = 10, height = 8)

#Won't be using this in presentation
```

``` r
queer_books_genre %>% 
  as_shadow_upset() %>% 
  upset()
```

![](proposal_files/figure-gfm/check-na-shadow-1.png)<!-- -->

``` r
#Won't be using this in presentation
```

#### Genres’ average rating

``` r
all_book_genre <- queer_books_genre %>% 
  pivot_longer(cols = genre_1:genre_8, names_to = c("genre_1", "genre_2", "genre_3", "genre_4", "genre_5", "genre_6", "genre_7", "genre_8"), names_pattern = "(_)(_)(_)(_)(_)(_)(_)(_)", values_to = "all_genre", values_drop_na = TRUE) %>% 
  select(!genre_1:genre_8) 

all_book_genre %>% 
  ggplot(aes(x = fct_rev(fct_infreq(all_genre)), fill = rating_categories)) +
  geom_bar() +
  coord_flip() +
  scale_fill_viridis_d("Average Rating") +
  labs(title = "Average Rating per Genre",
       subtitle = "Organised by Binding Format",
       x = "Genre",
       y = "Number of Books")
```

<img src="proposal_files/figure-gfm/genre-rating-1.png" alt="Horizontal bar graph showing the number of books per genre, color-coded by Average Rating. The highest number is romance, with ratings 5, 4 and 3. The lowest is lowest is intersexual with ratings 3 and 4. There is only one rating of 5 within the genres of romance and lesbian, and the one rating of 2 in the asexual and fantasy genres."  />

``` r
ggsave(filename = "Genre-average-rating.png", width = 10, height = 8)
```

#### Books’ genre in each top publishers

``` r
books_publisher_genre <- Books_and_publishers %>% 
   pivot_longer(cols = genre_1:genre_8, names_to = c("genre_1", "genre_2", "genre_3", "genre_4", "genre_5", "genre_6", "genre_7", "genre_8"), names_pattern = "(_)(_)(_)(_)(_)(_)(_)(_)", values_to = "all_genre", values_drop_na = TRUE) %>% 
  select(!genre_1:genre_8) 

books_publisher_genre %>% 
  ggplot(aes(x = fct_rev(fct_infreq(all_genre)), fill = publisher)) +
  geom_bar() +
  coord_flip() +
  scale_fill_viridis_d() +
  labs(title = "Genres within the Top Publishers",
       x = "Genre",y = "Number of Books",
       fill = "Top 8 Publishers")
```

<img src="proposal_files/figure-gfm/top-publishers-genre-1.png" alt="Horizontal bar graph showing the genres within the top 8 publishing companies. The highest number of books per genre is fantasy with 48 books and has all the publishing companies. The lowest is polyamourous with 1, published by Less then Three Press"  />

``` r
ggsave(filename = "books-per-genre-top-publishers.png", width = 10, height = 8)

#Won't be using this graph in the presentation
```

#### Books’ genre in each top publishers by rating

``` r
books_publisher_genre %>% 
  ggplot(aes(x = fct_rev(fct_infreq(all_genre)), fill = publisher)) +
  geom_bar() +
  coord_flip() +
  scale_fill_viridis_d() +
  facet_wrap(~rating_categories) +
  labs(title = "Books' genre and average rating of top publisher",
       x = "genre",
       fill = "average rating")
```

![](proposal_files/figure-gfm/top-publisher-genre-rating-1.png)<!-- -->

``` r
#Won't be using these graphs in the presentation
```

#### Visualise books’ average rating and number of rating in each year by genre (only top publishers’s books)

``` r
books_publisher_genre %>% 
  ggplot(aes(x = all_genre, y = year_published, size = num_ratings, fill = rating_categories)) +
  geom_point(alpha=0.7, shape = 21, color = "black") +
  coord_flip() +
  scale_fill_viridis_d() +
  theme_ipsum() +
  labs(title = "Books' genre and average rating of top publisher",
       x = "Genre",
       y = "Year of Publication",
       color = "Average Rating",
       size = "Number of Reviews")
```

<img src="proposal_files/figure-gfm/genre-toppublish-rating-1.png" alt="Bubble plot showing data from the top 8 publishers. Genre on x-axis, Year of publication of the y-axis. Colour of the bubbles is determined by the Rating (Lowest is 2, Highest is 4), and size of bubble is determined by Number of Revies. The largest bubbles are yellow (rating of 4), published in 2020 in the genres: fantasy, gay, mystery-thriller, queer, and romance. Second largest bubbles are blue (rating of 3), published in 2011 in the genres: fantasy, horror, queer, religio, and romance."  />

``` r
ggsave(filename = "top-publishers-genre-rating-publicationyear.png", width = 10, height = 8)
```

#### Visualise books’ average rating and number of rating in each year by genre (all the books)

``` r
all_book_genre %>% 
  ggplot(aes(x = all_genre, y = year_published, size = num_ratings, fill = rating_categories)) +
  geom_point(alpha=0.7, shape = 21, color = "black") +
  coord_flip() +
  scale_fill_manual(values = c("#ff5dbc", "#21928c", "#fde725", "#440154")) +
  theme_ipsum() +
  labs(title = "Genre categorised by Rating and Number of Reviews",
       subtitle = "Year of Publication",
       x = "Genre",
       y = "Year of Publication",
       fill = "Average rating",
       size = "Number of Reviews") +
  scale_size_continuous(range = c(2, 25))
```

    ## Warning: Removed 5 rows containing missing values or values outside the scale range
    ## (`geom_point()`).

<img src="proposal_files/figure-gfm/genre-rating-year-1.png" alt="Bubble point graph showing all the data from the Queer Lit sample. Genre on the x-axis, publication year on the y-axis. Color of the bubble is determined by Average Rating (2 - 5), and the size of the bubble is by number of reviews from 1mil - 3 mil"  />

``` r
ggsave(filename = "all-data-bubble-graph.png", width = 12, height = 10)
```

    ## Warning: Removed 5 rows containing missing values or values outside the scale range
    ## (`geom_point()`).

``` r
book_genre %>% 
  pivot_longer(cols = genre_1:genre_8, names_to = c("genre_1", "genre_2", "genre_3", "genre_4", "genre_5", "genre_6", "genre_7", "genre_8"), names_pattern = "(_)(_)(_)(_)(_)(_)(_)(_)", values_to = "all_genre", values_drop_na = TRUE) %>% 
  select(!genre_1:genre_8) 
```

    ## # A tibble: 1,664 × 2
    ##    title                       all_genre
    ##    <chr>                       <chr>    
    ##  1 Welcome to Your Afterlife   aromantic
    ##  2 Welcome to Your Afterlife   asexual  
    ##  3 Welcome to Your Afterlife   bisexual 
    ##  4 Welcome to Your Afterlife   fantasy  
    ##  5 Welcome to Your Afterlife   romance  
    ##  6 Hazel's Theory of Evolution aromantic
    ##  7 Hazel's Theory of Evolution asexual  
    ##  8 Hazel's Theory of Evolution fiction  
    ##  9 The Bone People             aromantic
    ## 10 The Bone People             asexual  
    ## # ℹ 1,654 more rows

``` r
#book_genre <- mutate(book_genre, type = genre_all(c("genre_1", "genre_2", "genre_3", "genre_4", "genre_5", "genre_6", "genre_7", "genre_8")))
#  ggplot(aes(x = "all_genre"))+
#  geom_point()
```
