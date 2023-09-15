# Exercises

## Exercise 1: printing a grid (revisited)

This [exercise ](#user-content-fn-1)[^1]can be done using only the statements and other features we have learned so far.

1. Write a function `twoByTwoGrid` that draws a grid like the following:

```
+ - + - +
|   |   |
+ - + - +
|   |   |
+ - + - +
```

{% hint style="info" %}
This time, you should use iteration
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
def twoByTwoGrid():
    print('+', '-', '+', '-', '+')
    print('|', ' ', '|', ' ', '|')
    print('+', '-', '+', '-', '+')
    print('|', ' ', '|', ' ', '|')
    print('+', '-', '+', '-', '+')


```
{% endcode %}

Note: this is not a very good solution, a better approach is used in the solution for the function `fourByFourGrid.`

</details>

2. Write another function `fourByFourGrid` to draw a similar grid with four rows and four columns.

<details>

<summary>Answer</summary>

{% code lineNumbers="true" %}
```python
def fourByFourGrid ():
    oddLine = '+ - ' * 4 + '+\n'
    evenLine = '|   ' * 4 + '|\n'
    grid = (oddLine + evenLine) * 4 + oddLine
    print(grid)
```
{% endcode %}

Note: This solution is better than the one given for the function `twoByTwoGrid`. It is important to familiarise ourselves with manipulating string to build the expected output.

</details>

3. Write a more generic function `xbyYGrid(rows, cols)` that draws a similar grid with `rows` rows and `cols` columns.

## Exercise 2: Srinivasa Ramanujan infinite series

The brilliant mathematician Srinivasa Ramanujan found an [infinite series](https://www.wikipedia.org/wiki/Pi) that can be used to generate a numerical approximation of $$\pi$$:

$$
\frac{1}{\pi} = \frac{2\sqrt{2}}{9801} \sum^\infty_{k=0} \frac{(4k)!(1103+26390k)}{(k!)^4 396^{4k}}
$$

Write a function `estimatePI()` that uses this formula to compute and return an estimate of $$\pi$$. It should use a `while` loop to compute terms of the summation until the last term is smaller than `1e-15` (which is Python notation for $$10^{-15}$$). You can check the result by comparing it to `math.pi`.

<details>

<summary>Answer</summary>



</details>

[^1]: Based on an exercise in Oualline, _Practical C Programming_, Third Edition, O'Reilly (1997)
