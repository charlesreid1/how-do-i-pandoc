## Filtering Text with Custom Filters

This guide will skip most of the details of 
writing custom filters, since it would rapidly
expand the scope of this tutorial.

However, we include a few notes about how custom
filters work and how to apply them.

## How Custom Filters Work

`pandoc` converts every document, regardless of structure,
into a universal JSON document structure. This is what 
enables it to convert among formats, and it is also where
any document filters are applied.

To illustrate: imagine we have some abstract custom filter
called `foobar` that will make all bold text underlined 
(for example), and we are applying it when converting
from Markdown to HTML.

The process to apply this filter is as follows:

```
Input fmt --(pandoc)--> JSON -- Filter --> JSON --(pandoc)--> Output fmt 
```

In practice, we can create this pipeline on the 
command line, or from Python.

Also note, it is important to use pandoc with the `-s`
(standalone document) flag.

## Writing Custom Filters

See [this example](https://github.com/sergiocorreia/panflute/blob/master/docs/source/_static/fenced-template.py)
for a Panflute filter template.

The important parts of a pandoc filter are:

* **Prepare function** - run once, before the document is filtered. This is
    useful for initializing lists, dictionaries, or files.

* **Finalize function** - run once, after the document has been filtered.
    This is useful for doing something with information extracted from
    the document.

* **Filter actions** - these functions are run once for each chunk of text.
    Each filter action is passed a chunk of text in.
    If a filter action returns nothing, the section of text is left unmodified. 
    Otherwise, the (filtered) text returned by the function is used in its place.
    There can be multiple filter actions per document. 

* **Main function** - this is where the filter is actually applied.

Here is a barebones filter:

```
def main(doc=None):
    return pf.run_filter(action,
                         prepare=prepare, 
                         finalize=finalize,
                         doc=doc)

def prepare(doc):
    pass

def action(elem, doc):
    pass

def finalize(doc):
    pass

if __name__=="__main__":
    main()
```

## Using Custom Filters

### Command Line

Following the example above, let us apply a filter 
while converting `index.md` from github flavored markdown
to HTML.

Start with the initial step, which is markdown to JSON
(include the `-s` flag):

```
$ cat index.md | pandoc -s -f gfm -t json
```

Now this JSON is passed through a filter,
which also returns JSON (more details below).
If we have a `panflute` filter that is in the
file `foobar.py`, it will take JSON input
and return JSON output. We use it like this:

```
$ cat index.md | pandoc -s -f gfm -t json | python foobar.py
```

This will output filtered JSON text. (More on the
filter itself in a moment.)

The output from the filter `foobar.py` can now be passed to
another Pandoc process and converted to a document in the same
or a different format:

```
$ cat index.md | pandoc -s -f gfm -t json | python foobar.py | pandoc -s -f json -t html -o index.html
```

Lastly, if we make `foobar.py` into an executable file called `foobar`
by adding the header `#!/usr/bin/env python` and `chmod +x foobar`,
we can use it as follows:

```
$ cat index.md | pandoc -s -f gfm -t json | foobar | pandoc -s -f json -t html -o index.html
```


### Pypandoc

Custom filters can also be applied using [pypandoc](https://github.com/bebraw/pypandoc), 
a thin Python wrapper for the Pandoc command line client.





