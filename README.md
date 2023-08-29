# domed

The `domed` package provides a Pythonic approach for manipulating the DOM structure of a web document.
It is intended for code running in the browser using [pyodide](https://pyodide.org/en/stable/) or [pyscript](https://pyscript.net/).
A typical usage is for single-page applications with dynamically changing page content.
The name is an abbreviation for DOM editing.

The package provides an API that is greatly inspired by the [dominate](https://github.com/Knio/dominate) package.
The main difference is that dominate is intended to run on the server.
It creates a datastructure representing the DOM tree.
This datastructure can then be converted to HTML code as a string, which can be sent to a client.

Domed is intended for running in the browser.
It manipulates the DOM tree directly, without producing any HTML text.
This is achieved by wrapping the Javascript DOM structure with Python objects.

The API allows the user to build the hierarchical structure of a DOM tree using context managers.
It allows setting attributes, and adding event handlers.
Through DOM queries, a suitable parent node for the created structure can be selected.
It also allows a clearing children of a DOM node.

## Installation

See the documentation for installing packages from PyPI in pyodide and pyscript, respectively.

## Usage examples

A typical usage looks as follows:

```
from domed import document
from domed.html import *

with document.query(".body").clear():
    with ol():
        with ul():
            with li("Item 1.1"):
                event_listener("click", lambda _: print("Click"))
            li("Item 1.2")
        with li("Item 2") as item:
            item["id"] = "item2"
        li("Item 3", id = "item3")
```

The first line finds the body element of the document, and clears it of all existing content.
Then, it adds an ordered list under it, each with some list items or sublists.
The item 1.1 shows how to add an event listener, responding to the click event.
Item 2 shows how an attribute of an element can be set after its creation.
Item 3 shows how to set it while creating it.

## Demonstration examples

There is a [playground](https://jakobaxelsson.github.io/domed/playground.html) application in which it is possible to evaluate
snippets of `domed`` code, and see the effects directly in the browser.
It can also be used as a boilerplate for starting new `domed` based projects.

An example of a larger example being build with `domed`` is the [system-of-systems simulator (SoSSim)](https://github.com/jakobaxelsson/sossim).