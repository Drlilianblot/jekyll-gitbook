# Iteration

The following code repeats the same task twice:

{% code lineNumbers="true" %}
```python
word = 'Lilian' 
print(word) 
print(word)
```
{% endcode %}

If we wanted to write a script that print the same thing a thousand times, this approach would be impractical. Thankfully we can do the same thing more concisely via **iteration**.

In programming, iteration refers to the process of repeatedly executing a block of code until a certain condition is met. Iteration is often used in loops, which allow you to iterate over a sequence of values or perform a certain operation a specific number of times.

There are two main types of loops in Python: `for` loops and `while` loops.

`for` loops are used to perform a certain operation a specific number of times or to iterate over a sequence of values, such as a list, tuple, or string. The for loop is also referred to as a count-controlled loops.

To print my name a thousand times can be done concisely with a `for` statement as shown below.

{% code lineNumbers="true" %}
```python
word = 'Lilian' 
for i in range(1000): 
    print(word) 
```
{% endcode %}

This is the simplest use of the `for` statement; we will see more later.&#x20;

`while` loops, on the other hand, are used to iterate until a certain condition is met. They are sometimes referred to as condition-controlled loops.

In both cases, iteration allows us to execute a block of code multiple times, which can be useful for performing repetitive tasks or iterating over a sequence of values.
