# Exercises

## **Exercise 1**&#x20;

Draw a stack diagram for the following program. What does the program print?

{% code lineNumbers="true" %}
```python
def b(z): 
    prod = a(z, z) 
    print(z, prod)
    return prod
    
def a(x, y): 
    x = x + 1 
    return x * y

def c(x, y, z): 
    sum = x + y + z 
    pow = b(sum)**2 
    return pow
    
x = 1 
y = x + 1 
print c(x, y+3, x+y)
```
{% endcode %}

<details>

<summary>Answer</summary>



</details>

## **Exercise 2**&#x20;

The [Ackermann function](https://www.wikipedia.org/wiki/Ackermann\_function), $$A(m, n)$$, is defined by:

$$
\begin{eqnarray} A(m, n) = \begin{cases} n+1 & \mbox{if } m = 0 \\ A(m-1, 1) & \mbox{if } m > 0 \mbox{ and } n = 0 \\ A(m-1, A(m, n-1)) & \mbox{if } m > 0 \mbox{ and } n > 0. \end{cases} \end{eqnarray}
$$

Write a **recursive** function named `ackerman` that evaluates Ackerman's function. Use your function to evaluate `ackerman(3, 4)`, which should be 125. What happens for larger values of `m` and `n`?

<details>

<summary>Answer</summary>



</details>

## **Exercise 3**&#x20;

A palindrome is a word that is spelled the same backward and forward, like `noon` and `redivider`. Recursively, a word is a palindrome if the first and last letters are the same and the middle is a palindrome. The following are functions that take a string argument and return the first, last, and middle letters:

```
def first(word): 
    return word[0]
    
def last(word): 
    return word[-1]
    
def middle(word): 
    return word[1:-1]
```

* Type these functions into a file named `.py` and test them out. What happens if you call `middle` with a string with two letters? One letter? What about the empty string, which is written `''` and contains no letters?
* Write a **recursive** function called `is_palindrome` that takes a string argument and returns `True` if it is a palindrome and `False` otherwise. Remember that you can use the built-in function `len` to check the length of a string.

<details>

<summary>Answer</summary>



</details>

## **Exercise 4**&#x20;

A number, $$a$$, is a power of $$b$$ if it is divisible by $$b$$ and $$a/b$$ is a power of $$b$$. Write a **recursive** function called `is_power` that takes parameters  `a` and `b` and returns `True` if `a` is a power of `b`, `False` otherwise.

<details>

<summary>Answer</summary>



</details>

## **Exercise 5**&#x20;

This exercise is based on an example from Abelson and Sussman's "Structure and Interpretation of Computer Programs". The greatest common divisor (GCD) of $$a$$ and $$b$$ is the largest number that divides both of them with no remainder. One way to find the GCD of two numbers is [Euclid's algorithm](https://www.wikipedia.org/wiki/Euclidean\_algorithm), which is based on the observation that if $$r$$ is the remainder when $$a$$ is divided by $$b$$, then $$gcd(a, b) = gcd(b, r)$$. As a base case, we can consider $$gcd(a, 0) = a$$.

Write a **recursive** function called `gcd` that takes parameters `a` and `b` and returns their greatest common divisor.

<details>

<summary>Answer</summary>



</details>
