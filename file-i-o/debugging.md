# Debugging

When you are reading and writing files, you might run into problems with whitespace. These errors can be hard to debug because spaces, tabs and newlines are normally invisible:

```bash
>>> s = '1 2\t 3\n 4' 
>>> print(s) 
 1 2	 3
  4
>>>
```

The built-in function `repr` can help. It takes any object as an argument and returns a string representation of the object. For strings, it represents whitespace characters with backslash sequences:

```bash
>>> print(repr(s))
 '1 2\t 3\n 4' 
>>>
```

This can be helpful for debugging.

One other problem you might run into is that different systems use different characters to indicate the end of a line. Some systems use a newline, represented `'\n'`. Others use a return character, represented `'\r'`. Some use both. If you move files between different systems, these inconsistencies might cause problems.
