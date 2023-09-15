# Exercises

## String

### Exercise 1

A string slice can take a third index that specifies the "step size"; that is, the number of spaces between successive characters. A step size of 2 means every other character; 3 means every third, etc.

```bash
>>> fruit = 'banana'
>>> fruit[0:5:2]
 'bnn'
>>>
```

A step size of -1 goes through the word backwards, so the slice `[::-1]` generates a reversed string. Use this idiom to write a one-line version of `is_palindrome` from previous exercise.&#x20;

<details>

<summary>Answer</summary>

{% code lineNumbers="true" %}
```python
def is_palindrome(word):
    return word == word[::-1]
```
{% endcode %}

</details>

### Exercise 2

[ROT13 ](https://www.wikipedia.org/wiki/ROT13)is a weak form of encryption that involves "rotating" each letter in a word by 13 places. To rotate a letter means to shift it through the alphabet, wrapping around to the beginning if necessary, so 'A' shifted by 3 is 'D' and 'Z' shifted by 1 is 'A'.

Write a function called `rotate_word` that takes a string and an integer as parameters, and that returns a new string that contains the letters from the original string "rotated" by the given amount.

For example, `'cheer'` rotated by 7 is `'jolly'` and `'melon'` rotated by -10 is `cubed`.\
You might want to use the `ascii_lowercase` constant from the module `string`.  Look at the documentation for that module.

<details>

<summary>Answer</summary>

{% code lineNumbers="true" %}
```python
def rotate_word(word, shift):
    rotated = ''
    for letter in word.lower():
        index = ascii_lowercase.find(letter)
        index = (index + shift) % len(ascii_lowercase)
        rotated += ascii_lowercase[index]
    return rotated
```
{% endcode %}



</details>

### Exercise 3

Read the documentation of the [string methods](https://www.docs.python.org/lib/string-methods.html) and experiment with some of them to make sure you understand how they work. `strip` and `replace` are particularly useful. The documentation uses a syntax that might be confusing. For example, in `find(sub[, start[, end]])`, the brackets indicate optional arguments. So `sub` is required, but `start` is optional, and if you include `start`, then `end` is optional.&#x20;

{% hint style="info" %}
The ability to read and understand documentation is a key skill. You need to spend time exploring the Python documentation, as well as some useful modules, such as `math` and `random`.
{% endhint %}

### Exercise  4

The following functions are **all** _intended_ to check whether a string contains any lowercase letters, but at least some of them are wrong. For each function, describe what the function actually does (assuming that the parameter is a string). First try to understand what a function does by only reading the code, then devise a series of tests to check if a function is correctly implemented.

{% code lineNumbers="true" %}
```python
def any_lowercase1(s): 
    for c in s: 
        if c.islower(): 
            return True 
        else: 
            return False
            
def any_lowercase2(s): 
    for c in s:  
        if 'c'.islower(): 
            return 'True' 
        else: 
            return 'False'
            
def any_lowercase3(s):
    for c in s: 
        flag = c.islower() 
    return flag
               
def any_lowercase4(s): 
    flag = False 
    for c in s: 
        flag = flag or c.islower() 
    return flag
      
def any_lowercase5(s): 
    for c in s: 
        if not c.islower(): 
            return False 
    return True
```
{% endcode %}

## Lists

### Exercise 5&#x20;

Write a function called `is_sorted` that takes a list as a parameter and returns `True` if the list is sorted in ascending order, `False` otherwise. You can assume (as a precondition) that the elements of the list can be compared with the relational operators `<`, `>`, etc.

For example, `is_sorted([1,2,2])` should return `True` and `is_sorted(['b','a'])` should return `False`.

<details>

<summary>Answer</summary>

{% code lineNumbers="true" %}
```python
def is_sorted(elements):
    for index in range(len(elements) - 1):
        if elements[index] > elements[index+1]:
            return False
    return True
```
{% endcode %}

</details>

### Exercise 6

Two words are anagrams if you can rearrange the letters from one to spell the other. Write a function called `is_anagram` that takes two strings as parameters and returns `True` if they are anagrams. For example, "dusty" and "study" are anagrams. On the other hand, "elbow" and "bellow" are not due to the additional "L" in bellow.

<details>

<summary>Answer</summary>

{% code lineNumbers="true" %}
```python
def is_anagram(word1, word2):
    word1_letters = list(word1)
    word2_letters = list(word2)
    return sorted(word1_letters) == sorted(word2_letters)
```
{% endcode %}

</details>

### Exercise 7

The (so-called) Birthday Paradox:

1. Write a function called `has_duplicates` that takes a list and returns `True` if there is any element that appears more than once. It should not modify the original list.&#x20;
2. If there are 23 students in your class, what are the chances that two of you have the same birthday? You can estimate this probability by generating random samples of 23 birthdays and checking for matches. Hint: you can generate random birthdays with the `randint` function in the `random` module.

You can read about this problem on [wikipedia](https://www.wikipedia.org/wiki/Birthday\_paradox).

<details>

<summary>Answer</summary>



</details>

### Exercise 8

Write a function called `remove_duplicates` that takes a list as parameter and returns a new list with only the unique elements from the original. Hint: they don't have to be in the same order.

<details>

<summary>Answer</summary>

{% code lineNumbers="true" %}
```python
def has_duplicates(elements):
    visited = []
    for elt in elements:
        if elt in visited:
            return True
        else:
            visited.append(elt)
    return False
```
{% endcode %}

An alternative implementation is given below. Is this  implementation correct or not? Try to understand the code and explain your answer.

{% code lineNumbers="true" %}
```python
def has_duplicates2(elements):
    for index in range(len(elements)-1):
        if elements[index] in elements[index+1:]:
            return True
    return False
```
{% endcode %}

</details>

### Exercise 9

Two words are a "reverse pair" if each is the reverse of the other. Write a function `find_reverse_pair(list_of_words)` that finds all the reverse pairs in the list of words passed in the parameter. The method should return a list of pair (tuple of two strings) where each pair contains a word and its reversed.

<details>

<summary>Answer</summary>

{% code lineNumbers="true" %}
```python
def find_reverse_pair(list_of_words):
    pairs = []
    for index in range(len(list_of_words)-1):
        word = list_of_words[index]
        if word[::-1] in list_of_words[index+1:]:
            print((word, word[::-1]))
            pairs.append((word, word[::-1]))

    return pairs
```
{% endcode %}



</details>

### Exercise 10

To check whether a word is in an ordered word list, you could use the `in` operator, but it would be slow because it searches through the words in order.

Because the words are in alphabetical order, we can speed things up with a bisection search (also known as binary search), which is similar to what you do when you look a word up in the dictionary. You start in the middle and check to see whether the word you are looking for comes before the word in the middle of the list. If so, then you search the first half of the list the same way. Otherwise you search the second half.

Either way, you cut the remaining search space in half. If the word list has 113,809 words, it will take about 17 steps to find the word or conclude that it's not there.

Write a function called `bisect` that takes a sorted list of strings and a target value and returns the index of the value in the list, if it's there, or `None` if it's not.

Once you have completed your implementation, have a look at the documentation of the `bisect` module and write an alternative solution using the function from that module.

<details>

<summary>Answer</summary>

{% code lineNumbers="true" %}
```python
def bisect(wordlist, word):
    start = 0
    end = len(wordlist) - 1
    while start <= end:
        middle = (end + start)//2
        if word == wordlist[middle]:
            return middle
        elif word < wordlist[middle]:
            end = middle - 1
        else:
            start = middle + 1
    return -1
```
{% endcode %}

To compute the result we need three variables:

1. `start` that represents the index from where we should start our search initialise to `0` (the beginning of the list),
2. `end` that represents the index from where we should stop our search initialise to `len(wordlist) - 1` (the index of the last element in the list),
3. and `middle`, that represents the middle of the area we need to search.

The search for the word finishes when `start` is strictly greater than `end`, which means that we could not find the element (line 4). Therefore we exit the loop and return `-1` (line 12).&#x20;

The search also finishes when the element in the middle of the section we are currently searching is the same as `word` (line 6). In this case we need to return the `middle` (line 7).

If the search is not finished, we need to determine which segment of the list we need to explore further. If the `word` we are looking for is before the word stored at the `middle` position, then we need to search the word between the indices `start` and `middle-1` (line 8-9). Otherwise, we need to search the word between the indices `middle+1` and  `end` (line 10-11).&#x20;

</details>

### Exercise 11

Two words "interlock" if taking alternating letters from each forms a new word. For example, "shoe" and "cold" interlock to form "schooled".

1. Write a function `interlock(list_of_words)` that finds and returns all pairs of words that interlock from the list passed in the parameter. Note that two words from the list interlock only if the resulting word is in the list itself. For example, if the list contains the words "shoe" and "cold" but not the word "schooled", the two words should not be returned.

<details>

<summary>Answer</summary>



</details>

2. Can you find any words that are three-way interlocked; that is, every third letter forms a word, starting from the first, second or third?

<details>

<summary>Answer</summary>



</details>

{% hint style="info" %}
This exercise is inspired by an example at puzzlers.org.
{% endhint %}

### Exercise 12

Write a function called `most_frequent` that takes a string and prints the letters in decreasing order of frequency. Find text samples from several different languages and see how letter frequency varies between languages. Compare your results with the tables given in the [Wikipedia's letter frequencies page](https://www.wikipedia.org/wiki/Letter\_frequencies).&#x20;

<details>

<summary>Answer</summary>



</details>
