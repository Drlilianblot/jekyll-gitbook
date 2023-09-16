# Exercises

## Exercise 1: printing a grid (revisited)

This [exercise ](#user-content-fn-1)[^1]can be done using only the `print` statements and other features we have learned so far.

1. Write a function `two_by_two_grid` that draws a grid like the following:

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

**Hint:**

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
    for i in range(2):
        print('+', '-', '+', '-', '+')
        print('|', ' ', '|', ' ', '|')
    print('+', '-', '+', '-', '+')
```
{% endcode %}

</details>

2. Write another function `n_by_n_grid(size)` to draw a similar grid with four rows and four columns.

<details>

<summary>Answer</summary>

{% code lineNumbers="true" %}
```python
def n_by_n_grid(size):
    grid = ''
    for row in range(size):
        odd_line = ''
        even_line = ''
        for column in range(size):
            odd_line += '+ - '
            even_line += '|   '
        odd_line += '+\n'
        even_line += '|\n'
        grid += odd_line + even_line
    grid += odd_line
    print(grid)
```
{% endcode %}

Note: This solution is overly complex, and one could wonder if the use of `for` loops is wise. It is important to familiarise ourselves with manipulating string to build the expected output. A more readable implementation of the function is given below:

{% code lineNumbers="true" %}
```python
def n_by_n_grid (size):
    odd_line = '+ - ' * size + '+\n'
    even_line = '|   ' * size + '|\n'
    grid = (odd_line + even_line) * size + odd_line
    print(grid)

```
{% endcode %}

</details>

3. Write a more generic function `x_by_y_grid(rows, cols)` that draws a similar grid with `rows` rows and `cols` columns.

## Exercise 2: Srinivasa Ramanujan infinite series

The brilliant mathematician Srinivasa Ramanujan found an [infinite series](https://www.wikipedia.org/wiki/Pi) that can be used to generate a numerical approximation of $$\pi$$:

$$
\frac{1}{\pi} = \frac{2\sqrt{2}}{9801} \sum^\infty_{k=0} \frac{(4k)!(1103+26390k)}{(k!)^4 396^{4k}}
$$

Write a function `estimate_pi()` that uses this formula to compute and return an estimate of $$\pi$$. It should use a `while` loop to compute terms of the summation until the last term is smaller than `1e-15` (which is Python notation for $$10^{-15}$$). You can check the result by comparing it to `math.pi`.

<details>

<summary>Answer</summary>

You will notice that the solution has two functions. The second function `compute_term(k)` is a convenience function that computes a single term of the series. Convenience functions are used to make the code easier to read. As you can see, the function `estimate_pi()` needs to compute the term of a series in two places (line 11 and 15). Rather than duplicating the code (remember it is bad practice), I have created a function and called it twice.

{% code lineNumbers="true" %}
```python
import math

def estimate_pi():
    """return the apporximation of PI using Srinivasa Ramanujan's 
    infinite series.

    Returns:
        float: the apporximation of PI
    """
    k = 0
    term = compute_term(k)
    inverse_pi = term
    while term > 1e-15:
        k = k + 1
        term = compute_term(k)
        inverse_pi += term
    inverse_pi *= (2 * pow(2, 0.5)) / 9801
    return 1 / inverse_pi


def compute_term(k):
    """compute a single term of the summation of Srinivasa Ramanujan 
    infinite series.

    Args:
        k (int): the index of the term's series

    Returns:
        float: the kth term of the summation
    """
    output = (math.factorial(4*k)* (1103 + 26390 * k))
    output /= pow(math.factorial(k), 4) * pow(396, 4*k)
    return output

```
{% endcode %}

Note also that the index `k` is incremented at the start of the loop (line 14) rather than the end. This is to ensure that the term `k=0` is not computed twice.

Finally, the code is documented via docstring. You can learn more about docstring and documenting your code in the chapter "[Code documentation](../code-documentation/)".



</details>

[^1]: Based on an exercise in Oualline, _Practical C Programming_, Third Edition, O'Reilly (1997)
