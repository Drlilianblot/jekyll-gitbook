# Debugging

\section{Debugging} \index{debugging}

\index{traversal}

When you use indices to traverse the values in a sequence, it is tricky to get the beginning and end of the traversal right. Here is a function that is supposed to compare two words and return {\tt True} if one of the words is the reverse of the other, but it contains two errors:

\beforeverb \begin{pycode} def is\_reverse(word1, word2): if len(word1) != len(word2): return False

```
i = 0
j = len(word2)

while j > 0:
    if word1[i] != word2[j]:
        return False
    i = i+1
    j = j-1

return True
```

\end{pycode} \afterverb % The first {\tt if} statement checks whether the words are the same length. If not, we can return {\tt False} immediately and then, for the rest of the function, we can assume that the words are the same length. This is an example of the guardian pattern in \prettyref{sec:guardian}. % \index{guardian pattern} \index{pattern!guardian} \index{index} % {\tt i} and {\tt j} are indices: {\tt i} traverses {\tt word1} forward while {\tt j} traverses {\tt word2} backward. If we find two letters that don't match, we can return {\tt False} immediately. If we get through the whole loop and all the letters match, we return {\tt True}.

If we test this function with the words `pots'' and` stop'', we expect the return value {\tt True}, but we get an IndexError:

\index{IndexError} \index{exception!IndexError}

\beforeverb \begin{pyinterpreter}

> > > is\_reverse('pots', 'stop') ... File "reverse.py", line 15, in is\_reverse if word1\[i] != word2\[j]: IndexError: string index out of range \end{pyinterpreter} \afterverb % For debugging this kind of error, my first move is to print the values of the indices immediately before the line where the error appears.

\beforeverb \begin{pycode} while j > 0: print(i, j) # print here

```
    if word1[i] != word2[j]:
        return False
    i = i+1
    j = j-1
```

\end{pycode} \afterverb % Now when I run the program again, I get more information:

\beforeverb \begin{pyinterpreter}

> > > is\_reverse('pots', 'stop') 0 4 ... IndexError: string index out of range \end{pyinterpreter} \afterverb % The first time through the loop, the value of {\tt j} is 4, which is out of range for the string \verb"'pots'". The index of the last character is 3, so the initial value for {\tt j} should be {\tt len(word2)-1}.

\index{semantic error} \index{error!semantic}

If I fix that error and run the program again, I get:

\beforeverb \begin{pyinterpreter}

> > > is\_reverse('pots', 'stop') 0 3 1 2 2 1 True \end{pyinterpreter} \afterverb % This time we get the right answer, but it looks like the loop only ran three times, which is suspicious. To get a better idea of what is happening, it is useful to draw a state diagram. During the first iteration, the frame for \verb"is\_reverse" looks like this:

\index{state diagram} \index{diagram!state}

\beforefig \centerline{\includegraphics{figs/state4.eps\}} \afterfig

I took a little license by arranging the variables in the frame and adding dotted lines to show that the values of {\tt i} and {\tt j} indicate characters in {\tt word1} and {\tt word2}.

\begin{exercise} \label{exo:is-reverse} Starting with this diagram, execute the program on paper, changing the values of {\tt i} and {\tt j} during each iteration. Find and fix the second error in this function. \end{exercise}



## List

\section{Debugging} \index{debugging}

Careless use of lists (and other mutable objects) can lead to long hours of debugging. Here are some common pitfalls and ways to avoid them:

\begin{enumerate}

\item Don't forget that most list methods modify the argument and return {\tt None}. This is the opposite of the string methods, which return a new string and leave the original alone.

If you are used to writing string code like this:

\beforeverb \begin{pycode} word = word.strip() \end{pycode} \afterverb

It is tempting to write list code like this:

\beforeverb \begin{pycode} t = t.sort() # WRONG! \end{pycode} \afterverb

\index{sort method} \index{method!sort}

Because {\tt sort} returns {\tt None}, the next operation you perform with {\tt t} is likely to fail.

Before using list methods and operators, you should read the documentation carefully and then test them in interactive mode. The methods and operators that lists share with other sequences (like strings) are documented at \url{docs.python.org/lib/typesseq.html}. The methods and operators that only apply to mutable sequences are documented at \url{docs.python.org/lib/typesseq-mutable.html}.

\item Pick an idiom and stick with it.

Part of the problem with lists is that there are too many ways to do things. For example, to remove an element from a list, you can use {\tt pop}, {\tt remove}, {\tt del}, or even a slice assignment. % To add an element, you can use the {\tt append} method or the {\tt +} operator. Assuming that {\tt t} is a list and {\tt x} is a list element, these are right:

\beforeverb \begin{pycode} t.append(x) t = t + \[x] \end{pycode} \afterverb

And these are wrong:

\beforeverb \begin{pycode} t.append(\[x]) # WRONG! t = t.append(x) # WRONG! t + \[x] # WRONG! t = t + x # WRONG! \end{pycode} \afterverb

Try out each of these examples in interactive mode to make sure you understand what they do. Notice that only the last one causes a runtime error; the other three are legal, but they do the wrong thing.

\newpage

\item Make copies to avoid aliasing.

\index{aliasing!copying to avoid} \index{copy!to avoid aliasing}

If you want to use a method like {\tt sort} that modifies the argument, but you need to keep the original list as well, you can make a copy.

\beforeverb \begin{pycode} copied = t.copy() copied.sort() \end{pycode} \afterverb Alternatively, you can do a copy using slicing: \beforeverb \begin{pycode} copied = t\[:] copied.sort() \end{pycode} \afterverb

In this example you could also use the built-in function {\tt sorted}, which returns a new, sorted list and leaves the original alone. But in that case you should avoid using {\tt sorted} as a variable name!

\end{enumerate}
