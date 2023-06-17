# Scope of a variable

In programming, variables are used to store values that can be manipulated and used in various parts of the code. The concept of scope refers to the part of the code where a variable can be accessed and modified. In Python 3, variables can have different scopes, which affects how they can be used in the code. In this section, we will explore the concept of scope in Python 3, and explain how it affects variable usage in the code.

## Built-in scope

In Python 3, the built-in scope is a distinct Python scope implemented as a standard library module called `builtins`. This scope contains all of Python's built-in objects, which are automatically loaded when the Python interpreter is run. This includes functions like `print()`, `len()`, `range()`, we have seen earlier.

You can access the built-in scope from any module or function in Python without having to import any modules or define any functions. This is because the built-in scope is automatically available to every Python program.

Here's an example of how to access the built-in `len()` function:

{% code lineNumbers="true" %}
```python
# Define a list
my_list = [1, 2, 3, 4, 5]

# Use the len() function to get the length of the list
length = len(my_list)

# Print the length of the list
print("The length of the list is:", length)    
# Output: The length of the list is: 5
```
{% endcode %}

In this example, we use the built-in `len()` function to get the length of a list called `my_list`. We don't have to import any modules or define any functions to use the `len()` function, because it's part of the built-in scope.

It's important to note that you should avoid defining variables or functions with the same name as built-in functions or modules, as this can cause unexpected behaviour and errors in your program as shown in the next code snippet.

```bash
>>> sum([1,2,3,4]) # uses the built-in function sum    
10
>>> sum = 10 # redefined the built-in name sum within the global scope    
>>> sum([1,2,3])      
Traceback (most recent call last):
  File "<pyshell#13>", line 1, in <module>
    sum([1,2,3])
TypeError: 'int' object is not callable

```

What happens here will become clearer when we look at the [LEGB Rule](scope-of-a-variable.md#pythons-legb-rules) for Python Scope.

## Global Scope:&#x20;

Variables that are defined outside of any function or class have global scope. This means that they can be accessed and modified anywhere in the code. Global variables can be useful for storing values that need to be shared across different parts of the code. However, overuse of global variables can make the code harder to maintain and debug, since any part of the code can modify them.

{% code lineNumbers="true" %}
```python
# Define a global variable
x = 10

# Define a function that uses the global variable
def print_x():
    print("The value of x is:", x)

# Call the function
print_x()    # Output: The value of x is: 10
```
{% endcode %}

In this example, the variable `x` is defined outside of any function, which gives it global scope. The function `print_x()` uses the global variable `x` and can access its value without any issues.

## Local Scope:&#x20;

Variables that are defined inside a function or class have local scope. This means that they can only be accessed and modified within the function or class where they are defined. Local variables are useful for storing values that are only needed within a specific part of the code, and can help keep the code organized and easier to read. Local variables are also automatically destroyed when the function or class where they are defined is finished executing, which can help prevent memory leaks.

{% code lineNumbers="true" %}
```python
# Define a function that uses a local variable
def add_numbers(a, b):
    # Define a local variable
    sum_ = a + b
    print("The sum is:", sum_)

# Call the function
add_numbers(5, 7)    # Output: The sum is: 12

# Try to access the local variable from outside the function
print(sum_)    # Raises a NameError: name 'sum_' is not defined
```
{% endcode %}

In this example, the variable `sum` is defined inside the `add_numbers()` function, which gives it local scope. The variable can only be accessed and modified within the function, and any attempts to access it from outside the function will result in a `NameError`.

## Enclosing (or nonlocal or nested) scope:&#x20;

In Python 3, it is possible to define functions and classes inside other functions or classes. When this happens, the inner functions and classes have **nested** scope, which means that they can access variables defined in the outer functions or classes. However, the outer functions or classes cannot access variables defined in the inner functions or classes. This can be useful for creating modular code that is easier to maintain and reuse.

{% code lineNumbers="true" %}
```python
# Define an outer function
def outer_function():
    # Define a variable in the outer function
    x = "outer"

    # Define an inner function
    def inner_function():
        # Access the variable from the outer function
        print("The value of x is:", x)

    # Call the inner function
    inner_function()

# Call the outer function
outer_function()    # Output: The value of x is: outer
```
{% endcode %}

In this example, the variable `x` is defined in the outer function, and the inner function can access it due to nested scope. However, if we define another variable with the same name inside the inner function, it will create a new local variable that shadows the outer variable:

{% code lineNumbers="true" %}
```python
# Define an outer function
def outer_function():
    # Define a variable in the outer function
    x = "outer"

    # Define an inner function
    def inner_function():
        # Define a variable with the same name as the outer variable
        x = "inner"
        print("The value of x is:", x)

    # Call the inner function
    inner_function()

# Call the outer function
outer_function()    # Output: The value of x is: inner
```
{% endcode %}

In this example, the inner function defines a new variable `x` with the same name as the outer variable. When we call the inner function, it prints the value of the inner variable, which shadows the outer variable.

## `global` and `nonlocal` Keywords&#x20;

In Python 3, the `global` keyword can be used to access global variables from within a function or class. When the `global` keyword is used before a variable name, it tells Python that the variable should be treated as a global variable, even if it is defined inside a function or class.

The `nonlocal` keyword can be used to access variables from the outer function scope in a nested function. When the `nonlocal` keyword is used before a variable name, it tells Python that the variable should be treated as a nonlocal variable, which means that it can be accessed and modified by the inner function.&#x20;

Example 1: Using the `global` Keyword

{% code lineNumbers="true" %}
```python
# Define a global variable
x = 10

# Define a function that modifies the global variable
def modify_x():
    global x    # Use the global keyword to access the global variable
    x = 20

# Call the function
modify_x()

# Print the value of the global variable
print("The value of x is:", x)    # Output: The value of x is: 20
```
{% endcode %}

In this example, the `global` keyword is used to access and modify the global variable `x` from inside the function `modify_x()`. Without the `global` keyword, Python would create a new local variable with the same name inside the function, which would not affect the value of the global variable.

Example 2: Using the `nonlocal` Keyword

{% code lineNumbers="true" %}
```python
# Define an outer function
def outer_function():
    # Define a variable in the outer function
    x = "outer"

    # Define an inner function that modifies the outer variable
    def inner_function():
        nonlocal x    # Use the nonlocal keyword to access the outer variable
        x = "inner"

    # Call the inner function
    inner_function()

    # Print the value of the outer variable
    print("The value of x is:", x)

# Call the outer function
outer_function()    # Output: The value of x is: inner
```
{% endcode %}

In this example, the `nonlocal` keyword is used to access and modify the variable `x` from the outer function inside the inner function. Without the `nonlocal` keyword, Python would create a new local variable with the same name inside the inner function, which would not affect the value of the outer variable.

Note that the `global` and `nonlocal` keywords should be used with caution, as they can make the code harder to read and maintain. In general, it is recommended to avoid using global variables and to use function arguments and return values instead. Similarly, it is usually better to refactor nested functions to avoid the need for `nonlocal` variables.

## The assignment operator and the Python scope

Whenever you assign a value to a name in Python, one of two things can happen:

1. You **create** a new name
2. You **update** an existing name

However, the behaviour of name assignment depends on the Python scope in which it occurs. For example, if you try to assign a value to a global name inside a function, you'll create a new local name in the function's scope that shadows or overrides the global name. This will prevent you from modifying variables defined outside the function from within the function.

Therefore, the following code may not behave as you expect:

{% code title="scope.py" lineNumbers="true" %}
```python
x = 0 # declare a global variable

def increment():
    x = x + 1 # update the global variable x

increment()
print(x)
```
{% endcode %}

when executing the module `scope.py` the following happens:

```
Traceback (most recent call last):
  File "c:/scope.py", line 6, in <module>
    increment()
  File "D:/scope.py", line 4, in increment
    x = x + 1 # update the global variable x
UnboundLocalError: local variable 'x' referenced before assignment
```

Within `increment()`, you try to increment the global variable, `x`. Since `x` isn’t declared `global` inside `increment()`, Python creates a new local variable with the same name, `x`, inside the function. In the process, Python realises that you’re trying to use the local `x` before its first assignment (`x + 1`), so it raises an `UnboundLocalError`.

## Python's LEGB Rules

In Python, variable names are resolved using the LEGB rule, which stands for Local, Enclosing, Global, and Built-in. This rule defines the order in which Python looks up a name to find its corresponding value.

1. Local: This is the innermost scope, which contains names defined within a function. Any variable defined within a function is local to that function and can only be accessed within that function.
2. Enclosing: This refers to the scope of the enclosing function, which contains the local scopes of any nested functions. If a variable is not found in the local scope of a function, Python searches the enclosing scope next.
3. Global: This refers to the global scope, which contains names defined at the top level of a module or explicitly declared as global within a function. If a variable is not found in the local or enclosing scopes, Python searches the global scope next.
4. Built-in: This refers to the built-in scope, which contains the names of all built-in functions, exceptions, and other objects. If a variable is not found in any of the previous scopes, Python searches the built-in scope.

It's important to note that Python always searches the scopes in this order, from local to built-in. If a name is found in a higher-level scope, Python stops searching and uses the value from that scope. Remember the code snippet we wrote in the [builtin section](scope-of-a-variable.md#built-in-scope), where we redefined the `sum` name in the global scope and shown below for convenience.&#x20;

<pre class="language-bash"><code class="lang-bash"><strong>>>> sum([1,2,3,4]) # uses the built-in function sum  
</strong><strong>10
</strong>>>> sum = 10 # redefined the built-in name sum within the global scope
>>> sum([1,2,3])      
Traceback (most recent call last):
  File "&#x3C;pyshell#13>", line 1, in &#x3C;module>
    sum([1,2,3])
TypeError: 'int' object is not callable
</code></pre>

Now we can explain why an error occurred. when executing the statement sum(\[1,2,3]), the interpreter searches the name `sum` in global scope first, and find it is a variable of type `int` having the value `10`, and not a function. As the interpreter found the name `sum` in the global scope, it never looks at the `builtin` scope. The function `sum` is no more accessible within your program.&#x20;

{% hint style="info" %}
I cannot emphasise enough that you should avoid defining variables or functions with the same name as built-in functions or modules, as this can cause unexpected behaviour and errors in your program.
{% endhint %}

Understanding the LEGB rule is essential to writing clean and maintainable code. It allows you to use descriptive variable names without worrying about naming conflicts, and it helps you avoid modifying global variables unintentionally.

## Summary

Now you should be able to understand the output from the code we have seen in the section Nested Function.

{% code lineNumbers="true" %}
```python
x = 10

def outer_function():
    x = 5
    
    def inner_function():
        print(x)
    
    inner_function()

outer_function() # Output: 5
print(x) # Output: 10
```
{% endcode %}

In this code snippet, we define a global variable `x` with a value of `10`. We then define an outer function `outer_function` that defines a **local** variable `x` with a value of `5`. The **local** variable `x` shadows the **global** variable `x`.

We then define an inner function `inner_function` that prints the value of `x`. When we call `inner_function` from `outer_function`, it prints the value of the **local** variable `x`, which is `5`.

When we call `outer_function`, it prints the value of `x` from the **local** scope of `outer_function`. After calling `outer_function`, we print the value of the **global** variable `x`, which is still `10`.

The table below summarises some of the implications of Python scope:

<table><thead><tr><th>Action</th><th width="154">Global Code</th><th>Local Code</th><th>Nested Function Code</th></tr></thead><tbody><tr><td>Access or reference names that live in the global scope</td><td>Yes</td><td>Yes</td><td>Yes</td></tr><tr><td>Modify or update names that live in the global scope</td><td>Yes</td><td>No (unless declared <code>global</code>)</td><td>No (unless declared <code>global</code>)</td></tr><tr><td>Access or reference names that live in a local scope</td><td>No</td><td>Yes (its own local scope), No (other local scope)</td><td>Yes (its own local scope), No (other local scope)</td></tr><tr><td>Override names in the built-in scope</td><td>Yes</td><td>Yes (during function execution)</td><td>Yes (during function execution)</td></tr><tr><td>Access or reference names that live in their enclosing scope</td><td>N/A</td><td>N/A</td><td>Yes</td></tr><tr><td>Modify or update names that live in their enclosing scope</td><td>N/A</td><td>N/A</td><td>No (unless declared <code>nonlocal</code>)</td></tr></tbody></table>

### Best practices

In Python, global names refer to variables that are defined in the global scope of a program. Global names can be accessed and modified from anywhere in the program, making them a powerful but potentially problematic programming tool.

While it is possible to modify global names from any place in your code using the global statement, this practice is generally considered bad programming practice for several reasons.&#x20;

* First, modifying global names can make it difficult to debug code since any statement in the program can change the value of a global name.&#x20;
* Second, global modifications can make code hard to understand since one must be aware of all statements that access and modify global names.&#x20;
* Finally, global modifications can make code impossible to reuse since the code is dependent on global names that are specific to a concrete program.

To avoid these potential problems, good programming practice recommends using local names rather than global names whenever possible. Self-contained functions that rely on local names are easier to debug and understand, and they make it easier to reuse code in different contexts. When using global names, it is important to try to use unique object names regardless of the scope you are in, to avoid confusion and potential conflicts with other parts of the program. Additionally, it is advisable to avoid modifying global names throughout a program and to avoid cross-module name modifications. Instead, global names should be used as constants that do not change during a program's execution.

### Conclusion

The concept of scope is an important aspect of programming. Understanding the scope of a variable can help you write code that is easier to maintain, debug, and reuse. In Python 3, variables can have global, local, or nested scope, which affects how they can be accessed and modified in the code. The global and nonlocal keywords can be used to access variables from outside of the current scope, but overuse of these keywords can make the code harder to understand. By mastering the concept of scope, you can become a more proficient Python 3 programmer, and write code that is more efficient and effective.

