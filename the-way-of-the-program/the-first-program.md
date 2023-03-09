# The first program

Traditionally, the first program you write in a new language is called `"Hello, World!"` because all it does is display the words, "Hello, World!"

Before we can write our first program we need to launch the Python interpreter. In this book, we assume you have Python 3 installed on the Windows 10 or later operating system. There are two ways to launch Python:

* Open a command window, and at the prompt type `python.` If the interpreter is not started like shown in the figure below, you may want to check that Python is in your `PATH` environment variable.

<figure><img src="../.gitbook/assets/PythonShellCMD.png" alt=""><figcaption><p>Using the Python interpreter from the command shell</p></figcaption></figure>

* Open IDLE(Python 3.6 32 bits) from the Windows start menu. A Python shell opens and is ready to accept your code:

<figure><img src="../.gitbook/assets/IDLEshell.png" alt=""><figcaption><p>Using the Python interpreter via IDLE</p></figcaption></figure>

Now that we have a Python shell opened, we can write our program. In Python 3, it looks like this:

```python
>>> print('Hello, World!') 
Hello, World!
```

The quotation marks in the program mark the beginning and end of the text to be displayed; they don't appear in the result.

Now that we can start programming, it might be a good time to illustrate the type of errors we may encounter whilst programming. The first one we mentioned was a syntax error like this one:

```python
>>> 1 + 2) 
SyntaxError: invalid syntax
>>>
```

where the opening bracket is missing.

The second type of error are runtime errors like the division by zero shown here:

```python
>>> print(10/0) 
Traceback (most recent call last): File "<pyshell#1>", line 1, in print(10/0) 
ZeroDivisionError: division by zero
>>>
```

Probably the most challenging one is a semantic error. For example, if we try to convert a temperature $$t_F$$ in Fahrenheit into Celsius the formula to use is:

$$
\begin{equation*} t_C = \frac{5}{9}(t_F - 32) \end{equation*}
$$

Now if we write the following implementation:

```python
>>> print('Fahrenheit 35 in Celsius degree is:', 5/9*35-32) 
Fahrenheit 35 in Celsius degree is: -12.555555555555554
```

the program runs and does not create any error. Does that mean that the program is correct? Unfortunately, NO. The result should have been `1.66` not `-12.55`.

#### Exercise

Write the correct implementation of the conversion from Fahrenheit to Celsius.

<details>

<summary>Answer</summary>

```python
print('Fahrenheit 35 in Celsius degree is:', 5/9*(35-32))
```

</details>

In conclusion, it is not because your program runs and returns a result that your work is finished. You must ensure that the returned result is correct. It is essential when implementing a code to define a series of tests (i.e. a series of known outputs given certain inputs) that can validate your code.
