# Basics of Commenting Code

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

According to PEP8, comments should have a maximum length of 72 characters. This is true even if your project changes the max line length to be greater than the recommended 80 characters. You should use two spaces after a sentence-ending period in multi- sentence comments, except after the final sentence. Paragraphs inside a block comment are separated by a line containing a single `#`.

In addition, comments should be complete sentences. The first word should be capitalized, unless it is an identifier that begins with a lower case letter (never alter the case of identifiers!). Furthermore, when writing English, you should follow [Strunk and White](https://faculty.washington.edu/heagerty/Courses/b572/public/StrunkWhite.pdf).

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

Remember that comments are designed for the reader, including yourself, to help guide them in understanding the purpose and design of the software. To that end, [Google Python style guide](https://google.github.io/styleguide/pyguide.html) recommends that&#x20;

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

In "Clean Code: A Handbook of Agile Software Craftsmanship" by Martin, Martin has a rather negative view on comments (not API Documentation). In particular, he list a series of bad habit that should be avoided at all costs. Here is a sub-sample of the thing to be avoided, for the full list please read chapter 4 of "Clean Code: A Handbook of Agile Software Craftsmanship".&#x20;

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
