# More on Tuples

## Tuples as return values

Strictly speaking, a function can only return one value, but if the value is a tuple, the effect is the same as returning multiple values. For example, if you want to divide two integers and compute the quotient and remainder, it is inefficient to compute `x/y` and then `x%y`. It is better to compute them both at the same time.

The built-in function `divmod` takes two arguments and returns a tuple of two values, the quotient and remainder. You can store the result as a tuple:

```bash
>>> t = divmod(7, 3) 
>>> print(t)
 (2, 1)
>>>
```

Or use [tuple assignment](../variables-expressions-and-statements/values-and-types.md#multiple-assignment) to store the elements separately:

```bash
>>> quot, rem = divmod(7, 3)
>>> print(quot)
 2
>>> print(rem)
 1 
>>>
```

Here is an example of a function that returns a tuple:

{% code lineNumbers="true" %}
```python
def min_max(t): 
    return min(t), max(t)
```
{% endcode %}

`max` and `min` are built-in functions that find the largest and smallest elements of a sequence. `min_max` computes both and returns a tuple of two values. Note that in the return statement, the `()` are omitted.

## Lists and tuples

`zip` is a built-in function that takes two or more sequences and "zips"' them into an iterator of tuples (for most purposes, an iterator behaves like a list) where each tuple contains one element from each sequence.

This example zips a string and a list, and build a list using the list constructor `list()`:

```bash
>>> list(zip('abc', [1,2,3]))
 [('a', 0), ('b', 1), ('c', 2)]
>>>
```

The result is a list of tuples where each tuple contains a character from the string and the corresponding element from the list.

{% hint style="info" %}
If the sequences are not the same length, the result has the length of the shorter one.

`>>> list(zip('abc', (1,2,3,4)))`

&#x20; `[('a', 1), ('b', 2), ('c', 3)]`&#x20;

`>>>`
{% endhint %}

You can use tuple assignment in a `for` loop to traverse a list of tuples:

{% code lineNumbers="true" %}
```python
t = [('a', 0), ('b', 1), ('c', 2)] 
for letter, number in t: 
    print(number, letter)
```
{% endcode %}

Each time through the loop, Python selects the next tuple in the list and assigns the first element of the tuple to `letter` and the second to `number`. The output of this loop is:

```bash
0 a 
1 b 
2 c
```

If you combine `zip`, `for` and tuple assignment, you get a useful idiom for traversing two (or more) sequences at the same time. For example, `has_match` takes two sequences, `t1` and `t2`, and returns `True` if there is an index `i` such that `t1[i] == t2[i]`:

{% code lineNumbers="true" %}
```python
def has_match(t1, t2): 
    for x, y in zip(t1, t2): 
        if x == y: 
            return True 
    return False 
```
{% endcode %}

If you need to traverse the elements of a sequence and their indices, you can use the built-in function `enumerate`:

{% code lineNumbers="true" %}
```python
for index, element in enumerate('abc'): 
    print(index, element)
```
{% endcode %}

The output of this loop is:

```
0 a 
1 b 
2 c 
```

## Comparing tuples

The relational operators work with tuples and other sequences; Python starts by comparing the first element from each sequence. If they are equal, it goes on to the next elements, and so on, until it finds elements that differ. Subsequent elements are not considered (even if they are really big).

```bash
>>> (0, 1, 2) < (0, 3, 4) 
 True
>>> (0, 1, 2000000) < (0, 3, 4)
 True
>>>
```

The `sort` function works the same way. It sorts primarily by first element, but in the case of a tie, it sorts by second element, and so on. This feature lends itself to a pattern called `DSU` for:

* **D**ecorate a sequence by building a list of tuples with one or more sort keys preceding the elements from the sequence,
* **S**ort the list of tuples, and
* **U**ndecorate by extracting the sorted elements of the sequence.

For example, suppose you have a list of words and you want to sort them from longest to shortest:

{% code lineNumbers="true" %}
```python
def sort_by_length(words): 
    t = [] 
    for word in words: 
        t.append((len(word), word))
    t.sort(reverse=True)
    res = []
    for length, word in t:
        res.append(word)
    return res
```
{% endcode %}

The first loop builds a list of tuples, where each tuple is a word preceded by its length. `sort` compares the first element, length, first, and only considers the second element to break ties. The keyword argument `reverse=True` tells `sort` to go in decreasing order. The second loop traverses the list of tuples and builds a list of words in descending order of length.

**Exercise:** In this example, words with the same length appear in reverse alphabetical order. Modify this example so that words with the same length appear in random order. \
_Hint:_ see the `random` function in the `random` module.

<details>

<summary>Answer:</summary>

{% code lineNumbers="true" %}
```python
from random import random

def sort_by_length(words): 
    t = [] 
    for word in words: 
        t.append((len(word), random(), word))
    t.sort(reverse=True)
    res = []
    for length, position, word in t:
        res.append(word)
    return res
```
{% endcode %}

First we must import the function `random` from the module `random`. On line 6, we create a triplet with the length of the word, followed by a random number, followed by the word itself. On line 7, the method `sort` sort the triplets by comparing first the length of the words, and if the length are the same, the method break ties by comparing the random numbers generated.

If you run the function `sort_by_length` twice with the same parameter, the output may differ.

```bash
>>> words = ['a', 'to', 'an', 'oh', 'two', 'one', 'and', 'or', 'i']
>>> print(sort_by_length(words))
 ['and', 'two', 'one', 'to', 'oh', 'an', 'or', 'a', 'i']
>>> print(sort_by_length(words))
 ['one', 'and', 'two', 'oh', 'an', 'or', 'to', 'a', 'i']
>>>
```

</details>

## Tuple Comprehension

You can use a similar approach to list comprehension to create tuples.  However, there's a subtle difference: in Python, tuple comprehension is not directly supported like list comprehension. Instead, you can use generator expressions to create tuples and then convert them into tuples using the `tuple()` constructor.

Here's how you can achieve tuple comprehension-like behaviour:

```python
new_tuple = tuple(expression for item in iterable if condition)
```

For example to create a tuple containing the square of even numbers we could write the following code:

```python
# Using a generator expression to create a tuple
numbers = (1, 2, 3, 4, 5)
squares = tuple(x**2 for x in numbers if x % 2 == 0)

# 'squares' will be a tuple: (4, 16)
```

In this example, we use a generator expression inside the `tuple()` constructor to create a new tuple `squares` containing the squares of the even numbers from the original tuple `numbers`. At this stage, you don't need to understand what generator expression are in Python, just use the given expression format.

While tuple comprehension is not a direct syntax like list comprehension, this approach allows you to achieve similar functionality when you want to create tuples by applying an expression to items from an existing iterable. Note that `numbers` could have been a list or another type of iterable (like [set, a data type covered in another chapter](../page-1/sets.md)), it does not need to be a tuple.

## Sequences of sequences

I have focused on lists of tuples, but almost all of the examples in this chapter also work with lists of lists, tuples of tuples, and tuples of lists. To avoid enumerating the possible combinations, it is sometimes easier to talk about sequences of sequences.&#x20;

In many contexts, the different kinds of sequences (strings, lists and tuples) can be used interchangeably. So how and why do you choose one over the others?

To start with the obvious, strings are more limited than other sequences because the elements have to be characters. They are also immutable. If you need the ability to change the characters in a string (as opposed to creating a new string), you might want to use a list of characters instead.

Lists are more common than tuples, mostly because they are mutable. But there are a few cases where you might prefer tuples:

* In some contexts, like a `return` statement, it is syntactically simpler to create a tuple than a list. In other contexts, you might prefer a list.&#x20;
* If you are passing a sequence as an argument to a function, using tuples reduces the potential for unexpected behaviour due to aliasing.

Because tuples are immutable, they don't provide methods like `sort` and `reverse`, which modify existing lists. But Python provides the built-in functions `sorted` and `reversed`, which take any sequence as a parameter and return a new list with the same elements in a different order.
