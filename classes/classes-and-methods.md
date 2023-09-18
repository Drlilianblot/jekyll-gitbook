# Classes and Methods

{% embed url="https://youtu.be/8xi38rzaO8w?si=IsOh6YpIdQH6Hr8d" %}

## Object-oriented features

Python is an **object-oriented programming language**, which means that it provides features that support object-oriented programming. It is not easy to define object-oriented programming, but we have already seen some of its characteristics:

* Programs are made up of object definitions and function definitions, and most of the computation is expressed in terms of operations on objects.
* Each object definition corresponds to some object or concept in the real world, and the functions that operate on that object correspond to the ways real-world objects interact.

For example, the [`Time` class defined earlier](classes-and-functions.md#time) corresponds to the way people record the time of day, and the functions we defined correspond to the kinds of things people do with times. Similarly, the `Point` and `Rectangle` classes correspond to the mathematical concepts of a point and a rectangle.

So far, we have not taken advantage of the features Python provides to support object-oriented programming. These features are not strictly necessary; most of them provide alternative syntax for things we have already done. But in many cases, the alternative is more concise and more accurately conveys the structure of the program.

For example, in the `Time` program, there is no obvious connection between the class definition and the function definitions that follow. With some examination, it is apparent that every function takes at least one `Time` object as an argument. This observation is the motivation for **methods**; a method is a function that is associated with a particular class. We have seen methods for strings, lists, dictionaries and tuples. In this chapter, we will define methods for user-defined types.

Methods are semantically the same as functions, but there are two syntactic differences:

* Methods are defined inside a class definition in order to make the relationship between the class and the method explicit.
* The syntax for invoking a method is different from the syntax for calling a function.

In the next few sections, we will take the functions from the previous two chapters and transform them into methods. This transformation is purely mechanical; you can do it simply by following a sequence of steps. If you are comfortable converting from one form to another, you will be able to choose the best form for whatever you are doing.

## What is an instance?

Before we get into creating a class itself, we need to understand an important distinction. A class is something that just contains structure – it defines how something should be laid out or structured, but doesn't actually fill in the content. For example, the `Time` class says that a time needs to have hours, minutes and seconds, but it does not actually say what the `time` is. This is where instances come in. An instance is a specific copy of the class that does contain all of the content. For example, if I create a time `t` of 1 hour 45 minutes and 10 seconds, then `t` **is an instance of** `Time`.

This can sometimes be a very difficult concept to master, so let’s look at it from another angle. Let’s say that the government has a particular tax form that it requires everybody to fill out. Everybody has to fill out the same type of form, but the content that people put into the form differs from person to person. A class is like the form: it specifies what content should exist. Your copy of the form with your specific information is like an instance of the class: it specifies what the content actually is.

## Printing objects

Earlier we defined a [class named `Time`](classes-and-functions.md#time) and you wrote a function named `print_time`:

{% code lineNumbers="true" %}
```python
class Time: 
    """represents the time of day. 
    attributes: hour, minute, second"""
    
    
def print_time(time): 
    print('%.2d:%.2d:%.2d' % (time.hour, time.minute, time.second))
```
{% endcode %}

To call this function, you have to pass a `Time` object as an argument:

```bash
>>> start = Time() 
>>> start.hour = 9 
>>> start.minute = 45 
>>> start.second = 0 
>>> print_time(start) 
 09:45:00 
>>>
```

To make `print_time` a method, all we have to do is move the function definition inside the class definition. Notice the change in indentation.

{% code lineNumbers="true" %}
```python
class Time(object): 
   """represents the time of day. 
   attributes: hour, minute, second"""
   
   def print_time(time):
       print('%.2d:%.2d:%.2d' % (time.hour,time.minute,time.second))
```
{% endcode %}

The second (and more concise) way is to use method syntax:

```bash
>>> start = Time() 
>>> start.hour = 9 
>>> start.minute = 45 
>>> start.second = 0 >>> start.print_time() 
 09:45:00 
>>> 
```

In this use of **dot** notation, `print_time` is the name of the method (again), and `start` is the object the method is invoked on, which is called the **subject**. Just as the subject of a sentence is what the sentence is about, the subject of a method invocation is what the method is about.

Inside the method, the subject is assigned to the first parameter, so in this case `start` is assigned to `time`.

## The `self` variable

By convention, the first parameter of a method is called `self`, so it would be more common to write `print_time` like this:

{% code lineNumbers="true" %}
```python
class Time(object): 
    """represents the time of day. 
    attributes: hour, minute, second"""
    
    def print_time(self):
        print('%.2d:%.2d:%.2d'%(self.hour,self.minute,self.second))
```
{% endcode %}

Invoking the method remains the same:

```bash
>>> start.print_time()
 09:45:00 
>>> 
```

The reason for this convention is an implicit metaphor:

* The syntax for a function call, `print_time(start)`, suggests that the function is the active agent. It says something like, "Hey `print_time`! Here's an object for you to print."
* In object-oriented programming, the objects are the active agents. A method invocation like `start.print_time()` says "Hey `start`! Please print yourself."

This change in perspective might be more polite, but it is not obvious that it is useful. In the examples we have seen so far, it may not be. But sometimes shifting responsibility from the functions onto the objects makes it possible to write more versatile functions, and makes it easier to maintain and reuse code.

{% hint style="info" %}
**Remark:** You might have noticed that the `print_time` method have this self variable as parameter, but that when you call the method you do not have to pass any value in the parameter. Why don’t we have to pass in the `self` parameter?&#x20;

This phenomena is a special behaviour of Python:&#x20;

when you call a method of an instance, Python automatically figures out what `self` should be (from the instance) and passes it to the function. In the case of `print_time`, Python first creates `self` and then passes it in.

To make it a little bit clearer as to what is going on, we can look at two different ways of calling `print_time`.&#x20;

* The first way is the standard way of doing it: `start.print_time()`&#x20;
* The second, while not conventional, is equivalent: `Time.print_time(start)` In this use of dot notation, `Time` is the name of the class, and `print_time` is the name of the method. `start` is passed as a parameter.

Having shown both ways, the first way is the preferred way.

Note how in the second example we had to pass in the instance because we did not call the method via the instance. Python can’t figure out what the instance is if it doesn't have any information about it.
{% endhint %}

**Exercise:** Rewrite the [function `time_to_int`](classes-and-functions.md#prototyping-versus-planning) defined earlier as a method. It is probably not appropriate to rewrite `int_to_time` as a method; it's not clear what object you would invoke it on!&#x20;

<details>

<summary>Answer</summary>

{% code lineNumbers="true" %}
```python
    # inside class Time:
    def time_to_int(self): 
        minutes = self.hour * 60 + self.minute 
        seconds = minutes * 60 + self.second 
        return seconds 
```
{% endcode %}

</details>

## Another example

Here's a version of `increment` (see previous implementation in [the section on modifiers](classes-and-functions.md#modifiers)) rewritten as a method:

{% code lineNumbers="true" %}
```python
    # inside class Time:
    def increment(self, seconds):
        seconds += self.time_to_int()
        return int_to_time(seconds)
```
{% endcode %}

This version assumes that `time_to_int` is written as a method, as in the previous exercise. Also, note that it is a pure function, not a modifier.

Here's how you would invoke `increment`:

```bash
>>> start.print_time() 
 09:45:00 
>>> end = start.increment(1337)
>>> end.print_time() 
 10:07:17 
>>>
```

The subject, `start`, gets assigned to the first parameter, `self`. The argument, `1337`, gets assigned to the second parameter, `seconds`.

This mechanism can be confusing, especially if you make an error. For example, if you invoke `increment` with two arguments, you get:

```bash
>>> end = start.increment(1337, 460) 
  TypeError: increment() takes exactly 2 arguments (3 given) 
>>>
```

The error message is initially confusing, because there are only two arguments in parentheses. But the subject is also considered an argument, so all together that's three.

## A more complicated example

`is_after` is slightly more complicated because it takes two `Time` objects as parameters. In this case it is conventional to name the first parameter `self` and the second parameter `other`:

{% code lineNumbers="true" %}
```python
    ## inside class Time:
    def is_after(self, other):
        return self.time_to_int() > other.time_to_int()
```
{% endcode %}

To use this method, you have to invoke it on one object and pass the other as an argument:

```bash
>>> end.is_after(start)
 True 
>>>
```

One nice thing about this syntax is that it almost reads like English: "end is after start?"

## The `__init__` method

The `__init__` method (short for "initialization") is a special method that gets invoked when an object is instantiated. Its full name is **`__init__`** (two underscore characters, followed by `init`, and then two more underscores). An init method for the `Time` class might look like this:

{% code lineNumbers="true" %}
```python
    # inside class Time:
    def __init__(self, hour=0, minute=0, second=0):
        self.hour = hour
        self.minute = minute
        self.second = second
```
{% endcode %}

It is common for the parameters of `__init__` to have the same names as the attributes. The statement `self.hour = hour` stores the value of the parameter `hour` as an attribute of `self`.

The parameters are optional, so if you call `Time()` with no arguments, you get the default values.

```bash
>>> time = Time() 
>>> time.print_time() 
 00:00:00 
>>>
```

&#x20;If you provide one argument, it overrides `hour`:

```bash
>>> time = Time (9) 
>>> time.print_time() 
 09:00:00 
>>>
```

If you provide two arguments, they override `hour` and `minute`.

```bash
>>> time = Time(9, 45) 
>>> time.print_time() 
 09:45:00 
>>>
```

And if you provide three arguments, they override all three default values.

**Exercise:** Write an init method for the `Point` class that takes `x` and `y` as optional parameters and assigns them to the corresponding attributes.&#x20;

<details>

<summary>Answer</summary>

{% code lineNumbers="true" %}
```python
class Point: 
    """represents a point in 2-D space""" 

    def __init__(self, x=0, y=0):
        self.x = x
        self.y = y
```
{% endcode %}

</details>

## The `__str__` method

`__str__` is a special method, like `__init__`, that is supposed to return a string representation of an object. For example, here is a `__str__` method for `Time` objects:

{% code lineNumbers="true" %}
```python
    # inside class Time:
    def __str__(self):
        return ('%.2d:%.2d:%.2d' 
                % (self.hour, self.minute, self.second))
```
{% endcode %}

When you `print` an object, Python invokes the `__str__` method:

```bash
>>> time = Time(9, 45) 
>>> print(time) 
 09:45:00 
>>>
```

When I write a new class, I almost always start by writing `__init__`, which makes it easier to instantiate objects, and `__str__`, which is useful for debugging.

**Exercise:** Write a `__str__` method for the `Point` class. Create a Point object and print it.&#x20;

<details>

<summary>Answer</summary>

{% code lineNumbers="true" %}
```python
Class Point:
    ...
    ...
    # inside class Point (indented)
    def __str__(self):
        return f'({self.x}, {self.y})'

# outside class Point (not indented
p = Point(4,  0)
print(p)
```
{% endcode %}

</details>

## Operator overloading

By defining other special methods, you can specify the behaviour of operators on user-defined types. For example, if you define a method named `__add__` for the `Time` class, you can use the `+` operator on Time objects.

Here is what the definition might look like:

{% code lineNumbers="true" %}
```python
    # inside class Time:
    def __add__(self, other):
        seconds = self.time_to_int() + other.time_to_int()
        return int_to_time(seconds)
```
{% endcode %}

And here is how you could use it:

```bash
>>> start = Time(9, 45) 
>>> duration = Time(1, 35) 
>>> print(start + duration) 
 11:20:00 
>>>
```

When you apply the `+` operator to `Time` objects, Python invokes `__add__`. When you print the result, Python invokes `__str__`. So there is quite a lot happening behind the scenes!

Changing the behaviour of an operator so that it works with user-defined types is called **operator overloading**. For every operator in Python there is a corresponding special method, like `__add__`. For more details, see the [special names docummentation](https://docs.python.org/3/reference/datamodel.html#special-method-names).

## Overloading the operator `==`

In Python, you can overload the `==` operator, also known as the equality operator, for custom classes by defining a special method called `__eq__()`. Overloading this operator allows you to specify how instances of your class should be compared for equality.

Here's how you can overload the `==` operator for a custom class:

```python
class MyClass:
    def __init__(self, value):
        self.value = value

    def __eq__(self, other):
        if not isinstance(other, MyClass):
            return False
        return self.value == other.value 
```

In the example above:

1. We define a custom class `MyClass` with an `__init__` method to initialize instances with a `value` attribute.
2. We overload the `==` operator by defining the `__eq__` method within the class. This method takes two arguments: `self` and `other`, where `self` represents the instance on the left side of the `==` operator, and `other` is the instance on the right side.
3. Inside the `__eq__` method, we check if `other` is an instance of `MyClass` using `isinstance`. If it is not we return `False`, otherwise we compare the `value` attribute of both instances and return `True` if they are equal, indicating that the instances are considered equal, `False` if it is not the case.

By overloading the `==` operator, you can define custom equality logic for instances of your class, making it possible to compare them based on specific attributes or criteria that are meaningful for your application.

Here is an example of overloading the `==` operator for the class `Time`.

{% code lineNumbers="true" %}
```python
    # inside class Time:
    def __eq__(self, other):
        if not isinstance(other, Time):
            return False
        return (self.hour == other.hour
                and self.minute == other.minute
                and self.second == other.second)
```
{% endcode %}

**Exercise:** Write an `__add__` method for the Point, and overload the operator == for class Point.

<details>

<summary>Answer</summary>

{% code lineNumbers="true" %}
```python
    # inside class Point
    def __add__(self, other):
        if not isinstance(other, Point):
            raise TypeError('unsupported operand type(s) for +.')
        self.x += other.x
        self.y += other.y

    def __eq__(self, other):
        if not isinstance(other, Point):
            return False
        return (self.x == other.x and self.y == other.y)
```
{% endcode %}

</details>

## Type-based dispatch

In the previous section we added two `Time` objects, but you also might want to add an integer to a `Time` object. The following is a version of `__add__` that checks the type of `other` and invokes either `add_time` or `increment`:

{% code lineNumbers="true" %}
```python
    # inside class Time:
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
{% endcode %}

The built-in function `isinstance` takes a value and a class object, and returns `True` if the value is an instance of the class.

If `other` is a `Time` object, `__add__` invokes `add_time`. Otherwise it assumes that the parameter is a number and invokes `increment`. This operation is called a **type-based dispatch** because it dispatches the computation to different methods based on the type of the arguments.

Here are examples that use the `+` operator with different types:

```bash
>>> start = Time(9, 45) 
>>> duration = Time(1, 35) 
>>> print(start + duration) 
 11:20:00 
>>> print(start + 1337)
 10:07:17 
>>>
```

Unfortunately, this implementation of addition is not commutative. If the integer is the first operand, you get

```
>>> print(1337 + start) 
 TypeError: unsupported operand type(s) for +: 'int' and 'instance' 
>>>
```

The problem is, instead of asking the `Time` object to add an integer, Python is asking an integer to add a `Time` object, and it doesn't know how to do that. But there is a clever solution for this problem: the special method `__radd__`, which stands for "right-side add". This method is invoked when a Time object appears on the right side of the `+` operator. Here's the definition:

{% code lineNumbers="true" %}
```python
    # inside class Time:
    def __radd__(self, other):
        return self.__add__(other)
```
{% endcode %}

And here's how it's used:

```bash
>>> print(1337 + start) 
 10:07:17 
>>> 
```

Unfortunately we are not done yet. For example, adding a Boolean `True` to a time has no sense and should raise an exception. However, our current solution allows such operation has shown here:

```bash
>>> print(start + True) 
 09:45:01 
>>> print(start + 1.1) 
 09:45:01 
>>>
```

The following code solves the issue by managing legal and illegal addition operations, ensuring that only additions with another `Time` object or an `int` are allowed.

{% code lineNumbers="true" %}
```python
    # inside class Time:
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
{% endcode %}

We have now achieved the desired behaviour, where trying to do an illegal addition raises an exception.

```
>>> print(start + True) 
  Traceback (most recent call last): ... 
  TypeError: can't add Time with bool
>>> print(start + 1.5) 
  Traceback (most recent call last): ... 
  TypeError: can't add Time with float
>>> print(start + '11:05:03') 
  Traceback (most recent call last): ... 
  TypeError: can't add Time with str 
>>>
```

{% hint style="info" %}
**Remark:** You may have noticed the Boolean expression `not isinstance(other, bool)` in the `elif` clause. One could wonder why we needed to this additional condition. As we mentioned earlier in , in Python `True` and `1` can be used interchangeably, the same applies between `False` and `0`. Therefore, adding `True` to an `int` is a valid operation.\
So why don't we allow the the addition between `Time` object and Booleans?\
We apply this restriction on the addition operator to preserve the semantic coherence of the `Time` type. The moral of the story is "It's not because we can do something that we should do it!". When building new types, it is essential to preserve semantic coherence for this type, and refrain from using any shortcut.&#x20;
{% endhint %}

**Exercise:** In most cases it does not make sense to add a string to a `Time`. However, the statement `print(start + '11:05:03')` tries to add a `Time` object to a well formatted string representing a valid time. At the moment, the statement raises an exception, change the definition of `__add__` in order to accept well formatted string representing a time value.

**Hint:** The following strings are not well formatted time values:

* `':10:15'` needs at least one digit for hours. Can have more than two digits for hours, for example both `'102:10:15'` and `'02:10:15'` are valid.
* `'01:1:15'` and `'01:10:1'` are invalid. Both minutes and seconds need **exactly** two digits.
* `'01:75:60'` is invalid for two reasons, minutes and seconds must be between `00` and `59`.&#x20;
* `'01:01:15.5'` only whole seconds are allowed.

**Exercise:** Write an `__add__` method for Points that works with either a Point object or a&#x20;

* If the second operand is a `Point`, the method should return a new `Point` whose $$x$$ coordinate is the sum of the $$x$$ coordinates of the operands, and likewise for the \$$y$ $coordinates.
* item If the second operand is a tuple, the method should add the first element of the tuple to the $$x$$ coordinate and the second element to the $$y$$ coordinate, and return a new `Point` with the result.

## `Polymorphism`

Type-based dispatch is useful when it is necessary, but (fortunately) it is not always necessary. Often you can avoid it by writing functions that work correctly for arguments with different types.

Many of the functions we wrote for strings will actually work for any kind of sequence. For example, in section histogram we used `histogram` to count the number of times each letter appears in a word.

{% code lineNumbers="true" %}
```python
def histogram(s): 
    d = dict() 
    for c in s: 
        if c not in d: 
            d[c] = 1 
        else: 
            d[c] = d[c]+1 
    return d 
```
{% endcode %}

This function also works for lists, tuples, and even dictionaries, as long as the elements of `s` are hashable, so they can be used as keys in `d`.

```bash
>>> t = ['spam', 'egg', 'spam', 'spam', 'bacon', 'spam'] 
>>> histogram(t) 
 {'bacon': 1, 'egg': 1, 'spam': 4}
>>>
```

Functions that can work with several types are called **polymorphic**. Polymorphism can facilitate code reuse. For example, the built-in function `sum`, which adds the elements of a sequence, works as long as the elements of the sequence support addition.

Since `Time` objects provide an `__add__` method, they work with `sum`:

```bash
>>> t1 = Time(7, 43) 
>>> t2 = Time(7, 41) 
>>> t3 = Time(7, 37) 
>>> total = sum([t1, t2, t3]) 
>>> print(total) 
 23:01:00 
>>> 
```

In general, if all of the operations inside a function work with a given type, then the function works with that type.

The best kind of polymorphism is the unintentional kind, where you discover that a function you already wrote can be applied to a type you never planned for.

## Debugging

It is legal to add attributes to objects at any point in the execution of a program, but if you are a stickler for type theory, it is a dubious practice to have objects of the same type with different attribute sets. It is usually a good idea to initialise all of an objects attributes in the `__init__` method.

If you are not sure whether an object has a particular attribute, you can use the built-in function `hasattr` (see <mark style="background-color:red;">\prettyref{sec:hasattr}</mark>).

Another way to access the attributes of an object is through the special attribute `__dict__`, which is a dictionary that maps attribute names (as strings) and values:

```bash
>>> p = Point(3, 4) 
>>> print(p.__dict__)
 {'y': 4, 'x': 3} 
>>>
```

For purposes of debugging, you might find it useful to keep this function handy:

{% code lineNumbers="true" %}
```python
def print_attributes(obj): 
    for attr in obj.dict: 
        print(attr, getattr(obj, attr))
```
{% endcode %}

`print_attributes` traverses the items in the object's dictionary and prints each attribute name and its corresponding value.

The built-in function `__getattr__` takes an object and an attribute name (as a string) and returns the attribute's value.
