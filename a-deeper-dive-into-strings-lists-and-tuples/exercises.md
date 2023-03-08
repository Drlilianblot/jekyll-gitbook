# Exercises

this is an updated version

<iframe width="560" height="315" src="https://www.youtube.com/embed/kgEP202a2MU" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

\section{Exercises}

\begin{exercise}

\index{step size} \index{slice operator} \index{operator!slice}

A string slice can take a third index that specifies the \`\`step size;'' that is, the number of spaces between successive characters. A step size of 2 means every other character; 3 means every third, etc.

\beforeverb \begin{pyexo}

> > > fruit = 'banana' fruit\[0:5:2] 'bnn' \end{pyexo} \afterverb

A step size of -1 goes through the word backwards, so the slice \verb"\[::-1]" generates a reversed string. % \index{palindrome} % Use this idiom to write a one-line version of \verb"is\_palindrome" from \prettyref{exo:palindrome}. \end{exercise}

\begin{exercise} \index{letter rotation} \index{rotation, letter}

\label{exo:rotate} ROT13 is a weak form of encryption that involves \`\`rotating'' each letter in a word by 13 places\footnote{See \url{wikipedia.org/wiki/ROT13}.}. To rotate a letter means to shift it through the alphabet, wrapping around to the beginning if necessary, so 'A' shifted by 3 is 'D' and 'Z' shifted by 1 is 'A'.

Write a function called \verb"rotate\_word" that takes a string and an integer as parameters, and that returns a new string that contains the letters from the original string \`\`rotated'' by the given amount.

For example, `cheer'' rotated by 7 is` jolly'' and `melon'' rotated by -10 is` cubed''.\
% %%For example `sleep'' %%rotated by 9 is` bunny'' and `latex'' rotated by 7 is` shale''. % You might want to use the built-in functions {\tt ord}, which converts a character to a numeric code, and {\tt chr}, which converts numeric codes to characters. % %Potentially offensive jokes on the Internet are sometimes encoded %in ROT13. If you are not easily offended, find and decode some %of them. \end{exercise}

\newpage

\begin{exercise} \index{string method} \index{method!string}

Read the documentation of the string methods at \url{docs.python.org/lib/string-methods.html}. You might want to experiment with some of them to make sure you understand how they work. {\tt strip} and {\tt replace} are particularly useful. % The documentation uses a syntax that might be confusing. For example, in \verb"find(sub\[, start\[, end]])", the brackets indicate optional arguments. So {\tt sub} is required, but {\tt start} is optional, and if you include {\tt start}, then {\tt end} is optional. \end{exercise}

\begin{exercise} The following functions are all {\em intended} to check whether a string contains any lowercase letters, but at least some of them are wrong. For each function, describe what the function actually does (assuming that the parameter is a string).

\begin{pyexo} def any\_lowercase1(s): for c in s: if c.islower(): return True else: return False \end{pyexo}

%\begin{pyexo} %def any\_lowercase2(s): % for c in s: % if 'c'.islower(): % return 'True' % else: % return 'False' %\end{pyexo}

\begin{pyexo} def any\_lowercase3(s): for c in s: flag = c.islower() return flag \end{pyexo}

\begin{pyexo} def any\_lowercase4(s): flag = False for c in s: flag = flag or c.islower() return flag \end{pyexo}

\begin{pyexo} def any\_lowercase5(s): for c in s: if not c.islower(): return False return True \end{pyexo}

\end{exercise}

## Lists

\section{Exercises}

\begin{exercise} Write a function called \verb"is\_sorted" that takes a list as a parameter and returns {\tt True} if the list is sorted in ascending order and {\tt False} otherwise. You can assume (as a precondition) that the elements of the list can be compared with the relational operators {\tt <}, {\tt >}, etc.

\index{precondition}

For example, \verb"is\_sorted(\[1,2,2])" should return {\tt True} and \verb"is\_sorted(\['b','a'])" should return {\tt False}. \end{exercise}

\begin{exercise} \label{exo:anagram}

\index{anagram}

Two words are anagrams if you can rearrange the letters from one to spell the other. Write a function called \verb"is\_anagram" that takes two strings and returns {\tt True} if they are anagrams. \end{exercise}

\begin{exercise} \label{exo:duplicate}

The (so-called) Birthday Paradox:

\begin{enumerate}

\index{birthday paradox} \index{duplicate}

\item Write a function called \verb"has\_duplicates" that takes a list and returns {\tt True} if there is any element that appears more than once. It should not modify the original list.

\item If there are 23 students in your class, what are the chances that two of you have the same birthday? You can estimate this probability by generating random samples of 23 birthdays and checking for matches. Hint: you can generate random birthdays with the {\tt randint} function in the {\tt random} module.

\index{random module} \index{module!random} \index{randint function} \index{function!randint}

\end{enumerate}

You can read about this problem at \url{wikipedia.org/wiki/Birthday\_paradox}, and you can see my solution at \url{thinkpython.com/code/birthday.py}.

\end{exercise}

\begin{exercise}

\index{duplicate} \index{uniqueness}

Write a function called \verb"remove\_duplicates" that takes a list and returns a new list with only the unique elements from the original. Hint: they don't have to be in the same order. \end{exercise}

\begin{exercise} \index{append method} \index{method append} \index{list!concatenation} \index{concatenation!list}

Write a function that reads the file {\tt words.txt} and builds a list with one element per word. Write two versions of this function, one using the {\tt append} method and the other using the idiom {\tt t = t + \[x]}. Which one takes longer to run? Why?

You can see my solution at \url{thinkpython.com/code/wordlist.py}. \end{exercise}

\begin{exercise} \index{reverse word pair}

Two words are a \`\`reverse pair'' if each is the reverse of the other. Write a program that finds all the reverse pairs in the word list. \end{exercise}

\newpage

\begin{exercise} \label{exo:bisection}

\index{membership!bisection search} \index{bisection search} \index{search, bisection}

\index{membership!binary search} \index{binary search} \index{search, binary}

To check whether a word is in the word list, you could use the {\tt in} operator, but it would be slow because it searches through the words in order.

Because the words are in alphabetical order, we can speed things up with a bisection search (also known as binary search), which is similar to what you do when you look a word up in the dictionary. You start in the middle and check to see whether the word you are looking for comes before the word in the middle of the list. If so, then you search the first half of the list the same way. Otherwise you search the second half.

Either way, you cut the remaining search space in half. If the word list has 113,809 words, it will take about 17 steps to find the word or conclude that it's not there.

Write a function called {\tt bisect} that takes a sorted list and a target value and returns the index of the value in the list, if it's there, or {\tt None} if it's not.

\index{bisect module} \index{module!bisect}

Or you could read the documentation of the {\tt bisect} module and use that! \end{exercise}

\begin{exercise} \index{interlocking words}

Two words `interlock'' if taking alternating letters from each forms a new word\footnote{This exercise is inspired by an example at \url{puzzlers.org}.}. For example,` shoe'' and `cold'' interlock to form` schooled.''

\begin{enumerate}

\item Write a program that finds all pairs of words that interlock. Hint: don't enumerate all pairs!

\item Can you find any words that are three-way interlocked; that is, every third letter forms a word, starting from the first, second or third?

\end{enumerate} \end{exercise}
