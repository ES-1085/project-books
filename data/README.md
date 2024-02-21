# data


```{r load-data}

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

```{r glimpse-data-frame}
glimpse(queer_books_data)
```

## name of data file

- `variable1`: Description of variable 1
- `variable2`: Description of variable 2
- `variable3`: Description of variable 3
- ...
