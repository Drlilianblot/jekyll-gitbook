# Exercises

## Exercise 1

Python provides a built-in function called `len` that returns the length of a string, so the value of `len('allen')` is 5.

Write a function named `right_justify`" that takes a string named `s` as a parameter and prints the string with enough leading spaces so that the last letter of the string is in column 70 of the display.

```sh
>>> right_justify('allen') 
                                                     allen
```

<details>

<summary>Answer</summary>

```python
def rightJustify(s):
    print(' ' * (70 - len(s)) + s)
```

</details>

## Exercise 2

This [exercise ](#user-content-fn-1)[^1]can be done using only the statements and other features we have learned so far.

1. Write a function `two_by_two_grid` that draws a grid like the following:

```
+ - + - +
|   |   |
+ - + - +
|   |   |
+ - + - +
```

{% hint style="info" %}
Hint: to print more than one value on a line, you can print a comma-separated sequence like `print('+', '-').`

In order to build a string spanning several lines, we can use the string character `'\n'` which represents the newline character. The newline character can be embedded in a string, or can be concatenated using the `+` operator as shown in the following examples.
{% endhint %}

```bash
>>> print('line 1 \nline 2')
 line 1 
 line 2 
>>> print('line 1' + '\n' + 'line 2')
 line 1 
 line 2
>>> 
```

A `print` statement all by itself ends the current line and goes to the next line.

<details>

<summary>Answer</summary>

{% code lineNumbers="true" %}
```python
def two_by_two_grid():
    print('+', '-', '+', '-', '+')
    print('|', ' ', '|', ' ', '|')
    print('+', '-', '+', '-', '+')
    print('|', ' ', '|', ' ', '|')
    print('+', '-', '+', '-', '+')


```
{% endcode %}

Note: this is not a very good solution, a better approach is used in the solution for the function `four_by_four_grid.`

</details>

2. Write another function `four_by_four_grid`to draw a similar grid with four rows and four columns.

<details>

<summary>Answer</summary>

{% code lineNumbers="true" %}
```python
def four_by_four_grid():
    oddLine = '+ - ' * 4 + '+\n'
    evenLine = '|   ' * 4 + '|\n'
    grid = (oddLine + evenLine) * 4 + oddLine
    print(grid)
```
{% endcode %}

Note: This solution is better than the one given for the function `two_by_two_grid`. It is important to familiarise ourselves with manipulating string to build the expected output.

</details>

3. Write a more generic function `x_by_y_grid(rows, cols)` that draws a similar grid with `rows` rows and `cols` columns.

<details>

<summary>Answer</summary>

{% code lineNumbers="true" %}
```python
def x_by_y_grid(rows, cols):
    oddLine = '+ - ' * cols + '+\n'
    evenLine = '|   ' * cols + '|\n'
    grid = (oddLine + evenLine) * rows + oddLine
    print(grid)
```
{% endcode %}

Note: once we have written the generic function, we can refactor (rewrite) both the `two_by_two_grid` **and** `four_by_four_grid`to functions by calling the `x_by_y_grid(rows, cols)` function as shown below.

{% code lineNumbers="true" %}
```python
def two_by_two_grid():
    x_by_y_grid(2, 2)
    
def four_by_four_gridto():
    x_by_y_grid(4, 4)
```
{% endcode %}

</details>

[^1]: Based on an exercise in Oualline, _Practical C Programming_, Third Edition, O'Reilly (1997)
