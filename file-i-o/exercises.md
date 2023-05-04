# Exercises

## **Exercise 1:**

&#x20;Write a program that reads `words.txt` and prints only the words with more than 20 characters (not counting whitespace).

## **Exercise 2:**

<mark style="background-color:red;">Modify the exercises below so they read/write on files. Create an exericse that replace forbidden letters with an underscore.</mark>

Write a function named  `avoids` that takes a word and a string of forbidden letters, and that returns `True` if the word doesn't use any of the forbidden letters.

Modify your program to prompt the user to enter a string of forbidden letters and then print the number of words from the file `words.txt` that don't contain any of them. Can you find a combination of 5 forbidden letters that excludes the smallest number of words?

## **Exercise 3: G**adsby&#x20;

In 1939 Ernest Vincent Wright published a 50,000 word novel called "Gadsby" that does not contain the letter **e**.' Since **e**' is the most common letter in English, that's not easy to do.

Write a function called `has_no_e(word)` that returns `True` if the given word doesn't have the letter **e** in it.

Modify your program from the previous section to print only the words that have no **e** and compute the percentage of the words in the list that have no e.

## **Exercise 4:**

Write a function named `uses_only` that takes a word and a string of letters, and that returns `True` if the word contains only letters in the list. Can you make a sentence using only the letters `acefhlo`? Other than "Hoe alfalfa"?

## **Exercise 5:**

Write a function named `uses_all` that takes a word and a string of required letters, and that returns `True` if the word uses all the required letters at least once. How many words are there that use all the vowels "aeiou"}? How about  "aeiouy"}?&#x20;

## **Exercise 6:** abecedarian

Write a function called `is_abecedarian` that returns `True` if the letters in a word appear in alphabetical order (double letters are ok).\
How many abecedarian words are there?&#x20;
