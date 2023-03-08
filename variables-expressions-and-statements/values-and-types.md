# Values and types

A **value** is one of the basic things a program works with, like a letter or a number. The values we have seen so far are `1`, `2`, and `'Hello, World!'`.

These values belong to different **types** also known as **classes** in Python 3. For example, `2` is an integer, and `'Hello, World!'` is a **string**, so-called because it contains a string of letters. You (and the interpreter) can identify strings because they are enclosed in quotation marks.

The print statement also works for integers.

```python
>>> print(4) 
4
```

If you are not sure what type a value has, the interpreter can tell you.

<pre class="language-python"><code class="lang-python"><strong>>>> type('Hello, World!') 
</strong><strong>&#x3C;class 'str'> 
</strong><strong>>>> type(17) 
</strong><strong>&#x3C;class 'int'>
</strong></code></pre>

&#x20;Not surprisingly, strings belong to the type (class) `str` and integers belong to the type (class) `int`. Less obviously, numbers with a decimal point belong to a type called `float`, because these numbers are represented in a format called **floating-point**.

```python
>>> type(3.2) 
<class 'float'> 
```

What about values like `'17'` and `'3.2'`? They look like numbers, but they are in quotation marks like strings.&#x20;

```python
>>> type('17') 
<class 'str'> 
>>> type('3.2') 
<class 'str'>
```

They are strings.

When you type a large integer, you might be tempted to use commas between groups of three digits, as in `1,000,000`. This is not a legal integer in Python, but it is legal:

<pre class="language-python"><code class="lang-python"><strong>>>> print(1,000,000) 
</strong><strong>1 0 0 
</strong></code></pre>

Well, that's not what we expected at all! Python interprets `1,000,000` as a comma-separated sequence of integers, which it prints with spaces between. This is the first example we have seen of a semantic error: the code runs without producing an error message, but it doesn't do the "right" thing.

## Common Built-in data types

### Strings

A string is a **sequence** of characters. You can access the characters one at a time with the bracket operator:

```bash
>>> fruit = 'banana' 
>>> letter = fruit[1] 
```

The second statement selects character number 1 from `fruit` and assigns it to `letter`. The expression in brackets is called an **index**. The index indicates which character in the sequence you want (hence the name). But be careful with indices, you might not get what you expect:

```bash
>>> print(letter)
 a 
```

For most people, the first letter (meaning at position 1) of `'banana'` is `b`, not `a`. But for computer scientists, the index is an offset from the beginning of the string, and the offset of the first letter is zero.

```bash
>>> letter = fruit[0] 
>>> print(letter)
 b 
>>>
```

So `b` is the $$0^{th}$$ letter ("zero-eth") of `'banana'`, `a` is the $$1^{th}$$ letter ("one-eth"), and `n` is the $$2^{th}$$ ("two-eth"") letter.

You can use any expression, including variables and operators, as an index, but the value of the index has to be an integer. Otherwise you get a `TypeError`:

```bash
>>> letter = fruit[1.5] 
TypeError: string indices must be integers
```

#### String slices

A segment of a string is called a **slice**. Selecting a slice is similar to selecting a character:

```bash
>>> s = 'Monty Python' 
>>> print(s[0:5])
 Monty 
>>> print(s[6:12])
 Python 
>>>
```

The operator `[n:m]` returns the part of the string from the `n-eth` character to the `m-eth` character, including the first but excluding the last. This behavior is counter intuitive, but it might help to imagine the indices pointing _between_ the characters, as in the following diagram:

<mark style="background-color:blue;">\beforefig \centerline{\includegraphics{figs/banana.eps\}} \afterfig</mark>

If you omit the first index (before the colon), the slice starts at the beginning of the string. If you omit the second index, the slice goes to the end of the string:

```bash
>>> fruit = 'banana' 
>>> fruit[:2]
 'ba' 
>>> fruit[2:]
 'nana' 
```

If the first index is greater than or equal to the second the result is an **empty string**, represented by two quotation marks:

```bash
>>> fruit = 'banana' 
>>> fruit[3:3] 
 '' 
>>>
```

An empty string contains no characters and has length 0, but other than that, it is the same as any other string.

<details>

<summary>Given that <code>fruit</code> is a string, what does <code>fruit[:]</code> mean?</summary>

**Answer:** It means the entire string assigned to `fruit`, that is `banana`.

</details>

#### Strings are immutable

It is tempting to use the `[ ]` operator on the left side of an assignment, with the intention of changing a character in a string. For example:

```bash
>>> greeting = 'Hello, world!' 
>>> greeting[0] = 'J'
 TypeError: object does not support item assignment
```

The "object" in this case is the string and the "item'' is the character you tried to assign. For now, an **object** is the same thing as a value, but we will refine that definition later. An **item** is one of the values in a sequence. The reason for the error is that strings are **immutable**, which means you can't change an existing string. The best you can do is create a new string that is a variation on the original:

<pre class="language-bash"><code class="lang-bash">>>> greeting = 'Hello, world!' 
>>> new_greeting = 'J' + greeting[1:] 
>>> print(new_greeting)
 Jello, world!
>>> print(greeting)
<strong> Hello, world!
</strong><strong>>>>
</strong></code></pre>

This example concatenates a new first letter onto a slice of `greeting`. It has no effect on the original string.

### Lists

Like a string, a **list** is a sequence of values. In a string, the values are all characters; in a list, they can be any type. The values in a list are called **elements** or sometimes **items**.

There are several ways to create a new list; the simplest is to enclose the elements in square brackets (`[` and `]`):

```bash
>>> numbers = [10, 20, 30, 40] 
>>> frenchCuisine = ['crunchy frog', 'ram bladder', 'lark vomit']
>>>
```

The first example is a list of four integers. The second is a list of three strings. The elements of a list don't have to be the same type. The following list contains a string, a float, an integer, and another list:

```
>>> mixedData = ['spam', 2.0, 5, [10, 20]] 
>>>
```

A list within another list is said to be **nested**. A list that contains no elements is called an **empty list**; you can create one with empty brackets, `[]`. As you might expect, you can assign list values to variables:&#x20;

```bash
>>> cheeses = ['Cheddar', 'Edam', 'Gouda'] 
>>> numbers = [17, 123] 
>>> empty = [] 
>>> print(cheeses, numbers, empty)
 ['Cheddar', 'Edam', 'Gouda'] [17, 123] [] 
>>>
```

#### Lists are mutable

The syntax for accessing the elements of a list is the same as for accessing the characters of a string - the bracket operator. The expression inside the brackets specifies the index. Remember that the indices start at 0:

```bash
>>> print(cheeses[0])
 Cheddar 
>>>
```

Unlike strings, lists are **mutable**. When the bracket operator appears on the left side of an assignment, it identifies the element of the list that will be assigned.

```bash
>>> numbers = [17, 123] 
>>>> numbers[1] = 5 
>>> print(numbers)
 [17, 5]
>>>
```

The one-eth element of `numbers`, which used to be `123`, is now `5`.

You can think of a list as a relationship between indices and elements. This relationship is called a **mapping**; each index "maps to" one of the elements. Here is a state diagram showing `cheeses`, `numbers` and `empty`:

<mark style="background-color:blue;">\beforefig \centerline{\includegraphics{figs/list\_state.eps\}} \afterfig</mark>

Lists are represented by boxes with the word "list" outside and the elements of the list inside. `cheeses` refers to a list with three elements indexed `0`, `1` and `2`. `numbers` contains two elements; the diagram shows that the value of the second element has been reassigned from `123` to `5`. `empty` refers to a list with no elements.  List indices work the same way as string indices:

* Any integer expression can be used as an index.
* If you try to read or write an element that does not exist, you get an `IndexError`.
* If an index has a negative value, it counts backward from the end of the list.

Similarly to the string data type, a list can be sliced:

```bash
>>> numbers = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
>>> numbers[2:5]
 [2, 3, 4]
>>> numbers[3:]
 [3, 4, 5, 6, 7, 8, 9]
>>> numbers[:7]
 [0, 1, 2, 3, 4, 5, 6]
>>>
```

#### List slices

The slice operator also works on lists:

```bash
>>> t = ['a', 'b', 'c', 'd', 'e', 'f'] 
>>> t[1:3]
 ['b', 'c']
>>> t[:4]
 ['a', 'b', 'c', 'd']
>>> t[3:]
 ['d', 'e', 'f'] 
>>>
```

If you omit the first index, the slice starts at the beginning. If you omit the second, the slice goes to the end. So if you omit both, the slice is a copy of the whole list.

```bash
>>> t[:]
 ['a', 'b', 'c', 'd', 'e', 'f'] 
>>>
```

Since lists are mutable, it is often useful to make a copy before performing operations that fold, spindle or mutilate lists.

A slice operator on the left side of an assignment can update multiple elements:

```bash
>>> t = ['a', 'b', 'c', 'd', 'e', 'f'] 
>>> t[1:3] = ['x', 'y'] 
>>> print(t) 
 ['a', 'x', 'y', 'd', 'e', 'f'] 
>>>
```

You can add elements to a list by squeezing them into an empty slice:

```
>>> t = ['a', 'd', 'e', 'f'] 
>>> t[1:1] = ['b', 'c'] 
>>> print(t) 
 ['a', 'b', 'c', 'd', 'e', 'f'] 
>>>
```

And you can remove elements from a list by assigning the empty list to them:

```
>>> t = ['a', 'b', 'c', 'd', 'e', 'f'] 
>>> t[1:3] = [] 
>>> print t 
 ['a', 'd', 'e', 'f'] 
```

But both of those operations can be expressed more clearly with list methods shown in the section ["more on List"](../a-deeper-dive-into-strings-lists-and-tuples/more-on-lists.md#list-methods).

### Tuples

A tuple is a sequence of values. The values can be any type, and they are indexed by integers., so in that respect tuples are a lot like lists. The important difference is that tuples are **immutable** (like Strings).  Syntactically, a tuple is a comma-separated list of values:

<pre class="language-python"><code class="lang-python"><strong>t = 'a', 'b', 'c', 'd', 'e' 
</strong></code></pre>

Although it is not necessary, it is common to enclose tuples in parentheses:

```python
t = ('a', 'b', 'c', 'd', 'e')
```

To create a tuple with a single element, you have to include a final comma:

```bash
>>> t1 = ('a',) 
>>> type(t1) 
 <type 'tuple'> 
>>>
```

Be careful, a value in parentheses is not a tuple:

```bash
>>> t2 = ('a') 
>>> type(t2)
 <type 'str'>
>>>
```

Another way to create a tuple is the built-in function `tuple`. With no argument, it creates an empty tuple:

```bash
>>> t = tuple() 
>>> print(t) 
 ()
>>> 
```

If the argument is a sequence (string, list or tuple), the result is a tuple with the elements of the sequence:

```bash
>>> t = tuple('lupins') 
>>> print(t) 
 ('l', 'u', 'p', 'i', 'n', 's')
>>>
```

Because `tuple` is the name of a built-in function, you should avoid using it as a variable name. Most list operators also work on tuples. The bracket operator indexes an element:

```
>>> t = ('a', 'b', 'c', 'd', 'e') 
>>> print(t[0]) 
 a
```

Similarly to the strings and lists, the slice operator selects a range of elements.

<pre class="language-bash"><code class="lang-bash"><strong>>>> print(t[1:3])
</strong><strong> ('b', 'c') 
</strong><strong>>>> 
</strong></code></pre>

But if you try to modify one of the elements of the tuple, you get an error:

```
>>> t[0] = 'A' 
 TypeError: object doesn't support item assignment
```

You can't modify the elements of a tuple, but you can replace one tuple with another:

```bash
>>> t = ('A',) + t[1:] 
>>> print(t)
 ('A', 'b', 'c', 'd', 'e')
>>>
```

#### Tuple assignment

It is often useful to swap the values of two variables. With conventional assignments, you have to use a temporary variable. For example, to swap `a` and `b`:

{% code lineNumbers="true" %}
```python
temp = a 
a = b 
b = temp
```
{% endcode %}

This solution is cumbersome; **tuple assignment** is more elegant:

{% code lineNumbers="true" %}
```python
a, b = b, a 
```
{% endcode %}

The left side is a tuple of variables; the right side is a tuple of expressions. Each value is assigned to its respective variable. All the expressions on the right side are evaluated before any of the assignments. The number of variables on the left and the number of values on the right **have to be** the same:

```bash
>>> a, b = 1, 2, 3 
 ValueError: too many values to unpack
```

More generally, the right side can be any kind of sequence (string, list or tuple). For example, to split an email address into a user name and a domain, you could write:

```
>>> addr = 'monty@python.org' 
>>> uname, domain = addr.split('@')
```

The return value from `split` is a list with two elements; the first element is assigned to `uname`, the second to `domain`.

```bash
>>> print(uname) 
 monty 
>>> print(domain)
 python.org 
>>>
```

It is recommended to read the [documentation about the `split`](https://python-reference.readthedocs.io/en/latest/docs/str/split.html) "function"[^1] from the string (`str`) data type as it is a very useful function.

### Function `len`

`len` is a built-in function that returns the number of characters in a string or the number of elements in a list or a tuple:

```bash
>>> fruit = 'banana' 
>>> len(fruit)
 6 
>>> even = [0, 2, 4, 6, 8]
>>> len(even)
 5
>>> position = (1, 10, -2)
>>> len(position)
 3
>>>
```

To get the last letter of a string, a list or a tuple you might be tempted to try something like this:

```bash
>>> length = len(fruit) 
>>> last = fruit[length] 
IndexError: string index out of range 
```

The reason for the `IndexError` is that there is no letter in `'banana'` with the index 6. Since we started counting at zero, the six letters are numbered 0 to 5. To get the last character, you have to subtract 1 from `length`:

```bash
>>> last = fruit[length-1] 
>>> print(last)
 a
>>> 
```

Alternatively, you can use negative indices, which count backward from the end of the string. The expression `fruit[-1]` yields the last letter, `fruit[-2]` yields the second to last, and so on.

[^1]: The proper term is "**method**" instead of function. This will be covered when we will be covering Python classes.
