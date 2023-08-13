# Tonc (Community Edition)

This is a community-maintained version of Tonc, the GBA programming tutorial originally written by Jasper Vijn (cearn).

## Setup

You'll need Python 3 + pip.

```sh
# install dependencies
pip install pelican markdown

# clone the repo
git clone git@github.com:gbadev-org/tonc.git
cd tonc

# run the development server
make devserver
```

Then open http://127.0.0.1:8000/toc.html in your browser.


## Converting pages to markdown

Conversion can be done one page at a time.

You can use `pandoc` to get you started:

```sh
cd content/pages

# rename to avoid conflicts in page generation
mv intro.htm intro-old.htm

# run through pandoc minus some extensions to get sane output
pandoc --from=html --to=markdown-fenced_divs-bracketed_spans-escaped_line_breaks-smart --wrap=none -o intro.md intro-old.htm
```

Then, add metadata and replace the table of contents with a `[TOC]` marker:

```md
Title: Introduction to Tonc
Date: 2003-09-01
Modified: 2023-08-13
Authors: Cearn

# ii. Introduction to Tonc

[TOC]
```

Then go through the page and fix anything that's broken.

For example:

*   `<span class="dfn">` should be changed back to `<dfn>` (for some reason pandoc messes this up)

*   Tables and Figures should be replaced with the raw HTML from Tonc.

*   Code blocks should have the correct language set on them (`c`, `asm`, `makefile`)

*   Container tags need a `markdown="1"` attribute adding to them, otherwise the Markdown within won't be rendered. e.g.
  
    ```html
    <div style="margin-left:1.2cm;" markdown> ... </div>
    ```

Once it's in good shape, you can delete the original .htm file.