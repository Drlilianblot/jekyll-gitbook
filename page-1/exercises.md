# Exercises

## Exercise 1

If you did <mark style="background-color:red;">\prettyref{exo:duplicate}</mark>, you already have a function named `has_duplicates` that takes a list as a parameter and returns `True` if there is any object that appears more than once in the list.

Use a dictionary to write a faster, simpler version of `has_duplicates`.

<details>

<summary>Answer</summary>



</details>

## Exercise 2: rotate-pairs

Two words are "rotate pairs" if you can rotate one of them and get the other (see `rotate_word` in <mark style="background-color:red;">\prettyref{exo:rotate}</mark>). Write a program that reads a wordlist and finds all the rotate pairs.&#x20;

<details>

<summary>Answer</summary>



</details>

## Exercise 3

Here's another Puzzler from [Car Talk](https://www.cartalk.com/puzzler/browse):

> This was sent in by a fellow named Dan O'Leary. He came upon a common one-syllable, five-letter word recently that has the following unique property. When you remove the first letter, the remaining letters form a homophone of the original word, that is a word that sounds exactly the same. Replace the first letter, that is, put it back and remove the second letter and the result is yet another homophone of the original word. And the question is, what's the word?
>
> Now I'm going to give you an example that doesn't work. Let's look at the five-letter word, "wrack". W-R-A-C-K, you know like "to wrack with pain". If I remove the first letter, I am left with a four-letter word, R-A-C-K. It's a perfect homophone. If you put the `w` back, and remove the `r`, instead, you're left with the word, "wack", which is a real word, it's just not a homophone of the other two words.
>
> But there is, however, at least one word that Dan and we know of, which will yield two homophones if you remove either of the first two letters to make two, new four-letter words. The question is, what's the word?

You can use the dictionary from <mark style="background-color:red;">\prettyref{exo:wordlist2}</mark> to check whether a string is in the word list. To check whether two words are homophones, you can download the[ CMU Pronouncing Dictionary](https://www.speech.cs.cmu.edu/cgi-bin/cmudict).

Write a program that lists all the words that solve the Puzzler.&#x20;

<details>

<summary>Answer</summary>



</details>
