# Conditional execution

In order to write useful programs, we almost always need the ability to check conditions and change the behaviour of the program accordingly. **Conditional statements** give us this ability. The simplest form is the `if` statement:

{% code lineNumbers="true" %}
```python
if x > 0: 
    print('x is positive') 
```
{% endcode %}

The Boolean expression after the `if` statement is called the **condition**. If it is true, then the indented statement gets executed. If not, nothing happens. This is illustrated in the flow diagram below.

<figure><img src="../.gitbook/assets/ifstatementdiagram.png" alt="figure representing the Conditional if statement control flow diagram."><figcaption><p>Conditional <code>if</code> statement flow control diagram.</p></figcaption></figure>

`if` statements have the same structure as function definitions: a header followed by an indented body. Statements like this are called **compound statements**. There is no limit on the number of statements that can appear in the body, but there has to be at least one. Occasionally, it is useful to have a body with no statements (usually as a place keeper for code you haven't written yet). In that case, you can use the `pass` statement, which does nothing.

{% code lineNumbers="true" %}
```python
if x < 0: 
    pass # need to handle negative values! 
```
{% endcode %}
