# Documenting Code via Python Docstring

Documenting code is describing its use and functionality to your users. While it may be helpful in the development process, the main intended audience is the users.

Python uses documentation string (docstring) to document code. A docstring is a string that is the first statement in a package, module, class or function. The docstring is a special attribute of the object (`object.`**`doc`**) and, for consistency, is surrounded by triple double quotes (per PEP 257<mark style="background-color:red;">\~\cite{PEP0257}</mark>). These strings can be extracted automatically by `pydoc` (try running pydoc on your module to see how it looks.).

A docstring should be organized as a summary line (one physical line) terminated by a period, question mark, or exclamation point, followed by a blank line, followed by the rest of the docstring starting at the same cursor position as the first quote of the first line (see example below).

```python
"""This is the form of a docstring.
It can be spread over several lines.
""" 
```

Although it may seems obvious it is worth reiterating the Google Python style guide<mark style="background-color:red;">\~\cite{googlepythonstyle}</mark> recommendation to pay attention to punctuation, spelling, and grammar; it is easier to read well-written comments than badly written ones.&#x20;

The selection of the docstring format is up to you, but you should stick with the same format throughout your document/project.

## Google Comments and Docstrings Standard

This section is directly taken from Google's Python style guide<mark style="background-color:red;">\~\cite{googlepythonstyle}</mark>. Some of the elements have been omitted as they were not relevant to the module taught, however the interested reader should have a look at the full documentation.

### Functions and Methods

In this section, "function" means a method or a function. A function must have a docstring, unless it meets all of the following criteria:&#x20;

* not externally visible&#x20;
* very short&#x20;
* obvious

A docstring should give enough information to write a call to the function without reading the function's code. The docstring should be descriptive (`"""Fetches rows from a Bigtable."""`) rather than imperative (`"""Fetch rows from a Bigtable."""`). A docstring should describe the function's calling syntax and its semantics, **not its implementation**. For tricky code, comments alongside the code are more appropriate than using docstrings.

Certain aspects of a function should be documented in special sections, listed below. Each section begins with a heading line, which ends with a colon. Sections should be indented two spaces, except for the heading.

* **Args:** List each parameter by name. A description should follow the name, and be separated by a colon and a space. If the description is too long to fit on a single 80-character line, use a hanging indent of 2 or 4 spaces (be consistent with the rest of the file). \
  The description should include required type(s) if the code does not contain a corresponding type annotation. If a function accepts `*args` (variable length argument lists) and/or `**kwargs` (arbitrary keyword arguments), they should be listed as `*args` and `**kwargs`.
* **Returns:** Describe the type and semantics of the return value. If the function only returns `None`, this section is not required. It may also be omitted if the docstring starts with Returns or Yields (e.g. `"""Returns row from Bigtable as a tuple of strings."""`) and the opening sentence is sufficient to describe return value.&#x20;
* **Raises:** List all exceptions that are relevant to the interface.&#x20;

An example is given below:

{% code lineNumbers="true" %}
```python
def fetch_bigtable_rows( 
        big_table, 
        keys, 
        other_silly_variable=None): 
    """Fetches rows from a Bigtable.
    Retrieves rows pertaining to the given keys from the 
    Table instance represented by big_table.  Silly things
    may happen if other_silly_variable is not None.
    
    Args:
        big_table: An open Bigtable Table instance.
        keys: A sequence of strings representing the key
            of each table row to fetch.
        other_silly_variable: Another optional variable, 
            hat has a much longer name than the other 
        args, and which does nothing.

    Returns:
        A dict mapping keys to the corresponding table 
        row data fetched. Each row is represented as a
        tuple of strings. For example:

        {'Serak': ('Rigel VII', 'Preparer'),
         'Zim': ('Irk', 'Invader'),
         'Lrrr': ('Omicron Persei 8', 'Emperor')}

        If a key from the keys argument is missing from 
        the dictionary, then that row was not found in 
        the table.

    Raises:
        IOError: An error occurred accessing the 
            bigtable.Table object.
    """
```
{% endcode %}

### Modules

Every file should contain license boilerplate. Choose the appropriate boilerplate for the license used by the project (for example, Apache 2.0, BSD, LGPL, GPL)&#x20;
