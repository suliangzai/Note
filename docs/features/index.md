# Something about mkdocs

For full documentation visit [mkdocs.org](https://www.mkdocs.org).

## Commands

* `mkdocs new [dir-name]` - Create a new project.
* `mkdocs serve` - Start the live-reloading docs server.
* `mkdocs build` - Build the documentation site.
* `mkdocs -h` - Print help message and exit.

## Project layout

    mkdocs.yml    # The configuration file.
    docs/
        index.md  # The documentation homepage.
        ...       # Other markdown pages, images and other files.

## Code Annotation Examples

### Codeblocks

Some `code` goes here

### Plain codeblock

A plain codeblock:

```
Some code here
```

#### Code for a specific language

Some code with the `py` at the start:

``` py
import tensorflow as tf
def whatever()
```

#### with a title and line number

``` py title="sort.py" linenums="1"
def sort(items):
    for i in range(10):
```

#### highlighting lines

``` py hl_lines="2"
def sort(items):
    for i in range(10):
```

## Icons and Emojs

:smile:

:fontawesome-regular-face-laugh-wink:

:fontawesome-brands-twitter:{ .twitter }

:octicons-heart-fill-24:{ .heart }