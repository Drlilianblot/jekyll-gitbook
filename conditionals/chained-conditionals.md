# Chained conditionals

\section{} \index{chained conditional} \index{conditional!chained}

Sometimes there are more than two possibilities and we need more than two branches. One way to express a computation like that is a {\bf chained conditional} (aka {\tt if-elif-else} statement):

\beforeverb \begin{pycode} if x < y: print('x is less than y') elif x > y: print('x is greater than y') else: print('x and y are equal') \end{pycode} \afterverb % {\tt elif} is an abbreviation of \`\`else if.'' Again, exactly one branch will be executed. There is no limit on the number of {\tt elif} statements. If there is an {\tt else} clause, it has to be at the end, but there doesn't have to be one.

\index{elif keyword} \index{keyword!elif}

\beforeverb \begin{pycode} if choice == 'a': draw\_a() elif choice == 'b': draw\_b() elif choice == 'c': draw\_c() \end{pycode} \afterverb % Each condition is checked in order. If the first is false, the next is checked, and so on. If one of them is true, the corresponding branch executes, and the statement ends. Even if more than one condition is true, only the first true branch executes. The flow diagram of a chained conditional is shown in \prettyref{fig:if-elif-statement}.

\index{branch} \index{flow diagram!if-elif-else statement}

\begin{figure}\[htb]% \begin{center} \includegraphics\[height=8cm]{figs/ifelifstatementdiagram.png}% \caption{Conditional {\tt if-elif-else} statement control flow diagram.}% \label{fig:if-elif-statement}% \end{center} \end{figure}
