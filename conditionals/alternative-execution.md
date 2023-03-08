# Alternative execution

A second form of the `if` statement is `alternative execution` (also known as `if-else` statement), in which there are two possibilities and the condition determines which one gets executed. The syntax looks like this:

{% code lineNumbers="true" %}
```python
if x % 2 == 0: 
    print('x is even') 
else: 
    print('x is odd') 
```
{% endcode %}

If the remainder when `x` is divided by 2 is 0, then we know that `x` is even, and the program displays a message to that effect. If the condition is false, the second set of statements is executed. Since the condition must be true or false, exactly one of the alternatives will be executed. The alternatives are called **branches**, because they are branches in the flow of execution. This is clearly illustrated in the flow diagram shown below.

<figure><img src="../.gitbook/assets/ifelsestatementdiagram.png" alt="figure representing the conditional if-else statement flow control diagram."><figcaption><p>Conditional <code>if-else</code> statement flow control diagram.</p></figcaption></figure>
