# Exercises

## Exercise 1

If you did the exercise `duplicate` you already have a function named `has_duplicates` that takes a list as a parameter and returns `True` if there is any object that appears more than once in the list.

Use a set to write a faster, simpler version of `has_duplicates`.

<details>

<summary>Answer</summary>

Checking the membership of an element in a set (line 4) is very fast (constant time) compared to checking the membership in a list (linear time). This is why this implementation should be preferred to the one given in a [previous exercise](../a-deeper-dive-into-strings-lists-and-tuples/exercises.md#exercise-7).

{% code lineNumbers="true" %}
```python
def has_duplicates(elements):
    visited = set()
    for i in range(len(elements)):
        if elements[i] in visited:
            return True
        else:
            visited.add(elements[i])
    return False

```
{% endcode %}

</details>

## Exercise 2: rotate-pairs

Two words are "rotate pairs" if you can rotate one of them and get the other (see [`rotate_word`](../a-deeper-dive-into-strings-lists-and-tuples/exercises.md#exercise-2)). Write a program that reads a wordlist and finds all the rotate pairs.&#x20;

<details>

<summary>Answer</summary>

For convenience, we provide the implementation of `rotate_word`, that rotates a word by a given shift.

{% code lineNumbers="true" %}
```python
from string import ascii_lowercase

def rotate_word(word, shift):
    rotated = ''
    for letter in word.lower():
        index = ascii_lowercase.find(letter)
        index = (index + shift) % len(ascii_lowercase)
        rotated += ascii_lowercase[index]
    return rotated

def find_rotate_pairs(words_list):
    words_set = {word.strip().lower() for word in words_list}
    rotate_pairs = []
    for word in words_set:
        for shift in range(1, len(ascii_lowercase)):
            rotated = rotate_word(word, shift)
            if rotated in words_set:
                rotate_pairs.append((word, rotated, shift))
    return rotate_pairs

```
{% endcode %}

Although there is an overhead for transforming the list of words into a set (line 10), for large list it improve considerably the performance when checking the membership of the rotated word (line18).

</details>
