
# testbook

<!-- badges: start -->
[![Netlify Status](https://api.netlify.com/api/v1/badges/9a2052c9-6b2c-42b2-bc92-32715076e447/deploy-status)](https://app.netlify.com/sites/hugo-pagedjs-book/deploys)
[![Project Status: Concept – Minimal or no implementation has been done yet, or the repository is only intended to be a limited example, demo, or proof-of-concept.](https://www.repostatus.org/badges/latest/concept.svg)](https://www.repostatus.org/#concept)
<!-- badges: end -->

The goal of testbook is to try and generate a beautiful book as html and PDF using [Hugo](https://gohugo.io/) and [paged.js](https://www.pagedjs.org/). 
It's a proof-of-concept.

The .md files could be created from .Rmd, therefore making this an alternative to the excellent [`bookdown`](https://github.com/rstudio/bookdown).
Compared to creating a gitbook with `bookdown`, one could customize the html website more easily, and use any Hugo feature.

This proof-of-concept is based on the great [hugo-book theme](https://github.com/alex-shpak/hugo-book). 
This repo just adds a bit of setup magic (Netlify config, config/ dir) to work with existing great tools.

The idea is to run two Hugo builds with [different configurations](https://gohugo.io/getting-started/configuration/)

* One of them, `hugo -d public --environment 'website'`, creates the html website with a link to "book.pdf" somewhere, in the public/ folder.
* The second one, `hugo -d public2 --environment 'pdf'`, creates a website with a special page containing _all_ the book content, and potentially a print CSS stylesheet.
* Then that page is printed to PDF using pagedjs-cli and copied as "book.pdf" to public/. `pagedjs-cli public2/all/index.html -o public/book.pdf"`
* The live website uses public so it has the website and the PDF.

Netlify can run all these commands

```toml
[build]
publish = "/public"
command = "hugo -d public --environment 'website' && hugo -d public2 --environment 'pdf' && pagedjs-cli public2/all/index.html -o public/book.pdf"
```

The dependency on pagedjs-cli is indicated with packages.json.

## Further work

If I decide to take this further, that is!

* Actually work on the CSS print sheet.
* Make Katex, Mermaid etc. work for the PDF version.
* Make hugo-book features for ordering/including content work.
* Try and embed a tweet.
* Try the idea with another book theme?
* Write some content from Rmd.

## Related work

To get a paged.js button in your Hugo website (i.e. not pre-generating the PDF, letting the reader do that from their browser) check out the [Hugo paged-js theme](https://gitlab.pagedmedia.org/julientaq/pagedjs-hugo) that you could use as a [theme component](https://gohugo.io/hugo-modules/theme-components/).
