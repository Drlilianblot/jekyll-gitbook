# File I/O

## Persistence

Most of the programs we have seen so far are transient in the sense that they run for a short time and produce some output, but when they end, their data disappears. If you run the program again, it starts with a clean slate.

Other programs are **persistent**: they run for a long time (or all the time); they keep at least some of their data in permanent storage (a hard drive, for example); and if they shut down and restart, they pick up where they left off.&#x20;

Examples of persistent programs are operating systems, which run pretty much whenever a computer is on, and web servers, which run all the time, waiting for requests to come in on the network. One of the simplest ways for programs to maintain their data is by reading and writing text files. A text file is a sequence of characters stored on a permanent medium like a hard drive, flash memory, or CD-ROM.

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

## \section{Format operator}

\index{format operator} \index{operator!format}

The argument of {\tt write} has to be a string, so if we want to put other values in a file, we have to convert them to strings. The easiest way to do that is with {\tt str}:

\beforeverb \begin{pyinterpreter}

> > > x = 52 f.write(str(x)) \end{pyinterpreter} \afterverb % An alternative is to use the {\bf format operator}, {\tt %\}. When applied to integers, {\tt %\} is the modulus operator. But when the first operand is a string, {\tt %\} is the format operator. % \index{format string} % The first operand is the {\bf format string}, which contains one or more {\bf format sequences}, which specify how the second operand is formatted. The result is a string. % \index{format sequence} % For example, the format sequence \verb"'%d'" means that the second operand should be formatted as an integer ({\tt d} stands for \`\`decimal''):

\beforeverb \begin{pyinterpreter}

> > > camels = 42 '%d' % camels '42' \end{pyinterpreter} \afterverb % The result is the string \verb"'42'", which is not to be confused with the integer value {\tt 42}. % A format sequence can appear anywhere in the string, so you can embed a value in a sentence:

\beforeverb \begin{pyinterpreter}

> > > camels = 42 'I have spotted %d camels.' % camels 'I have spotted 42 camels.' \end{pyinterpreter} \afterverb % If there is more than one format sequence in the string, the second argument has to be a tuple. Each format sequence is matched with an element of the tuple, in order. % The following example uses \verb"'%d'" to format an integer, \verb"'%g'" to format a floating-point number (don't ask why), and \verb"'%s'" to format a string:

\beforeverb \begin{pyinterpreter}

> > > 'In %d years I have spotted %g %s.' % (3, 0.1, 'camels') 'In 3 years I have spotted 0.1 camels.' \end{pyinterpreter} \afterverb % The number of elements in the tuple has to match the number of format sequences in the string. Also, the types of the elements have to match the format sequences:

\index{exception!TypeError} \index{TypeError}

\beforeverb \begin{pyinterpreter}

> > > '%d %d %d' % (1, 2) TypeError: not enough arguments for format string '%d' % 'dollars' TypeError: illegal argument type for built-in operation \end{pyinterpreter} \afterverb % In the first example, there aren't enough elements; in the second, the element is the wrong type.

The format operator is powerful, but it can be difficult to use. You can read more about it at \url{docs.python.org/2.5/lib/typesseq-strings.html}.

% You can specify the number of digits as part of the format sequence. % For example, the sequence \verb"'%8.2f'" % formats a floating-point number to be 8 characters long, with % 2 digits after the decimal point:

% \beforeverb % \begin{pyinterpreter} % >>> '%8.2f' % 3.14159 % ' 3.14' % \end{pyinterpreter} % \afterverb % % % The result takes up eight spaces with two % digits after the decimal point.

\section{Filenames and paths} \label{sec:paths}

\index{filename} \index{path} \index{directory} \index{folder}

Files are organized into {\bf directories} (also called `folders''). Every running program has a` current directory,'' which is the default directory for most operations.\
For example, when you open a file for reading, Python looks for it in the current directory.

\index{os module} \index{module!os}

The {\tt os} module provides functions for working with files and directories (`os'' stands for` operating system''). {\tt os.getcwd} returns the name of the current directory:

\index{getcwd function} \index{function!getcwd}

\beforeverb \begin{pyinterpreter}

> > > import os cwd = os.getcwd() print(cwd) /home/dinsdale \end{pyinterpreter} \afterverb % {\tt cwd} stands for \`\`current working directory.'' The result in this example is {\tt /home/dinsdale}, which is the home directory of a user named {\tt dinsdale}. % \index{working directory} \index{directory!working} % A string like {\tt cwd} that identifies a file is called a {\bf path}. A {\bf relative path} starts from the current directory; an {\bf absolute path} starts from the topmost directory in the file system. % \index{relative path} \index{path!relative} \index{absolute path} \index{path!absolute} % The paths we have seen so far are simple filenames, so they are relative to the current directory. To find the absolute path to a file, you can use {\tt os.path.abspath}:

\beforeverb \begin{pyinterpreter}

> > > os.path.abspath('memo.txt') '/home/dinsdale/memo.txt' \end{pyinterpreter} \afterverb % {\tt os.path.exists} checks whether a file or directory exists:

\index{exists function} \index{function!exists}

\beforeverb \begin{pyinterpreter}

> > > os.path.exists('memo.txt') True \end{pyinterpreter} \afterverb % If it exists, {\tt os.path.isdir} checks whether it's a directory:

\beforeverb \begin{pyinterpreter}

> > > os.path.isdir('memo.txt') False os.path.isdir('music') True \end{pyinterpreter} \afterverb % Similarly, {\tt os.path.isfile} checks whether it's a file.

{\tt os.listdir} returns a list of the files (and other directories) in the given directory:

\beforeverb \begin{pyinterpreter}

> > > os.listdir(cwd) \['music', 'photos', 'memo.txt'] \end{pyinterpreter} \afterverb % To demonstrate these functions, the following example \`\`walks'' through a directory, prints the names of all the files, and calls itself recursively on all the directories.

\index{walk, directory} \index{directory!walk}

\beforeverb \begin{pycode} def walk(dir): for name in os.listdir(dir): path = os.path.join(dir, name)

```
    if os.path.isfile(path):
        print(path)
    else:
        walk(path)
```

\end{pycode} \afterverb % {\tt os.path.join} takes a directory and a file name and joins them into a complete path.

\begin{exercise} Modify {\tt walk} so that instead of printing the names of the files, it returns a list of names. \end{exercise}

\begin{exercise} The {\tt os} module provides a function called {\tt walk} that is similar to this one but more versatile. Read the documentation and use it to print the names of the files in a given directory and its subdirectories. \end{exercise}

\section{Catching exceptions} \label{sec:catch}

A lot of things can go wrong when you try to read and write files. If you try to open a file that doesn't exist, you get an {\tt IOError}:

\index{open function} \index{function!open} \index{exception!IOError} \index{IOError}

\beforeverb \begin{pyinterpreter}

> > > fin = open('bad\_file') FileNotFoundError: \[Errno 2] No such file or directory: 'bad\_file' \end{pyinterpreter} \afterverb % And if you try to open a directory for reading, you get

\beforeverb \begin{pyinterpreter}

> > > fin = open('/home') IOError: \[Errno 21] Is a directory \end{pyinterpreter} \afterverb % To avoid these errors, you could use functions like {\tt os.path.exists} and {\tt os.path.isfile}, but it would take a lot of time and code to check all the possibilities.

\index{exception, catching} \index{try statement} \index{statement!try}

It is better to go ahead and try, and deal with problems if they happen, which is exactly what the {\tt try} statement does. The syntax is similar to an {\tt if} statement:

\beforeverb \begin{pycode} try:\
fin = open('bad\_file') for line in fin: print(line) fin.close() except: print('Something went wrong.') \end{pycode} \afterverb % Python starts by executing the {\tt try} clause. If all goes well, it skips the {\tt except} clause and proceeds. If an exception occurs, it jumps out of the {\tt try} clause and executes the {\tt except} clause.

Handling an exception with a {\tt try} statement is called {\bf catching} an exception. In this example, the {\tt except} clause prints an error message that is not very helpful. In general, catching an exception gives you a chance to fix the problem, or try again, or at least end the program gracefully.

\newpage

\subsection\{{\tt finally} clause} There are two options to the \verb|try-except| statement. The first one is the clause {\tt finally}. All code included in the {\tt finally} clause will be executed, whether an exception occurred or not. This is a good place to clean up our program. For example this is a good place to close a file if it has been open in the {\tt try} clause. The code below shows how it is done.

\beforeverb \begin{pycode} fin = None try:\
print('Try to open a file.') fin = open('words.txt') for line in fin: print(line) except: print('Something went wrong.') finally: print('cleaning up') if fin is not None: print('closing the file') fin.close() \end{pycode} \afterverb

First we set the variable {\tt fin} to {\tt None}. In the {\tt try} clause, we open a file and then assign it to {\tt fin}. Two things can happen:

\begin{itemize} \item An exception occurs while we are trying to open the file, {\tt fin} is not assigned any new object and contains the value {\tt None}. The program jumps directly to the {\tt except} clause and executes the code in the {\tt except} block. Then the program jumps to the {\tt finally} clause and executes the code there.

```
\item The file is opened successfully, {\tt fin} is assigned the file object, and the rest
of the code in the {\tt try} statement is executed. Then the program jumps to the {\tt finally}
clause and executes the code there.
```

\end{itemize}

\subsection\{{\tt else} clause} The second option is the {\tt else} clause, which should be after the {\tt except} clause and before the {\tt finally} clause. The code in the {\tt else} clause is executed only if no exceptions were raised. It is executed before the {\tt finally} clause. The {\tt else} clause is use for all code that does not raise any exception.

\newpage

In our previous code, it would be the place to read the lines in the file. The refactored code is:

\beforeverb \begin{pycode} fin = None try:\
fin = open('word.txt') except: print('Something went wrong.') else: print('Do your thing if all went well.') for line in fin: print(line)\
finally: print('cleaning up.') if fin is not None: print('closing the file.') fin.close() \end{pycode} \afterverb

As you can see, the {\tt try} clause contains only the code that may raise an exception. \begin{itemize} \item If an exception occurs whilst opening the file, the program jumps to the {\tt except} clause and then executes the {\tt finally} clause. In this case, the output is:

\begin{pyoutput} TRY: open file. EXCEPT: Something went wrong. FINALLY: cleaning up. \end{pyoutput}

```
\item If no exceptions are raised, the program skips the {\tt except} clause, and jumps to the {\tt else} clause. Once the code in the {\tt else} clause has been executed, the program jumps to the {\tt finally} clause. In this case, the output is: 
```

\begin{pyoutput} TRY: open file. --> file open successfully. ELSE: Do your thing if all went well. --> line 1 of text file

\--> line 2 of text file

\--> last line of text file

FINALLY: cleaning up. --> closing the file. \end{pyoutput}

\end{itemize}

\section{Writing modules} \label{sec:modules}

\index{module, writing} \index{word count}

Any file that contains Python code can be imported as a module. For example, suppose you have a file named {\tt wc.py} with the following code:

\beforeverb \begin{pycode} def linecount(filename): count = 0 for line in open(filename): count += 1 return count

print(linecount('wc.py')) \end{pycode} \afterverb % If you run this program, it reads itself and prints the number of lines in the file, which is 7. You can also import it like this:

\beforeverb \begin{pyinterpreter}

> > > import wc 7 \end{pyinterpreter} \afterverb % Now you have a module object {\tt wc}:

\index{module object} \index{object!module}

\beforeverb \begin{pyinterpreter}

> > > print(wc) \<module 'wc' from 'wc.py'> \end{pyinterpreter} \afterverb % That provides a function called \verb"linecount":

\beforeverb \begin{pyinterpreter}

> > > wc.linecount('wc.py') 7 \end{pyinterpreter} \afterverb % So that's how you write modules in Python.

The only problem with this example is that when you import the module it executes the test code at the bottom. Normally when you import a module, it defines new functions but it doesn't execute them.

\index{import statement} \index{statement!import}

Programs that will be imported as modules often use the following idiom:

\beforeverb \begin{pycode} if **name** == '**main**': print(linecount('wc.py')) \end{pycode} \afterverb % \verb"**name**" is a built-in variable that is set when the program starts. If the program is running as a script, \verb"**name**" has the value \verb"**main**"; in that case, the test code is executed. Otherwise, if the module is being imported, the test code is skipped.

\begin{exercise} Type this example into a file named {\tt wc.py} and run it as a script. Then run the Python interpreter and {\tt import wc}. What is the value of \verb"**name**" when the module is being imported?

Warning: If you import a module that has already been imported, Python does nothing. It does not re-read the file, even if it has changed.

\index{module!reload} \index{reload function} \index{function!reload}

If you want to reload a module, you can use the built-in function {\tt reload}, but it can be tricky, so the safest thing to do is restart the interpreter and then import the module again. \end{exercise}

\section{Debugging}

\index{debugging} \index{whitespace}

When you are reading and writing files, you might run into problems with whitespace. These errors can be hard to debug because spaces, tabs and newlines are normally invisible:

\beforeverb \begin{pyinterpreter}

> > > s = '1 2\t 3\n 4' print(s) 1 2 3 4 \end{pyinterpreter} \afterverb

\index{repr function} \index{function!repr} \index{string representation}

The built-in function {\tt repr} can help. It takes any object as an argument and returns a string representation of the object. For strings, it represents whitespace characters with backslash sequences:

\beforeverb \begin{pyinterpreter}

> > > print(repr(s)) '1 2\t 3\n 4' \end{pyinterpreter} \afterverb

This can be helpful for debugging.

One other problem you might run into is that different systems use different characters to indicate the end of a line. Some systems use a newline, represented \verb"\n". Others use a return character, represented \verb"\r". Some use both. If you move files between different systems, these inconsistencies might cause problems.

\index{end of line character}

For most systems, there are applications to convert from one format to another. You can find them (and read more about this issue) at \url{wikipedia.org/wiki/Newline}. Or, of course, you could write one yourself.

\newpage

\section{Glossary}

\begin{vocabulary}\[persistent:] Pertaining to a program that runs indefinitely and keeps at least some of its data in permanent storage. \index{persistence} \end{vocabulary}

\begin{vocabulary}\[format operator:] An operator, {\tt %\}, that takes a format string and a tuple and generates a string that includes the elements of the tuple formatted as specified by the format string. \index{format operator} \index{operator!format} \end{vocabulary}

\begin{vocabulary}\[format string:] A string, used with the format operator, that contains format sequences.\
\index{format string} \end{vocabulary}

\begin{vocabulary}\[format sequence:] A sequence of characters in a format string, like {\tt %d}, that specifies how a value should be formatted. \index{format sequence} \end{vocabulary}

\begin{vocabulary}\[text file:] A sequence of characters stored in permanent storage like a hard drive. \index{text file} \end{vocabulary}

\begin{vocabulary}\[directory:] A named collection of files, also called a folder. \index{directory} \end{vocabulary}

\begin{vocabulary}\[path:] A string that identifies a file. \index{path} \end{vocabulary}

\begin{vocabulary}\[relative path:] A path that starts from the current directory. \index{relative path} \end{vocabulary}

\begin{vocabulary}\[absolute path:] A path that starts from the topmost directory in the file system. \index{absolute path} \end{vocabulary}

\begin{vocabulary}\[catch:] To prevent an exception from terminating a program using the {\tt try} and {\tt except} statements. \end{vocabulary}

\section{Exercises} \label{sec:files-exercises}

\begin{exercise} \label{exo:urllib}

\index{urllib module} \index{module!urllib} \index{URL}

The {\tt urllib} module provides methods for manipulating URLs and downloading information from the web. The following example downloads and prints a secret message from {\tt thinkpython.com}:

\beforeverb \begin{pyexo} import urllib

conn = urllib.urlopen('http://thinkpython.com/secret.html') for line in conn.fp: print(line.strip()) \end{pyexo} \afterverb

Run this code and follow the instructions you see there.

\index{secret exercise} \index{exercise, secret}

\end{exercise}

\begin{exercise} \label{exo:words-file} Write a program that reads {\tt words.txt} and prints only the words with more than 20 characters (not counting whitespace).

\index{whitespace}

\end{exercise}

\begin{exercise} \label{exo:avoids} Write a function named {\tt avoids} that takes a word and a string of forbidden letters, and that returns {\tt True} if the word doesn't use any of the forbidden letters.

Modify your program to prompt the user to enter a string of forbidden letters and then print the number of words that don't contain any of them. Can you find a combination of 5 forbidden letters that excludes the smallest number of words? \end{exercise}

\newpage

\begin{exercise} \label{exo:gadsby} In 1939 Ernest Vincent Wright published a 50,000 word novel called {\em Gadsby} that does not contain the letter `e.'' Since` e'' is the most common letter in English, that's not easy to do.

In fact, it is difficult to construct a solitary thought without using that most common symbol. It is slow going at first, but with caution and hours of training you can gradually gain facility.

All right, I'll stop now.

Write a function called \verb"has\_no\_e" that returns {\tt True} if the given word doesn't have the letter \`\`e'' in it.

Modify your program from the previous section to print only the words that have no `e'' and compute the percentage of the words in the list have no` e.''

\index{lipogram}

\end{exercise}

\begin{exercise} \label{exo:uses-only}

Write a function named \verb"uses\_only" that takes a word and a string of letters, and that returns {\tt True} if the word contains only letters in the list. Can you make a sentence using only the letters {\tt acefhlo}? Other than \`\`Hoe alfalfa?'' \end{exercise}

\begin{exercise} \label{exo:uses-all}

Write a function named \verb"uses\_all" that takes a word and a string of required letters, and that returns {\tt True} if the word uses all the required letters at least once. How many words are there that use all the vowels {\tt aeiou}? How about {\tt aeiouy}? \end{exercise}

\begin{exercise} \label{exo:abecedarian}

Write a function called \verb"is\_abecedarian" that returns {\tt True} if the letters in a word appear in alphabetical order (double letters are ok).\
How many abecedarian words are there? \end{exercise}

\index{abecedarian}

\begin{exercise} \label{exo:palindrome} A palindrome is a word that reads the same forward and backward, like `rotator'' and` noon.'' Write a boolean function named \verb"is\_palindrome" that takes a string as a parameter and returns {\tt True} if it is a palindrome.

Modify your program from the previous section to print all of the palindromes in the word list and then print the total number of palindromes. \end{exercise}
