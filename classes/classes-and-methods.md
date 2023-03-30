# Classes and Methods

\chapter{Classes and methods}

\section{Object-oriented features}

\index{object-oriented programming}

Python is an {\bf object-oriented programming language}, which means that it provides features that support object-oriented programming. % It is not easy to define object-oriented programming, but we have already seen some of its characteristics:

\begin{itemize}

\item Programs are made up of object definitions and function definitions, and most of the computation is expressed in terms of operations on objects.

\item Each object definition corresponds to some object or concept in the real world, and the functions that operate on that object correspond to the ways real-world objects interact.

\end{itemize}

For example, the {\tt Time} class defined in \prettyref{cha:time} corresponds to the way people record the time of day, and the functions we defined correspond to the kinds of things people do with times. Similarly, the {\tt Point} and {\tt Rectangle} classes correspond to the mathematical concepts of a point and a rectangle.

So far, we have not taken advantage of the features Python provides to support object-oriented programming. These features are not strictly necessary; most of them provide alternative syntax for things we have already done. But in many cases, the alternative is more concise and more accurately conveys the structure of the program.

For example, in the {\tt Time} program, there is no obvious connection between the class definition and the function definitions that follow. With some examination, it is apparent that every function takes at least one {\tt Time} object as an argument. % \index{method} \index{function} % This observation is the motivation for {\bf methods}; a method is a function that is associated with a particular class. We have seen methods for strings, lists, dictionaries and tuples. In this chapter, we will define methods for user-defined types.

\index{syntax} \index{semantics}

Methods are semantically the same as functions, but there are two syntactic differences:

\begin{itemize}

\item Methods are defined inside a class definition in order to make the relationship between the class and the method explicit.

\item The syntax for invoking a method is different from the syntax for calling a function.

\end{itemize}

In the next few sections, we will take the functions from the previous two chapters and transform them into methods. This transformation is purely mechanical; you can do it simply by following a sequence of steps. If you are comfortable converting from one form to another, you will be able to choose the best form for whatever you are doing.

\section{What is an instance?} \label{sec:instance}

Before we get into creating a class itself, we need to understand an important distinction. A class is something that just contains structure – it defines how something should be laid out or structured, but does't actually fill in the content. For example, the {\tt Time} class says that a time needs to have hours, minutes and seconds, but it does not actually say what the {\tt time} is. This is where instances come in. An instance is a specific copy of the class that does contain all of the content. For example, if I create a time {\tt t} of 1 hour 45 minutes and 10 seconds, then {\tt t} is an instance of {\tt Time}.

This can sometimes be a very difficult concept to master, so let’s look at it from another angle. Let’s say that the government has a particular tax form that it requires everybody to fill out. Everybody has to fill out the same type of form, but the content that people put into the form differs from person to person. A class is like the form: it specifies what content should exist. Your copy of the form with your specific information if like an instance of the class: it specifies what the content actually is.

\section{Printing objects} \label{sec:print-time}

\index{object!printing}

In \prettyref{cha:time}, we defined a class named {\tt Time} and in \prettyref{exo:printtime}, you wrote a function named \verb"print\_time":

\beforeverb \begin{pycode} class Time(object): """represents the time of day. attributes: hour, minute, second"""

def print\_time(time): print('%.2d:%.2d:%.2d' % (time.hour, time.minute, time.second)) \end{pycode} \afterverb % To call this function, you have to pass a {\tt Time} object as an argument:

\beforeverb \begin{pyinterpreter}

> > > start = Time() start.hour = 9 start.minute = 45 start.second = 00 print\_time(start) 09:45:00 \end{pyinterpreter} \afterverb % To make \verb"print\_time" a method, all we have to do is move the function definition inside the class definition. Notice the change in indentation.

\index{indentation}

\beforeverb \begin{pycode} class Time(object): """represents the time of day. attributes: hour, minute, second"""

```
def print_time(time):
    print('%.2d:%.2d:%.2d' %
          (time.hour, time.minute, time.second))
```

\end{pycode} \afterverb %

The second (and more concise) way is to use method syntax:

\index{method syntax}

\beforeverb \begin{pyinterpreter}

> > > start.print\_time() 09:45:00 \end{pyinterpreter} \afterverb % In this use of dot notation, \verb"print\_time" is the name of the method (again), and {\tt start} is the object the method is invoked on, which is called the {\bf subject}. Just as the subject of a sentence is what the sentence is about, the subject of a method invocation is what the method is about.

\index{subject}

Inside the method, the subject is assigned to the first parameter, so in this case {\tt start} is assigned to {\tt time}.

\index{self (parameter name)} \index{parameter!self}

\section{The {\tt self} variable} \label{sec:self}

By convention, the first parameter of a method is called {\tt self}, so it would be more common to write \verb"print\_time" like this:

\beforeverb \begin{pycode} class Time(object): """represents the time of day. attributes: hour, minute, second"""

```
def print_time(self):
    print('%.2d:%.2d:%.2d' %
          (self.hour, self.minute, self.second))
```

\end{pycode} \afterverb % Invoking the method remains the same:

\beforeverb \begin{pyinterpreter}

> > > start.print\_time() 09:45:00 \end{pyinterpreter} \afterverb

The reason for this convention is an implicit metaphor:

\index{metaphor, method invocation}

\begin{itemize}

\item The syntax for a function call, \verb"print\_time(start)", suggests that the function is the active agent. It says something like, \`\`Hey \verb"print\_time"! Here's an object for you to print.''

\item In object-oriented programming, the objects are the active agents. A method invocation like \verb"start.print\_time()" says \`\`Hey {\tt start}! Please print yourself.''

\end{itemize}

This change in perspective might be more polite, but it is not obvious that it is useful. In the examples we have seen so far, it may not be. But sometimes shifting responsibility from the functions onto the objects makes it possible to write more versatile functions, and makes it easier to maintain and reuse code.

\begin{remark} You might have noticed that the \verb"print\_time" method have this self variable as parameter, but that when you call the method you do not have to pass any value in the parameter. Why don’t we have to pass in the {\tt self} parameter? This phenomena is a special behavior of Python: when you call a method of an instance, Python automatically figures out what {\tt self} should be (from the instance) and passes it to the function. In the case of \verb"print\_time", Python first creates self and then passes it in.

To make it a little bit clearer as to what is going on, we can look at two different ways of calling \verb"print\_time". \begin{itemize} \item The first way is the standard way of doing it: \ \verb"start.print\_time()"

```
\item The second, while not conventional, is equivalent: \\
\verb"Time.print_time(start)"\\
In this use of dot notation, {\tt Time} is the name of the class,
```

and \verb"print\_time" is the name of the method. {\tt start} is passed as a parameter. \end{itemize}

Note how in the second example we had to pass in the instance because we did not call the method via the instance. Python can’t figure out what the instance is if it doesn't have any information about it.

\end{remark}

\begin{exercise} \label{exo:convert} Rewrite \verb"time\_to\_int" (from \prettyref{sec:prototype}) as a method. It is probably not appropriate to rewrite \verb"int\_to\_time" as a method; it's not clear what object you would invoke it on! \end{exercise}

\section{Another example}

\index{increment}

Here's a version of {\tt increment} (from \prettyref{sec:increment}) rewritten as a method:

\beforeverb \begin{pycode}

## inside class Time:

```
def increment(self, seconds):
    seconds += self.time_to_int()
    return int_to_time(seconds)
```

\end{pycode} \afterverb % This version assumes that \verb"time\_to\_int" is written as a method, as in \prettyref{exo:convert}. Also, note that it is a pure function, not a modifier.

Here's how you would invoke {\tt increment}:

\beforeverb \begin{pyinterpreter}

> > > start.print\_time() 09:45:00 end = start.increment(1337) end.print\_time() 10:07:17 \end{pyinterpreter} \afterverb % The subject, {\tt start}, gets assigned to the first parameter, {\tt self}. The argument, {\tt 1337}, gets assigned to the second parameter, {\tt seconds}.

This mechanism can be confusing, especially if you make an error. For example, if you invoke {\tt increment} with two arguments, you get:

\index{exception!TypeError} \index{TypeError}

\beforeverb \begin{pyinterpreter}

> > > end = start.increment(1337, 460) TypeError: increment() takes exactly 2 arguments (3 given) \end{pyinterpreter} \afterverb % The error message is initially confusing, because there are only two arguments in parentheses. But the subject is also considered an argument, so all together that's three.

\section{A more complicated example}

\verb"is\_after" (from \prettyref{exo:is-after}) is slightly more complicated because it takes two Time objects as parameters. In this case it is conventional to name the first parameter {\tt self} and the second parameter {\tt other}:

\index{other (parameter name)} \index{parameter!other}

\beforeverb \begin{pycode}

## inside class Time:

```
def is_after(self, other):
    return self.time_to_int() > other.time_to_int()
```

\end{pycode} \afterverb % To use this method, you have to invoke it on one object and pass the other as an argument:

\beforeverb \begin{pyinterpreter}

> > > end.is\_after(start) True \end{pyinterpreter} \afterverb % One nice thing about this syntax is that it almost reads like English: \`\`end is after start?''

\section{The init method}

\index{init method} \index{method!init}

The init method (short for \`\`initialization'') is a special method that gets invoked when an object is instantiated.\
Its full name is \verb"**init**" (two underscore characters, followed by {\tt init}, and then two more underscores). An init method for the {\tt Time} class might look like this:

\beforeverb \begin{pycode}

## inside class Time:

```
def __init__(self, hour=0, minute=0, second=0):
    self.hour = hour
    self.minute = minute
    self.second = second
```

\end{pycode} \afterverb % It is common for the parameters of \verb"**init**" to have the same names as the attributes. The statement

\beforeverb \begin{pycode} self.hour = hour \end{pycode} \afterverb % stores the value of the parameter {\tt hour} as an attribute of {\tt self}.

\index{optional parameter} \index{parameter!optional} \index{default value} \index{override}

The parameters are optional, so if you call {\tt Time} with no arguments, you get the default values.

\beforeverb \begin{pyinterpreter}

> > > time = Time() time.print\_time() 00:00:00 \end{pyinterpreter} \afterverb % If you provide one argument, it overrides {\tt hour}:

\beforeverb \begin{pyinterpreter}

> > > time = Time (9) time.print\_time() 09:00:00 \end{pyinterpreter} \afterverb % If you provide two arguments, they override {\tt hour} and {\tt minute}.

\beforeverb \begin{pyinterpreter}

> > > time = Time(9, 45) time.print\_time() 09:45:00 \end{pyinterpreter} \afterverb % And if you provide three arguments, they override all three default values.

\begin{exercise} \index{Point class} \index{class!Point}

Write an init method for the {\tt Point} class that takes {\tt x} and {\tt y} as optional parameters and assigns them to the corresponding attributes. \end{exercise}

\section{The {\tt \_\_str\_\_} method}

\index{str method@\_\_str\_\_ method} \index{method!\_\_str\_\_}

\verb"**str**" is a special method, like \verb"**init**", that is supposed to return a string representation of an object.

\index{string representation}

For example, here is a {\tt str} method for Time objects:

\beforeverb \begin{pycode}

## inside class Time:

```
def __str__(self):
    return ('%.2d:%.2d:%.2d'
            % (self.hour, self.minute, self.second))
```

\end{pycode} \afterverb % When you {\tt print} an object, Python invokes the {\tt str} method:

\index{print statement} \index{statement!print}

\beforeverb \begin{pyinterpreter}

> > > time = Time(9, 45) print(time) 09:45:00 \end{pyinterpreter} \afterverb % When I write a new class, I almost always start by writing \verb"**init**", which makes it easier to instantiate objects, and \verb"**str**", which is useful for debugging.

\begin{exercise} Write a {\tt str} method for the {\tt Point} class. Create a Point object and print it. \end{exercise}

\section{Operator overloading} \label{sec:operator-overloading}

By defining other special methods, you can specify the behavior of operators on user-defined types. For example, if you define a method named \verb"**add**" for the {\tt Time} class, you can use the {\tt +} operator on Time objects.

Here is what the definition might look like:

\index{add method} \index{method!add}

\beforeverb \begin{pycode}

## inside class Time:

```
def __add__(self, other):
    seconds = self.time_to_int() + other.time_to_int()
    return int_to_time(seconds)
```

\end{pycode} \afterverb % And here is how you could use it:

\beforeverb \begin{pyinterpreter}

> > > start = Time(9, 45) duration = Time(1, 35) print(start + duration) 11:20:00 \end{pyinterpreter} \afterverb % When you apply the {\tt +} operator to Time objects, Python invokes \verb"**add**". When you print the result, Python invokes \verb"**str**". So there is quite a lot happening behind the scenes!

\index{operator overloading}

Changing the behavior of an operator so that it works with user-defined types is called {\bf operator overloading}. For every operator in Python there is a corresponding special method, like \verb"**add**". For more details, see \url{docs.python.org/ref/specialnames.html}.

\begin{exercise} Write an {\tt add} method for the Point class.\
\end{exercise}

\section{Type-based dispatch}

In the previous section we added two Time objects, but you also might want to add an integer to a Time object. The following is a version of \verb"**add**" that checks the type of {\tt other} and invokes either \verb"add\_time" or {\tt increment}:

\beforeverb \begin{pycode}

## inside class Time:

```
def __add__(self, other):
    if isinstance(other, Time):
        return self.add_time(other)
    else:
        return self.increment(other)

def add_time(self, other):
    seconds = self.time_to_int() + other.time_to_int()
    return int_to_time(seconds)

def increment(self, seconds):
    seconds += self.time_to_int()
    return int_to_time(seconds)
```

\end{pycode} \afterverb % The built-in function {\tt isinstance} takes a value and a class object, and returns {\tt True} if the value is an instance of the class.

\index{isinstance function} \index{function!isinstance}

If {\tt other} is a Time object, \verb"**add**" invokes \verb"add\_time". Otherwise it assumes that the parameter is a number and invokes {\tt increment}. This operation is called a {\bf type-based dispatch} because it dispatches the computation to different methods based on the type of the arguments.

\index{type-based dispatch} \index{dispatch, type-based}

Here are examples that use the {\tt +} operator with different types:

\beforeverb \begin{pyinterpreter}

> > > start = Time(9, 45) duration = Time(1, 35) print(start + duration) 11:20:00 print(start + 1337) 10:07:17 \end{pyinterpreter} \afterverb % Unfortunately, this implementation of addition is not commutative. If the integer is the first operand, you get

\index{commutativity}

\beforeverb \begin{pyinterpreter}

> > > print(1337 + start) TypeError: unsupported operand type(s) for +: 'int' and 'instance' \end{pyinterpreter} \afterverb % The problem is, instead of asking the Time object to add an integer, Python is asking an integer to add a Time object, and it doesn't know how to do that. But there is a clever solution for this problem: the special method \verb"**radd**", which stands for \`\`right-side add.'' This method is invoked when a Time object appears on the right side of the {\tt +} operator. Here's the definition:

\index{radd method} \index{method!radd}

\beforeverb \begin{pycode}

## inside class Time:

```
def __radd__(self, other):
    return self.__add__(other)
```

\end{pycode} \afterverb % And here's how it's used:

\beforeverb \begin{pyinterpreter}

> > > print(1337 + start) 10:07:17 \end{pyinterpreter} \afterverb % Unfortunately we are not done yet. For example, adding a Boolean {\tt True} to a time has no sense and should raise an exception. However, our current solution allows such operation has shown here:

\beforeverb \begin{pyinterpreter}

> > > print(start + True) 09:45:01 print(start + 1.1) 09:45:01 \end{pyinterpreter} \afterverb

The following code solves the issue by managing legal and illegal addition operations, ensuring that only additions with another {\tt Time} object or an {\tt int} are allowed.

\beforeverb \begin{pycode}

## inside class Time:

```
def __add__(self, other):
    if isinstance(other, Time):
        return self.add_time(other)
    elif (isinstance(other, int)
              and not isinstance(other, bool)):
        return self.increment(other)
    else:
        raise TypeError("can't add Time with " +
                        type(other).__qualname__)
```

\end{pycode} \afterverb

We have now achieved the desired behaviour, where trying to do an illegal addition raises an exception.

\beforeverb \begin{pyinterpreter}

> > > print(start + True) Traceback (most recent call last): ... TypeError: can't add Time with bool

> > > print(start + 1.5) Traceback (most recent call last): ... TypeError: can't add Time with float

> > > print(start + '11:05:03') Traceback (most recent call last): ... TypeError: can't add Time with str \end{pyinterpreter} \afterverb

\begin{remark} You may have noticed the Boolean expression \pyinline{not isinstance(other, bool)} in the {\tt elif} clause. One could wonder why we needed to this additional condition. As we mentioned earlier in \prettyref{sec:logical-operator}, in Python True and 1 can be used interchangeably, the same applies between {\tt False} and 0. Therefore, adding {\tt True} to an {\tt int} is a valid operation.

So why don't we allow the the addition between {\tt Time} object and Booleans?

We apply this restriction on the addition operator to preserve the semantic coherence of the {\tt Time} type. The moral of the story is \`\`It's not because we can do something that we should do it!''. When building new types, it is essential to preserve semantic coherence for this type, and refrain from using any shortcut. \end{remark}

\begin{exercise} In most cases it does not make sense to add a string to a {\tt Time}. However, the statement \pyinline{print(start + '11:05:03')} tries to add a {\tt Time} object to a well formatted string representing a valid time. At the moment, the statement raises an exception, change the definition of \verb|**add**| in order to accept well formatted string representing a time value.

{\bf Hint:} The following strings are not well formatted time values: \begin{itemize} \item \verb|':10:15'| needs at least one digit for hours. Can have more than two digits for hours, for example both \verb|'102:10:15'| and \verb|'02:10:15'| are valid. \item \verb|'01:1:15'| and \verb|'01:10:1'| are invalid. Both minutes and seconds need {\bf exactly} two digits. \item \verb|'01:75:60'| is invalid for two reasons, minutes and seconds must be between {\tt 00} and {\tt 59}. \item \verb|'01:01:15.5'| only whole seconds are allowed. \end{itemize} \end{exercise}

\begin{exercise} Write an {\tt add} method for Points that works with either a Point object or a tuple:\
\begin{itemize}

\item If the second operand is a Point, the method should return a new Point whose $x$ coordinate is the sum of the $x$ coordinates of the operands, and likewise for the $y$ coordinates.

\item If the second operand is a tuple, the method should add the first element of the tuple to the $x$ coordinate and the second element to the $y$ coordinate, and return a new Point with the result.

\end{itemize}

\end{exercise}

\section{Polymorphism}

Type-based dispatch is useful when it is necessary, but (fortunately) it is not always necessary. Often you can avoid it by writing functions that work correctly for arguments with different types.

\index{type-based dispatch} \index{dispatch!type-based}

Many of the functions we wrote for strings will actually work for any kind of sequence. For example, in \prettyref{sec:histogram} we used {\tt histogram} to count the number of times each letter appears in a word.

\beforeverb \begin{pycode} def histogram(s): d = dict() for c in s: if c not in d: d\[c] = 1 else: d\[c] = d\[c]+1 return d \end{pycode} \afterverb % This function also works for lists, tuples, and even dictionaries, as long as the elements of {\tt s} are hashable, so they can be used as keys in {\tt d}.

\beforeverb \begin{pyinterpreter}

> > > t = \['spam', 'egg', 'spam', 'spam', 'bacon', 'spam'] histogram(t) {'bacon': 1, 'egg': 1, 'spam': 4} \end{pyinterpreter} \afterverb % Functions that can work with several types are called {\bf polymorphic}. Polymorphism can facilitate code reuse. For example, the built-in function {\tt sum}, which adds the elements of a sequence, works as long as the elements of the sequence support addition.

\index{polymorphism}

Since Time objects provide an {\tt add} method, they work with {\tt sum}:

\beforeverb \begin{pyinterpreter}

> > > t1 = Time(7, 43) t2 = Time(7, 41) t3 = Time(7, 37) total = sum(\[t1, t2, t3]) print(total) 23:01:00 \end{pyinterpreter} \afterverb % In general, if all of the operations inside a function work with a given type, then the function works with that type.

The best kind of polymorphism is the unintentional kind, where you discover that a function you already wrote can be applied to a type you never planned for.

\section{Debugging} \index{debugging}

It is legal to add attributes to objects at any point in the execution of a program, but if you are a stickler for type theory, it is a dubious practice to have objects of the same type with different attribute sets. It is usually a good idea to initialize all of an objects attributes in the init method.

\index{init method} \index{attribute!initializing}

If you are not sure whether an object has a particular attribute, you can use the built-in function {\tt hasattr} (see \prettyref{sec:hasattr}).

\index{hasattr function} \index{function!hasattr} \index{dict attribute@\_\_dict\_\_ attribute} \index{attribute!\_\_dict\_\_}

Another way to access the attributes of an object is through the special attribute \verb"**dict**", which is a dictionary that maps attribute names (as strings) and values:

\beforeverb \begin{pyinterpreter}

> > > p = Point(3, 4) print p.**dict** {'y': 4, 'x': 3} \end{pyinterpreter} \afterverb % For purposes of debugging, you might find it useful to keep this function handy:

\beforeverb \begin{pycode} def print\_attributes(obj): for attr in obj.**dict**: print attr, getattr(obj, attr) \end{pycode} \afterverb % \verb"print\_attributes" traverses the items in the object's dictionary and prints each attribute name and its corresponding value.

\index{traversal!dictionary} \index{dictionary!traversal}

The built-in function {\tt getattr} takes an object and an attribute name (as a string) and returns the attribute's value.

\index{getattr function} \index{function!getattr}

\section{Glossary}

\begin{description}

\item\[object-oriented language:] A language that provides features, such as user-defined classes and method syntax, that facilitate object-oriented programming. \index{object-oriented language}

\item\[object-oriented programming:] A style of programming in which data and the operations that manipulate it are organized into classes and methods. \index{object-oriented programming}

\item\[method:] A function that is defined inside a class definition and is invoked on instances of that class. \index{method}

\item\[subject:] The object a method is invoked on. \index{subject}

\item\[operator overloading:] Changing the behavior of an operator like {\tt +} so it works with a user-defined type. \index{overloading} \index{operator!overloading}

\item\[type-based dispatch:] A programming pattern that checks the type of an operand and invokes different functions for different types. \index{type-based dispatch}

\item\[polymorphic:] Pertaining to a function that can work with more than one type.

\index{polymorphism}

\end{description}

\section{Exercises}

\begin{exercise}

\index{default value!avoiding mutable} \index{mutable object, as default value} \index{worst bug} \index{bug!worst}

This exercise is a cautionary tale about one of the most common, and difficult to find, errors in Python.

\begin{enumerate}

\index{Kangaroo class} \index{class!Kangaroo}

\item Write a definition for a class named {\tt Kangaroo} with the following methods:

\begin{enumerate}

\item An \verb"**init**" method that initializes an attribute named \verb"pouch\_contents" to an empty list.

\item A method named \verb"put\_in\_pouch" that takes an object of any type and adds it to \verb"pouch\_contents".

\item A \verb"**str**" method that returns a string representation of the Kangaroo object and the contents of the pouch.

\end{enumerate} % Test your code by creating two {\tt Kangaroo} objects, assigning them to variables named {\tt kanga} and {\tt roo}, and then adding {\tt roo} to the contents of {\tt kanga}'s pouch.

\item Download \url{thinkpython.com/code/BadKangaroo.py}. It contains a solution to the previous problem with one big, nasty bug. Find and fix the bug.

If you get stuck, you can download \url{thinkpython.com/code/GoodKangaroo.py}, which explains the problem and demonstrates a solution.

\index{aliasing} \index{embedded object} \index{object!embedded}

\end{enumerate}

\end{exercise}
