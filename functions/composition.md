# Composition

So far, we have looked at the elements of a program -variables, expressions, and statements- in isolation, without talking about how to combine them.

One of the most useful features of programming languages is their ability to take small building blocks and **compose** them. For example, the argument of a function can be any kind of expression, including arithmetic operators:

```python
x = math.sin(degrees / 360.0 * 2 * math.pi) t
```

And even function calls:

```python
x = math.exp(math.log(x+1))
```

&#x20;Almost anywhere you can put a value, you can put an arbitrary expression, with one exception: the left side of an assignment statement has to be a variable name. Any other expression on the left side is a syntax error (We will see exceptions to this rule later).

{% code lineNumbers="true" %}
```python
hours = 2 # correct 
minutes = hours * 60 # correct 
hours * 2 = minutes # wrong SyntaxError: can't assign to operator
```
{% endcode %}
