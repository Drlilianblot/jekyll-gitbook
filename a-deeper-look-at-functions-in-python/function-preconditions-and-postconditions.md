# Function Preconditions and Postconditions

In software engineering, a **precondition** is a condition that must be true before a function can be called safely and correctly. A **postcondition** is a condition that is guaranteed to be true after a function has finished executing if the preconditions have been satisfied.

> **Postconditions are only guaranteed if the preconditions are satisfied**

Preconditions and postconditions can be used to help ensure the correctness of a program. By specifying the preconditions and postconditions for each function, we can help to ensure that the function is only called in the correct way and that it always produces the correct results.

In Python, preconditions and postconditions can be specified using assertions. An assertion is a statement that checks a condition and raises an error if the condition is not met.

Here is an example of a function with a precondition and postcondition:

{% code lineNumbers="true" %}
```python
def factorial(n):
  """
  Calculates the factorial of n.

  Precondition: n >= 0

  Postcondition:
    - The return value is the factorial of n.
    - The function does not modify n.
  """

  if n < 0:
    raise ValueError('n must be non-negative')

  output = 1
  for i in range(2, n+1):
    output *= i
  return output
```
{% endcode %}

The precondition for the `factorial()` function is that `n` must be non-negative. This means that the function will only work correctly if the value of `n` is greater than or equal to 0. The postcondition for the `factorial()` function states that the return value is the factorial of `n` and that the function does not modify `n`.

The `factorial()` function uses assertions to check the precondition. If the precondition is not met, the `raise` statement will cause an error to be raised.&#x20;

Preconditions and postconditions can be specified in any programming language that supports assertions. In Python, assertions can be specified using the `assert` keyword.

{% code lineNumbers="true" %}
```python
assert precondition, "Error: precondition not met"
assert postcondition, "Error: postcondition not met"
```
{% endcode %}

Preconditions and postconditions are an important part of software engineering. They can be used to improve the quality of software by ensuring the correctness of a program. By specifying the preconditions and postconditions for each function, we can help to ensure that the function is only called in the correct way and that it always produces the correct results. In addition, They can also be used to write unit tests for functions, which can help to catch bugs and errors early in the development process. Unit tests is an essential tool in the software engineers arsenal to write robust programs, and it will be covered later in the book.
