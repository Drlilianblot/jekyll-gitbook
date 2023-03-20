# Code Format

Perhaps you thought that "getting it working" was the most important part of coding. This is not the case, the most important aspect of your code is about communication. When working as a professional developer, the code that you create today has a good chance of changing in subsequent releases, but the readability of your code will have a profound effect on all the changes that will ever be made. The coding style and readability set precedents that continue to affect maintainability and extensibility long after the original code has been changed beyond recognition. Your style and discipline survives, even though your code does not.

> Code formatting is important. It is too important to ignore and it is too important to treat religiously. \[Robert C. Martin]

The guidelines provided in this chapter are specific to the Python language, and will vary depending on the language used. If you are implementing a project using a different language, you should first look for the conventions specific to that language in addition to conventions set for the given project.

## Coding Conventions - PEP 8

Throughout this book, we will be adding to the conventions described in this chapter. To find these conventions easily, they will be grouped into a single section within a chapter. The title of such sections will contains the keyword PEP. We will be exploring part of the <mark style="background-color:red;">PEP 8\~\cite{PEP0008}</mark> and <mark style="background-color:red;">PEP 257\~\cite{PEP0257}</mark> (Docstring Conventions) where it applies. PEP 8 and PEP 257 were adapted from Guido's original Python Style Guide essay, with some additions from Barry's style guide <mark style="background-color:red;">\[2]</mark>. The Python style guide evolves over time as additional conventions are identified and past conventions are rendered obsolete by changes in the language itself.

Note that many projects have their own coding style guidelines. In the event of any conflicts, such project-specific guides should take precedence for that project. It is essential that conventions within a project remain consistent.

## A Foolish Consistency is the Hobgoblin of Little Minds

One of Guido's key insights is that code is read much more often than it is written. The guidelines provided throughout the booklet are intended to improve the readability of code and make it consistent across the wide spectrum of Python code. As <mark style="background-color:red;">PEP 20\~\cite{PEP0020}</mark> says, "Readability counts".

> Code is more often read than written. \[Guido Van Rossum]

A style guide is about consistency. Consistency with the PEP 8 style guide is important. Consistency within a project is more important. Consistency within one module or function is the most important.

{% hint style="info" %}
However, know when to be inconsistent -- sometimes style guide recommendations just aren't applicable. When in doubt, use your best judgement. Note, this is beyond the scope of what you will be learning in your first year at University.&#x20;
{% endhint %}

## Code Layout

* **Indentation:** Use 4 spaces per indentation level.
* **Tabs or Spaces?** Spaces are the preferred indentation method. Tabs should be used solely to remain consistent with code that is already indented with tabs. Python 3 disallows mixing the use of tabs and spaces for indentation.&#x20;
* **Maximum Line Length:** Limit all lines to a maximum of 79 characters. For flowing long blocks of text with fewer structural restrictions (docstrings or comments), the line length should be limited to 72 characters. Limiting the required editor window width makes it possible to have several files open side-by-side, and works well when using code review tools that present the two versions in adjacent columns.\
  The default wrapping in most tools disrupts the visual structure of the code, making it more difficult to understand. The limits are chosen to avoid wrapping in editors with the window width set to 80, even if the tool places a marker glyph in the final column when wrapping lines. Some web based tools may not offer dynamic line wrapping at all.\
  The preferred way of wrapping long lines is by using Python's implied line continuation inside parentheses, brackets and braces. Long lines can be broken over multiple lines by wrapping expressions in parentheses. These should be used in preference to using a backslash for line continuation.

### **Should a Line Break Before or After a Binary Operator?**

For decades the recommended style was to break after binary operators. But this can hurt readability in two ways: the operators tend to get scattered across different columns on the screen, and each operator is moved away from its operand and onto the previous line. Here, the eye has to do extra work to tell which items are added and which are subtracted:

{% code lineNumbers="true" %}
```python
# No: operators sit far away from their operands
income = (gross_wages + 
          taxable_interest + 
          (dividends - qualified_dividends) - 
          ira_deduction - 
          student_loan_interest) 
```
{% endcode %}

To solve this readability problem, mathematicians and their publishers follow the opposite convention. Donald Knuth explains the traditional rule in his Computers and Typesetting series: "Although formulas within a paragraph always break after binary operations and relations, displayed formulas always break before binary operations" <mark style="background-color:red;">\[3]</mark>.

Following the tradition from mathematics usually results in more readable code:

{% code lineNumbers="true" %}
```python
# Yes: easy to match operators with operands
income = (gross_wages 
          + taxable_interest 
          + (dividends - qualified_dividends) 
          - ira_deduction 
          - student_loan_interest)
```
{% endcode %}

In Python code, it is permissible to break before or after a binary operator, as long as the convention is consistent locally. For new code Knuth's style is suggested.

### Whitespace in Expressions and Statements

* Avoid extraneous whitespace. For example, more than one space around an assignment (or other) operator to align it with another.

{% code lineNumbers="true" %}
```python
#Yes: 
x = 1 
y = 2 
long_variable = 3

#No: 
x             = 1 
y             = 2 
long_variable = 3
```
{% endcode %}

* Avoid trailing whitespace anywhere. Because it's usually invisible, it can be confusing: e.g. a backslash followed by a space and a newline does not count as a line continuation marker. Some editors don't preserve it and many projects (like CPython itself) have pre-commit hooks that reject it.
* Always surround these binary operators with a single space on either side: assignment (`=`), augmented assignment (`+=`, `-=` etc.), comparisons (`==`, `<`, `>`, `!=`, `<>`, `<=`, `>=`, `in`, `not in`, `is`,\
  &#x20;`is not`), Booleans (`and`, `or`, `not`).
* If operators with different priorities are used, consider adding whitespace around the operators with the lowest priority(ies). Use your own judgment; however, never use more than one space, and always have the same amount of whitespace on both sides of a binary operator.

```
#Yes: 
i = i + 1 
submitted += 1 
x = x_2 - 1 
hypot2 = x_x + y*y 
c = (a+b) * (a-b)

#No: 
i=i+1 
submitted +=1 
x = x * 2 - 1 
hypot2 = x * x + y * y 
c = (a + b) * (a - b)
```

### Variable Names

Variable names should be lowercase, with words separated by underscores as necessary to improve readability.

**mixedCase** is allowed only in contexts where that's already the prevailing style (e.g. threading.py), to retain backwards compatibility.

{% hint style="info" %}
When using acronyms in mixedCase, capitalize all the letters of the acronym. Thus HTTPServerError is better than httpServerError.&#x20;
{% endhint %}
