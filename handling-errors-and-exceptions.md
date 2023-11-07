# 12 - Handling Errors and Exceptions

{% embed url="https://youtu.be/7Kf-gOQV2RU?si=ZA7P_57CQteQyvxt" %}

In the realm of programming, errors and unexpected situations are inevitable. To handle these scenarios gracefully and maintain the stability and reliability of your software, the concept of raising and catching exceptions is a fundamental technique. Exceptions are objects that represent errors or exceptional conditions in your code. They provide a structured and efficient way to deal with issues that can arise during program execution.

## Raising exceptions

Raising an exception in programming means intentionally triggering an error or an exceptional condition within your code. When an exception is raised, it signifies that something unexpected or erroneous has occurred during the execution of your program. This action is a deliberate way to signal that a problem exists and needs to be addressed.

{% embed url="https://youtu.be/mTXgx52l9YU" %}

Here are the key aspects of raising exceptions:

1. **Intentional Error Signalling**: Raising an exception is a way for programmers to signal that a specific condition or scenario requires special attention due to its exceptional or erroneous nature. It's akin to saying, "Something unusual happened here, and we need to handle it."
2. **Exception Object**: When an exception is raised, it typically generates an exception object that contains information about the error, such as its type and an optional error message. This information is used for debugging and error handling.
3. **Interrupting Normal Flow**: Raising an exception interrupts the normal flow of the program. If the exception is not caught and handled somewhere in the code, it will propagate up the call stack, potentially leading to program termination.
4. **Structured Error Handling**: Exception handling provides a structured way to deal with errors. It separates the code that detects and raises exceptions from the code that handles them. This separation of concerns makes the code more maintainable and readable.

Here's an example of raising an exception:

```python
def divide(a, b):
    if b == 0:
        raise ZeroDivisionError("Division by zero is not allowed")
    return a / b

try:
    result = divide(10, 0)
except ZeroDivisionError as e:
    print(f"Error: {e}")
else:
    print(f"Result: {result}")
```

In this code snippet, the `divide` function raises a `ZeroDivisionError` if the denominator (`b`) is zero. This exception is intentionally triggered to handle the case where division by zero occurs. When the exception is raised, it is caught in a `try...except` block, and an error message is printed. If no exception occurs, the result of the division is printed.

Raising exceptions is a fundamental part of error handling in programming. It allows you to detect and respond to unexpected situations in a controlled and structured manner, making your code more robust and reliable.

### The Use Cases for Raising Exceptions

Raising exceptions serves various purposes in programming, making it a versatile and indispensable tool:

1. **Error Signalling**: Exceptions are primarily used to signal that something unexpected or erroneous has occurred in your code. Whether it's a division by zero, an attempt to access a non-existent file, or an invalid input, exceptions provide a clear and standardized way to communicate such issues.
2. **Error Recovery**: Exceptions allow you to gracefully recover from errors or exceptional conditions. Instead of crashing your program, you can catch and handle exceptions, potentially allowing the program to continue its execution or terminate gracefully with meaningful error messages.
3. **Debugging Aid**: Exceptions can be invaluable during the debugging process. When an exception is raised, it typically includes a traceback, which shows the call stack, helping you identify where the error originated. This information is immensely helpful in diagnosing and fixing issues.
4. **Program Flow Control**: Exceptions can also be used as a control flow mechanism. By raising and catching exceptions in specific situations, you can direct the flow of your program based on various conditions. This can be useful for implementing complex logic or handling specific scenarios.

## Catching exceptions

A lot of things can go wrong when you try to read and write files. If you try to open a file that doesn't exist, you get an `OSError`:

```bash
>>> fin = open('bad_file') 
  FileNotFoundError: [Errno 2] No such file or directory: 'bad_file'
>>>
```

And if you try to open a directory for reading, you get

```bash
>>> fin = open('/home') 
  PermissionError: [Errno 13] Permission denied: '/home' 
```

Note that `FileNotFoundError` and `PermissionError` are both  `OSError`, in other words they are more specific types of `OSError`. In object oriented programming we say that `OSError` is the super class of `FileNotFoundError` and `PermissionError`. The object oriented paradigm and the concepts of inheritance, super classes and subclasses is beyond the scope of this course and this book.

To avoid these errors, you could use functions like `os.path.exists()` and `os.path.isfile()`, but it would take a lot of time and code to check all the possibilities.

### `try` statement

It is better to go ahead and try, and deal with problems if they happen, which is exactly what the `try` statement does. The syntax is similar to an `if` statement:

{% code lineNumbers="true" %}
```python
try:
    fin = open('bad_file') 
    for line in fin: 
        print(line) 
    fin.close() 
except: 
    print('Something went wrong.')
```
{% endcode %}

Python starts by executing the `try` clause. If all goes well, it skips the `except` clause and proceeds. If an exception occurs, it jumps out of the `try` clause and executes the `except` clause.&#x20;

Handling an exception with a `try` statement is called **catching** an exception. In this example, the `except` clause prints an error message that is not very helpful. In general, catching an exception gives you a chance to fix the problem, or try again, or at least end the program gracefully.

### `finally` clause&#x20;

There are two options to the `try-except` statement. The first one is the clause `finally`. All code included in the `finally` clause will be executed, whether an exception occurred or not. This is a good place to clean up our program. For example this is a good place to close a file if it has been open in the `try` clause. The code below shows how it is done.&#x20;

{% code lineNumbers="true" %}
```python
fin = None 
try:
    print('TRY: open file.') 
    fin = open('words.txt') 
    print('--> file open successfully.')
    for line in fin: 
        print('--> ' + line) 
except: 
    print('EXCEPT: Something went wrong.') 
finally: 
    print('FINALLY: cleaning up.') 
    if fin is not None: 
        print('--> closing the file') 
        fin.close()
```
{% endcode %}

First we set the variable `fin` to `None`. In the `try` clause, we open a file and then assign it to `fin`. Two things can happen:

* An exception occurs while we are trying to open the file, `fin` is not assigned any new object and contains the value `None`. The program jumps directly to the `except` clause and executes the code in the `except` block. Then the program jumps to the `finally` clause and executes the code there.
* The file is opened successfully, `fin` is assigned the file object, and the rest of the code in the `try` statement is executed. Then the program jumps to the `finally` clause and executes the code there.

### `else` clause&#x20;

The second option is the `else` clause, which should be after the `except` clause and before the `finally` clause. The code in the `else` clause is executed only if no exceptions were raised. It is executed before the `finally` clause. The `else` clause is use for all code that does not raise any exception.

In our previous code, it would be the place to read the lines in the file. The refactored code is:

{% code lineNumbers="true" %}
```python
fin = None 
try:
    print('TRY: open file.') 
    fin = open('word.txt') 
    print('--> file open successfully.')
except: 
    print('EXCEPT: Something went wrong.') 
else: 
    print('ELSE: Do your thing if all went well.') 
    for line in fin: 
        print('--> ' + line)
finally: 
    print('FINALLY: cleaning up.') 
    if fin is not None: 
        print('--> closing the file.') 
        fin.close() 
```
{% endcode %}

As you can see, the `try` clause contains only the code that may raise an exception.&#x20;

* If an exception occurs whilst opening the file, the program jumps to the `except` clause and then executes the `finally` clause. In this case, the output is:

```
TRY: open file. 
EXCEPT: Something went wrong. 
FINALLY: cleaning up.
```

* If no exceptions are raised, the program skips the `except` clause, and jumps to the `else` clause. Once the code in the `else` clause has been executed, the program jumps to the `finally` clause. In this case, the output is:

```
TRY: open file. 
--> file open successfully. 
ELSE: Do your thing if all went well. 
--> line 1 of text file
--> line 2 of text file
--> last line of text file
FINALLY: cleaning up. 
--> closing the file. 
```

## Catching multiple exceptions

We have seen that a try statement allows you to catch and handle exceptions that may occur during program execution. It provides a way to handle errors gracefully, without crashing the program. But what happens if different types of errors may occur, and how can we handle them differently?

This is where multiple except clauses come in. A try statement with multiple except clauses looks like this:

```python
try:
    # some code that may raise an exception
except ExceptionType1:
    # handle exception of type ExceptionType1
except ExceptionType2:
    # handle exception of type ExceptionType2
...
except ExceptionTypeN:
    # handle exception of type ExceptionTypeN
```

In this example, the try block contains the code that may raise an exception. The except clauses are used to handle exceptions of different types. Each except clause is associated with a specific exception type. When an exception is raised in the try block, Python checks each except clause in order, and executes the first one that matches the exception type. If none of the except clauses match the exception type, the exception is passed up to the calling code.

It's important to note that the except clauses should be ordered from the most specific to the most general exception type. This is because Python checks each except clause in order, and the first one that matches the exception type is executed. If you have a more general exception type (like `OSError`) before a more specific one (like `FileNotFoundError`), the more general one will catch the exception first, and the more specific one will never be executed.

Here's an example of a try statement with multiple except clauses:

```python
try:
    num1 = int(input("Enter a number: "))
    num2 = int(input("Enter another number: "))
    result = num1 / num2
    print("Result:", result)
except ZeroDivisionError:
    print("Error: division by zero")
except ValueError:
    print("Error: invalid input")
except:
    print("Unknown error occurred")
```

In this example, the user is asked to enter two numbers. If the user enters an invalid input (i.e. something that can't be converted to an integer), a `ValueError` will be raised. If the user enters 0 as the second number, a `ZeroDivisionError` will be raised. If any other type of exception occurs, the last except clause will handle it.

You can also use a tuple to specify multiple exception types in a single except clause. Here's an example:

```python
try:
    # some code that may raise an exception
except (ExceptionType1, ExceptionType2, ..., ExceptionTypeN):
    # handle exceptions of type ExceptionType1, ExceptionType2, ..., ExceptionTypeN
```

In this example, the except clause will catch exceptions of any of the specified types. This can be useful if you want to handle a group of related exceptions in the same way.

Here's an example of using a tuple to catch multiple exception types:

```python
try:
    num1 = int(input("Enter a number: "))
    num2 = int(input("Enter another number: "))
    result = num1 / num2
    print("Result:", result)
except (ZeroDivisionError, ValueError):
    print("Error: invalid input or division by zero")
except:
    print("Unknown error occurred")
```

In this example, the same except clause is used to handle both `ZeroDivisionError` and `ValueError` exceptions.

In conclusion, multiple except clauses in a try statement provide a way to handle exceptions of different types in different ways. By specifying one or more except clauses, you can catch specific exceptions and handle them gracefully, without crashing the program.

## The Utility of Exception Handling

Exception handling is a critical aspect of writing robust and maintainable code. Here's why raising and handling exceptions is so useful:

1. **Graceful Degradation**: Exception handling allows your program to fail gracefully. Instead of abruptly crashing, it can inform users of issues and continue functioning in a degraded state or shut down cleanly.
2. **Error Isolation**: By raising exceptions at the point of error, you isolate problems and prevent them from propagating throughout your code. This makes it easier to locate and fix issues.
3. **Enhanced Debugging**: When exceptions are raised, you get a clear indication of where things went wrong. This significantly speeds up the debugging process, reducing the time it takes to identify and rectify problems.
4. **Predictable Behaviour**: Exception handling provides a structured way to deal with errors, making your code more predictable and reliable. It ensures that errors are handled consistently and doesn't leave the program in an undefined state.

## When to Use Exception Handling

While exceptions are a powerful tool, they should be used judiciously. Here are some guidelines on when to use exception handling:

1. **Use Exceptions for Exceptional Conditions**: Reserve exception handling for situations that are genuinely exceptional and unexpected. Routine, predictable scenarios should be handled with standard control flow mechanisms (if-else statements, for example).
2. **Consider Performance**: Exception handling can introduce performance overhead, so it's essential to balance its use. For critical sections of code where performance is crucial, consider alternative error-checking strategies if possible.
3. **Keep It Simple**: Exception handling should not complicate your code unnecessarily. Avoid using exceptions for flow control in routine scenarios; they should be reserved for error handling.
4. **Provide Meaningful Messages**: When raising exceptions, include informative error messages that help developers understand the problem. This aids in debugging and makes your code more user-friendly.

In conclusion, raising exceptions in programming is a vital technique for handling errors and exceptional conditions. When used appropriately, it enhances the robustness, maintainability, and reliability of your software. By following best practices and using exceptions judiciously, you can build software that gracefully handles unexpected situations, making it more resilient and user-friendly.
