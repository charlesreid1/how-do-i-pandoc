## Filtering Text with Custom Filters

This guide will skip most of the details of 
writing custom filters, since it would rapidly
expand the scope of this tutorial.

However, we include a few notes about how custom
filters work and how to apply them.

### How Custom Filters Work

pandoc converts every document, regardless of structure,
into a universal JSON document structure. This is what 
enables it to convert among formats, and it is also where
any document filters are applied.

To illustrate: imagine we have some abstract custom filter
called `foobar` that will make all bold text underlined 
(for example), and we are applying it when converting
from Markdown to HTML.

The process to apply this filter is as follows:

```
Input fmt --(pandoc)--> JSON --(filter)--> JSON --(pandoc)--> Output fmt 
```

In practice, we can create this pipeline on the 
command line, or from Python.

Also note, it is important for us to use pandoc with the `-s`
(standalone document) flag.

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
Using the abstract `foobar` filter,

```
$ cat index.md | pandoc -s -f gfm -t json | foobar 
```

This can now be passed to pandoc again, and converted
to a different format:

```
$ cat index.md | pandoc -s -f gfm -t json | foobar | pandoc -s -f json -t html -o index.html
```




