# Positional and Keywords arguments

In programming, calling a function is the act of executing the function with specific parameters. In this section, we will explore two methods of calling a function: positional arguments and keyword arguments.

Consider the function `feet_to_meters()`, which takes two integer parameters: one for the number of `feet` and one for the number of `inches`. The function returns the measurement in meters.&#x20;

{% code lineNumbers="true" %}
```python
INCHES_TO_METERS = 0.0254
INCHES_PER_FOOT = 12

def feet_to_meters(feet, inches):
    total_inches = (feet * INCHES_PER_FOOT) + inches
    meters = total_inches * INCHES_TO_METERS
    return meters
```
{% endcode %}

The code defines two constants `INCHES_TO_METERS` and `INCHES_PER_FEET`. `INCHES_TO_METERS` is a conversion factor that will be used to convert inches to meters. `INCHES_PER_FOOT` is the number of inches in one foot. The function calculates the total number of inches by multiplying the number of feet by the constant `INCHES_PER_FOOT` and adding the number of inches. The function then multiplies the total number of inches by the constant `INCHES_TO_METERS` to convert inches to meters. The function returns the result of the calculation in meters. Using constants in this way can make the code easier to read and maintain, especially if the conversion factors are used in multiple places throughout the code.

## Positional arguments

When calling the function with two integer values for arguments, the given arguments are matched to the formal arguments in the function definition based on their position. The first argument `5` is matched to the first formal argument, which is `feet`, and the second argument `9`is matched to the second formal argument, which is `inches`. The formal arguments are then assigned the values passed in the parameters, and the body of the function is executed with these two values. Once the expression is evaluated, the result `1.7526` is returned and displayed on the console.

```bash
>>> feet_to_meters(5, 9)
 1.7526
>>> feet_to_meters(9, 5)
 2.8702
>>>
```

However, if we call the same function but change the order of the values passed in the parameters, we obtain a different result. This is because the position of the arguments matters in positional arguments.

## Keyword arguments

Alternatively, we can call a function using keyword arguments, where we use the names of the arguments in the function call. In this case, we use the keywords `feet` and `inches` and assign them a value within the call.&#x20;

<pre class="language-bash"><code class="lang-bash"><strong>>>> feet_to_meters(feet=5, inches=9)
</strong> 1.7526
>>> feet_to_meters(inches=9, feet=5)
 1.7526
>>>
</code></pre>

When executing the function, the value `5` will be assigned to the formal parameter `feet`, and the value `9` will be assigned to the formal parameter `inches`. If we reverse the order of the arguments in the function call, `9` is matched to `inches`, and `5` is matched to `feet`. We will still obtain the same result as the previous function call. However, it is important to remember that using a keyword that is not part of the formal arguments will raise an error. For example, trying to call the function with the keyword `yard` will raise an error.

```bash
>>> feet_to_meters(inches=9, yards=5)      
Traceback (most recent call last):
  File "<pyshell#15>", line 1, in <module>
    feet_to_meters(inches=9, yards=5)
TypeError: feet_to_meters() got an unexpected keyword argument 'yards'
```

It is also possible to mix positional and keyword arguments.&#x20;

```bash
>>> feet_to_meters(5, inches=9)
 1.7526
```

In this case, `5` is matched to the first formal argument, and then the keyword parameter `inches` is matched to the formal argument `inches`.&#x20;

However, it is essential to be careful when mixing positional and keyword arguments. Positional parameters must be declared first, followed by keyword arguments; failing to do so will result in a syntax error.

```bash
>>> feet_to_meters(feet=5, 9)         
SyntaxError: positional argument follows keyword argument
```

Overall, both positional and keyword arguments are useful for calling functions with specific parameters. Knowing how to use both methods correctly can make your code more efficient and easier to read.

## Default parameter values

In Python functions, you can specify default values for parameters. This means that if the function is called without providing a value for that parameter, the default value will be used. Default parameters are a convenient feature that can make your code more convenient to reuse and more readable.

Defining a default parameter is simple. You just need to include the default value as part of the parameter definition in the function header. Here's an example:

{% code lineNumbers="true" %}
```python
def greet(name="World"):
    print("Hello, " + name + "!")
```
{% endcode %}

In this function, the parameter `name` has a default value of `"World"`. So, if we call the function without providing a value for `name`, it will use the default value:

```bash
>>> greet()
 "Hello, World!"
>>>
```

However, if we provide a value for `name`, the default value will be overridden:

```bash
>>> greet("John")
 "Hello, John!"
>>>
```

Default parameters can also be used in conjunction with other parameters. Here's an example:

{% code lineNumbers="true" %}
```python
def power(base, exponent=2):
    result = base ** exponent
    print(result)
```
{% endcode %}

In this function, the `base` parameter is required, but the `exponent` parameter has a default value of 2. So, we can call the function with only the `base` parameter:

```bash
>>> power(3) 
 9
>>>
```

Or we can provide a value for `exponent`:

```bash
>>> power(3, 3)
 27
>>>
```

It's important to note that default parameter values are only evaluated once, when the function is defined. This means that if you use a mutable object as a default parameter value (like a list or dictionary), you need to be careful, as changes made to that object will persist across function calls.

Here's an example to illustrate this:

{% code lineNumbers="true" %}
```python
def add_item(item, lst=[]):
    lst.append(item)
    print(lst)
```
{% endcode %}

In this function, the `lst` parameter has a default value of an empty list. If we call the function and don't provide a value for `lst`, it will use the default value of an empty list:

```bash
>>> add_item("apple")
 ["apple"]
>>>
```

If we call the function again without providing a value for `lst`, it will use the same list object as before:

```bash
>>> add_item("banana")
 ["apple", "banana"]
>>>
```

This behavior can be surprising and lead to hard-to-find bugs. To avoid this, you can use `None` as a default value and create a new object in the function if the parameter is `None`:

{% code lineNumbers="true" %}
```python
def add_item(item, lst=None):
    if lst is None:
        lst = []
    lst.append(item)
    print(lst)
```
{% endcode %}

Now, if we call the function and don't provide a value for `lst`, it will create a new list object:

```bash
>>> add_item("apple") 
 ["apple"]
>>>
```

And if we call the function again without providing a value for `lst`, it will create a new list object again:

```bash
>>> add_item("banana") 
 ["banana"]
>>>
```

Default parameters are a useful feature in Python functions that allow you to specify default values for parameters. However, you need to be careful when using mutable objects as default parameter values, as changes made to those objects will persist across function calls.

## Variable-length argument tuples

Functions can take a variable number of arguments. A parameter name that begins with `*` **gathers** arguments into a tuple.&#x20;



In Python, functions can accept a variable number of arguments using the special parameter `*args`. This is a powerful feature that allows developers to write functions that can accept any number of arguments without needing to specify them in the function definition. In this section, we will explore what `*args` is, how it works, and how to use it effectively in Python functions.

`*args` is a special syntax that allows a function to accept an arbitrary number of arguments. It is a shorthand for **variable-length arguments** and is denoted by an asterisk (`*`) followed by the parameter name (args is a common convention, but any name can be used).

The `*args` parameter is typically used when you don't know how many arguments a function will receive at the time of definition. Instead, the arguments are passed at runtime, and the function will handle them accordingly. This makes it a useful tool for functions that need to work with an unknown number of inputs, such as mathematical operations, aggregations, or sorting algorithms.

Here's an example of a function that takes a variable number of arguments using \*args:

{% code lineNumbers="true" %}
```python
def concatenate(*args):
    result = ''
    for arg in args:
        result += arg
    return result
```
{% endcode %}

In this example, the function `concatenate` accepts any number of string arguments, and concatenates them into a single string. The parameter `*args` collects all arguments passed to the function into a tuple, which can be iterated over using a loop or other sequence operations.

To call the `concatenate` function, you can pass any number of string arguments:

```bash
>>> print(concatenate('hello', 'world')) 
 helloworld
>>> print(concatenate('foo', 'bar', 'baz'))
 foobarbaz
>>>
```

As you can see, the function accepts any number of arguments, and the result is concatenated into a single string.

In addition to accepting any number of arguments, `*args` can be combined with other parameters in a function definition. For example, a function can accept a fixed number of arguments as well as a variable number of arguments:

{% code lineNumbers="true" %}
```python
def print_args(name, *args):
    print(f'{name}: {args}')
```
{% endcode %}

In this example, the function `print_args` accepts a mandatory parameter `name` and a variable number of arguments using `*args`. The arguments passed to `*args` will be collected into a tuple and printed to the console.

To call the `print_args` function, you can pass any number of arguments:

```bash
>>> print_args('foo', 1, 2, 3) 
 foo: (1, 2, 3)
>>> print_args('bar', 'hello', 'world') 
 bar: ('hello', 'world')
>>>
```

As you can see, the function accepts any number of arguments, and the output shows the name of the function followed by a tuple of arguments.

One thing to note when using `*args` is that the arguments passed to it must be of the same data type. If the arguments are of different types, the function may raise an error or return unexpected results.

The complement of gather is **scatter**. If you have a sequence of values and you want to pass it to a function as multiple arguments, you can use the `*` operator. For example, `divmod` takes exactly two arguments; it doesn't work with a tuple:

```bash
>>> t = (7, 3)
>>> divmod(t)
 TypeError: divmod expected 2 arguments, got 1 
```

But if you scatter the tuple, it works:

```bash
>>> divmod(*t)
 (2, 1)
>>>
```

But `sum` does not.

**Exercise:** Many of the built-in functions use variable-length argument tuples. For example, `print`, `max` and `min` can take any number of arguments but `sum` does not.

```bash
>>> sum(1,2,3)
 TypeError: sum expected at most 2 arguments, got 3
```

&#x20;Write a function called `sum_all` that takes any number of arguments and returns their sum.

<details>

<summary>Answer:</summary>



</details>

In conclusion, the `*args` parameter is a useful tool for Python developers to handle functions that accept an unknown number of arguments at runtime. By using this feature, developers can write more flexible and dynamic functions that can accept a variable number of arguments without having to specify them in the function definition.
