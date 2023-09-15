# Exercises

### Exercise 1:

Write a function called `mul_time` that takes a Time object and a number and returns a new `Time` object that contains the product of the original `Time` and the number.

Then use `mul_time` to write a function that takes a `Time` object that represents the finishing time in a race, and a number that represents the distance, and returns a `Time` object that represents the average pace (time per mile).

<details>

<summary>Answer</summary>



</details>

### Exercise 2:

Write a class definition for a `Date` object that has attributes `day`, `month` and `year`. Write a function called `increment_date` that takes a `Date` object, `date` and an integer, `n`, and returns a new `Date` object that represents the day `n` days after `date`.

{% hint style="info" %}
"Thirty days hath September..." Challenge: does your function deal with [leap years](https://www.wikipedia.org/wiki/Leap\_year) correctly?
{% endhint %}

<details>

<summary>Answer</summary>



</details>

### Exercise 3:

The `datetime` module provides `date` and `time` objects that are similar to the `Date` and `Time` objects in this chapter, but they provide a rich set of methods and operators. Read the [documentation of both objects](https://www.docs.python.org/lib/datetime-date.html).&#x20;

* Use the `datetime` module to write a program that gets the current date and prints the day of the week.
* Write a program that takes a birthday as input and prints the user's age and the number of days, hours, minutes and seconds until their next birthday.&#x20;

<details>

<summary>Answer</summary>



</details>

### **Exercise 4:**

This exercise is a cautionary tale about one of the most common, and difficult to find, errors in Python.

*   Write a definition for a class named `Kangaroo` with the following methods:

    * An `__init__` method that initialises an attribute named `pouch_contents` to an empty list.
    * A method named `put_in_pouch` that takes an object of any type and adds it to `pouch_contents`.
    * A `__str__` method that returns a string representation of the `Kangaroo` object and the contents of the pouch.

    Test your code by creating two `Kangaroo` objects, assigning them to variables named `kanga`} and `roo`, and then adding `roo` to the contents of `kanga`'s pouch.
* Download [BadKangaroo.py](https://greenteapress.com/thinkpython/code/BadKangaroo.py). It contains a solution to the previous problem with one big, nasty bug. Find and fix the bug.

If you get stuck, you can download [GoodKangaroo.py](https://greenteapress.com/thinkpython/code/GoodKangaroo.py), which explains the problem and demonstrates a solution.
