## Filtering Text with Pre-Written Filters

Pandoc has multiple command line options that 
apply some useful pre-written filters.

For a list, just run `pandoc --help`.

Here we cover the most useful filters, and how to use them.
Here are a few example filters:

```
$ pandoc --help
pandoc [OPTIONS] [FILES]
                        --strip-empty-paragraphs
                        --extract-media=PATH
                        --eol=crlf|lf|native
                        --wrap=auto|none|preserve
                        --columns=NUMBER
                        --strip-comments
                        --toc, --table-of-contents
                        --toc-depth=NUMBER
                        --no-highlight
                        --highlight-style=STYLE|FILE
                        --syntax-definition=FILE
                        --reference-links
                        --reference-location=block|section|document
                        --default-image-extension=extension
                        --email-obfuscation=none|javascript|references
```


### Extracting Media

A useful filter is the extract media filter.
This filter is applied by adding a command line
flag to the pandoc call:

```plain
$ pandoc --extract-media=doc1_media doc1.docx
```

This creates a folder next to `doc1.docx` 
with the following structure:

```plain
$ ls -R
doc1.docx
doc1_media

./doc1_media:
media

./doc1_media/media:
embedded_image.png
```

