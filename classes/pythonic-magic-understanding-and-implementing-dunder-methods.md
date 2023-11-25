# Pythonic Magic: Understanding and Implementing Dunder Methods

Dunder methods, short for "double underscore" methods, are special methods in Python identified by their names enclosed in double underscores at the beginning and end, such as `__init__` or `__str__`. These methods play a crucial role in defining how objects behave in various contexts. In this section, we will be looking into their use, common implementations, best practices, and considerations.

{% embed url="https://www.youtube.com/watch?v=-KwmuCc0XIs" %}

## Purpose of Dunder Methods

Dunder methods are also known as magic methods or operator methods, because they are invoked automatically by the interpreter when certain operations or expressions are evaluated. For example, the `__len__` method is called when the `len()` function is applied to an object, and the `__eq__` method is called when the `==` operator is used between two objects.

Dunder methods can be implemented to customise the behaviour and functionality of user-defined classes. They allow programmers to define how objects of their classes interact with built-in functions, operators, and keywords. This customisation enhances the readability and expressiveness of your code, making it more aligned with Pythonic conventions.

We have already seen two dunder methods:

\- `__init__(self)`: For object initialisation.

\- `__str__(self)`: Creating a human-readable string representation.

Dunder methods should be implemented when you want to define custom behaviour for your class instances. For example, you can implement the commonly used dunder methods:

\- `__repr__(self)`: to provide a representation for debugging.

\- `__eq__(self, other)`: to customise equality comparisons.

\- `__ne__(self, other)`: to Implement inequality comparisons.

In addition, if you would like to use the custom class in a set or as dictionary keys, your class must implement the `__hash__(self)` enabling instances to be used as dictionary keys.

## Indexable classes

Indexable classes provide a familiar and intuitive interface for accessing elements within instances of a class. By implementing dunder methods associated with indexing, we can make our classes behave like sequences or containers, opening up a myriad of possibilities for efficient data manipulation.

To create indexable Classes you must implement the following dunder methods:

* `__getitem__(self, index)` - This method defines the behaviour of accessing an element at a specific index using square bracket notation. It should return the value associated with the given index.
* `__setitem__(self, index, value)` - For mutable indexable classes, this method allows us to set the value at a particular index. It is invoked when we use the assignment operator with square bracket notation.
* `__delitem__(self, index)` - When an element is removed using the del statement and square bracket notation, this method is called to handle the deletion of the specified index.

For example, consider a class representing a simplified version of a DVD catalogue:

{% code lineNumbers="true" %}
```python
class DVDCatalogue:
    def __init__(self, list_of_movies=None):
        if list_of_movies is None:
            self._movies = []
        else:
           self._movies = list_of_movies.copy()

    def add_movie(self, movie):
        self._movie.append(movie)

    def __getitem__(self, index):
        return self._movies[index]

    def __setitem__(self, index, value):
        self._movies[index] = value

    def __delitem__(self, index):
        del self._movies[index]

    def __len__(self):
        return len(self._movies)

    def __repr__(self):
        return f"DVDCatalog({self._movies})"

    def __iter__(self):
        self.current_index = 0
        return self

    def __next__(self):
        if self.current_index < len(self._movies):
            current_movie = self._movies[self.current_index]
            self.current_index += 1
            return current_movie
        else:
            raise StopIteration
```
{% endcode %}

In this example, we've defined \_`_getitem__`, `__setitem__`, and `__delitem__` to provide the indexable behaviour for our `DVDCatalogue` class. Additionally, `__len__` is implemented to allow the use of the built-in `len()` function, and `__repr__` is included for a readable representation of the object.

To use this class, we can now use indices to access specific DVDs in the catalogue.

{% code lineNumbers="true" %}
```python
from dundermethods import DVDCatalogue

movies = ['Sacré Graal ! ', 
          "Monty Python's Life of Brian", 
          "Monty Python's The Meaning of Life"]

my_dvds = DVDCatalogue(movies)
print('\n------Initial list---------------------')
for index in range(len(my_dvds)):
    print(index + 1, ':', my_dvds[index])

my_dvds[0] = 'Monty Python and the Holy Grail'
del my_dvds[2]

print('\n------Updated list---------------------')
for index in range(len(my_dvds)):
    print(index + 1, ':', my_dvds[index])
```
{% endcode %}

On line 9 we use the `len` function to get the number of DVDs in the catalogue. The call `len(my_dvds)` automatically invokes the dunder method `__len__` and executes it.

On line 10, the statement `print(index +1, my_dvds[index])` invokes the `__getitem__(self, index)` and on line 12 `my_dvds[0] = ‘...’` invokes the `__setitem__(self, index, value)`.

Finally, on line 13, the `del my_dvds[2]` calls the dunder method `__delitem__`. Executing this code results in the program output shown below.

```
------Initial list---------------------
1 : Sacré Graal !
2 : Monty Python's Life of Brian
3 : Monty Python's The Meaning of Life

------Updated list---------------------
1 : Monty Python and the Holy Grail
2 : Monty Python's Life of Brian
```

As you can see,  implementing these dunder methods makes our classes behave like sequences. It enhances the readability and expressiveness of your code, making it more aligned with Pythonic conventions.

## Iterable classes

Iterable classes allow us to traverse their elements in a systematic way, providing a natural integration with Python's iteration protocols. By implementing dunder methods associated with iteration, we can make our classes behave like built-in iterable types, such as lists or tuples.

To create iterable classes the following to methods should be implemented:

* `__iter__(self)` - This method defines how an instance of the class should behave when an iterator is requested. It should return an iterator object, which implements the \_\_next\_\_ method.
* `__next__(self)` - For iterable classes, this method is called to retrieve the next element in the iteration. It should raise StopIteration when there are no more elements to iterate.
* `__iter__` and `__next__` together form the basis of the iterator protocol, allowing instances of our class to seamlessly integrate with Python's iteration constructs, like for loops.

Let's revisit our previous class `DVDCatalogue`, we can expand our class functionality to allow iterating through all the books in the catalogue.

{% code lineNumbers="true" %}
```python
    def __iter__(self):
        self.current_index = 0
        return self

    def __next__(self):
        if self.current_index < len(self._movies):
            current_movie = self._movies[self.current_index]
            self.current_index += 1
            return current_movie
        else:
            raise StopIteration
```
{% endcode %}

First we need to define an attribute `current_index` storing the current position in our iteration. Every time an iterator is requested, the `__iter__` method is called and the `current_index` is set to `0`.

The method `__next__` on line 5 is called  to get the next item in the iteration. If the `current_index` is smaller than the length of the list of movies, it means the iteration is not finished yet. We must return the movie at position `current_index` and increment  the current index by one.

On line 11, the current index exceeds the length of the list, and therefore there are no more movies to iterate through. The method should raise the `StopIteration` exception to signal the end of iteration, as per the Python iterator protocol.

We can now use an instance of our class within a for loop as shown in the code here.

{% code lineNumbers="true" %}
```python
movies = ['Sacré Graal ! ', 
          "Monty Python's Life of Brian", 
          "Monty Python's The Meaning of Life"]

my_dvds = DVDCatalogue(movies)
print('\n------Iterable list--------------------')
for movie in my_dvds:
    print(movie)
```
{% endcode %}

On line 7, the statement `for movie in my_dvds` invokes the `__iter__` method to request an iterator. Then the `__next__` method is called to assign the movie at index `0` to the variable movie. At the end of each iteration, that is after the print statement on line 8 is executed, the `__next__` method is called again. The process repeats until the method `__next__` raises the `StopIteration` exception.

The output of the program can is shown below.

```
------Iterable list--------------------
Sacré Graal !
Monty Python's Life of Brian
Monty Python's The Meaning of Life
```

## Comparable classes

Comparable classes enable us to establish a meaningful order among instances of a class. This is particularly useful when sorting or searching through collections of objects. By implementing dunder methods related to comparisons, we can customise the behaviour of these operators based on the attributes of our class instances.

Here are the Key Dunder Methods for Comparable Classes:

* `__eq__(self, other)` - The equality operator (`==`) can be customised by defining this method. It returns `True` if the current instance is equal to the other instance, and `False` otherwise.
* `__lt__(self, other)` - The less-than operator (<) is defined by implementing this method. It returns True if the current instance is less than the other instance, and False otherwise.
* `__le__(self, other)` - Similar to `__lt__`, this method defines the less-than-or-equal-to operator (<=).
* `__gt__(self, other)` - The greater-than operator (>) is implemented by defining this method. It returns `True` if the current instance is greater than the other instance, and `False` otherwise.
* `__ge__(self, other)` - Similar to `__gt__`, this method defines the greater-than-or-equal-to operator (>=).

Let's consider a simple class representing roman numerals.

{% code lineNumbers="true" %}
```python
class RomanNumeral:
    ROMAN_MAP = {1: 'I', 4: 'IV', 5: 'V', 9: 'IX',
            10: 'X', 40: 'XL', 50: 'L', 90: 'XC', 100: 'C',
            400: 'CD', 500: 'D', 900: 'CM',1000: 'M'
        }
    
    def __init__(self, value):
        self.value = value

    def to_roman(self):
        result = ''
        num = self.value
        for val in sorted(self.ROMAN_MAP.keys(), reverse=True):
            while num >= val:
                result += self.ROMAN_MAP[val]
                num -= val
        return result

    def __eq__(self, other):
        if isinstance(other, RomanNumeral):
            return self.value == other.value
        return False

    def __lt__(self, other):
        if isinstance(other, RomanNumeral):
            return self.value < other.value
        raise TypeError("Comparison with incompatible type")

    def __ne__(self, other):
        return not self == other

    def __le__(self, other):
        return self == other or self < other
    
    def __ge__(self, other):
        return self == other or not self < other
    
    def __gt__(self, other):
        return self != other and not self < other
    
    def __repr__(self):
        return f"RomanNumeral({self.value})"
```
{% endcode %}

The class has one class attribute `roman_map`,  a dictionary to map some integers to their roman numeral counterpart, and one instance attribute, an `int` named `value` representing the roman numeral value in the decimal base.&#x20;

On line 7, the dunder method `__init__` initialises an instance with an `int` that is the decimal representation of the roman numeral.

On line 10, the method `to_roman` returns a string representing the decimal value as a roman numeral.&#x20;

Finally to provide an ordering of the roman numeral, we implement the six methods used for comparison. To compare two roman numerals, we compare the `value` attribute of each object, that is the ordering of decimal numbers.

If you look closely, the last four comparison methods use the `__eq__` and `__lt__` in a boolean expression. For example, on line 36, greater or equal operator is expressed as "self is equal to other or self is not less than other".

Having implemented these six dunder methods for comparison, we can use the python’s comparison operator to compare two instances of `RomanNumeral` as demonstrated in the code below.&#x20;

{% code lineNumbers="true" %}
```python
roman1 = RomanNumeral(14)
roman2 = RomanNumeral(8)
print(roman1.to_roman())  # XIV
print(roman2.to_roman())  # VIII
print(roman1 == roman2)   # False
print(roman1 < roman2)    # False
print(roman1 <= roman2)   # False
print(roman1 > roman2)    # True
print(roman1 >= roman2)   # True
```
{% endcode %}

The code is easier to implement and read. The expressiveness of the class is improved.

## Best Practices

Dunder methods should be implemented with care and following some best practices. For example,&#x20;

You should Follow the principle of least astonishment: Dunder methods should behave in a way that is consistent with the built-in types and the Python language semantics. For example, the `__eq__` method should return a boolean value, not raise an exception or modify the object's state.

In addition you should respect the reflexivity, symmetry, and transitivity properties: The equality and inequality comparisons should be:

* reflexive (x == x),&#x20;
* symmetric (x == y implies y == x),&#x20;
* and transitive (x == y and y == z implies x == z).&#x20;

Similarly, the ordering comparisons should be:

* reflexive (x <= x),&#x20;
* antisymmetric (x <= y and y <= x implies x == y),&#x20;
* and transitive (x <= y and y <= z implies x <= z).

If a class defines the `__eq__` method, it should also define the `__ne__` method, to ensure that the inequality comparison works as expected.&#x20;

The simplest way to do this is to use the `@functools.total_ordering` decorator. The `functools.total_ordering` decorator can automatically generate the other rich comparison methods (`__le__`, `__gt__`, `__ge__`) based on a few specified methods (usually `__eq__` and `__lt__`).&#x20;

This reduces boilerplate code as demonstrated on the refactored implementation of our class `RomanNumeral` where only the \_`_eq__` and `__lt__` have been implemented.

{% code lineNumbers="true" %}
```python
from functools import total_ordering

@total_ordering
class RomanNumeral:
    ROMAN_MAP = {1: 'I', 4: 'IV', 5: 'V', 9: 'IX',
            10: 'X', 40: 'XL', 50: 'L', 90: 'XC', 100: 'C',
            400: 'CD', 500: 'D', 900: 'CM',1000: 'M'
        }
    
    def __init__(self, value):
        self.value = value

    def to_roman(self):
        result = ''
        num = self.value
        for val in sorted(self.ROMAN_MAP.keys(), reverse=True):
            while num >= val:
                result += self.ROMAN_MAP[val]
                num -= val
        return result

    def __eq__(self, other):
        if isinstance(other, RomanNumeral):
            return self.value == other.value
        return False

    def __lt__(self, other):
        if isinstance(other, RomanNumeral):
            return self.value < other.value
        raise TypeError("Comparison with incompatible type")
    
    def __repr__(self):
        return f"RomanNumeral({self.value})"
```
{% endcode %}

Nonetheless, the other comparators are still working as shown in the code snippet here.

{% code lineNumbers="true" %}
```python
roman1 = RomanNumeral(14)
roman2 = RomanNumeral(8)
print(roman1.to_roman())  # XIV
print(roman2.to_roman())  # VIII
print(roman1 == roman2)   # False
print(roman1 < roman2)    # False
print(roman1 <= roman2)   # False
print(roman1 > roman2)    # True
print(roman1 >= roman2)   # True
```
{% endcode %}

Finally, use operator overloading sparingly. Dunder methods can be used to overload operators and provide syntactic sugar for common operations. However, this should not be abused or misused, as it can make the code less readable or intuitive. Operator overloading should only be used when it makes sense for the domain or problem at hand, and when it follows the established conventions and expectations of Python programmers.

## Conclusion

Dunder methods form a crucial aspect of Python's object-oriented programming paradigm. These special methods, identified by their names enclosed within double underscores at the beginning and end, provide a mechanism for defining customised behaviour in classes.

Dunder methods are often referred to as magic methods or operator methods due to their automatic invocation by the Python interpreter during specific operations or expressions. By implementing these methods, developers can tailor the behaviour of their classes to seamlessly integrate with built-in functions, operators, and Pythonic conventions.

Dunder methods enable the automatic invocation of specific behaviours, contributing to a more seamless and expressive coding experience.

Programmers can leverage dunder methods to customise how instances of their classes interact with fundamental operations, enhancing code readability and adherence to Pythonic conventions.

A few words of caution though, clear documentation of dunder method implementations is crucial for understanding their purpose and usage. Not all dunder methods need to be implemented in every class. The choice of which dunder methods to implement depends on the specific requirements of the class and its intended use. Overloading too many operators or using dunder methods inappropriately can lead to code that is difficult to maintain and understand which defeats the purpose of such methods. Consistent use of dunder methods contributes to a more predictable and maintainable codebase.

Incorporating dunder methods into your classes empowers you to create more flexible, intuitive, and Pythonic code. By adhering to best practices, documenting your implementation logic, and considering the context of your application, you can make the most of dunder methods to enhance the functionality and readability of your Python programs.
