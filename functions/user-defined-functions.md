# User Defined Functions

## Function Definition

So far, we have only been using the functions that come with Python, but it is also possible to add new functions. A **function definition** specifies the name of a new function and the sequence of statements that execute when the function is called.

Here is an example:

{% code lineNumbers="true" %}
```python
def print_lyrics(): 
    print("I'm a lumberjack, and I'm okay.") 
    print("I sleep all night and I work all day.")
```
{% endcode %}

**`def`** is a keyword that indicates that this is a function definition. The name of the function is `print_lyrics`. The rules for function names are the same as for variable names: letters, numbers and some punctuation marks are legal, but the first character can't be a number. You can't use a keyword as the name of a function, and although not illegal, you should (**must** would be a better word) avoid having a variable and a function with the same name.

The empty parentheses after the name indicate that this function doesn't take any arguments.

The first line of the function definition is called the **header**; the rest is called the **body**. The header has to end with a colon and the body has to be indented. By convention, the indentation is always four spaces (see the [section on editors](debugging.md#editor)). The body can contain any number of statements.

The strings in the print statements are enclosed in double quotes. Single quotes and double quotes do the same thing; most people use single quotes except in cases like this where a single quote (which is also an apostrophe) appears in the string.

{% hint style="info" %}
Although function can be defined via the interpreter prompt, you are strongly encourage to write your code within scripts from now on.
{% endhint %}

Defining a function creates a variable with the same name.

```bash
>>> print(print_lyrics) 
 <function print_lyrics at 0x03092C00> 
>>> type(print_lyrics) 
 <class 'function'> 
>>>
```

The value of `print_lyrics` is a **function object**, which has type **function**.

The syntax for calling the new function is the same as for built-in functions:

```bash
>>> print_lyrics() 
 I'm a lumberjack, and I'm okay. 
 I sleep all night and I work all day. 
>>>
```

Once you have defined a function, you can use it inside another function. For example, to repeat the previous refrain, we could write a function called `repeat_lyrics`:

{% code lineNumbers="true" %}
```python
def repeat_lyrics(): 
    print_lyrics() 
    print_lyrics() 
```
{% endcode %}

And then call `repeat_lyrics`:

```bash
>>> repeat_lyrics() 
 I'm a lumberjack, and I'm okay. 
 I sleep all night and I work all day. 
 I'm a lumberjack, and I'm okay. 
 I sleep all night and I work all day.
>>>
```

## Definitions and uses

Pulling together the code fragments from the previous section, the whole program looks like this:

{% code lineNumbers="true" %}
```python
def print_lyrics(): 
    print("I'm a lumberjack, and I'm okay.") 
    print("I sleep all night and I work all day.")
    
def repeat_lyrics(): 
    print_lyrics() 
    print_lyrics()
    
repeat_lyrics() # function call
```
{% endcode %}

This program contains two function definitions: `print_lyrics` and `repeat_lyrics`. Function definitions get executed just like other statements, but the effect is to create function objects. The statements inside the function do not get executed until the function is called, and the function definition generates no output.

As you might expect, you have to create a function before you can execute it. In other words, the function definition has to be executed before the first time it is called.

<details>

<summary>Try it</summary>

Move the last line of this program to the top, so the function call appears before the definitions. Run the program and see what error message you get.

</details>

<details>

<summary>Try it</summary>

Move the function call back to the bottom and move the definition of `print_lyrics` after the definition of `repeat_lyrics`. What happens when you run this program?

</details>

## Flow of execution

In order to ensure that a function is defined before its first use, you have to know the order in which statements are executed, which is called the **flow of execution**. Execution always begins at the first statement of the program. Statements are executed one at a time, in order from top to bottom. Function definitions do not alter the flow of execution of the program, but remember that statements inside the function are not executed until the function is called.

A function call is like a detour in the flow of execution. Instead of going to the next statement, the flow jumps to the body of the function, executes all the statements there, and then comes back to pick up where it left off. That sounds simple enough, until you remember that one function can call another. While in the middle of one function, the program might have to execute the statements in another function. But while executing that new function, the program might have to execute yet another function!

Fortunately, Python is good at keeping track of where it is, so each time a function completes, the program picks up where it left off in the function that called it. When it gets to the end of the program, it terminates. What's the moral of this sordid tale? When you read a program, you don't always want to read from top to bottom. Sometimes it makes more sense if you follow the flow of execution.

## Parameters and arguments

Some of the built-in functions we have seen require arguments. For example, when you call `math.sin` you pass a number as an argument. Some functions take more than one argument like `math.pow` takes two, the base and the exponent.

Inside the function, the arguments are assigned to variables called **parameters**. Here is an example of a user-defined function that takes an argument:

{% code lineNumbers="true" %}
```python
def print_twice(word): 
    print(word) 
    print(word)
```
{% endcode %}

This function assigns the argument to a parameter named `word`. When the function is called, it prints the value of the parameter (whatever it is) twice. This function works with any value that can be printed.

```bash
>>> print_twice('Spam') 
 Spam
 Spam 
>>> print_twice(17)
 17 
 17 
>>> print_twice(math.pi)
 3.14159265359 
 3.14159265359 
>>>
```

The same rules of composition that apply to built-in functions also apply to user-defined functions, so we can use any kind of expression as an argument for `print_twice`:

<pre class="language-bash"><code class="lang-bash"><strong>>>> print_twice('Spam ' * 4) 
</strong><strong> Spam Spam Spam Spam 
</strong><strong> Spam Spam Spam Spam 
</strong><strong>>>> print_twice(math.cos(math.pi)) 
</strong><strong> -1.0 
</strong><strong> -1.0
</strong><strong>>>> 
</strong></code></pre>

The argument is evaluated before the function is called, so in the examples the expressions `'Spam '*4` and `math.cos(math.pi)` are only evaluated once.

You can also use a variable as an argument:

```shell
>>> michael = 'Eric, the half a bee.' 
>>> print_twice(michael) 
 Eric, the half a bee. 
 Eric, the half a bee. 
>>>
```

{% hint style="info" %}
The name of the variable we pass as an argument (`michael`) has nothing to do with the name of the parameter (`word`).
{% endhint %}

## Variables and parameters are local

When you create a variable inside a function, it is **local**, which means that it only exists inside the function. For example:

{% code lineNumbers="true" %}
```python
def cat_twice(part1, part2): 
    cat = part1 + part2 
    print_twice(cat) 
```
{% endcode %}

This function takes two arguments, concatenates them, and prints the result twice. Here is an example that uses it:

```sh
>>> line1 = 'Bing tiddle ' 
>>> line2 = 'tiddle bang.' 
>>> cat_twice(line1, line2) 
 Bing tiddle tiddle bang. 
 Bing tiddle tiddle bang. 
>>>
```

When `cat_twice` terminates, the variable `cat` is destroyed. If we try to print it, we get an exception:

```sh
>>> print(cat) 
 NameError: name 'cat' is not defined 
```

Parameters are also **local**. For example, outside `print_twice`, there is no such thing as `word`.

## Stack diagrams

To keep track of which variables can be used where, it is sometimes useful to draw a **stack diagram**. Like state diagrams, stack diagrams show the value of each variable, but they also show the function each variable belongs to. Each function is represented by a **frame**. A frame is a box with the name of a function beside it and the parameters and variables of the function inside it. The stack diagram for the previous example looks like this:

<figure><img src="../.gitbook/assets/stack (1).png" alt="" width="376"><figcaption><p>Stack diagram showing the values assigned to the functions parameters</p></figcaption></figure>

The frames are arranged in a stack that indicates which function called which, and so on. In this example, `print_twice` was called by `cat_twice`, and `cat_twice` was called by **`main`**, which is a special name for the topmost frame. When you create a variable outside of any function, it belongs to **main**. Such variable is said to be **global** as opposed to local.

Each parameter refers to the same value as its corresponding argument. So, `part1` has the same value as `line1`, `part2` has the same value as `line2`, and `word` has the same value as `cat`. If an error occurs during a function call, Python prints the name of the function, and the name of the function that called it, and the name of the function that called _that_, all the way back to **main**.

For example, if you try to access `cat` from within `print_twice` - for example by adding the statement `print(cat)` in the definition of `print_twice` (as shown below in the file `test.py`),

{% code title="test.py" lineNumbers="true" %}
```python
def print_twice(word): 
    print(word) 
    print(word)
    print(cat)
    
def cat_twice(part1, part2): 
    cat = part1 + part2 
    print_twice(cat) 
    
line1 = 'Bing tiddle ' 
line2 = 'tiddle bang.' 
cat_twice(line1, line2) 
```
{% endcode %}

And then executing the script, you get a `NameError`:

```sh
Traceback (innermost last): 
  File "test.py", line 12, in __main__ 
     cat_twice(line1, line2) 
  File "test.py", line 8, in cat_twice 
     print_twice(cat) 
  File "test.py", line 4, in print_twice 
     print(cat) 
NameError: name 'cat' is not defined 
```

This list of functions is called a **traceback**. It tells you what program file the error occurred in, and what line, and what functions were executing at the time. It also shows the line of code that caused the error. The order of the functions in the traceback is the same as the order of the frames in the stack diagram. The function that is currently running is at the bottom.

## Void functions and non-void functions

Some of the functions we are using, such as the `math` functions, yield results; for lack of a better name, we call them **non-void functions**. Other functions, like `print_twice`, perform an action but don't return a value. They are called **void functions**.

When you call a non-void function, you almost always want to do something with the result; for example, you might assign it to a variable or use it as part of an expression:

{% code lineNumbers="true" %}
```python
x = math.cos(radians) 
golden = (math.sqrt(5) + 1) / 2 
```
{% endcode %}

When you call a function in interactive mode, Python displays the result:

```sh
>>> math.sqrt(5)
 2.2360679774997898 
>>>
```

But in a script, if you call a non-void function all by itself, the return value is lost forever!

{% code title="nonvoidfunction.py" lineNumbers="true" %}
```python
import math

math.sqrt(5) 
```
{% endcode %}

This script computes the square root of 5, but since it doesn't store or display the result, it is not very useful.

Void functions might display something on the screen or have some other effect, but they don't have a return value. If you try to assign the result to a variable, you get a special value called `None`. Note the capital letter **`N`** in `None`.

```bash
>>> result = print_twice('Bing') 
 Bing Bing 
>>> print(result) 
 None
>>> 
```

The value `None` is not the same as the string `'None'`. It is a special value that has its own type:

```sh
>>> print(type(None)) 
 <type 'NoneType'> 
>>>
```

The functions we have written so far are all void. We will start writing non-void functions in a few chapters.
