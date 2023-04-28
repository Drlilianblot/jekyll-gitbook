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

A step size of -1 goes through the word backwards, so the slice `[::-1]` generates a reversed string. Use this idiom to write a one-line version of `is_palindrome`from <mark style="background-color:red;">\prettyref{exo:palindrome}</mark>.&#x20;

<details>

<summary>Answer</summary>



</details>

### Exercise 2

[ROT13 ](https://www.wikipedia.org/wiki/ROT13)is a weak form of encryption that involves "rotating" each letter in a word by 13 places. To rotate a letter means to shift it through the alphabet, wrapping around to the beginning if necessary, so 'A' shifted by 3 is 'D' and 'Z' shifted by 1 is 'A'.

Write a function called `rotate_word` that takes a string and an integer as parameters, and that returns a new string that contains the letters from the original string "rotated" by the given amount.

For example, `'cheer'` rotated by 7 is `'jolly'` and `'melon'` rotated by -10 is `cubed`.\
You might want to use the built-in functions `ord`, which converts a character to a numeric code, and `chr`, which converts numeric codes to characters.&#x20;

<details>

<summary>Answer</summary>



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
    return flag}
    
    
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



</details>

### Exercise 6

Two words are anagrams if you can rearrange the letters from one to spell the other. Write a function called `is_anagram` that takes two strings as parameters and returns `True` if they are anagrams. For example, "dusty" and "study" are anagrams. On the other hand, "elbow" and "bellow" are not due to the additional "L" in bellow.

<details>

<summary>Answer</summary>



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



</details>

### Exercise 9

Two words are a "reverse pair" if each is the reverse of the other. Write a function `findReversePair(listOfWords)` that finds all the reverse pairs in the list of words passed in the parameter. The method should return a list of pair (tuple of two strings) where each pair contains a word and its reversed.

<details>

<summary>Answer</summary>



</details>

### Exercise 10

To check whether a word is in an ordered word list, you could use the `in` operator, but it would be slow because it searches through the words in order.

Because the words are in alphabetical order, we can speed things up with a bisection search (also known as binary search), which is similar to what you do when you look a word up in the dictionary. You start in the middle and check to see whether the word you are looking for comes before the word in the middle of the list. If so, then you search the first half of the list the same way. Otherwise you search the second half.

Either way, you cut the remaining search space in half. If the word list has 113,809 words, it will take about 17 steps to find the word or conclude that it's not there.

Write a function called `bisect` that takes a sorted list of strings and a target value and returns the index of the value in the list, if it's there, or `None` if it's not.

Once you have completed your implementation, have a look at the documentation of the `bisect` module and write an alternative solution using the function from that module.

<details>

<summary>Answer</summary>



</details>

### Exercise 11

Two words "interlock" if taking alternating letters from each forms a new word. For example, "shoe" and "cold" interlock to form "schooled".

1. Write a function `interlock(listOfWords)` that finds and returns all pairs of words that interlock from the list passed in the parameter. Hint: don't enumerate all pairs!
2. Modify your implementation so that two words from the list interlock only if the resulting word is in the list itself. For example, if the list contains the words "shoe" and "cold" but not the word "schooled", the two words should not be returned.
3. Can you find any words that are three-way interlocked; that is, every third letter forms a word, starting from the first, second or third?

{% hint style="info" %}
This exercise is inspired by an example at puzzlers.org.
{% endhint %}

<details>

<summary>Answer</summary>



</details>

### Exercise 12

Write a function called `most_frequent` that takes a string and prints the letters in decreasing order of frequency. Find text samples from several different languages and see how letter frequency varies between languages. Compare your results with the tables given in the [Wikipedia's letter frequencies page](https://www.wikipedia.org/wiki/Letter\_frequencies).&#x20;

<details>

<summary>Answer</summary>



</details>
