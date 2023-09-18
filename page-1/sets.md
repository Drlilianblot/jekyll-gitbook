# Sets

{% embed url="https://youtu.be/MCwtsnKRuxY?si=rme43wqa8WqyAk1V" %}

In Python, a set is an unordered collection of unique elements. It is similar to a list or a tuple but with a few differences. One of the most important differences is that a set only contains unique elements, meaning that no duplicates are allowed. Another important difference is that sets are mutable, which means that you can add or remove elements from them. Sets are very useful when it comes to solving problems that involve finding unique elements, such as removing duplicates or determining the intersection of two lists.

## Creating a Set in Python

To create a set in Python, you can use either curly braces or the built-in `set()` function. For example:

{% code lineNumbers="true" %}
```python
# Using curly braces
my_set = {1, 2, 3, 4, 5}

# Using the set() function
my_set = set([1, 2, 3, 4, 5])
```
{% endcode %}

In both cases, we create a set that contains the numbers 1 through 5.

## Adding and Removing Elements from a Set

One of the main benefits of using a set is the ability to easily add and remove elements from it. To add an element to a set, you can use the `add()` method. For example:

```bash
>>> my_set = {1, 2, 3}
>>> my_set.add(4)
>>> print(my_set) 
 {1, 2, 3, 4}
>>>
```

To remove an element from a set, you can use the `remove()` method. For example:

```bash
>>> my_set = {1, 2, 3}
>>> my_set.remove(3)
>>> print(my_set) 
 {1, 2}
>>>
```

You can also use the `discard()` method to remove an element from a set, but it won't raise an error if the element is not found in the set. For example:

```bash
>>> my_set = {1, 2, 3}
>>> my_set.discard(3)
>>> my_set.discard(4)
>>> print(my_set) 
 {1, 2}
>>>
```

## Basic Set Operations

In addition to adding and removing elements from a set, there are several other useful set operations. Here are a few examples:

* Union: The union of two sets is a new set that contains all the elements from both sets, with no duplicates.

```bash
>>> set1 = {1, 2, 3}
>>> set2 = {3, 4, 5}
>>> union_set = set1.union(set2)
>>> print(union_set) 
 {1, 2, 3, 4, 5}
>>>
```

* Intersection: The intersection of two sets is a new set that contains only the elements that are common to both sets.

```bash
>>> set1 = {1, 2, 3}
>>> set2 = {3, 4, 5}
>>> intersection_set = set1.intersection(set2)
>>> print(intersection_set) 
 {3}
>>> 
```

* Difference: The difference of two sets is a new set that contains only the elements that are in one set but not the other.

```bash
>>> set1 = {1, 2, 3}
>>> set2 = {3, 4, 5}
>>> difference_set = set1.difference(set2)
>>> print(difference_set) 
 {1, 2}
>>> 
```

* Symmetric Difference: The symmetric difference of two sets is a new set that contains only the elements that are in one set or the other, but not both.

```bash
>>>  set1 = {1, 2, 3}
>>> set2 = {3, 4, 5}
>>> symmetric_difference_set = set1.symmetric_difference(set2)
>>> print(symmetric_difference_set) 
 {1, 2, 4, 5} 
>>> 
```

Sets can also be used to remove duplicates from a list. Here is an example:

```scss
>>> my_list = [1, 2, 3, 2, 1, 4, 5, 4]
>>> my_set = set(my_list)
>>> my_list = list(my_set)
>>> print(my_list)
 [1, 2, 3, 4, 5]
>>> 
```

## Iterating through a `set`

You can iterate through a set using a `for` loop in Python. Here's an example:

{% code lineNumbers="true" %}
```python
my_set = {1, 2, 3, 4, 5}

for item in my_set:
    print(item)
```
{% endcode %}

In this example, the `for` loop iterates through each item in the `my_set` set, and prints each item to the console. The order in which the items are printed may not be in the same order as they were added to the set, as sets are unordered data structures.

## **Set Comprehension**

Set comprehension in Python shares similarities with [list comprehension](../a-deeper-dive-into-strings-lists-and-tuples/more-on-lists.md#list-comprehension-in-python) but has distinct characteristics that make it a valuable tool in certain situations.

### **Similarities:**

1. **Comprehension Syntax:** Both list and set comprehensions use a similar comprehension syntax, where you define an expression to generate new values based on items from an iterable.
   * List Comprehension: `[expression for item in iterable if condition]`
   * Set Comprehension: `{expression for item in iterable if condition}`
2. **Iteration:** Both comprehensions iterate over an iterable (e.g., a list, range, or another iterable) and apply an expression to each item to generate new values.

### **Differences:**

1. **Uniqueness:**
   * List Comprehension: Retains all values from the iterable, including duplicates.
   * Set Comprehension: Automatically removes duplicates, preserving only unique values.
2. **Order:**
   * List Comprehension: Maintains the order of items from the original iterable.
   * Set Comprehension: Does not guarantee a specific order; the result may be unordered.

### An Example

Here's a brief example illustrating the differences:

```python
# List Comprehension
numbers = [1, 2, 2, 3, 4, 4, 5]
squared_list = [x**2 for x in numbers]
# squared_list is a list: [1, 4, 4, 9, 16, 16, 25]

# Set Comprehension
unique_squares = {x**2 for x in numbers}
# unique_squares is a set: {1, 4, 9, 16, 25}
```

In this example, list comprehension produces a list `squared_list` that retains duplicate values, while set comprehension generates a set `unique_squares` that automatically removes duplicates, resulting in a set of unique squared values.

Set comprehensions are particularly useful when you want to extract unique elements from an iterable, as they simplify the process of deduplication. However, if you need to maintain the order of items or keep duplicates, list comprehensions are more appropriate. Understanding the similarities and differences between these comprehensions helps you choose the right tool for your specific data manipulation needs.
