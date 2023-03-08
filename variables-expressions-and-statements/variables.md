# Variables

## Variables

One of the most powerful features of a programming language is the ability to manipulate **variables**. A variable is a name that refers to a value. An **assignment statement** creates new variables and gives them values:

```python
>>> message = 'And now for something completely different' 
>>> n = 17 
>>> pi = 3.1415926535897931
```

This example makes three assignments. The first assigns a string to a new variable named  `message`; the second gives the integer `17` to `n`; the third assigns the (approximate) value of $$\pi$$to `pi`.

A common way to represent variables on paper is to write the name with an arrow pointing to the variable's value. This kind of figure is called a **state diagram** because it shows what state each of the variables is in (think of it as the variable's state of mind). This diagram shows the result of the previous example:

<mark style="background-color:red;">\beforefig \centerline{\includegraphics{figs/state2.eps\}} \afterfig</mark>

To display the value of a variable, you can use a print statement:

```python
>>> print(n) 
17 
>>> print(pi) 
3.14159265359
```

&#x20;The type of a variable is the type of the value it refers to.

<pre class="language-python"><code class="lang-python"><strong>>>> type(message)
</strong><strong>&#x3C;class 'str'> 
</strong><strong>>>> type(n) 
</strong><strong>&#x3C;class 'int'> 
</strong><strong>>>> type(pi) 
</strong><strong>&#x3C;class 'float'>
</strong></code></pre>

:information\_source: If you type an integer with a leading zero, you might get a confusing error:

```python
>>> zipcode = 02492 
                  ^
SyntaxError: invalid token 
```

## Variable names and keywords

Programmers generally choose names for their variables that are meaningful-they document what the variable is used for. Variable names can be arbitrarily long. They can contain both letters and numbers, but they have to begin with a letter. It is legal to use uppercase letters, but it is a good idea to begin variable names with a lowercase letter (you'll see why later). The underscore character `'_'` can appear in a name. It is often used in names with multiple words, such as `my_name` or `airspeed_of_unladen_swallow`.

If you give a variable an illegal name, you get a syntax error:

```
>>> 76trombones = 'big parade' 
SyntaxError: invalid syntax 
>>> more@ = 1000000 
SyntaxError: invalid syntax 
>>> class = 'Advanced Theoretical Zymurgy' 
SyntaxError: invalid syntax 
```

`76trombones` is illegal because it does not begin with a letter.  `more@` is illegal because it contains an illegal character, `@`. But what's wrong with `class`? It turns out that  `class` is one of Python's  **keywords**. The interpreter uses keywords to recognise the structure of the program, and they cannot be used as variable names. Python 3 has 33 keywords has shown in the table below

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

A statement is a unit of code that the Python interpreter can execute. We have seen two kinds of statements: `print` and **assignment**.  When you type a statement in interactive mode, the interpreter executes it and displays the result, if there is one. A script usually contains a sequence of statements. If there is more than one statement, the results appear one at a time as the statements execute.

For example, the script

{% code lineNumbers="true" %}
```python
print(1) 
x = 2 
print(x) 
```
{% endcode %}

produces the output

```
1
2
```

The assignment statement produces no output.
