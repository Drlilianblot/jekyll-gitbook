# Newton's method

## Algorithms

[Newton's method](newtons-method.md#section-square-roots) to compute the square root described in the next section is an example of an **algorithm**: it is a mechanical process for solving a category of problems (in this case, computing square roots). It is not easy to define an algorithm. It might help to start with something that is not an algorithm. When you learned to multiply single-digit numbers, you probably memorised the multiplication table. In effect, you memorised 100 specific solutions. That kind of knowledge is not algorithmic. But if you were "cleverly lazy", you probably cheated by learning a few tricks. For example, to find the product of $$n$$ and $$9$$, you can write $$n-1$$ as the first digit and $$10-n$$ as the second digit. This trick is a general solution for multiplying any single-digit number by $$9$$. That's an algorithm!

Similarly, the techniques you learned for addition with carrying, subtraction with borrowing, and long division are all algorithms. One of the characteristics of algorithms is that they do not require any intelligence to carry out. They are mechanical processes in which each step follows from the last according to a simple set of rules.

On the other hand, the process of designing algorithms is interesting, intellectually challenging, and a central part of what we call programming. Some of the things that people do naturally, without difficulty or conscious thought, are the hardest to express algorithmically. Understanding natural language is a good example. We all do it, but so far no one has been able to explain _how_ we do it, at least not in the form of an algorithm.

## Newton's method for computing square root

Loops are often used in programs that compute numerical results by starting with an approximate answer and iteratively improving it. For example, one way of computing square roots is Newton's method. Suppose that you want to know the square root of $$a$$. If you start with almost any estimate, $$x$$, you can compute a better estimate with the following formula:

$$
y = \frac{x + a/x}{2}
$$

For example, if $$a$$ is $$4$$ and $$x$$ is $$3$$:

```bash
>>> a = 4.0 
>>> x = 3.0 
>>> y = (x + a/x) / 2 
>>> print(y) 
 2.16666666667 
>>>
```

Which is closer to the correct answer ($$\sqrt{4} = 2$$). If we repeat the process with the new estimate, it gets even closer:

```bash
>>> x = y 
>>> y = (x + a/x) / 2 
>>> print(y)
 2.00641025641 
>>>
```

After a few more updates, the estimate is almost exact:

```bash
>>> x = y 
>>> y = (x + a/x) / 2 
>>> print(y) 
 2.00001024003 
>>> x = y 
>>> y = (x + a/x) / 2 
>>> print(y) 
 2.00000000003 
>>>
```

In general we don't know ahead of time how many steps it takes to get to the right answer, but we know when we get there because the estimate stops changing:

```bash
>>> x = y 
>>> y = (x + a/x) / 2 
>>> print(y) 
 2.0 
>>> x = y 
>>> y = (x + a/x) / 2 
>>> print(y) 
 2.0 
>>>
```

When `y == x`, we can stop. Here is a loop that starts with an initial estimate, `x`, and improves it until it stops changing:

{% code lineNumbers="true" %}
```python
while True: 
    print(x) 
    y = (x + a/x) / 2 
    if y == x: 
        break 
    x = y
```
{% endcode %}

For most values of `a` this works fine, but in general it is dangerous to test `float` equality. Floating-point values are only approximately right: most rational numbers, like $$1/3$$, and irrational numbers, like $$\sqrt{2}$$, can't be represented exactly with a `float`. Rather than checking whether `x` and `y` are exactly equal, it is safer to use the built-in function `abs` to compute the absolute value, or magnitude, of the difference between them:

{% code lineNumbers="true" %}
```python
if abs(y-x) < epsilon: 
    break 
```
{% endcode %}

Where `epsilon` has a value like $$0.0000001$$ that determines how close is close enough.
