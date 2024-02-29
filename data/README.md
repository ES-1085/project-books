# data


```{r load-data}

queer_books_data <- read_excel("../data/queer-books_all.xlsx")

```

```{r glimpse-data-frame}
glimpse(queer_books_data)
```
Rows: 500
Columns: 16
$ id                          <dbl> 58155951, 61780641, 28165393, 34376899, 58357901, …
$ Title                       <chr> "The Farthest Place", "A Tearful Dozen", "Vigilanc…
$ Author                      <chr> "E. Barnes", "Kieran Frank", "Alex Kost", "Ash Gra…
$ `Author l-f`                <chr> "Barnes, E.", "Frank, Kieran", "Kost, Alex", "Gray…
$ `Additional Authors`        <chr> NA, NA, NA, NA, NA, "Sara Parker", NA, NA, "Emily …
$ ISBN                        <chr> NA, NA, NA, NA, NA, "6.92545069E8", NA, "1.5236338…
$ ISBN13                      <dbl> NA, NA, NA, NA, NA, 9.780693e+12, NA, 9.781524e+12…
$ `Average Rating`            <dbl> 4.33, 4.33, 4.00, 4.00, 3.33, 4.43, 4.30, 4.70, 4.…
$ `Num Ratings`               <dbl> 3, 3, 4, 5, 6, 7, 10, 10, 11, 13, 15, 15, 16, 17, …
$ Publisher                   <chr> NA, "JMS Books LLC", NA, "Amazon Digital Services …
$ Binding                     <chr> "Kindle Edition", "Kindle Edition", "ebook", "Kind…
$ `Number of Pages`           <dbl> 218, 38, NA, 385, NA, 38, 261, 284, NA, 260, NA, N…
$ `Year Published`            <dbl> 2021, 2022, 2016, 2017, 2021, 2015, 2020, 2016, 20…
$ `Original Publication Year` <dbl> NA, 2022, NA, 2017, NA, NA, NA, 2016, 2023, 1987, …
$ `Exclusive Shelf`           <chr> "queer-books_all", "queer-books_all", "queer-books…
$ republished_book            <lgl> TRUE, TRUE, TRUE, TRUE, TRUE, TRUE, TRUE, TRUE, TR…

## name of data file

Codebook

id: Book number

title: Book title

author: Book author

author_l-f: Book author last name and then first name

additional_authors: Additional author beside the first author

ISBN: Book identifier number

ISBN_13: Book identifier number with 13-digits long

average_rating: Book average rating 

num-rating: Total number of rating 

publisher: Book publisher

binding: Book binding type

number_of_pages: Number of pages of the book

year_published: Book’s year published (first and/or latest publication)

original_publication_year: First publication year

exclusive_shelf: file name

Codebook- Genres
aromantic: book containing aromantic themes, characters, relationships

asexual: book containing asexual and a-spectrum (demi-sexual, gray-sexual ect) themes, characters, relationships

bisexual: book containing bisexual themes, characters, relationships

dystopian: books including one of the following: dystopian, futuristic, science-fiction, speculative fiction, alien

fantasy: books including the following: fantasy, High-Fantasy, Science-Fiction Fantasy, Magic, Paranormal, Urban Fantasy, Supernatural

fiction: books that didn't contain any of the other genres, including Historical Fiction, poetry, short stories, Contemporary, Anthologies, Fiction Essays, Graphic Novels

gay: books including themes of homosexuality pertaining to male and male relationships, characters identifying as gay

horror: books including one of the following genres: Horror, Paranormal, Dark Fantasy, Supernatural, thriller, Gothic

intersexual: books containing intersexual themes, characters, relationships

lesbian: books including themes of homosexuality pertaining to female and female relationships, characters identifying as lesbian

mystery-thriller: books including one of the following genres: mystery, thriller, crime, investigation, detective

non-binary: books that don't fall within the gender binary of just male or female, and includes themes of:queer, genderfluid, trans, intersexual, agender, involves characters who identify as non-binary, could also invlove themes of gender discussion and gender exploration

non-fiction: books that are not fictional

polyamourous: books containing polyamoruous themes, characters, relationships

queer: books that are categorized generally, include multiple facets of queerness, and are hard to define into a singular generalisation already considered in the other genres

queer-platonic: books containing relationships that are not strictly sexual or romantic 

religion: books containing religious themes, characters including Christianity, Buddhism, Muslim, Hindi or containing religious themes: demons, angels, deities, gods, old-religions, balasura, 

romance: books that include romance 

trans: books containing transgender and transexual themes, characters, relationships, discussions
