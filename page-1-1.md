# Python's Type Hinting

Python is a dynamically typed programming language, which means that the type of a variable is determined at runtime, not at compile time. This feature allows for more flexibility and rapid prototyping but can also lead to errors that are difficult to catch and fix. To address this issue, Python introduced type hinting in version 3.5, a way of annotating code with hints about the types of variables and function arguments.

Type hinting is not enforced by the Python interpreter, which means that it is optional and does not affect the runtime behaviour of the program. However, type hints can be useful for improving code readability, catching errors early in the development process, and enabling better code analysis and documentation.

In this chapter, we will explore the basics of type hinting in Python, including the syntax for annotating variables and functions, the types that can be used, and the tools available for type checking and enforcement. We will also discuss some best practices and common pitfalls when using type hints, and how to integrate type hinting with other Python features such as decorators and inheritance. By the end of this chapter, you will have a solid understanding of type hinting and how to use it effectively in your Python code.

## Introduction&#x20;

Type hinting is a feature in Python that allows programmers to annotate the types of variables, arguments, and return values in their code. This annotation is not enforced by the Python interpreter, but rather serves as a tool to help developers catch errors and improve code readability.

The primary purpose of type hinting is to make code more maintainable and easier to understand. By providing type annotations, developers can more clearly communicate the intended types of data in their code, which can reduce confusion and improve collaboration. Additionally, type hints can help catch errors at development time, before they cause issues in production code.

Type hinting in Python has several advantages, including:

1. Improved code readability: Type hints can make code more self-documenting, allowing other developers to more easily understand the purpose and expected behavior of functions and variables.
2. Earlier error detection: Type hints can help catch errors early in the development process, before they cause issues in production code.
3. Better tooling support: Many modern integrated development environments (IDEs) and code editors can use type hints to provide improved auto-complete, code highlighting, and other features.
4. Easier refactoring: Type hints can make refactoring code easier by helping developers understand the flow of data in their code.
5. Improved code quality: Type hints can help catch subtle errors that may be difficult to catch with traditional debugging techniques.

## Basic Syntax of Type Hinting&#x20;

### A. Basic Type Hinting&#x20;

Function type hinting is a powerful feature in Python that allows developers to specify the expected types of arguments and return values of functions. This provides several benefits, such as improving code readability, catching errors early during development, and helping with code documentation. Let's take a look at some examples of how to use function type hinting.

First, let's define a simple function that takes two integers and returns their sum:

{% code lineNumbers="true" %}
```python
def add(x: int, y: int) -> int:
    return x + y
```
{% endcode %}

In this example, we use the `int` type hint to specify that both `x` and `y` are expected to be integers, and the return type hint of `-> int` specifies that the function should return an integer. This type hinting makes it clear to other developers what types of inputs and outputs the function expects.

We can also use type hinting with default arguments. For example:

{% code lineNumbers="true" %}
```python
def greet(name: str = "world") -> str:
    return f"Hello, {name}!"
```
{% endcode %}

In this example, we specify that the `name` argument is expected to be a string, and that the function should return a string. We also provide a default value of `"world"` for the `name` argument. This makes it clear to other developers what the default behavior of the function is, and what types of inputs and outputs it expects.

In addition to basic types such as `int`, `str`, and `bool`, we can also use more complex types such as lists, dictionaries, and custom classes in function type hinting. For example:

{% code lineNumbers="true" %}
```python
from typing import List, Dict, Tuple

def process_data(data: List[Dict[str, int]]) -> Tuple[int, int]:
    total = 0
    count = 0
    for item in data:
        total += item["value"]
        count += 1
    return total, count
```
{% endcode %}

In this example, we use the `List` and `Dict` types from the `typing` module to specify that the `data` argument is expected to be a list of dictionaries, where each dictionary has string keys and integer values. The function then processes the data and returns a tuple of two integers.

Using function type hinting can be especially helpful when working with complex projects or collaborating with other developers. It can help to reduce errors and improve code readability, making it easier for other developers to understand and work with your code.

However, it's important to remember that function type hinting is not enforced by Python itself, and so it's still possible for code to be written that doesn't adhere to the specified types. Therefore, it's important to use type hinting as a guideline, but not rely on it entirely for ensuring correct behaviour.

We can also use type hints for variables, class attributes, and function arguments that have default values. For example, the following code demonstrates how to use type hints for a variable:

```python
x: int = 10
```

In this code, `x` is a variable of type `int`, and its initial value is 10.

### Type Checking Tools

Python does not include built-in type checking functionality. However, there are third-party tools that can perform static or dynamic type checking based on type hints. These tools can detect type-related errors, such as type mismatches, before the code is executed. Some popular type checking tools for Python include Mypy, Pyright, PyCharm, and PyLint.

The following example demonstrates how type checking works with Mypy, a static type checker for Python. First, we need to install Mypy using pip:

```sh
pip install mypy
```

Then, we can create a file named `example.py` with the following code:

{% code title="example.py" lineNumbers="true" %}
```python
def add(a: int, b: int) -> int:
    return a + b

result = add(1, '2')
```
{% endcode %}

In this code, we are calling the `add()` function with two arguments of different types (`1` and `'2'`). This would result in a type error if we run the code. However, if we run Mypy on the code, we get the following error message:

```go
example.py:4: 
error: Argument 2 to "add" has incompatible type "str"; expected "int"
```

This error message indicates that the second argument to `add()` has the wrong type (`str` instead of `int`), as specified by the type hint.

### Advanced Type Hinting

Python's type hinting system goes beyond basic types and allows for more advanced type hinting to enhance code readability and maintainability. In this section, we will cover Union Types, Optional Types, Typed Dictionaries, and Callable Types.

#### Union Types:&#x20;

Union types are used when a variable can accept more than one type. This is achieved by using the "|" operator between types. Here's an example:

{% code lineNumbers="true" %}
```python
def square(num: Union[int, float]) -> Union[int, float]:
    return num * num
```
{% endcode %}

In the above example, the function `square` takes a parameter `num` which can either be an integer or a float. The return type of the function can also be either an integer or a float.

#### Optional Types:&#x20;

Optional types are used when a variable can be of a specific type or None. This is achieved by using the "Optional" keyword from the typing module. Here's an example:

{% code lineNumbers="true" %}
```python
from typing import Optional

def greeting(name: Optional[str]) -> str:
    if name is not None:
        return f"Hello, {name}!"
    return "Hello, World!"
```
{% endcode %}

In the above example, the function `greeting` takes an optional parameter `name` which can either be a string or None. If `name` is not None, the function returns a greeting with the name. If `name` is None, the function returns a generic greeting.

#### Typed Dictionaries:&#x20;

Typed dictionaries allow you to specify the types of keys and values in a dictionary. This is achieved by using the "TypedDict" keyword from the typing module. Here's an example:

{% code lineNumbers="true" %}
```python
from typing import TypedDict

class User(TypedDict):
    name: str
    age: int
    email: str
```
{% endcode %}

In the above example, the `User` class is a typed dictionary that specifies the types of the keys and values in the dictionary. The keys in the dictionary are `name`, `age`, and `email`, and their respective types are `str`, `int`, and `str`.

#### Callable Types:&#x20;

Callable types are used when a variable can be a function or a method. This is achieved by using the "Callable" keyword from the typing module. Here's an example:

{% code lineNumbers="true" %}
```python
from typing import Callable

def apply_function(func: Callable[[int], int], num: int) -> int:
    return func(num)

def double(num: int) -> int:
    return num * 2

result = apply_function(double, 5)
print(result)
```
{% endcode %}

In the above example, the function `apply_function` takes two parameters: a callable function `func` that takes an integer parameter and returns an integer, and an integer `num`. The function `apply_function` calls the function `func` with the `num` parameter and returns the result. The function `double` is defined as a callable function that doubles the value of the parameter passed to it. The `apply_function` function is called with the `double` function and an integer value of `5`, and the result is printed, which is `10`.

#### Aliases

To avoid repetition and make the code more readable, type aliases can be used.

{% code lineNumbers="true" %}
```python
from typing import Dict, Union

DictStrIntOrStr = Dict[str, Union[int, str]]

def print_dict(d: DictStrIntOrStr) -> None:
    for key, value in d.items():
        print(f"{key}: {value}")

my_dict: DictStrIntOrStr = {"age": 42, 
                            "firstname": "Lilian", 
                            "surname": "Blot"}
print_dict(my_dict)
```
{% endcode %}

In this example, we define the `DictStrIntOrStr` alias to represent a dictionary with string keys and values that can be either integers or strings. We then define a function `print_dict` that takes a dictionary of this type and prints out each key-value pair.

We create an example dictionary `my_dict` of this type and pass it to the `print_dict` function. When we run the code, we see the following output:

```makefile
age: 42
firstname: Lilian
surname: Blot
```

This example demonstrates how aliases can be used to make our code more readable and easier to maintain. By defining the `DictStrIntOrStr` alias, we can use it throughout our code to represent dictionaries with a specific set of key-value types. If we need to change the types of the values in our dictionary, we can simply update the alias definition, rather than modifying the type annotations throughout our codebase.

Advanced type hinting allows developers to specify more complex data types and function signatures, making their code more readable and maintainable. Union types, optional types, typed dictionaries, and callable types are just some of the tools available in Python's type hinting system. By using these tools, developers can write better code with fewer bugs, making their programs more efficient and reliable.

## Best Practices for Type Hinting&#x20;

1. Choosing the Correct Type Hint&#x20;
2. Avoiding Overuse of Type Hints&#x20;
3. Documenting Type Hints&#x20;
4. Updating Type Hints

Using type hinting can greatly improve the readability and maintainability of your Python code. However, simply adding type hints is not enough. It is important to follow best practices to ensure that your code is clear and consistent. Here are some best practices to follow when using type hinting in Python:

1. Be consistent: Consistency is key when it comes to type hinting. Make sure that you use type hints consistently throughout your codebase. This means using the same style of type hinting, and being consistent with the names and types of variables and parameters.
2. Use descriptive variable names: When using type hinting, it is important to use descriptive variable names. This will make it easier for others to understand what the variable is for and what type it should be.
3. Use Union types for variables that can have multiple types: Union types allow you to specify that a variable can have more than one type. This can be useful when dealing with variables that can have multiple types, such as a parameter that can be either a string or a list.
4. Use Optional types for optional parameters: Optional types allow you to specify that a parameter is optional. This can be useful when dealing with functions that have optional parameters.
5. Use Typed Dictionaries: Typed dictionaries are a great way to define a dictionary with specific key-value pairs. This can be useful when working with APIs that require specific input formats.
6. Use Callable types for functions that take functions as arguments: Callable types allow you to specify the type of function that is expected as an argument. This can be useful when working with higher-order functions that take functions as arguments.
7. It is important to be precise with the types being used. This means avoiding generic types like `Any` and instead using more specific types like `List[str]` or `Tuple[int, str]`. This helps make the code more self-documenting and easier to understand.
8. It is a good practice to use type aliases to avoid repetition and make the code more readable. For example, instead of writing `Dict[str, Union[int, str]]`, a type alias `DictStrIntOrStr` can be defined and used throughout the code

To illustrate these best practices, consider the following example code:

{% code lineNumbers="true" %}
```python
from typing import List, Dict, Tuple

# Consistent type hinting style
def greet(name: str) -> str:
    return f"Hello, {name}!"

# Descriptive variable names
def calculate_average_grade(student_grades: List[int]) -> float:
    total = sum(student_grades)
    return total / len(student_grades)

# Union types for variables that can have multiple types
def get_first_element(data: Union[List[str], str]) -> str:
    if isinstance(data, list):
        return data[0]
    return data
    
# Use type aliases to avoid repetition and make code more readable
DictStrIntOrStr = Dict[str, Union[int, str]]

# Be precise with types being used
def get_longest_string(strings: List[str]) -> str:
    longest = ""
    for string in strings:
        if len(string) > len(longest):
            longest = string
    return longest

# Use type hints consistently throughout the codebase
def add_student_scores(
        scores: Dict[str, int], 
        student_scores: List[Tuple[str, int]]) -> Dict[str, int]:
    for student, score in student_scores:
        scores[student] = scores.get(student, 0) + score
    return scores


```
{% endcode %}

In this example, type aliases are used to avoid repetition and make the code more readable. Precise types like `List[str]`, `Dict[str, int]`, and `Tuple[str, int]` are used to provide more information and make the code more self-documenting.

## Conclusion

Overall, type hinting is a powerful tool for improving code maintainability, reducing errors, and enhancing collaboration among developers. In the following chapter, we will explore the syntax and usage of type hints in Python, as well as best practices for implementing them in your own code.
