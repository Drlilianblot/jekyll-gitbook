# Sets and dictionaries

## Set

In Python, a set is an unordered collection of unique elements. It is similar to a list or a tuple but with a few differences. One of the most important differences is that a set only contains unique elements, meaning that no duplicates are allowed. Another important difference is that sets are mutable, which means that you can add or remove elements from them. Sets are very useful when it comes to solving problems that involve finding unique elements, such as removing duplicates or determining the intersection of two lists.

Creating a Set in Python

To create a set in Python, you can use either curly braces or the built-in set() function. For example:

```sql
sqlCopy code# Using curly braces
my_set = {1, 2, 3, 4, 5}

# Using the set() function
my_set = set([1, 2, 3, 4, 5])
```

In both cases, we create a set that contains the numbers 1 through 5.

Adding and Removing Elements from a Set

One of the main benefits of using a set is the ability to easily add and remove elements from it. To add an element to a set, you can use the `add()` method. For example:

```scss
scssCopy codemy_set = {1, 2, 3}
my_set.add(4)
print(my_set) # Output: {1, 2, 3, 4}
```

To remove an element from a set, you can use the `remove()` method. For example:

```scss
scssCopy codemy_set = {1, 2, 3}
my_set.remove(3)
print(my_set) # Output: {1, 2}
```

You can also use the `discard()` method to remove an element from a set, but it won't raise an error if the element is not found in the set. For example:

```scss
scssCopy codemy_set = {1, 2, 3}
my_set.discard(3)
my_set.discard(4)
print(my_set) # Output: {1, 2}
```

Basic Set Operations

In addition to adding and removing elements from a set, there are several other useful set operations. Here are a few examples:

* Union: The union of two sets is a new set that contains all the elements from both sets, with no duplicates.

```makefile
makefileCopy codeset1 = {1, 2, 3}
set2 = {3, 4, 5}
union_set = set1.union(set2)
print(union_set) # Output: {1, 2, 3, 4, 5}
```

* Intersection: The intersection of two sets is a new set that contains only the elements that are common to both sets.

```makefile
makefileCopy codeset1 = {1, 2, 3}
set2 = {3, 4, 5}
intersection_set = set1.intersection(set2)
print(intersection_set) # Output: {3}
```

* Difference: The difference of two sets is a new set that contains only the elements that are in one set but not the other.

```makefile
makefileCopy codeset1 = {1, 2, 3}
set2 = {3, 4, 5}
difference_set = set1.difference(set2)
print(difference_set) # Output: {1, 2}
```

* Symmetric Difference: The symmetric difference of two sets is a new set that contains only the elements that are in one set or the other, but not both.

```makefile
makefileCopy codeset1 = {1, 2, 3}
set2 = {3, 4, 5}
symmetric_difference_set = set1.symmetric_difference(set2)
print(symmetric_difference_set) # Output: {1, 2, 4, 5}
```

Sets can also be used to remove duplicates from a list. Here is an example:

```scss
scssCopy codemy_list = [1, 2, 3, 2, 1, 4, 5, 4]
my_set = set(my_list)
my_list = list(my_set)
print(my_list)
```

This code will output

```
[1, 2, 3, 4, 5]
```

### Iterating through a `set`

You can iterate through a set using a `for` loop in Python. Here's an example:

```bash
bashCopy codemy_set = {1, 2, 3, 4, 5}

for item in my_set:
    print(item)
```

In this example, the `for` loop iterates through each item in the `my_set` set, and prints each item to the console. The order in which the items are printed may not be in the same order as they were added to the set, as sets are unordered data structures.

## Dictionaries

A **dictionary** is like a list, but more general. In a list, the indices have to be integers; in a dictionary they can be (almost) any type. You can think of a dictionary as a mapping between a set of indices (which are called **keys**) and a set of values. Each key maps to a value. The association of a key and a value is called a **key-value pair** or sometimes an **item**. As an example, we'll build a dictionary that maps from English to French words, so the keys and the values are all strings.

The function `dict` creates a new dictionary with no items. Because `dict` is the name of a built-in function, you should avoid using it as a variable name.

```bash
>>> eng2fr = dict()
>>> print(eng2fr)
 {} 
>>>
```

The curly-brackets, `{}`, represent an empty dictionary. To add items to the dictionary, you can use square brackets:

```bash
>>> eng2fr['one'] = 'un'
>>>
```

This line creates an item that maps from the key `'one'` to the value `'un'`. If we print the dictionary again, we see a key-value pair with a colon between the key and value:

```bash
>>> print(eng2fr)
 {'one': 'un'}
>>>
```

This output format is also an input format. For example, you can create a new dictionary with three items:

```bash
>>> eng2fr = {'one': 'un', 'two': 'deux', 'three': 'trois'}
```

But if you print `eng2fr`, you might be surprised:

```bash
>>> print(eng2fr)
 {'one': 'un', 'three': 'trois', 'two': 'deux'}
>>>
```

The order of the key-value pairs is not the same. In fact, if you type the same example on your computer, you might get a different result. In general, for Python version 3.6 or earlier, the order of items in a dictionary is unpredictable. However, since Python 3.7, the order in which the pair are added is retained. Anyway, that's not a problem because the elements of a dictionary are never indexed with integer indices. Instead, you use the keys to look up the corresponding values:

```bash
>>> print(eng2fr['two'])
 'deux'
>>>
```

The key `'two'` always maps to the value `'deux'` so the order of the items doesn't matter. If the key isn't in the dictionary, you get an exception:

```bash
>>> print(eng2fr['four'])
 Traceback (most recent call last): 
    File "<pyshell#19>", line 1, in 
    print(eng2fr['four']) 
 KeyError: 'four'
```

The `len` function works on dictionaries; it returns the number of key-value pairs:

```bash
>>>len(eng2fr)
 3
>>>
```

The `in` operator works on dictionaries; it tells you whether something appears as a _key_ in the dictionary (appearing as a value is not good enough).

```bash
>>> 'one' in eng2fr 
 True
>>> 'un' in eng2fr
 False
>>>
```

To see whether something appears as a value in a dictionary, you can use the method `values()`, which returns the values as a list, and then use the `in` operator:

```bash
>>> vals = eng2fr.values()
>>> 'un' in vals
 True 
>>>
```

The `in` operator uses different algorithms for lists and dictionaries. For lists, it uses a search algorithm, as in <mark style="background-color:red;">{\color{red} \prettyref{sec:find\}}</mark>. As the list gets longer, the search time gets longer in direct proportion. For dictionaries, Python uses an algorithm called a **hashtable** that has a remarkable property: the `in` operator takes about the same amount of time no matter how many items there are in a dictionary. I won't explain how that's possible, but you can read more about it on the [hashtable Wikipedia page](https://www.wikipedia.org/wiki/Hash\_table).

### Dictionary as a set of counters

Suppose you are given a string and you want to count how many times each letter appears. There are several ways you could do it:

1. You could create 26 variables, one for each letter of the alphabet. Then you could traverse the string and, for each character, increment the corresponding counter, probably using a chained conditional.
2. You could create a list with 26 elements. Then you could convert each character to a number (using the built-in function `ord`), use the number as an index into the list, and increment the appropriate counter.
3. You could create a dictionary with characters as keys and counters as the corresponding values. The first time you see a character, you would add an item to the dictionary. After that you would increment the value of an existing item.

Each of these options performs the same computation, but each of them implements that computation in a different way. An **implementation** is a way of performing a computation; some implementations are better than others. For example, an advantage of the dictionary implementation is that we don't have to know ahead of time which letters appear in the string and we only have to make room for the letters that do appear. Here is what the code might look like:

{% code lineNumbers="true" %}
```python
def histogram(text): 
    hist = dict() 
    for character in text: 
        if character not in hist: 
            hist[character] = 1 
        else: 
            hist[character] += 1 
    return hist
```
{% endcode %}

The name of the function is **histogram**, which is a statistical term for a set of counters (or frequencies).

Line 2 creates an empty dictionary named `hist`. The `for` loop traverses the string `text`. Each time through the loop, if the character `character` is not in the dictionary, we create a new item with key `character` and the initial value `1` (since we have seen this letter once). If `character` is already in the dictionary we increment `hist[character]`. Here's how it works:

```bash
>>> h = histogram('brontosaurus')
>>> print(h)
 {'a': 1, 'b': 1, 'o': 2, 'n': 1, 's': 2, 'r': 2, 'u': 2, 't': 1}
>>>
```

The histogram indicates that the letters `'a'` and `'b'` appear once; `'o'` appears twice, and so on.

**Exercise:** Write a function that reads the words in a long string (or a text file) and stores them as keys in a dictionary. The values are the number of time the word appears in the text. Then you can use the `in` operator as a fast way to check whether a string is in the dictionary. If you did <mark style="background-color:red;">{\color{red} \prettyref{exo:wordlist1\}}</mark>, you can compare the speed of this implementation with the list `in` operator and the bisection search.

<details>

<summary>Answer:</summary>



</details>

**Exericse:** <mark style="background-color:red;">TOREWRITE</mark> Dictionaries have a method called `get` that takes a key and a default value. If the key appears in the dictionary, `get` returns the corresponding value; otherwise it returns the default value. For example:

```bash
>>> h = histogram('brontosaurus')
>>> print(h)
 {'a': 1, 'b': 1, 'o': 2, 'n': 1, 's': 2, 'r': 2, 'u': 2, 't': 1}
>>> h.get('a', 0)
 1 
>>> h.get('z', 0)
 0
>>>
```

Use `get` to write `histogram` more concisely. You should be able to eliminate the {\tt if} statement. \end{exercise}

## \section{Looping and dictionaries}

\index{dictionary!looping with} \index{looping!with dictionaries} \index{traversal}

If you use a dictionary in a {\tt for} statement, it traverses the keys of the dictionary. For example, \verb"print\_histogram" prints each key and the corresponding value:

\beforeverb \begin{pycode} def print\_histogram(hist): for character in hist: print(character, hist\[character]) \end{pycode} \afterverb % Here's what the output looks like:

\beforeverb \begin{pyinterpreter}

> > > h = histogram('parrot') print\_histogram(h) a 1 p 1 r 2 t 1 o 1 \end{pyinterpreter} \afterverb % Again, the keys are in no particular order.

\begin{exercise}

\index{keys method} \index{method!keys}

Dictionaries have a method called {\tt keys} that returns the keys of the dictionary, in no particular order, as a list. % Modify \verb"print\_histogram" to print the keys and their values in alphabetical order. \end{exercise}

\section{Reverse lookup}

\index{dictionary!lookup} \index{dictionary!reverse lookup} \index{lookup, dictionary} \index{reverse lookup, dictionary}

Given a dictionary {\tt d} and a key {\tt k}, it is easy to find the corresponding value {\tt v = d\[k]}. This operation is called a {\bf lookup}.

But what if you have {\tt v} and you want to find {\tt k}? You have two problems: first, there might be more than one key that maps to the value {\tt v}. Depending on the application, you might be able to pick one, or you might have to make a list that contains all of them. Second, there is no simple syntax to do a {\bf reverse lookup}; you have to search. % Here is a function that takes a value and returns the first key that maps to that value:

\beforeverb \begin{pycode} def reverse\_lookup(dico, value): for key in dico: if dico\[key] == value: return key raise ValueError('No such value in dictionary!') \end{pycode} \afterverb % This function is yet another example of the search pattern, but it uses a feature we haven't seen before, {\tt raise}. The {\tt raise} statement causes an exception; in this case it causes a {\tt ValueError}, which generally indicates that there is something wrong with the value of a parameter. % \index{search} \index{pattern!search} \index{raise statement} \index{statement!raise} \index{exception!ValueError} \index{ValueError} % If we get to the end of the loop, that means {\tt value} doesn't appear in the dictionary as a value, so we raise an exception. %

Here is an example of a successful reverse lookup:

\beforeverb \begin{pyinterpreter}

> > > h = histogram('brontosaurus') k = reverse\_lookup(h, 1) print(k) b \end{pyinterpreter} \afterverb % And an unsuccessful one:

\beforeverb \begin{pyinterpreter}

> > > h = histogram('brontosaurus') k = reverse\_lookup(h, 3) Traceback (most recent call last): File "\<pyshell#9>", line 1, in k = reverse\_lookup(h, 3) File "D:/Python/dictionaries.py", line 20, in reverse\_lookup raise ValueError('No such value in dictionary!') ValueError: No such value in dictionary! \end{pyinterpreter} \afterverb % The result when you raise an exception is the same as when Python raises one: it prints a traceback and an error message. % \index{traceback} \index{optional argument} \index{argument!optional} % %The {\tt raise} statement takes a detailed error message as an %optional argument. For example: % %\beforeverb %\begin{pycode} %>>> raise ValueError('value does not appear in the dictionary') %Traceback (most recent call last): %File "", line 1, in ? %ValueError: value does not appear in the dictionary %\end{pycode} %\afterverb

A reverse lookup is much slower than a forward lookup; if you have to do it often, or if the dictionary gets big, the performance of your program will suffer.

\vspace{4ex}

\begin{exercise} Modify \verb"reverse\_lookup" so that it builds and returns a list of {\em all} keys that map to a value {\tt v}, or an empty list if there are none. \end{exercise}

\section{Dictionaries and lists}

Lists can appear as values in a dictionary. For example, if you were given a dictionary that maps from letters to frequencies, you might want to invert it; that is, create a dictionary that maps from frequencies to letters. Since there might be several letters with the same frequency, each value in the inverted dictionary should be a list of letters.

\index{invert dictionary} \index{dictionary!invert}

\newpage

Here is a function that inverts a dictionary:

\beforeverb \begin{pycode} def invert\_dict(dico): inverted = dict() for key in dico: value = dico\[key] if value not in inverted: inverted\[value] = \[key] else: inverted\[value].append(key) return inverted \end{pycode} \afterverb % Each time through the loop, {\tt key} gets a key from {\tt dico} and {\tt value} gets the corresponding value. If {\tt value} is not in {\tt inverted}, that means we haven't seen it before, so we create a new item and initialize it with a {\bf singleton} (a list that contains a single element). Otherwise we have seen this value before, so we append the corresponding key to the list.

\index{singleton}

Here is an example:

\beforeverb \begin{pyinterpreter}

> > > h = histogram('parrot') print(h) {'p': 1, 'a': 1, 'r': 2, 'o': 1, 't': 1} inv = invert\_dict(h) print(inv) {1: \['p', 'a', 'o', 't'], 2: \['r']} \end{pyinterpreter} \afterverb % %And here is a diagram showing {\tt h} and {\tt inv}: % %\index{state diagram} %\index{diagram!state} %% %\beforefig %\centerline{\includegraphics{figs/dict1.eps\}} %\afterfig %% %A dictionary is represented as a box with the type {\tt dict} above it %and the key-value pairs inside. If the values are integers, floats or %strings, I usually draw them inside the box, but I usually draw lists %outside the box, just to keep the diagram simple.

Lists can be values in a dictionary, as this example shows, but they cannot be keys. Here's what happens if you try: % \index{TypeError} \index{exception!TypeError} %

\beforeverb \begin{pyinterpreter}

> > > lst = \[1,2,3] dico = dict() dico\[lst] = 'oops' Traceback (most recent call last): File "\<pyshell#17>", line 1, in dico\[lst] = 'oops' TypeError: unhashable type: 'list' \end{pyinterpreter} \afterverb % I mentioned earlier that a dictionary is implemented using a hashtable and that means that the keys have to be {\bf hashable}. % \index{hash function} \index{hashable} % A {\bf hash} is a function that takes a value (of any kind) and returns an integer. Dictionaries use these integers, called hash values, to store and look up key-value pairs. % \index{immutability} % This system works fine if the keys are immutable. But if the keys are mutable, like lists, bad things happen. For example, when you create a key-value pair, Python hashes the key and stores it in the corresponding location. If you modify the key and then hash it again, it would go to a different location. In that case you might have two entries for the same key, or you might not be able to find a key. Either way, the dictionary wouldn't work correctly. % That's why the keys have to be hashable, and why mutable types like lists aren't. The simplest way to get around this limitation is to use tuples, which we will see in \prettyref{cha:tuples}. % Since dictionaries are mutable, they can't be used as keys, but they {\em can} be used as values.

\vspace{4ex}

\begin{exercise} Read the documentation of the dictionary method {\tt setdefault} and use it to write a more concise version of \verb"invert\_dict".

\index{setdefault method} \index{method!setdefault}

\end{exercise}

\section{Debugging} \index{debugging}

As you work with bigger datasets it can become unwieldy to debug by printing and checking data by hand. Here are some suggestions for debugging large datasets:

\begin{description}

\item\[Scale down the input:] If possible, reduce the size of the dataset. For example if the program reads a text file, start with just the first 10 lines, or with the smallest example you can find. You can either edit the files themselves, or (better) modify the program so it reads only the first {\tt n} lines. % If there is an error, you can reduce {\tt n} to the smallest value that manifests the error, and then increase it gradually as you find and correct errors.

\item\[Check summaries and types:] Instead of printing and checking the entire dataset, consider printing summaries of the data: for example, the number of items in a dictionary or the total of a list of numbers. % A common cause of runtime errors is a value that is not the right type. For debugging this kind of error, it is often enough to print the type of a value.

\item\[Write self-checks:] Sometimes you can write code to check for errors automatically. For example, if you are computing the average of a list of numbers, you could check that the result is not greater than the largest element in the list or less than the smallest. This is called a `sanity check'' because it detects results that are` insane.'' % \index{sanity check} \index{consistency check} % Another kind of check compares the results of two different computations to see if they are consistent. This is called a \`\`consistency check.''

\item\[Pretty print the output:] Formatting debugging output can make it easier to spot an error. The {\tt pprint} module provides a {\tt pprint} function that displays built-in types in a more human-readable format.

\index{pretty print} \index{pprint module} \index{module!pprint}

\end{description}

Again, time you spend building scaffolding can reduce the time you spend debugging.

\index{scaffolding}

\newpage

\section{Glossary}

\begin{vocabulary}\[dictionary:] A mapping from a set of keys to their corresponding values. \index{dictionary} \end{vocabulary}

\begin{vocabulary}\[key-value pair:] The representation of the mapping from a key to a value. \index{key-value pair} \end{vocabulary}

\begin{vocabulary}\[item:] Another name for a key-value pair. \index{item!dictionary} \end{vocabulary}

\begin{vocabulary}\[key:] An object that appears in a dictionary as the first part of a key-value pair. \index{key} \end{vocabulary}

\begin{vocabulary}\[value:] An object that appears in a dictionary as the second part of a key-value pair. This is more specific than our previous use of the word \`\`value.'' \index{value} \end{vocabulary}

\begin{vocabulary}\[implementation:] A way of performing a computation. \index{implementation} \end{vocabulary}

\begin{vocabulary}\[hashtable:] The algorithm used to implement Python dictionaries. \index{hashtable} \end{vocabulary}

\begin{vocabulary}\[hash function:] A function used by a hashtable to compute the location for a key.%{\color{red} may want to expend} \index{hash function} \end{vocabulary}

\begin{vocabulary}\[hashable:] A type that has a hash function. Immutable types like integers, floats and strings are hashable; mutable types like lists and dictionaries are not. \index{hashable} \end{vocabulary}

\begin{vocabulary}\[lookup:] A dictionary operation that takes a key and finds the corresponding value. \index{lookup} \end{vocabulary}

\begin{vocabulary}\[reverse lookup:] A dictionary operation that takes a value and finds one or more keys that map to it. \index{reverse lookup, dictionary} \end{vocabulary}

\begin{vocabulary}\[singleton:] A list (or other sequence) with a single element. \index{singleton} \end{vocabulary}

\begin{vocabulary}\[call graph:] A diagram that shows every frame created during the execution of a program, with an arrow from each caller to each callee. %{\color{red}may want to remove} \index{call graph} \index{diagram!call graph} \end{vocabulary}

\begin{vocabulary}\[histogram:] A histogram is an accurate representation of the distribution of numerical data. In simpler terms, it could be seen as a set of counters in a program. \index{histogram} \end{vocabulary}

\begin{vocabulary}\[memo:] A computed value stored to avoid unnecessary future computation. \index{memo} \end{vocabulary}

\begin{vocabulary}\[global variable:] A variable defined outside a function. Global variables can be accessed from any function. \index{global variable} \end{vocabulary}

\begin{vocabulary}\[flag:] A boolean variable used to indicate whether a condition is true. \index{flag} \end{vocabulary}

\begin{vocabulary}\[declaration:] A statement like {\tt global} that tells the interpreter something about a variable. \index{declaration} \end{vocabulary}

\section{Exercises}

\begin{exercise} \index{duplicate}

If you did \prettyref{exo:duplicate}, you already have a function named \newline \verb"has\_duplicates" that takes a list as a parameter and returns {\tt True} if there is any object that appears more than once in the list.

Use a dictionary to write a faster, simpler version of \verb"has\_duplicates". \end{exercise}

\begin{exercise} \label{exo:rotate-pairs}

\index{letter rotation} \index{rotation!letters}

Two words are \`\`rotate pairs'' if you can rotate one of them and get the other (see \verb"rotate\_word" in \prettyref{exo:rotate}).

Write a program that reads a wordlist and finds all the rotate pairs. \end{exercise}

\newpage

\begin{exercise} \index{Car Talk} \index{Puzzler}

Here's another Puzzler from {\em Car Talk}\footnote{\url{https://www.cartalk.com/puzzler/browse}.}:

\begin{quote} This was sent in by a fellow named Dan O'Leary. He came upon a common one-syllable, five-letter word recently that has the following unique property. When you remove the first letter, the remaining letters form a homophone of the original word, that is a word that sounds exactly the same. Replace the first letter, that is, put it back and remove the second letter and the result is yet another homophone of the original word. And the question is, what's the word?

Now I'm going to give you an example that doesn't work. Let's look at the five-letter word, `wrack'. W-R-A-C-K, you know like to` wrack with pain'. If I remove the first letter, I am left with a four-letter word, R-A-C-K. It's a perfect homophone. If you put the `w' back, and remove the` r', instead, you're left with the word, \`wack', which is a real word, it's just not a homophone of the other two words.

But there is, however, at least one word that Dan and we know of, which will yield two homophones if you remove either of the first two letters to make two, new four-letter words. The question is, what's the word? \end{quote}

\index{homophone} \index{reducible word} \index{word, reducible}

You can use the dictionary from \prettyref{exo:wordlist2} to check whether a string is in the word list.

To check whether two words are homophones, you can use the CMU Pronouncing Dictionary. You can download it from \url{www.speech.cs.cmu.edu/cgi-bin/cmudict}.

% or from %\url{thinkpython.com/code/c06d} and you can also download %\url{thinkpython.com/code/pronounce.py}, which provides a function %named \verb"read\_dictionary" that reads the pronouncing dictionary and %returns a Python dictionary that maps from each word to a string that %describes its primary pronunciation.

Write a program that lists all the words that solve the Puzzler. %You can see my solution at \url{thinkpython.com/code/homophone.py}.

\end{exercise}



\section{Dictionaries and tuples}

\index{dictionary} \index{items method} \index{method!items} \index{key-value pair}

Dictionaries have a method called {\tt items} that returns a {\tt dict\_items} object (kind of a list of tuples), where each tuple is a key-value pair. But a proper list can be created from the object using the {\tt list} constructor.

\beforeverb \begin{pycode}

> > > d = {'a':0, 'b':1, 'c':2} t = list(d.items()) print(t) \[('a', 0), ('c', 2), ('b', 1)] \end{pycode} \afterverb % As you should expect from a dictionary, the items are in no particular order.

\index{dictionary!initialize}

Conversely, you can use a list of tuples to initialize a new dictionary:

\beforeverb \begin{pycode}

> > > t = \[('a', 0), ('c', 2), ('b', 1)] d = dict(t) print(d) {'a': 0, 'c': 2, 'b': 1} \end{pycode} \afterverb

Combining {\tt dict} with {\tt zip} yields a concise way to create a dictionary:

\index{zip function!use with dict}

\beforeverb \begin{pycode}

> > > d = dict(zip('abc', range(3))) print(d) {'a': 0, 'c': 2, 'b': 1} \end{pycode} \afterverb % The dictionary method {\tt update} also takes a list of tuples and adds them, as key-value pairs, to an existing dictionary.

\index{update method} \index{method!update}

\index{traverse!dictionary} \index{dictionary!traversal}

Combining {\tt items}, tuple assignment and {\tt for}, you get the idiom for traversing the keys and values of a dictionary:

\beforeverb \begin{pycode} for key, val in d.items(): print(val, key) \end{pycode} \afterverb % The output of this loop is:

\beforeverb \begin{pyoutput} 0 a 2 c 1 b \end{pyoutput} \afterverb % Again.

\index{tuple!as key in dictionary} \index{hashable}

\newpage

It is common to use tuples as keys in dictionaries (primarily because you can't use lists). For example, a telephone directory might map from last-name, first-name pairs to telephone numbers. Assuming that we have defined {\tt last}, {\tt first} and {\tt number}, we could write:

\beforeverb \begin{pycode} directory\[(last,first)] = number \end{pycode} \afterverb % The expression in brackets is a tuple. We could use tuple assignment to traverse this dictionary.

\index{tuple!in brackets}

\beforeverb \begin{pycode} for last, first in directory: print(first, last, directory\[(last,first)]) \end{pycode} \afterverb % This loop traverses the keys in {\tt directory}, which are tuples. It assigns the elements of each tuple to {\tt last} and {\tt first}, then prints the name and corresponding telephone number.

There are two ways to represent tuples in a state diagram. The more detailed version shows the indices and elements just as they appear in a list. For example, the tuple \verb"('Cleese', 'John')" would appear:

\index{state diagram} \index{diagram!state}

\vspace{4ex}

&#x20;\beforefig \centerline{\includegraphics{figs/tuple1.eps\}} \afterfig \vspace{4ex}

But in a larger diagram you might want to leave out the details. For example, a diagram of the telephone directory might appear:

\vspace{4ex} \beforefig \centerline{\includegraphics{figs/dict2.eps\}} \afterfig \vspace{4ex}

Here the tuples are shown using Python syntax as a graphical shorthand. % The telephone number in the diagram is the complaints line for the BBC, so please don't call it.

## Summary

In Python 3, lists, tuples, sets and dictionaries are all built-in collections. They differ in their properties and use cases.

* **List**: A list is an ordered collection of elements that can contain duplicate values. It is mutable which means you can change its content.
* **Tuple**: A tuple is similar to a list but it is immutable which means you cannot change its content once created [1](https://dev.to/arvindmehairjan/what-are-the-differences-between-a-list-tuple-dictionary-set-in-python-2lm6).
* **Set**: A set is an unordered collection of unique elements [1](https://dev.to/arvindmehairjan/what-are-the-differences-between-a-list-tuple-dictionary-set-in-python-2lm6).
* **Dictionary**: A dictionary stores key-value pairs. [It is an ordered collection since Python 3.7 ](https://www.scaler.com/topics/python/difference-between-dictionary-list-tuple-and-set-in-python/)[2](https://www.scaler.com/topics/python/difference-between-dictionary-list-tuple-and-set-in-python/).

In Python, an **ordered** collection means that the elements in the collection have a specific order that is determined by their position in the collection. The order of elements is preserved when you add or remove elements from the collection. For example, a list is an ordered collection. If you create a list with the elements `['apple', 'banana', 'cherry']`, the element `'apple'` will always be before `'banana'`, and `'banana'` will always be before `'cherry'` . In other word the data structure retains the order in which the data was added.

On the other hand, a set is an **unordered** collection. If you create a set with the same elements as above (`{'apple', 'banana', 'cherry'}`), there is no guarantee about the order of elements when you iterate over them. The order in which they are added may not be retained by the data structure.

| Collection | Mutable | Ordered | Indexing | Duplicate Data |
| ---------- | ------- | ------- | -------- | -------------- |
| List       | ✔       | ✔       | ✔        | ✔              |
| Tuple      | 𐄂      | ✔       | ✔        | ✔              |
| Set        | ✔       | 𐄂      | 𐄂       | 𐄂             |
| Dictionary | ✔       | ✔       | ✔        | 𐄂             |

The choice of which collection to use depends on the specific use case and requirements.

* **List**: Use a list when you need an ordered collection of elements that can contain duplicates. Lists are useful for storing and retrieving elements based on their position in the collection .
* **Tuple**: Use a tuple when you have an ordered collection of elements that should not be changed. Tuples are often used to represent a single record or data structure with multiple fields .
* **Set**: Use a set when you need to store unique elements and perform set operations such as union, intersection and difference .
* **Dictionary**: Use a dictionary when you need to store key-value pairs and retrieve values based on their keys. Dictionaries are useful for representing mappings from one set of values to another .

Here are some steps you can follow to determine which collection to use:

1. **Identify the requirements**: Determine what kind of data you need to store and how you will be using it. Do you need to store ordered data? Do you need to store unique elements? Do you need to store key-value pairs?
2. **Evaluate the properties of each collection**: Consider the properties of each collection and how they align with your requirements. For example, if you need to store ordered data that can contain duplicates, a list might be a good choice.
3. **Consider performance**: Different collections have different performance characteristics for common operations such as adding, removing and accessing elements. Choose a collection that provides good performance for the operations you will be performing most frequently.
