# Exercises

A great resource to download text files is the [Project Gutenberg](https://www.gutenberg.org/). Project Gutenberg is a library of over 70,000 free eBooks, mostly older works for which U.S. copyright has expired. You can download them (including as text files) or read them online.&#x20;

Here is a small extract from the book "Photographic investigations of faint nebulae" by Edwin Hubble (1920). The [complete text](https://www.gutenberg.org/cache/epub/71654/pg71654.txt) is also available on the Project Gutenberg site.

{% file src="../.gitbook/assets/bookSampleHubble.txt" %}

## **Exercise 1:**

&#x20;Write a function that reads `bookSampleHubble.txt` and prints only the words with more than 10 characters (not counting whitespace).&#x20;



<details>

<summary>Answer</summary>

In order to extract the words from a text easily, i have implemented a method called `remove_nonalphanum(filename)` that reads a text files and replaces punctuation with a blank space. Again, I cannot emphasise enough how important it is to use convenience function to make your code easier to read.

Once the function has been implemented, the solution to the problem is straightforward. I have been using `set` comprehension and the join method from the str type to make the code clearer and more concise. Note that I could have used a list instead of a set. If you are still unfamiliar with these concepts, I recommend that you read the chapters on [list](../a-deeper-dive-into-strings-lists-and-tuples/more-on-lists.md) and [sets](../page-1/sets.md).&#x20;

```python
def remove_nonalphanum(filename):
    def remove_characters(text):
        output = ''
        for character in text:
            if character.isalnum() or character in ('\n', '\t', '\r', ' '):
                output += character
            else:
                output += ' '
        return output
    
    with open(filename, 'r') as file_input:
        text = ''
        for line in file_input:
            text += remove_characters(line)
        return text

def print_long_words(filename):
    text = remove_nonalphanum(filename)
    words = {w.strip() for w in text.split() if len(w) >= 10}
    print('\n'.join(words))
```

</details>

## **Exercise 2:**

In 1939 Ernest Vincent Wright published a 50,000 word novel called "[Gadsby](https://www.gutenberg.org/cache/epub/47342/pg47342.txt)" that does not contain the letter **e**.' Since **e**' is the most common letter in English, that's not easy to do.

Write a function called `has_no_e(filename)` that returns `True` if the given text file doesn't have the letter **e** in it.

Write a function `no_e_percentage(filename)` that computes the percentage of the words in the file that have no **e**.

## **Exercise 3: G**adsby&#x20;

Write a function named  `avoids(filename, forbidden)` that takes a text file's name and a string of forbidden letters, and that returns the `set` of words that don't use any of the forbidden letters.

Modify your program to find a combination of 5 forbidden letters that excludes the smallest number of words.

## **Exercise 4:**

Write a function named `redact_uses_only(inputfile, outputfile, letters)` that takes a text file `inputfile` as input, read the file and redact out all the words in the text file that is not only composed of characters from the string `letters`, and write the redacted text into the `outputfile`. For example, if `letters == 'ehlo'` the text `'Hello, I am in hell'` should be redacted to `'Hello, _ __ __ hell'`.&#x20;
