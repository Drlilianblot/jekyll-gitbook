# Which data structure should I use?

In Python 3, lists, tuples, sets and dictionaries are all built-in collections. They differ in their properties and use cases.

* **List**: A list is an ordered collection of elements that can contain duplicate values. It is mutable which means you can change its content.
* **Tuple**: A tuple is similar to a list but it is immutable which means you cannot change its content once created [1](https://dev.to/arvindmehairjan/what-are-the-differences-between-a-list-tuple-dictionary-set-in-python-2lm6).
* **Set**: A set is an unordered collection of unique elements [1](https://dev.to/arvindmehairjan/what-are-the-differences-between-a-list-tuple-dictionary-set-in-python-2lm6).
* **Dictionary**: A dictionary stores key-value pairs. [It is an insertion ordered collection since Python 3.7 ](https://www.scaler.com/topics/python/difference-between-dictionary-list-tuple-and-set-in-python/)[2](https://www.scaler.com/topics/python/difference-between-dictionary-list-tuple-and-set-in-python/).

In Python, an **ordered** collection means that the elements in the collection have a specific order that is determined by their position in the collection. The order of elements is preserved when you add or remove elements from the collection. For example, a list is an ordered collection. If you create a list with the elements `['apple', 'banana', 'cherry']`, the element `'apple'` will always be before `'banana'`, and `'banana'` will always be before `'cherry'` . In other word the data structure retains the order in which the data was added.

On the other hand, a set is an **unordered** collection. If you create a set with the same elements as above (`{'apple', 'banana', 'cherry'}`), there is no guarantee about the order of elements when you iterate over them. The order in which they are added may not be retained by the data structure.

<table><thead><tr><th>Collection</th><th width="122">Mutable</th><th>Ordered</th><th>Indexing</th><th>Duplicate Data</th></tr></thead><tbody><tr><td>List</td><td>✔</td><td>✔</td><td>✔</td><td>✔</td></tr><tr><td>Tuple</td><td>𐄂</td><td>✔</td><td>✔</td><td>✔</td></tr><tr><td>Set</td><td>✔</td><td>𐄂</td><td>𐄂</td><td>𐄂</td></tr><tr><td>Dictionary</td><td>✔</td><td>✔</td><td>✔</td><td>𐄂</td></tr></tbody></table>

The choice of which collection to use depends on the specific use case and requirements.

* **List**: Use a list when you need an ordered collection of elements that can contain duplicates. Lists are useful for storing and retrieving elements based on their position in the collection .
* **Tuple**: Use a tuple when you have an ordered collection of elements that should not be changed. Tuples are often used to represent a single record or data structure with multiple fields .
* **Set**: Use a set when you need to store unique elements and perform set operations such as union, intersection and difference .
* **Dictionary**: Use a dictionary when you need to store key-value pairs and retrieve values based on their keys. Dictionaries are useful for representing mappings from one set of values to another .

Here are some steps you can follow to determine which collection to use:

1. **Identify the requirements**: Determine what kind of data you need to store and how you will be using it. Do you need to store ordered data? Do you need to store unique elements? Do you need to store key-value pairs?
2. **Evaluate the properties of each collection**: Consider the properties of each collection and how they align with your requirements. For example, if you need to store ordered data that can contain duplicates, a list might be a good choice.
3. **Consider performance**: Different collections have different performance characteristics for common operations such as adding, removing and accessing elements. Choose a collection that provides good performance for the operations you will be performing most frequently.
