## Converting Text

To use pandoc to convert text, specify an output file, then feed it input files.
You can also specify input and output formats, and use some basic pandoc flags 
to control how the process goes.

To specify an output file, use the `-o` or `--output` flag.

All other file names passed on the command line are interpreted as input files.

For example, to convert text to HTML, we can either convert the text 
into a fragment of HTML, or into a full, standalone document using the `-s`
or `--standalone` flag:

```
$ pandoc -o output.html input.txt       # generate a fragment of html
$ pandoc -s -o output.html input.txt    # generate a standalone html document
```

To specify formats, use the `-t` or `--to` flag, and the `-f` or `--from` flag.
For example, converting from Github-flavored Markdown (gfm) to HTML looks like:

```
$ pandoc -f gfm -t html -o my_cool_html_file.html my_cool_markdown_file.md
```

See [list of formats](http://pandoc.org/MANUAL.html#options).

If no output file is specified, output will go to stdout. 
This enables pandoc to be chained together with other tools
into pipelines.

In that spirit, input to pandoc can also come from stdin.
To make pandoc a component of a data pipeline, simply feed
input from stdin and pipe output from stdout:

```
$ cat my_cool_markdown_file.md | pandoc -f gfm -t html | ...
```

We can also generate and convert documents on the fly from the command line:

```plain
$ echo "# Hello World

[this is the earth](https://earth.com)" | pandoc -f gfm -t html

<h1 id="hello-world">Hello World</h1>
<p><a href="https://earth.com">this is the earth</a></p>
```

