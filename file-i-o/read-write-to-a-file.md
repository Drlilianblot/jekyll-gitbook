# Read/Write to a file

## Reading from a file

In this chapter we will be using a list of English words. There are lots of word lists available on the Web, but the one most suitable for our purpose is one of the word lists collected and contributed to the public domain by Grady Ward as part of the [Moby lexicon project](https://www.wikipedia.org/wiki/Moby\_Project). It is a list of 113,809 official crosswords; that is, words that are considered valid in crossword puzzles and other word games. In the Moby collection, the filename is `113809of.fic`; <mark style="background-color:red;">I include a copy of this file, with the simpler name</mark> <mark style="background-color:red;"></mark><mark style="background-color:red;">`words.txt`</mark><mark style="background-color:red;">, along with Swampy</mark>.

This file is in plain text, so you can open it with a text editor, but you can also read it from Python. The built-in function `open` takes the name of the file as a parameter and returns a **file object** you can use to read the file.

```bash
>>> fin = open('words.txt')
>>> print(fin)
 <open file 'words.txt', mode 'r' at 0xb7f4b380>
>>>
```

`fin` is a common name for a file object used for input. Mode `'r'` indicates that this file is open for reading (as opposed to `'w'` for writing).

The file object provides several methods for reading, including `readline`, which reads characters from the file until it gets to a newline and returns the result as a string:

```bash
>>> fin.readline()
 'aa\r\n'
>>>
```

The first word in this particular list is `aa`, which is a kind of lava. The sequence `\r\n` represents two whitespace characters, a carriage return and a newline, that separate this word from the next.

The file object keeps track of where it is in the file, so if you call `readline` again, you get the next word:

```bash
>>> fin.readline()
 'aah\r\n' 
>>>
```

The next word is `aah`, which is, believe it or not, a perfectly legitimate word. If the whitespace is bothering you, we can get rid of it with the string method `strip()`:

```
>>> line = fin.readline()
>>> word = line.strip()
>>> word
 'aahed'
>>>
```

You can also use a file object as part of a `for` loop. This program reads `words.txt` and prints each word, one per line:

{% code lineNumbers="true" %}
```python
fin = open('words.txt') 
for line in fin: 
    word = line.strip() 
    print(word) 
```
{% endcode %}

When you are done reading, you should close the file as a matter of good practice.

```bash
>>> fin.close() 
>>>
```

## Writing to a file

To write a file, you have to open it with mode `'w'` as a second parameter:

```bash
>>> fout = open('output.txt', 'w')
>>> print(fout)
 <open file 'output.txt', mode 'w' at 0xb7eb2410>
>>>
```

If the file already exists, opening it in write mode clears out the old data and starts fresh, so be careful! If the file doesn't exist, a new one is created.

The `write` method puts data into the file.

```bash
>>> line1 = "This here's the wattle,\n" 
 fout.write(line1)
>>>
```

Again, the file object keeps track of where it is, so if you call `write` again, it adds the new data to the end.

```bash
>>> line2 = "the emblem of our land.\n" 
 fout.write(line2) 
>>>
```

When you are done writing, you have to close the file.

```bash
>>> fout.close() 
>>>
```

## `printf`-style String Formatting

The argument of `write` has to be a string, so if we want to put other values in a file, we have to convert them to strings. The easiest way to do that is with `str`:

```bash
>>> fout = open('output.txt', 'w')
>>> x = 52 
>>> fout.write(str(x)) 
>>>
```

An alternative is to format the string using `f-strings`. `F-strings` are covered in the section "[More on Strings](../a-deeper-dive-into-strings-lists-and-tuples/more-on-strings.md#string-formatting)". You are strongly encouraged to use `f-strings` however, knowing the old ways of formatting string using the format operator (`%`) is quite useful as it is similar in several languages.&#x20;

When applied to integers, `%` is the modulus operator. But when the first operand is a string, `%` is the format operator. The first operand is the **format string**, which contains one or more **format sequences**, which specify how the second operand is formatted. The result is a string. For example, the format sequence `'%d'` means that the second operand should be formatted as an integer (`d` stands for "decimal"):

```bash
>>> camels = 42
>>> '%d' % camels
 '42' 
>>>
```

The result is the string `'42'`, which is not to be confused with the integer value `42`.  A format sequence can appear anywhere in the string, so you can embed a value in a sentence:

```bash
>>> camels = 42 
>>> 'I have spotted %d camels.' % camels
 'I have spotted 42 camels.'
>>>
```

If there is more than one format sequence in the string, the second argument has to be a tuple. Each format sequence is matched with an element of the tuple, in order. The following example uses `'%d'` to format an integer, `'%g'` to format a floating-point number (don't ask why), and `'%s'` to format a string:

```bash
>>> 'In %d years I have spotted %g %s.' % (3, 0.1, 'camels')
 'In 3 years I have spotted 0.1 camels.' 
>>>
```

The number of elements in the tuple has to match the number of format sequences in the string. Also, the types of the elements have to match the format sequences:

```bash
>>> '%d %d %d' % (1, 2) 
 TypeError: not enough arguments for format string 
>>> '%d' % 'dollars' 
 TypeError: illegal argument type for built-in operation 
>>>
```

In the first example, there aren't enough elements; in the second, the element is the wrong type.

You can specify the number of digits as part of the format sequence. For example, the sequence `'%8.2f'` formats a floating-point number to be 8 characters long, with 2 digits after the decimal point:

```bash
>>> '%8.2f' % 3.14159
 '    3.14' 
>>>
```

The result takes up eight spaces with two digits after the decimal point. You can pad the string with 0s instead of blank spaces as shown below:

```bash
>>> '%08.2f' % 3.14159
 '00003.14'
>>>
```

The format operator is powerful, but it can be difficult to use. You can read more about it on the [python 3 print-f string formatting page](https://docs.python.org/3/library/stdtypes.html#printf-style-string-formatting).

