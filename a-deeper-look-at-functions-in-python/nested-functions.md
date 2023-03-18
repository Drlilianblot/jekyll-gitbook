# Nested Functions

Functions are an essential part of programming, and they provide a way to modularize code and reuse it in different parts of a program. In Python, functions can be defined inside other functions, and such functions are called **nested functions**. This feature allows for more complex and modular code structures, enabling programmers to write more efficient and readable code.

In this section, we'll explore the concept of nested functions in Python 3 and explain their significance in programming.

## What are Nested Functions?

In Python, a nested function is a function that is defined inside another function. The inner function is a local function, meaning it is only accessible within the enclosing function. Nested functions have access to the variables and parameters of the enclosing function, and they can modify their values.

Nested functions provide a way to break down complex tasks into smaller, more manageable tasks. By encapsulating functionality within nested functions, we can create a more modular design, with each function handling a specific task.

Another benefit of using nested functions is that they allow us to keep our code clean and maintainable. By keeping related functions together, we can easily modify or debug them without affecting other parts of the program.

Let's take a look at an example of a nested function:

{% code lineNumbers="true" %}
```python
def greeting(name):
    def inner_greeting():
        return "Hello"
    return f"{inner_greeting()}, {name}!"

print(greeting("John"))
```
{% endcode %}

In this example, we define a function `greeting` that takes a name argument. Inside the `greeting` function, we define another function called `inner_greeting` that simply returns the string "Hello". We then use the inner function to construct the final greeting message by concatenating it with the input name and a comma.

When we call `greeting("John")`, the inner function `inner_greeting` is called as a part of the `greeting` function's execution (on line 4), and its return value is used to construct the final message. The output of the function is `"Hello, John!"`.

This is a simple example, but it demonstrates how nested functions can be used to break up complex logic into smaller, more manageable pieces.

Let's take a look at another example:

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

In this example, we define a global variable `x` with a value of `10`. We then define an outer function `outer_function` that defines a **local** variable `x` with a value of `5`.

We then define an inner function `inner_function` that prints the value of `x`. When we call `inner_function` from `outer_function`, it prints the value of `x`, which is `5`.

When we call `outer_function`, it prints the value of `x` from the local scope of `outer_function`. After calling `outer_function`, we print the value of the global variable `x`, which is still

When using nested functions, it's essential to understand the **scope of variables**. Variables defined within a function are considered to be in the local scope of that function, and they cannot be accessed from outside the function.

However, if a variable with the same name is defined in the enclosing function, the inner function will have access to that variable. If no variable with the same name is defined in the enclosing function, the inner function will look for the variable in the global scope.

