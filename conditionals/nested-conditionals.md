# Nested conditionals

\section{} \index{nested conditional} \index{conditional!nested}

One conditional can also be nested within another. We could have written the trichotomy example like this:

\beforeverb \begin{pycode} if x == y: print('x and y are equal') else: if x < y: print('x is less than y') else: print('x is greater than y') \end{pycode} \afterverb % The outer conditional contains two branches. The first branch contains a simple statement. The second branch contains another {\tt if} statement, which has two branches of its own. Those two branches are both simple statements, although they could have been conditional statements as well. % Although the indentation of the statements makes the structure apparent, {\bf nested conditionals} become difficult to read very quickly. In general, it is a good idea to avoid them when you can.

Nested conditionals structures should be used when several statements are common to more than one sub-branch as illustrated in \prettyref{fig:nested-if-statements}. Here, statements {\tt B1} and {\tt B2} have been moved out of the nested {\tt if} statement as if is common to branches {\tt C} and {\tt D}. The same flow of execution could have been done using chained conditionals, however statements {\tt B1} and {\tt B2} would have to be duplicate in each sub-branch.

\index{flow diagram!nested if statements}

\begin{figure}\[htb]% \begin{center} \includegraphics\[height=8cm]{figs/ifnestedstatementsdiagram.png}% \caption{Nested conditionals {\tt if} statements control flow diagram.}% \label{fig:nested-if-statements}% \end{center} \end{figure}

Logical operators often provide a way to simplify nested conditional statements. For example, we can rewrite the following code using a single conditional:

\beforeverb \begin{pycode} if 0 < x: if x < 10: print('x is a positive single-digit number.') \end{pycode} \afterverb % The {\tt print} statement is executed only if we make it past both conditionals, so we can get the same effect with the {\tt and} operator:

\beforeverb \begin{pycode} if 0 < x and x < 10: print('x is a positive single-digit number.') \end{pycode} \afterverb
