# How Do I Pandoc?

A simple explanation of how to use pandoc, the C-3PO of documents.

Pandoc is a command line tool written in Haskell. It knows many different
dialects of document, so it is capable of extracting the content of 
documents in one format and converting them into another format.

Some examples: markdown, github-flavored markdown, reStructured text,
HTML, docx, OpenOffice.Org document format, etc.

It is also possible to write filters for pandoc to process text
in customized ways (e.g., extract all links in a document, or 
create a table of contents, or turn bold text into strikethrough
text).


## Installing

Available through most package managers. See [installing pandoc](http://www.pandoc.org/installing.html)
page in the pandoc documentation.

```
$ brew install pandoc

$ apt-get install pandoc
```

## Quickstart

There is a nice [getting started guide](http://pandoc.org/getting-started.html) 
in the pandoc documentation for those unfamiliar with command-line tools.

There is also a [user's guide](http://pandoc.org/MANUAL.html) that shows
basic usage of pandoc as a command line tool.

## Common Operations

There are a few common operations with pandoc:

* [Converting text](converting.md) from one format to another (basic)
* [Filtering text with pre-written filters](filtering_pre.md) (intermediate)
* [Filtering text with custom filters](filtering_custom.md) (advanced)
* Some combination of above

There are two ways to use pandoc, covered in each section:

* Pandoc command line tool - `pandoc` command
* Pypandoc API wrapper - [`pypandoc`](https://github.com/bebraw/pypandoc) library









