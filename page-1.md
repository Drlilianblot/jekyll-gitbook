# to add to the dictionary chapter

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

\newpage
