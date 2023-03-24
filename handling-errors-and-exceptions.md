# Handling Errors and Exceptions

## Catching exceptions

A lot of things can go wrong when you try to read and write files. If you try to open a file that doesn't exist, you get an `IOError`:

```bash
>>> fin = open('bad_file') 
  FileNotFoundError: [Errno 2] No such file or directory: 'bad_file'
>>>
```

And if you try to open a directory for reading, you get

```bash
>>> fin = open('/home') 
  IOError: [Errno 21] Is a directory 
```

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
