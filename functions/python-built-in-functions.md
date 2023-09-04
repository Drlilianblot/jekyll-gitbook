# Python "built-in" Functions

## Function calls

In the context of programming, a **function** is a named sequence of statements that performs a computation. When you define a function, you specify the name and the sequence of statements. Later, you can "call" the function by name.\
We have already seen one example of a **function call**:

```bash
>>>type(32) 
 <type 'int'>
>>>
```

The name of the function is **`type`**. The expression in parentheses is called the **argument** of the function. The result, for this function, is the type of the argument.

It is common to say that a function "takes'' an argument and "returns'' a result. The result is called the **return value**.

## Type conversion functions

Python provides **built-in** functions that convert values from one type to another. The `int` function takes any value and converts it to an integer, if it can, or complains otherwise:

```bash
>>> int('32')
 32 
>>> int('Hello') 
 Traceback (most recent call last): 
     File "<pyshell#40>", line 1, 
         in int('hello')
 ValueError: invalid literal for int() with base 10: 'Hello' 
```

`int` can convert floating-point values to integers, but it doesn't round off; it chops off the fraction part:

```bash
>>> int(3.99999)
 3
>>> int(-2.3)
 -2 
>>>
```

`float` converts integers and strings to floating-point numbers:

```bash
>>> float(32) 
 32.0 
>>> float('3.14159') 
 3.14159 
>>>
```

Finally, `str` converts its argument to a string:

```bash
>>> str(32)
 '32' 
>>> str(3.14159)
 '3.14159'
>>>
```

We know that the values returned are strings due to the single quotes around the numbers.

## Common built-in functions

Python provides many useful function for common programming tasks. We have already seen one, the **print**} function. A subset of the built-in function is given in the table below:

| Function          | Description                                                                                           | Example                                                                                                |
| ----------------- | ----------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------ |
| `abs(x)`          | Returns the absolute value for `x`.                                                                   | `abs(-2)` is 2.                                                                                        |
| `max(x1, x2,...)` | Returns the largest among `x1`, `x2`, ...                                                             | `max(1, 5, 2)` is 5.                                                                                   |
| `min(x1, x2,...)` | Returns the smallest among `x1`, `x2`, ...                                                            | `min(1, 5, -2)` is -2.                                                                                 |
| `pow(a, b)`       | Returns $$a^b$$. Same as `a**b`.                                                                      | `pow(2, 3)` is 8.                                                                                      |
| `round(x)`        | Returns an integer nearest to `x`. If `x` is equally close to two integers, the even one is returned. | <p><code>round(5.4)</code> is 5,<br><code>round(3.5)</code> is 4,<br><code>round(4.5)</code> is 4.</p> |

## Keyboard input

The programs we have written so far are a bit rude in the sense that they accept no input from the user. They just do the same thing every time.

Python provides a built-in function called `input` that gets input from the keyboard. When this function is called, the program stops and waits for the user to type something. When the user presses the "Return" or "Enter" key, the program resumes and `input` returns what the user typed as a string.

```bash
>>> user_input = input()
 What are you waiting for? 
>>> print(user_input) 
 What are you waiting for? 
>>>
```

Before getting input from the user, it is a good idea to print a prompt telling the user what to input. The function `input` can take a prompt as an argument:

```bash
>>> name = input('What...is your name?\n') 
 What...is your name? 
 Arthur, King of the Britons! 
>>> print(name)
 Arthur, King of the Britons! 
>>>
```

The sequence `'\n'` at the end of the prompt represents a **newline**, which is a special character that causes a line break. That's why the user's input appears below the prompt.

If you expect the user to type an integer, you can try to convert the return value to am `int`:

```bash
>>> prompt = 'What is the velocity of an unladen swallow?\n' 
>>> speed = input(prompt) 
 What is the velocity of an unladen swallow?
 17 
>>> int(speed) 
 17 
>>>
```

But if the user types something other than a string of digits, you get an error:

```bash
>>> speed = input(prompt) 
 What is the velocity of an unladen swallow? 
 What do you mean, an African or a European swallow? 
>>> int(speed) 
 Traceback (most recent call last): 
     File "<pyshell#4>", line 1, 
         in int(speed) 
 ValueError: invalid literal for int() with base 10: 'What do you mean, an 
             African or a European swallow?' 
>>>
```

We will see how to handle this kind of error later.
