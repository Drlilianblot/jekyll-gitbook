# Boolean expressions

{% embed url="https://youtu.be/H6DcSVN6xLk" %}

## The `bool` type

A **boolean expression** is an expression that is either true or false. The following examples use the operator `==`, which compares two operands and produces `True` if they are equal and `False` otherwise:

```bash
>>> 5 == 5
 True 
>>> 5 == 6 
 False 
```

`True` and `False` are special values that belong to the type `bool`; they are not strings:

```bash
>>> type(True)
 <type 'bool'> 
>>> type(False)a <type 'bool'> 
```

## Relational Operators

The `==` operator is one of the **relational operators**; the others are:

{% code lineNumbers="true" %}
```python
x != y # x is not equal to y 
x > y # x is greater than y 
x < y # x is less than y 
x >= y # x is greater than or equal to y 
x <= y # x is less than or equal to y 
```
{% endcode %}

Although these operations are probably familiar to you, the Python symbols are different from the mathematical symbols. A common error is to use a single equal sign (`=`) instead of a double equal sign (`==`). Remember that `=` is an assignment operator and `==` is a relational operator. There is no such thing as `=<` or `=>`.

## Logical operators

There are three **logical operators**: `and`, `or`, and `not`. The semantics (meaning) of these operators is similar to their meaning in English. If you are not familiar with the logical operators, their **truth table** are given in <mark style="background-color:red;">\prettyref{tab:truth\_table}</mark>. The tables read as follow, the operands value are given in the first row and first column. The operator is given in the first cell (top-left) of the table. Looking at the `and` operator, the result of the expression `True and True` is `True`, whereas the result of the expression `True and False` is `False`.

| and   | True  | False |
| ----- | ----- | ----- |
| True  | True  | False |
| False | False | False |

| or    | True | False |
| ----- | ---- | ----- |
| True  | True | True  |
| False | True | False |

| not | True  | False |
| --- | ----- | ----- |
|     | False | True  |

For example, `x > 0 and x < 10` is `True` only if `x` is greater than `0` _and_ less than 10. Another example, `n%2 == 0 or n%3 == 0` is true if _either_ of the conditions is true, that is, if the number is divisible by 2 _or_ 3. Finally, the `not` operator negates a boolean expression, so `not (x > y)` is `True` if `x > y` is false, that is, if `x` is less than or equal to `y`.

{% hint style="info" %}
Strictly speaking, the operands of the logical operators should be Boolean expressions, but Python is not very strict. Any nonzero number is interpreted as `True`, whereas as `0` is interpreted as `False`.\
For example `17 and True` evaluates to True .

This flexibility can be useful, but there are some subtleties to it that might be confusing. You might want to (shall I say MUST) avoid it, even if you know what you are doing. Another developer maintaining your code may not be familiar with the subtleties.
{% endhint %}
