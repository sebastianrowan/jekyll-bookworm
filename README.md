
# jekyll-bookworm

A bookshelf and book reviews for your Jekyll site, built for [Minima](https://github.com/jekyll/minima), based on [jekyll-book-review](https://github.com/robinmetral/jekyll-book-review). 📚

## In brief

The purpose of this project is to **provide Jekyll users with a simple, hackable template for managing their book reviews **.

It consists in two HTML layouts:

 - [`_layouts/books.html`](https://github.com/subhodeeps/jekyll-bookworm/blob/master/_layouts/books.html) displays a list of books (that is, a virtual bookshelf) that belong to a custom [Jekyll collection](https://jekyllrb.com/docs/collections/)
   - The books are sorted according to the year (specified by the user).
   - The books are further categorised as **Finished**, **Reading**, **Queued**, **Interested**, **Uncategorised**.
 - [`_layouts/review.html`](https://github.com/subhodeeps/jekyll-bookworm/blob/master/_layouts/review.html) displays an individual book review with the book's cover, either self-hosted or imported through the [Open Library Covers API](https://openlibrary.org/dev/docs/api/covers).

It was developed for Minima (the Jekyll default theme) and can be set up on a site running Minima in minutes, but it can also be easily adapted to any theme.


## Don't tell me, show me

Okay, here's [the demo](https://subhodeeps.github.io/jekyll-bookworm/) (on an out-of-the-box Jekyll site running Minima).


## Installation

**Requirements**: a functional Jekyll site.

**Summary** (for the Minima theme)

 1. Set up a custom `books` [collection](https://jekyllrb.com/docs/collections/)
 2. Add the `books.html` and `review.html` layouts to your `_layout` directory
 3. Add the `base_path` to your `_includes` direcotry
 4. Create a books list page with the `books` layout
 5. Write book reviews with the `review` layout

### 1. Set up a custom `books` collection

To get started with custom collections, you need to set them up in your [Jekyll configuration file](https://jekyllrb.com/docs/configuration/).

First, copy this code into your `_config.yml` file in your Jekyll root directory:

```
# Collections
collections:
    books:
        output: true
        permalink: /:collection/:title/

future: true

header_pages:
  - books.md
  - about.md

include:
  - images
```

What it does:
 - Define a new [Jekyll collection](https://jekyllrb.com/docs/collections/) named `books`
 - Specify that each book review should have its own page, and that the reviews' permalink should be [mywebsite.com/books/a-book-i-liked/](https://subhodeeps.github.io/jekyll-bookworm/books/kafka-0n-the-shore/)
 - The `future: true` option will help us list books that we would like to read (that is, books added now with a future date)
 - The `images` directory will store a folder named `covers` containing the book covers.

Then, create a folder named `_books` in your Jekyll root directory. This is where you'll write your book reviews!

For more information about collections, see [Jekyll's amazing docs](https://jekyllrb.com/docs/collections/).

### 2. Add the `books.html` and `review.html` layouts to your `_layouts` directory

This step is pretty straightforward.

Copy the `_layouts` folder at the root of this repo into your Jekyll root directory.

If you have an existing `_layouts` folder in your Jekyll root, simply add in there the two template files, [`books.html`](https://github.com/subhodeeps/jekyll-bookworm/blob/master/_layouts/books.html) and [`review.html`](https://github.com/subhodeeps/jekyll-bookworm/blob/master/_layouts/review.html).

### 3. Add the `base_path` file to your `_includes` directory

This file helps us fetch the base url of the website and is used to display the book covers

Copy the `base_path` filed at the `_includes` directory of this repo into your Jekyll `_includes` directory.


### 4. Create a books list page with the `books` layout

Copy [`books.md`](https://github.com/subhodeeps/jekyll-bookworm/blob/master/books.md) to your root Jekyll directory.

**The front matter:**
 - Make sure to specify `layout: books` in the front matter - this will display your books list
 - Optionally specify a `list_title: My reviews` in the front matter to override the default "Latest reviews"
 - Give a title to your page with `title: Books` and a permalink with `permalink: /books/`

**The contents:**
 - Write anything and it will be displayed before your books list

### 4. Write book reviews with the `review` layout

You're all set up!

Writing a book review works much like [writing a post](https://jekyllrb.com/docs/posts/).

Optionally, copy [`the book review template`](https://github.com/subhodeeps/jekyll-bookworm/blob/master/_books/2018-01-01-book.title.md) to your new `/_books` folder.

**The front matter:**
 - Make sure to specify `layout: review` in the front matter
 - Specify your review's date with `date: YYYY-MM-DD HH:MM:SS` (this will display as the date you've added(?) the book)
 - Specify the book's title: `title: A Great Book`
 - Specify the book's author: `author: My Favourite Writer`
 - Specify the book's publication year: `year: 2018`
 - If you want to display the book's cover image, there are two options:
   1. If you want to **self-host your cover images**: place a cover image in `/assets/covers` and specify your image's file name in front matter with `cover: "2018-01-01-book-cover.jpg"`
   2. If you want to **use the Open Library Covers API to display your cover images**: enter either the book's **Open Library ID** (which you can find on any [Open Library book page](https://openlibrary.org/books/OL7243520M/Strange_case_of_Dr._Jekyll_and_Mr._Hyde.) with for example `olid: OL7243520M` or the book's **ISBN** with for example `isbn: 9780156439619` (warning: some ISBNs do not yet have a listing on the Open Library and won't return a cover image)
   - You can specify your reading progress with `status`. It displays a colour-coded caption depending of the value you have entered, viz., "Finished", "Reading", "Queued", "Interested", and even "Abandoned".
   - you can use `start` and `end` to indicate the date you started and finished the book respectively.

*A few additional notes about book covers:*
 - We recommend using the Open Library API with an Open Library ID
 - Specify only one of either `cover:`, `olid:` or `isbn:`.
 - The review.html layout will first display an image specified with `cover:`, if not look for an Open Library ID, if not look for an ISBN, and if not will not display any cover image
 - In the future the system will support cover import from more varied sources

**The contents:**
 - Write your book review using Markdown! You can insert images, bloquotes, text styling and others. For more information see [the Markdown Cheatsheet](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet)!
