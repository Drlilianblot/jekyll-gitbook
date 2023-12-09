# 15 - Python's Type Hinting

{% embed url="https://youtu.be/yW__I5HGyEg" %}

Python is a dynamically typed programming language, which means that the type of a variable is determined at runtime, not at compile time. This feature allows for more flexibility and rapid prototyping but can also lead to errors that are difficult to catch and fix. To address this issue, Python introduced type hinting in version 3.5, a way of annotating code with hints about the types of variables and function arguments.

Type hinting is not enforced by the Python interpreter, which means that it is optional and does not affect the runtime behaviour of the program. However, type hints can be useful for improving code readability, catching errors early in the development process, and enabling better code analysis and documentation.

In this chapter, we will explore the basics of type hinting in Python, including the syntax for annotating variables and functions, the types that can be used, and the tools available for type checking and enforcement. We will also discuss some best practices and common pitfalls when using type hints. By the end of this chapter, you will have a solid understanding of type hinting and how to use it effectively in your Python code.

## Introduction&#x20;

Type hinting is a feature in Python that allows programmers to annotate the types of variables, arguments, and return values in their code. This annotation is not enforced by the Python interpreter, but rather serves as a tool to help developers catch errors and improve code readability.

The primary purpose of type hinting is to make code more maintainable and easier to understand. By providing type annotations, developers can more clearly communicate the intended types of data in their code, which can reduce confusion and improve collaboration. Additionally, type hints can help catch errors at development time, before they cause issues in production code.

Type hinting in Python has several advantages, including:

1. Improved code readability: Type hints can make code more self-documenting, allowing other developers to more easily understand the purpose and expected behaviour of functions and variables.
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
def greet(name: str="world") -> str:
    return f"Hello, {name}!"
```
{% endcode %}

In this example, we specify that the `name` argument is expected to be a string, and that the function should return a string. We also provide a default value of `"world"` for the `name` argument. This makes it clear to other developers what the default behaviour of the function is, and what types of inputs and outputs it expects.

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

data = [{'A': 1, 'B': 2}, {'C': 3}, {'D': 4, 'E': 5}]
print(process_data(data))
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

Python does not include built-in type checking functionality. However, there are third-party tools that can perform static or dynamic type checking based on type hints. These tools can detect type-related errors, such as type mismatches, before the code is executed. Some popular type checking tools for Python include Mypy, Pyright, and PyCharm.

The following example demonstrates how type checking works with Mypy, a static type checker for Python. First, we need to install Mypy using `pip`:

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

In this code, we are calling the `add()` function with two arguments of different types (`1` and `'2'`). This would result in a type error if we run the code. However, if we run `mypy` on the code, we get the following error message:

```go
example.py:4: 
error: Argument 2 to "add" has incompatible type "str"; expected "int"
```

This error message indicates that the second argument to `add()` has the wrong type (`str` instead of `int`), as specified by the type hint.

### Advanced Type Hinting

Python's type hinting system goes beyond basic types and allows for more advanced type hinting to enhance code readability and maintainability. In this section, we will cover `Union` Types, `Optional` Types, Typed Dictionaries, and `Callable` Types.

#### Union Types:&#x20;

The `Union` type is used to indicate that a variable can have multiple types. It is a way of expressing that a variable or parameter can be of one type or another. This is particularly useful when a function or variable can accept a range of data types.

The `Union` type is typically used from the typing module, and it is applied by using square brackets (`[]`). The syntax looks like `Union[type1, type2, ...]`.

Let's consider an example where a function takes a parameter that can be either a `str` or an `int`:

{% code title="typehinting.py" lineNumbers="true" %}
```python
from typing import Union

def sum_digits(number: Union[str, int]) -> int:
    digits = [int(x) for x in str(number)]
    return sum(digits)

print(sum_digits('1234')) #10
print(sum_digits(1234)) #10

# Invalid usage:
print(sum_digits(1234.0))
# The line above would result in a type error during static analysis:
#
# typehinting.py:11: error: Argument 1 to "sum_digits" has incompatible type 
#     "float"; expected "str | int" [arg-type]
# Found 1 error in 1 file (checked 1 source file)
```
{% endcode %}

This usage of Union allows the `sum_digits` function to handle both integers and string without causing a type error during static analysis.

`Union` provides flexibility in specifying that a parameter or variable can accept more than one type. It makes the code more explicit by indicating the expected types of data. It's commonly used when a function or variable can handle various data types, enhancing the versatility of the code. However, while `Union` is powerful, it's essential not to overuse it. Consider using more specific types when possible to maintain code clarity.

#### Optional Types:&#x20;

The `Optional` type is used to indicate that a variable can either have a specific type or `None`. This is useful when you want to specify that a function parameter is optional and can be omitted. The `Optional` type is part of the `typing` module, and it is often used in scenarios where a variable can have a specific type or be `None`. The syntax for using `Optional` involves using the keyword `Optional` and specifying the type within square brackets (`[]`). It looks like `Optional[type]`.

Let's consider an example where a function takes an optional parameter that can be either a `str` or `None`:

{% code title="typehinting_2.py" lineNumbers="true" %}
```python
from typing import Optional

def greet(name: Optional[str]=None) -> str:
    if name is not None:
        return f"Hello, {name}!"
    else:
        return "Hello, Stranger!"

# Valid usage
print(greet("Alice"))  # "Hello, Alice!"
print(greet())  # "Hello, Stranger!"

# Invalid usage (passing an integer)
print(greet(42))

# The line above would result in a type error during static analysis:
#
# typehinting_2.py:14: error: Argument 1 to "greet" has incompatible type "int";
#    expected "str | None"  [arg-type]
# Found 1 error in 1 file (checked 1 source file)
```
{% endcode %}

In this example:

* The `greet` function takes an optional parameter `name` of type `Optional[str]`, indicating that it can be either a `str` or `None`.
* If `name` is provided, it returns a personalised greeting; otherwise, it defaults to a generic greeting.

This usage of `Optional` allows the greet function to handle cases where the name parameter is optional, and it can be safely omitted.

When specifying a default value for the parameter, it's entirely valid to provide a default value other than `None`. The `Optional` type indicates that the parameter can take on the specified type or be omitted, defaulting to the provided default value if omitted.

Let's illustrate this by refactoring our previous example:

{% code lineNumbers="true" %}
```python
from typing import Optional

def greet(name: Optional[str]='Stranger') -> str:
    return f"Hello, {name}!"
```
{% endcode %}

In this example:

* The `greet` function takes an optional parameter name of type Optional\[str], indicating that it can be either a string or None.
* The default value for `name` is set to `"Stranger"` providing a default value other than `None`.
* Valid usages include providing a specific name or omitting the `name` parameter, in which case the default value `"Stranger"` is used.

This pattern is commonly used when you want to allow a parameter to be optional but provide a meaningful default value if it's omitted.

#### Typed Dictionaries:&#x20;

In Python type hinting, `TypedDict` is a class provided by the `typing` module that allows you to define a dictionary with specific key-value pairs and their corresponding types. This is particularly useful when you want to enforce a certain structure for dictionaries within your code, providing better static analysis and documentation.

`TypedDict` is used to create a type hint for a dictionary where you specify the expected keys and their corresponding value types.

The basic syntax for defining a `TypedDict` involves creating a class that inherits from `TypedDict` and specifying the keys and their types as class attributes.

For example,&#x20;

* We define a `UserProfile` class inheriting from `TypedDict` where `username`, `age`, and `email` are the expected keys with their respective types.
* The `print_user_profile` function takes a parameter user of type `UserProfile` and prints the user's information.
* When using the `UserProfile` type, the code analyser ensures that all required keys with their specified types are present in the dictionary. If a required key is missing, or an additional key is present,  or if there's a type mismatch, it raises a static analysis error.

{% code title="typehinting_6.py" overflow="wrap" lineNumbers="true" fullWidth="false" %}
```python
from typing import TypedDict

# Define a TypedDict class for a user profile
class UserProfile(TypedDict):
 username: str
 age: int
 email: str

# Function using TypedDict
def print_user_profile(user: UserProfile) -> None:
 print(f"Username: {user['username']}")
 print(f"Age: {user['age']}")
 print(f"Email: {user['email']}")

# Valid usage
valid_user_data: UserProfile = {'username': 'john_doe', 
                                'age': 25, 
                                'email': 'john@example.com'}
print_user_profile(valid_user_data)


# invalid_user_data: 
missing_key_data: UserProfile = {'username': 'jane_doe', 
                                 'email': 'jane@example.com'}
too_manyKeys_data: UserProfile = {'username': 'jane_doe', 
                                  'email': 'jane@example.com', 
                                  'age': 24, 
                                  'height': 175}

# The two lines above would result in a type error during static analysis
# typehinting_6.py:23: error: Missing key "age" for TypedDict "UserProfile"  [typeddict-item]
# typehinting_6.py:25: error: Extra key "height" for TypedDict "UserProfile"  [typeddict-unknown-key]
# Found 2 errors in 1 file (checked 1 source file)
```
{% endcode %}

In the above example, the `UserProfile` class is a typed dictionary that specifies the types of the keys and values in the dictionary. The keys in the dictionary are `name`, `age`, and `email`, and their respective types are `str`, `int`, and `str`.

`TypedDict` helps enforce a specific structure for dictionaries. It provides better static analysis during development. Use `TypedDict` when you want to communicate and enforce a specific structure for dictionaries in your code.

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

Using type hinting can greatly improve the readability and maintainability of your Python code. However, simply adding type hints is not enough. It is important to follow best practices to ensure that your code is clear and consistent. Here are some best practices to follow when using type hinting in Python:

1. Be consistent: Consistency is key when it comes to type hinting. Make sure that you use type hints consistently throughout your codebase. This means using the same style of type hinting, and being consistent with the names and types of variables and parameters.
2. Use descriptive variable names: When using type hinting, it is important to use descriptive variable names. This will make it easier for others to understand what the variable is for and what type it should be.
3. Use Typed Dictionaries: Typed dictionaries are a great way to define a dictionary with specific key-value pairs. This can be useful when working with APIs that require specific input formats.
4. It is important to be precise with the types being used. This means avoiding generic types like Any and instead using more specific types like List\[str] or Tuple\[int, str]. This helps make the code more self-documenting and easier to understand.

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

In this example, precise types like `List[str]`, `Dict[str, int]`, and `Tuple[str, int]` are used to provide more information and make the code more self-documenting.

## Conclusion

In the ever-evolving landscape of Python programming, the adoption of type hinting has emerged as a transformative practice, offering developers a valuable tool to enhance code quality, readability, and maintainability. As we wrap up our exploration of type hinting in Python, let's reflect on the key takeaways and the impact this feature has on modern Python development.

* Clarity and Readability: type hinting serves as a form of documentation, making code more explicit and self-explanatory. By providing insights into variable types, function parameters, and return types, developers can quickly understand the expected structure and behaviour of the code.
* Early Error Detection: one of the major advantages of type hinting is its role in catching errors early in the development process. By incorporating type annotations, developers can identify potential issues during static analysis, preventing runtime errors and enhancing overall code robustness.
* Collaboration and Communication: type hinting acts as a communication tool among developers working on a project. It facilitates collaboration by clearly defining the interfaces between different components, making it easier for team members to understand and contribute to the codebase.
* Enhanced Refactoring: type hints play a crucial role in making codebases more adaptable to changes. During refactoring, developers can rely on type annotations to understand the flow of data and make modifications with greater confidence, minimising the risk of introducing errors.
* Advanced Type Hinting Features: Python's type hinting system goes beyond basic types, offering features like Union Types, Optional Types, Typed Dictionaries, Callable Types, and more. These advanced features provide developers with a versatile toolkit to express complex data structures and function signatures.
* Type Hinting as a Guideline: it's important to note that while type hinting is a powerful aid, it is not enforced by the Python interpreter. Developers should view type hints as guidelines that enhance code quality but not as strict rules governing behaviour. The flexibility of Python remains intact, allowing for a balance between clarity and flexibility.

In summary, the adoption of type hinting represents a significant step forward in the evolution of Python. As the language continues to evolve, developers are empowered with tools that not only boost their productivity but also contribute to the creation of more reliable, understandable, and maintainable software. Type hinting, when used judiciously, becomes an integral part of the Pythonic journey, enriching the coding experience and ensuring the sustainability of Python projects in the long run.

\
