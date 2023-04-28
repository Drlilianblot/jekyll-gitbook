# Values, types and variables

{% embed url="https://youtu.be/z47VfZ8rn9E" %}

## Values

A **value** is one of the basic things a program works with, like a letter or a number. The values we have seen so far are `1`, `2`, and `'Hello, World!'`.

These values belong to different **types** also known as **classes** in Python 3. For example, `2` is an integer, and `'Hello, World!'` is a **string**, so-called because it contains a string of letters. You (and the interpreter) can identify strings because they are enclosed in quotation marks.

The print statement also works for integers.

```bash
>>> print(4) 
 4
>>>
```

If you are not sure what type a value has, the interpreter can tell you.

<pre class="language-bash"><code class="lang-bash"><strong>>>> type('Hello, World!') 
</strong><strong> &#x3C;class 'str'> 
</strong><strong>>>> type(17) 
</strong> &#x3C;class 'int'>
<strong>>>>
</strong></code></pre>

Not surprisingly, strings belong to the type (class) `str` and integers belong to the type (class) `int`. Less obviously, numbers with a decimal point belong to a type called `float`, because these numbers are represented in a format called **floating-point**.

```bash
>>> type(3.2) 
 <class 'float'> 
>>>
```

What about values like `'17'` and `'3.2'`? They look like numbers, but they are in quotation marks like strings.

```bash
>>> type('17') 
 <class 'str'> 
>>> type('3.2') 
 <class 'str'>
>>>
```

They are strings.

When you type a large integer, you might be tempted to use commas between groups of three digits, as in `1,000,000`. This is not a legal integer in Python, but it is legal:

<pre class="language-bash"><code class="lang-bash"><strong>>>> print(1,000,000) 
</strong><strong> 1 0 0 
</strong><strong>>>>
</strong></code></pre>

Well, that's not what we expected at all! Python interprets `1,000,000` as a comma-separated sequence of integers, which it prints with spaces between. This is the first example we have seen of a semantic error: the code runs without producing an error message, but it doesn't do the "right" thing.

## Variables

One of the most powerful features of a programming language is the ability to manipulate **variables**. A variable is a name that refers to a value. An **assignment statement** creates new variables and gives them values:

```bash
>>> message = 'And now for something completely different' 
>>> n = 17 
>>> pi = 3.1415926535897931
>>>
```

This example makes three assignments. The first assigns a string to a new variable named `message`; the second gives the integer `17` to `n`; the third assigns the (approximate) value of $$\pi$$to `pi`.

A common way to represent variables on paper is to write the name with an arrow pointing to the variable's value. This kind of figure is called a **state diagram** because it shows what state each of the variables is in (think of it as the variable's state of mind). This diagram shows the result of the previous example:

<mark style="background-color:red;">\beforefig \centerline{\includegraphics{figs/state2.eps\}} \afterfig</mark>

To display the value of a variable, you can use a print statement:

```bash
>>> print(n) 
 17 
>>> print(pi) 
 3.14159265359
>>>
```

The type of a variable is the type of the value it refers to.

<pre class="language-bash"><code class="lang-bash"><strong>>>> type(message)
</strong> &#x3C;class 'str'> 
<strong>>>> type(n) 
</strong><strong> &#x3C;class 'int'> 
</strong><strong>>>> type(pi) 
</strong><strong> &#x3C;class 'float'>
</strong><strong>>>>
</strong></code></pre>

:information\_source: If you type an integer with a leading zero, you might get a confusing error:

```bash
>>> zipcode = 02492 
                  ^
SyntaxError: invalid token 
```

### Variable names and keywords

Programmers generally choose names for their variables that are meaningful-they document what the variable is used for. Variable names can be arbitrarily long. They can contain both letters and numbers, but they have to begin with a letter. It is legal to use uppercase letters, but it is a good idea to begin variable names with a lowercase letter (you'll see why later). The underscore character `'_'` can appear in a name. It is often used in names with multiple words, such as `my_name` or `airspeed_of_unladen_swallow`.

If you give a variable an illegal name, you get a syntax error:

```bash
>>> 76trombones = 'big parade' 
 SyntaxError: invalid syntax 
>>> more@ = 1000000 
 SyntaxError: invalid syntax 
>>> class = 'Advanced Theoretical Zymurgy' 
 SyntaxError: invalid syntax 
```

`76trombones` is illegal because it does not begin with a letter. `more@` is illegal because it contains an illegal character, `@`. But what's wrong with `class`? It turns out that `class` is one of Python's **keywords**. The interpreter uses keywords to recognise the structure of the program, and they cannot be used as variable names. Python 3 has 33 keywords has shown in the table below

| False  | class    | finally | is       | return |
| ------ | -------- | ------- | -------- | ------ |
| None   | continue | for     | lambda   | try    |
| True   | def      | from    | nonlocal | while  |
| and    | del      | global  | not      | with   |
| as     | elif     | if      | or       | yield  |
| assert | else     | import  | pass     |        |
| break  | except   | in      | raise    |        |

You might want to keep this list handy. If the interpreter complains about one of your variable names and you don't know why, see if it is on this list.

:information\_source:There are two naming conventions used in the Python language. We have already seen the `snake_case` notation where variables name consisting of several words have the words in lowercase separated by an underscore, like `circle_area`. The other convention is `mixedCase`; if the name consists of several words, we concatenate them into one, making the first word lowercase and capitalising the first letter of each subsequent word, like `circleArea`.

## Statements

A statement is a unit of code that the Python interpreter can execute. We have seen two kinds of statements: `print` and **assignment**. When you type a statement in interactive mode, the interpreter executes it and displays the result, if there is one. A script usually contains a sequence of statements. If there is more than one statement, the results appear one at a time as the statements execute.

For example, the script

{% code lineNumbers="true" %}
```python
print(5) 
x = 8 
print(x) 
```
{% endcode %}

produces the output

```bash
5
8
```

The assignment statement produces no output.

## Multiple assignment

As you may have discovered, it is legal to make more than one assignment to the same variable. A new assignment makes an existing variable refer to a new value (and stop referring to the old value).

{% code lineNumbers="true" %}
```python
bruce = 5 
print(bruce) 
bruce = 7 
print(bruce)
```
{% endcode %}

The output of this program is:

```
5 
7 
```

Because the first time `bruce` is printed, its value is 5, and the second time, its value is 7. Here is what **multiple assignment** looks like in a state diagram:

<mark style="background-color:blue;">\beforefig \centerline{\includegraphics{figs/assign2.eps\}} \afterfig</mark>

With multiple assignment it is especially important to distinguish between an assignment operation and a statement of equality. Because Python uses the equal sign (`=`) for assignment, it is tempting to interpret a statement like `a = b` as a statement of equality. **It is not!**

First, equality is a symmetric relation and assignment is not. For example, in mathematics, if $$a = 7$$ then $$7 = a$$. But in Python, the statement `a = 7` is legal and `7 = a` is not. Furthermore, in mathematics, a statement of equality is either true or false, for all time. If $$a = b$$ now, then $$a$$ will always equal $$b$$. In Python, an assignment statement can make two variables equal, but they don't have to stay that way:

{% code lineNumbers="true" %}
```python
a = 5 
b = a # a and b are now equal 
a = 3 # a and b are no longer equal
```
{% endcode %}

The third line changes the value of `a` but does not change the value of `b`, so they are no longer equal. Although multiple assignment is frequently helpful, you should use it with caution. If the values of variables change frequently, it can make the code difficult to read and debug.

## Updating variables

One of the most common forms of multiple assignment is an `update`, where the new value of the variable depends on the old.

```python
x = x+1 
```

This means "get the current value of `x`, add one, and then update `x` with the new value." If you try to update a variable that doesn't exist, you get an error, because Python evaluates the right side before it assigns a value to `x`:

```bash
>>> y = y+1 
 Traceback (most recent call last): 
     File "<pyshell#49>", line 1, in <module> 
       y = y+1 
 NameError: name 'y' is not defined 
```

Before you can update a variable, you have to **initialise** it, usually with a simple assignment:

{% code lineNumbers="true" %}
```python
y = 0 
y = y+1
```
{% endcode %}

Updating a variable by adding 1 is called an **increment**; subtracting 1 is called a **decrement**.

##
