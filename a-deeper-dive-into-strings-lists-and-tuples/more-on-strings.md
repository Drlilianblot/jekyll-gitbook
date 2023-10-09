# More on Strings

## String traversal with a `for` loop

A lot of computations involve processing a string one character at a time. Often they start at the beginning, select each character in turn, do something to it, and continue until the end. This pattern of processing is called a **traversal**. One way to write a traversal is with a `while` loop:

{% code lineNumbers="true" %}
```python
fruit = 'banana'
index = 0 
while index < len(fruit): 
     letter = fruit[index] 
     print(letter) 
     index = index + 1 
```
{% endcode %}

This loop traverses the string and displays each letter on a line by itself. The loop condition is `index < len(fruit)`, so when `index` is equal to the length of the string, the condition is false, and the body of the loop is not executed. The last character accessed is the one with the index `len(fruit)-1`, which is the last character in the string.

**Exercise:** Write a function that takes a string as an argument and displays the letters backward, one per line.

<details>

<summary>Answer</summary>

{% code lineNumbers="true" %}
```python
def print_reversed(word):
    index = len(word) - 1
    while index >= 0:
        print(word[index])
        index -= 1
```
{% endcode %}

</details>

Another way to write a traversal is with a `for` loop:

{% code lineNumbers="true" %}
```python
for char in fruit: 
    print(char) 
```
{% endcode %}

Each time through the loop, the next character in the string is assigned to the variable `char`. The loop continues until no characters are left.

The following example shows how to use concatenation (string addition) and a `for` loop to generate an abecedarian series (that is, in alphabetical order). In Robert McCloskey's book "_Make Way for Ducklings_", the names of the ducklings are Jack, Kack, Lack, Mack, Nack, Ouack, Pack, and Quack. This loop outputs these names in order:

{% code lineNumbers="true" %}
```python
prefixes = 'JKLMNOPQ' 
suffix = 'ack'
for letter in prefixes: 
    print(letter + suffix) 
```
{% endcode %}

The output is:

```
Jack 
Kack 
Lack 
Mack 
Nack 
Oack 
Pack 
Qack 
```

Of course, that's not quite right because "Ouack" and "Quack" are misspelled.

**Exercise:** Modify the program to fix this error.

<details>

<summary>Answer</summary>

{% code lineNumbers="true" %}
```python
prefixes = 'JKLMNOPQ' 
suffix = 'ack'
for letter in prefixes: 
    if letter == 'O' or letter == 'Q':
        print(letter + 'u' + suffix) 
    else:
        print(letter + suffix) 
```
{% endcode %}

</details>

## Searching

What does the following function do?

{% code lineNumbers="true" %}
```python
def find(word, letter): 
    index = 0 
    while index < len(word): 
        if word[index] == letter: 
            return index 
        index = index + 1 
    return -1 
```
{% endcode %}

In a sense, `find` is the opposite of the `[ ]` operator. Instead of taking an index and extracting the corresponding character, it takes a character and finds the index where that character appears. If the character is not found, the function returns `-1`. This is the first example we have seen of a `return` statement inside a loop. If `word[index] == letter`, the function breaks out of the loop and returns immediately. If the character doesn't appear in the string, the program exits the loop normally and returns `-1`. This pattern of computation - traversing a sequence and returning when we find what we are looking for - is called a **search**.

**Exercise:** Modify `find` so that it has a third parameter, the index in `word` where it should start looking.

<details>

<summary>Answer</summary>

{% code lineNumbers="true" %}
```python
def find(word, letter, start): 
    index = start 
    while index < len(word): 
        if word[index] == letter: 
            return index 
        index = index + 1 
    return -1 
```
{% endcode %}

</details>

## Looping and counting

The following program counts the number of times the letter `a` appears in a string:

{% code lineNumbers="true" %}
```python
word = 'banana' 
count = 0 
for letter in word: 
    if letter == 'a': 
        count = count + 1 
print(count) 
```
{% endcode %}

This program demonstrates another pattern of computation called a **counter**. The variable `count` is initialized to `0` and then incremented each time an `a` is found. When the loop exits, `count` contains the result - the total number of `a`'s.

**Exercise:** Encapsulate this code in a function named `count`, and generalise it so that it accepts the string and the letter as arguments.

<details>

<summary>Answer</summary>

{% code lineNumbers="true" %}
```python
def count(word, char):
    count = 0 
    for letter in word: 
        if letter == char: 
            count = count + 1 
    print(count) 
```
{% endcode %}

</details>

**Exercise:** Rewrite this function so that instead of traversing the string from the beginning, it uses the three-parameter version of `find` from the previous section.

<details>

<summary>Answer</summary>

{% code lineNumbers="true" %}
```python
def count_with_find(word, char):
    count = 0 
    index = find(word, char, 0)
    while index >= 0:
        count += 1
        index = find(word, char, index + 1)
    print(count) 
```
{% endcode %}

</details>

## `String` methods

A `method` is similar to a function - it takes arguments and may return a value - but the syntax is different. For example, the method `upper` takes a string and returns a new string with all uppercase letters; Instead of the function syntax `upper(word)`, it uses the method syntax `word.upper()`. This is known as the **dot** notation.

```bash
>>> word = 'banana'
>>> new_word = word.upper() 
>>> print(new_word)
 BANANA 
>>>
```

This form of dot notation specifies the name of the method, `upper`, and the name of the string to apply the method to, `word`. The empty parentheses indicate that this method takes no argument.

A method call is called an **invocation**; in this case, we would say that we are invoking `upper` on the `word`. As it turns out, there is a string method named `find` that is remarkably similar to the function we wrote:

```bash
>>> word = 'banana' 
>>> index = word.find('a') 
>>> print(index) 
 1 
>>>
```

In this example, we invoke `find` on `word` and pass the letter we are looking for as a parameter. Actually, the `find` method is more general than our function; it can find substrings, not just characters:

```bash
>>> word.find('na') 
 2 
>>>
```

It can take as a second argument the index where it should start:

```bash
>>> word.find('na', 3)
 4 
>>>
```

And as a third argument the index where it should stop:

```bash
>>> name = 'bob' 
>>> name.find('b', 1, 2)
 -1
>>>
```

This search fails because `b` does not appear in the index range from `1` to `2` (not including `2`).

**Exercise:** There is a string method called `count` that is similar to the function in the previous exercise. Read the documentation of this method and write an invocation that counts the number of `a` in `banana`.

<details>

<summary>Answer</summary>

```bash
>>> word = 'banana'
>>> print(word.count('a'))
 3
>>>
```

</details>

## The `in` operator

The word `in` is a boolean operator that takes two strings and returns `True` if the first appears as a substring in the second:

```bash
>>> 'ana' in 'banana'
 True 
>>>'rama' in 'banana'
 False 
>>>
```

For example, the following function prints all the letters from `word1` that also appear in `word2`:

{% code lineNumbers="true" %}
```python
def in_both(word1, word2): 
    for letter in word1: 
        if letter in word2: 
            print(letter) 
```
{% endcode %}

With well-chosen variable names, Python sometimes reads like English. You could read this loop, "for (each) letter in (the first) word, if (the) letter (appears) in (the second) word, print (the) letter.

Here's what you get if you compare apples and oranges:

```bash
>>> in_both('apples', 'oranges')
 a e s 
```

## String comparison

The relational operators work on strings. To see if two strings are equal:

{% code lineNumbers="true" %}
```python
if word == 'banana': 
    print ('All right, bananas.') 
```
{% endcode %}

Other relational operations are useful for putting words in alphabetical order:

{% code lineNumbers="true" %}
```python
if word < 'banana': 
    print('Your word,' + word + ', comes before banana.') 
elif word > 'banana': 
    print('Your word,' + word + ', comes after banana.') 
else: 
    print('All right, bananas.') 
```
{% endcode %}

Python does not handle uppercase and lowercase letters the same way that people do. All the uppercase letters come before all the lowercase letters.

## String Formatting

Python f-strings are a convenient way to format strings by embedding expressions within curly braces `{}`. The `f` in f-strings stands for “formatted” and they were introduced in Python 3.6.

F-strings provide an easier, cleaner, and more concise way of formatting strings than the previous formatting methods available in Python. They allow you to insert values and expressions directly into string literals, making the code more readable and easier to maintain.

To create an f-string, you simply prepend the string literal with the letter "f" and then include the expressions you want to include inside curly braces. For example:

```bash
>>> name = "Alice"
>>> age = 25
>>> print(f"Hello, my name is {name} and I am {age} years old.")
 Hello, my name is Alice and I am 25 years old.
>>>
```

In this example, the f-string includes two expressions inside curly braces: `{name}` and `{age}`. When the string is evaluated, these expressions will be replaced with their corresponding values.

F-strings support a variety of expressions, including variables, literals, function calls, and arithmetic operations. You can also use f-strings to format numbers, dates, and times using specific formatting codes.

For example, to format a floating-point number with two decimal places, you can use the following code:

```bash
>>> pi = 3.14159265
>>> print(f"The value of pi is approximately {pi:.2f}.")
 The value of pi is approximately 3.14.
>>>
```

In this example, the `:.2f` after the expression specifies that the number should be formatted as a floating-point number with two decimal places.

Here's a table of some commonly used format specifiers:

<table><thead><tr><th width="194">Format specifier</th><th>Description</th></tr></thead><tbody><tr><td><code>:&#x3C;</code></td><td>Left align the value</td></tr><tr><td><code>:></code></td><td>Right align the value</td></tr><tr><td><code>:^</code></td><td>Center align the value</td></tr><tr><td><code>:0></code></td><td>Pad the value with zeroes on the left</td></tr><tr><td><code>:,</code></td><td>Add commas as thousands separators</td></tr><tr><td><code>:.2f</code></td><td>Format the value as a float with two decimal places</td></tr><tr><td><code>:e</code></td><td>Format the value in scientific notation</td></tr><tr><td><code>!s</code></td><td>Convert the value to a string</td></tr><tr><td><code>!r</code></td><td>Convert the value to a string and represent it as a valid Python expression</td></tr></tbody></table>

Below you can find some example of code using format specifiers.

1. Padding a number with zeroes using the `:0>` format specifier:

```bash
>>> x = 42
>>> print(f"The answer is: {x:0>4}")
 The answer is: 0042
>>>
```

2. Formatting a number as currency using the `:,.2f` format specifier:

```bash
>>> price = 12345.6789
>>> print(f"The price is: ${price:,.2f}")
 The price is: $12,345.68
>>>
```

3. Using the `!s` format specifier to convert a value to a string:

```bash
>>> x = 42
>>> print(f"The answer is: {x!s}") 
 The answer is: 42
>>>
```

4. Using the `!r` format specifier to convert a value to a string and represent it as a valid Python expression:

```bash
>>> x = "hello"
>>> print(f"The value of x is: {x!r}") 
 The value of x is: 'hello'
>>>
```

5. Using f-strings to format multiline strings:

{% code lineNumbers="true" %}
```python
name = "John"
age = 30
address = "123 Main St\nAnytown, USA"
message = f"""
Name: {name}
Age: {age}
Address:
{address}
"""
print(message)
```
{% endcode %}

Output:

```
Name: John
Age: 30
Address:
123 Main St
Anytown, USA
```

One of the biggest benefits of f-strings is that they make code more readable by eliminating the need for complicated string formatting syntax. For example, compare the following two code snippets:

Using f-strings:

{% code lineNumbers="true" %}
```python
name = "Alice"
age = 25
print(f"Hello, my name is {name} and I am {age} years old.")
```
{% endcode %}

Using old-style string formatting:

{% code lineNumbers="true" %}
```python
name = "Alice"
age = 25
print("Hello, my name is %s and I am %d years old." % (name, age))
```
{% endcode %}

The f-string version is much cleaner and easier to read. It's also less prone to errors, as it eliminates the need to manually count placeholders and arguments.

Another benefit of f-strings is that they are evaluated at runtime, which means you can use them to create dynamic strings that change based on the program's state. For example, you could use f-strings to create customized error messages that include specific details about the error.

To summarise, f-strings are a powerful and convenient way to format strings in Python. They make code more readable and easier to maintain by eliminating the need for complicated string formatting syntax. They also support a variety of expressions and formatting codes, making them versatile enough for a wide range of use cases.
