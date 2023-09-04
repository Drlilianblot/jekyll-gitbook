# Math Functions

Python has a math module that provides most of the familiar mathematical functions. A **module** is a file that contains a collection of related functions.

Before we can use the module, we have to import it:

```python
import math
```

This statement creates a **module object** named. The module object contains the functions and variables defined in the module. To access one of the functions, you have to specify the name of the module and the name of the function, separated by a dot (also known as a period). This format is called **dot notation**.

{% code lineNumbers="true" %}
```python
import math

# Example 1
ratio = signal_power / noise_power 
decibels = 10 * math.log10(ratio)

# Example 2
radians = 0.7 
height = math.sin(radians)
```
{% endcode %}

The first example computes the logarithm base 10 of the signal-to-noise ratio. The math module also provides a function called `log` that computes logarithms base `e`.

The second example finds the sine of `radians`. The name of the variable is a hint that `sin` and the other trigonometric functions (`cos`, `tan`, etc.) take arguments in radians. To convert from degrees to radians, divide by 360 and multiply by $$2 \pi$$:

```bash
>>> degrees = 45 
>>> radians = degrees / 360.0 * 2 * math.pi 
>>> math.sin(radians) 
 0.707106781187 
>>>
```

The expression `math.pi` gets the variable `pi` from the math module. The value of this variable is an approximation of $$\pi$$, accurate to about 15 digits.

<details>

<summary>Exercise</summary>

Explore the `math` module either by using the `help` function from the interpreter prompt or by visiting the [official python documentation webpage](https://docs.python.org/3/library/math.html).

</details>
