# Simple repetition

The following code repeats the same task twice:

{% code lineNumbers="true" %}
```python
word = 'Lilian' 
print(word) 
print(word)
```
{% endcode %}

If we wanted to write a script that print the same thing a thousand times, this approach would be impractical. Thankfully we can do the same thing more concisely with a `for` statement as shown below.

{% code lineNumbers="true" %}
```python
word = 'Lilian' 
for i in range(1000): 
    print(word) 
```
{% endcode %}

This is the simplest use of the `for` statement; we will see more later. The syntax of a `for` statement is similar to a function definition. It has a header that ends with a colon and an indented body. The body can contain any number of statements. A `for` statement is sometimes called a **loop** because the flow of execution runs through the body and then loops back to the top. In this case, it runs the body of the loop a thousand times.
