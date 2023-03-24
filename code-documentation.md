# Code Documentation

## Introduction

When you write code, you write it for two primary audiences: your end-users and developers (including yourself) in your project team. Both audiences are equally important.

There is a surprising amount of passionate debates within the developer community regarding the usefulness or desirability of comments in source code. Should source code include significant comments or none at all or something in-between?

To date, I haven't been able to find a study exploring the benefit (or lack of) of commenting code, and its economic impact (positive or negative). Similarly, I could not find any study exploring the benefits and drawbacks of different standards and approaches to documenting code. In the remainder of the chapter, I will present some best practices as well as several standards used in the Python community.

But first of all, we should have a look at the debate on the use of comments in code, and explore both side of the argument. In his article, <mark style="background-color:red;">Kunk\~\cite{kunk2011}</mark> summarise his thoughts on both side of the argument. Kunk lists three points in favour of using comments.

* **It's important to communicate what the code SHOULD be doing.** \
  ****Comments are required to communicate the intent of the source apart from its functionality. When reading source code, it is extremely difficult to be certain as to what the original author intended. Comments should clearly communicate the developer's intent and if needed, an explanation as to how the source code algorithm accomplishes that intent.
* **Comments show respect for the next developer to read your code.** \
  ****Source code should be written in the way that you yourself would most like to encounter unfamiliar code. It should be well-structured with a clear logic flow, and be both efficient and effective. Comments enhance the readability of the code, so that its intent and approach are immediately apparent with a clean appearance.
* **Comments indicate potential problem areas to avoid.**\
  ****Comments should mention factors that may be of concern for the developer or tester. Boundary conditions, valid argument ranges, and corner cases are all important factors to mention in comments for the benefit of future developers and testers.

In his column, he also lists three point against the use of comments in source code:&#x20;

* **Comments take time and have cost but do not influence runtime behaviour.** \
  ****Clearly, comments are not going to improve runtime performance, they are solely for the benefit of the developers. The creation of comment do take time, and may require additional maintenance when code is changed or re-factored. This obviously add an additional cost to the maintenance. Therefore, the comment must justify its cost by providing a benefit greater than its cost. Bad comments are an unnecessary cost.
* **Comments are not properly maintained.**\
  ****Under time pressure, comments are generally the last thing to be addressed (if at all) and may become out of sync with the current code.
* **Comments may simply be incorrect.**\
  ****Sometimes comments are written by developers that misunderstand the code and reinforce that misunderstanding through incorrect or misleading text. The feeling is that bad comments are worse than no comments.

Kunk concluded that he was generally in the camp in favour of documenting code. He added that comments have values and justifies the cost. However, he also warn that comments need to be maintained with the same diligence as executable source code.

In is column, <mark style="background-color:red;">Vogel\~\cite{vogel2013a}</mark> agrees on the first point from Kunk, that is comments should explain the "why" of the code and stop there. He extended the usefulness of comments to includes description of how inputs and outputs of a method/function are related, and a list of expected "side effects". \
What does he mean by "side effect"? \
A "side effect" is any result from executing the code that isn't reflected in the values that the code returns. For example, deleting a record, sorting a mutable object such as a `list` passed in the parameters.

Vogel also argues that comments (apart from end-user documentation) should be replaced by a ROC (Really Obvious Code) approach, supported by Test Driven Development (TDD) or at least a set of automated test suits, something that will be discussed later in the book.

So where do I stand on the issue of comments. I believe that comments are necessary, but one must strive to write good/useful comments. There are several reasons for this:&#x20;

* **Not all programmers can write really obvious code.** \
  In addition, judging whether code is obvious is a subjective call. What is obvious to one person might be cryptic for another. This is especially true if a novice programmer reads the code of an experienced developer. <mark style="background-color:red;">Mertz\~\cite{mertz2018}</mark> illustrates this point brilliantly. "If you’re like me, you’ve probably opened up old codebases and wondered to yourself, _What in the world was I thinking?_ If you’re having a problem reading your own code, imagine what your users or other developers are experiencing when they’re trying to use or contribute to your code."
* **Comments are not just for code.** \
  They can document important program information such as author, date, license, and copyright details. Although it should be noted this might be a mute point since version control systems are readily available.
* **Comments can be place holders for future work.** \
  This is a useful way to create an outline for a large program. Some Integrated Development Environment (IDE) uses tag within comments to create to-do lists.

In summary, both authors agree that good comments are useful and bad comments should be avoided at all costs. So what are good and bad comments?

Finally, a key message to get from this introduction is perfectly summarised by a quote from "The Elements of Programming Style"<mark style="background-color:red;">\~\cite{Kernighan1982}</mark>:

> Don’t comment bad code -- rewrite it. (Brian W. Kernighan and P. J. Plaugher)

## Why Documenting Your Code Is So Important

Conversely, I’m sure you’ve run into a situation where you wanted to do something in Python and found what looks like a great library that can get the job done. However, when you start using the library, you look for examples, write-ups, or even official documentation on how to do something specific and can’t immediately find the solution.

After searching, you come to realize that the documentation is lacking or even worse, missing entirely. This is a frustrating feeling that deters you from using the library, no matter how great or efficient the code is. Daniele Procida summarized this situation best:

> It doesn’t matter how good your software is, because if the documentation is not good enough, people will not use it. (Daniele Procida)

## Basics of Commenting Code

In general, commenting is describing your code to/for developers. The intended main audience is the maintainers and developers of the code. In conjunction with well-written code, comments help to guide the reader to better understand your code and its purpose and design:

> Code tells you how; Comments tell you why. (Jeff Atwood)

The following section describes how and when to comment your code. Comments are created in Python using the hash sign (`#`) and should be brief statements no longer than a few sentences. Here’s a simple example:

{% code lineNumbers="true" %}
```python
def hello_world(): 
    # A simple comment preceding a simple print statement 
    print("Hello World")
```
{% endcode %}

According to PEP8<mark style="background-color:red;">\cite{PEP0008}</mark>, comments should have a maximum length of 72 characters. This is true even if your project changes the max line length to be greater than the recommended 80 characters. You should use two spaces after a sentence-ending period in multi- sentence comments, except after the final sentence. Paragraphs inside a block comment are separated by a line containing a single `#`.

In addition, comments should be complete sentences. The first word should be capitalized, unless it is an identifier that begins with a lower case letter (never alter the case of identifiers!). Furthermore, when writing English, you should follow Strunk and White <mark style="background-color:red;">\cite{strunk2007elements}</mark>.

If a comment is going to be greater than the comment char limit, using multiple lines for the comment is appropriate:

{% code lineNumbers="true" %}
```python
def hello_long_world(): 
    # A very long statement that just goes on and on and 
    # on and on and never ends until after it's reached 
    # the 80 char limit. 
    print("Hellooooooooooooooooooooooooooooooooooo World")
```
{% endcode %}

Commenting your code serves multiple purposes, including:&#x20;

* **Planning and Reviewing:** When you are developing new portions of your code, it may be appropriate to first use comments as a way of planning or outlining that section of code. **Remember to remove these comments** once the actual coding has been implemented, reviewed, and tested. This is especially true if you are new at coding. This will help you formalise and organise your thoughts before you start coding.

<pre class="language-python"><code class="lang-python"><strong># First step
</strong># Second step
# Third step
</code></pre>

* **Code Description:** Comments can be used to explain the intent of specific sections of code:

<pre><code># Attempt a connection based on previous settings. If
<strong># unsuccessful, prompt user for new settings.
</strong></code></pre>

* **Algorithmic Description:** When algorithms are used, especially complicated ones, it can be useful to explain how the algorithm works or how it’s implemented within your code. It may also be appropriate to describe why a specific algorithm was selected over another.

```
# Using quick sort for performance gains
```

* **Tagging:** The use of tagging can be used to label specific sections of code where known issues or areas of improvement are located. Some examples are: BUG, FIXME, and TODO.

```
# TODO: Add condition for when val is None
```

Comments to your code should be kept brief and focused. Avoid using long comments when possible. Additionally, you should use the following four essential rules as suggested by Jeff Atwood:

* Keep comments as close to the code being documented as possible. Comments that aren’t near their describing code are frustrating to the reader and easily missed when updates are made.
* Don't use complex formatting (such as tables or ASCII figures). Complex formatting leads to distracting content and can be difficult to maintain over time.
* Don't include redundant information. Assume the reader of the code has a basic understanding of programming principles and language syntax.
* Design your code to comment itself. The easiest way to understand code is by reading it. When you design your code using clear, easy-to-understand concepts, the reader will be able to quickly conceptualize your intent.

Remember that comments are designed for the reader, including yourself, to help guide them in understanding the purpose and design of the software. To that end, Google<mark style="background-color:red;">\~\cite{googlepythonstyle}</mark> recommends that&#x20;

* comments must never describe the code. You should Assume the person reading the code knows the language (though not what you're trying to do) better than you do.&#x20;
* The place to have comments is in tricky parts of the code. Complicated operations get a few lines of comments before the operations commence. Non-obvious ones get comments at the end of the line. In addition, to improve legibility, these comments should be at least 2 spaces away from the code.&#x20;
* Furthermore, comments should be as readable as narrative text, with proper capitalization and punctuation. In many cases, complete sentences are more readable than sentence fragments.&#x20;
* Shorter comments, such as comments at the end of a line of code, can sometimes be less formal, but you should be consistent with your style. An example is given below:

{% code lineNumbers="true" %}
```python
# We use a weighted dictionary search to find out where i
# is in the array. We extrapolate position based on the
# largest num in the array and the array size and then do
# binary search to get the exact number.

if i & (i-1) == 0: # True if i is 0 or a power of 2. 
```
{% endcode %}

In<mark style="background-color:red;">\~\cite{martin2008}</mark>, Marting has a rather negative view on comments (not API Documentation). In particular, he list a series of bad habit that should be avoided at all costs. Here is a sub-sample of the thing to be avoided, for the full list please read chapter 4 of<mark style="background-color:red;">\~\cite{martin2008}</mark>.&#x20;

* **Inaccurate comments** are far worse than no comments at all. They delude and mislead.&#x20;
* **Comments Do Not Make Up for Bad Code.** Clear and expressive code with few comments is far superior to cluttered and complex code with lots of comments. Rather than spending time writing comments to explain your code, you should spend that time refactoring your code.
* **Noise comments** state the obvious and provide no new information. For example:&#x20;

```python
output = {} # The output dictionary returned by the 
            # function
```

A better comment would have been:&#x20;

{% code lineNumbers="true" %}
```python
# A dictionary containing the time of each athlete
# taking part in the 200 metre race.
# Key: str
#    The athlete's name
# Value: float
#    The athlete's time in seconds during that race
race_time_200m = {}
```
{% endcode %}

* **Commented-Out code.** If you do not need that code delete it. Others maintaining that piece of code would not know why it is commented, if it is important, or is it here for historical reasons. Overtime, this type of comments accumulate and clutter the source code.&#x20;

## Documenting Code via Python Docstring&#x20;

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

### Google Comments and Docstrings Standard

This section is directly taken from Google's Python style guide<mark style="background-color:red;">\~\cite{googlepythonstyle}</mark>. Some of the elements have been omitted as they were not relevant to the module taught, however the interested reader should have a look at the full documentation.

#### Functions and Methods

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

\begin{pycode}&#x20;

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

#### Modules

Every file should contain license boilerplate. Choose the appropriate boilerplate for the license used by the project (for example, Apache 2.0, BSD, LGPL, GPL)&#x20;
