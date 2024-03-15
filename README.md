Queer Lit Sample
================
Asy Xaytouthor & Kandi Grey

## Summary

Introduction: “We are what we read.” ~Bob Procter Goodreads is a site
and a tool used by people to categorise books they have written and
read. Goodreads has different ways to help users categorise books; I
(Kandi) created a ‘bookshelf’ to collect books from Lists that other
Goodreads users supplied. Having collected a sample of 500 books from
several Queer Literature lists to create the dataset we are using.

Goodreads is a site and a tool used by people to categorise books they
have written and read. Goodreads has different ways to help users
categorise books; the dataset is a ‘bookshelf’ I created to collect
books from Lists that other Goodreads users supplied. The reason why we
called it a sample is because there are only 500 books in this dataset.
500 books from the thousands that Goodreads has catalogued. Goodreads
has a rating and review system. A book can receive a rating from 0 - 5
stars, and the site automatically calculates the average rating from the
number of reviews it receives. To cross-examine the data, we also
factored in other variables, such as year of publication, categorised
genre, and binding formats. Using this data, we can examine the
correlation between the Average Rating and the Number of Reviews
received. But why queer literature specifically? The biggest reason is
because representation matters. There has been an increase in literature
released since the beginning of the century that isn’t just queer-coded
but has openly explicitly open characters, authors and themes
surrounding the LGBTQIA+ community. However, there is very little close
analysis of this new era of literature. That is what this project is
about - creating a starting point for a more close analysis of queer
literature.

Summary of our findings:

There is a very low correlation between the number of ratings and the
average rating in the dataset, which is the main question we are trying
to answer. To better understand the dataset, we also visualized other
variables such as year of publication, genre, and binding formats. While
the data was quite limited, these visualizations show some changes such
as the increase in number of books being published and the binding
format variety. It would be interesting to see similar visualizations
from the larger dataset. Furthermore, we are also would love to explore
other observations which were not available in this dataset such as
language, regions, and authors’ connection to queer community to gaze
how these factors influenced the literature and audience perception.

If we had more time: Gather a better and more inclusive dataset. Not
only from Kandi’s profile Include more variables such as language,
region the book is based on, region of publication, author background
(their connection with queer)

## Presentation

Our presentation can be found through this link:
<https://docs.google.com/presentation/d/1qIJJHtU8hIAJwpQz-tUzTOcdRspPrZIyEw6bnuUkJvg/edit?usp=sharing>.

## Data

``` r
library(readxl)

queer_books_data <- read_excel("./data/queer-books_data.xlsx")
book_genre <- read_excel("./data/data_genre (1).xlsx")
```

## References

Goodreads (Exported Feb 29th, 2024):
<https://www.goodreads.com/review/list/59261401-kandi-grey?shelf=queer-books_all>
Penguins:
<https://www.penguin.co.uk/articles/2023/06/fiction-lgbtq-history-novels>
Other Goodreads Lists: Queer History Books:
<https://www.goodreads.com/shelf/show/queer-history>
