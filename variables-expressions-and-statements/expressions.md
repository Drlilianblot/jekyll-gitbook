# Expressions

{% embed url="https://youtu.be/xqfforXbOGI" %}

## Operators and operands

**Operators** are special symbols that represent computations like addition and multiplication. The values the operator is applied to are called **operands**. The operators `+, -,` \*, `/` and `**` perform addition, subtraction, multiplication, division and exponentiation, as in the following examples:

{% code lineNumbers="true" %}
```python
20 + 32 
hour - 1 
hour*60 + minute 
minute/60 
5**2 
(5+9) * (15-7)
```
{% endcode %}

When a variable name appears in the place of an operand, it is replaced with its value before the operation is performed.

Python 3, as well as other languages have an **integer division** `//`. The integer division operates **floor division**, that is the operator returns the whole part of the division. The result of the integer division is an integer. If both operands are integer the value returned is a integer. Otherwise, if at least one of the operand is a float, the value returned is a float.

```python
>>> minute = 59 
>>> minute // 60
0
>>> minute = 61 
>>> minute // 60
1 
>>> minute // 60.0
1.0 
>>> minute / 60.0
1.0166666666666666 
```

## Expressions

An **expression** is a combination of values, variables, and operators. A value all by itself is considered an expression, and so is a variable, so the following are all legal expressions (assuming that the variable `x` has been assigned a value):

{% code lineNumbers="true" %}
```python
17
x 
x + 17
```
{% endcode %}

If you type an expression in interactive mode, the interpreter evaluates it and displays the result:

```python
>>> 1 + 1
2
```

But in a script, an expression all by itself doesn't do anything! This is a common source of confusion for beginners.

<details>

<summary>Exercise</summary>

Type the following statements in the Python interpreter to see what they do:

```
5 
x = 5 
x + 1
```

Now put the same statements into a script and run it. What is the output? Modify the script by transforming each expression into a `print` statement and then run it again.

</details>

You can use a variable in an expression, and you can assign the result of an expression to a variable. In addition, a variable can be used on both side of the assignment operator `=` like in `x = x + 1`. In this assignment statement the result of `x + 1` is assigned to `x`. For example, if `x` has the value `1` before the assignment statement is executed, then `x` becomes `2` after the statement is executed.

:information\_source:In mathematics, $$x = 2 * x + 1$$ denotes an equation (where $$x = -1$$ is the solution). In python, it is an assignment statement, and if `x` has the value `1` before the statement, executing the statement would change `x` to `3`.

## Order of operations

When more than one operator appears in an expression, the order of evaluation depends on the **rules of precedence**. For mathematical operators, Python follows mathematical convention. The acronym **PEMDAS** is a useful way to remember the rules:

1. **P**arentheses have the highest precedence and can be used to force an expression to evaluate in the order you want. Since expressions in parentheses are evaluated first, `2 * (3-1)` is 4, and `(1+1)**(5-2)` is 8. You can also use parentheses to make an expression easier to read, as in `(minute * 100) / 60`, even if it doesn't change the result.
2. **E**xponentiation has the next highest precedence, so `2**1+1` is 3, not 4, and `3*1**3` is 3, not 27.
3. **M**ultiplication and **D**ivision have the same precedence, which is higher than **A**ddition and **S**ubtraction, which also have the same precedence. So `2*3-1` is 5, not 4, and `6+4/2` is 8, not 5.
4. Operators with the same precedence are evaluated from left to right. So in the expression `degrees/2*pi`_,_ the division happens first and the result is multiplied by `pi`, therefore the expression is equal to $$\frac{\pi}{2}degrees$$. To divide by $$2\pi$$, you can use parentheses (e.g. `degrees/(2*pi)` or write `degrees/2/pi`.

| Operator                           | Description                                                        |
| ---------------------------------- | ------------------------------------------------------------------ |
| \*\*                               | Exponentiation (raise to the power)                                |
| +, -                               | Unary plus and minus (method names for the last two are +@ and -@) |
| \*, /, %, //                       | Multiply, divide, modulo and floor division                        |
| +, -                               | Addition and subtraction                                           |
| >>, <<                             | Right and left bitwise shift                                       |
| <=, <, >, >=                       | Comparison operators                                               |
| ==, !=                             | Equality operators                                                 |
| `is`, `is not`                     | Identity operators                                                 |
| `in`, `not in`                     | Membership operators                                               |
| not                                | Logical operator                                                   |
| and                                | Logical operator                                                   |
| or                                 | Logical operator                                                   |
| = ,%=, /=, //=, -=, +=, \*=, \*\*= | Assignment operators                                               |

## Modulus operator

The **modulus operator** works on integers and yields the remainder when the first operand is divided by the second. In Python, the modulus operator is a percent sign (`%`). The syntax is the same as for other operators:

```bash
>>> quotient = 7 // 3 
>>> print(quotient)
 2 
>>> remainder = 7 % 3 
>>> print(remainder) 
 1 
```

So 7 divided by 3 is 2 with 1 left over, or in other words $$7=3\times 2 + 1$$.

The modulus operator turns out to be surprisingly useful. For example, you can check whether one number is divisible by another - if `x % y` is zero, then `x` is divisible by `y`. Also, you can extract the right-most digit or digits from a number. For example, `x % 10` yields the right-most digit of `x` (in base 10). Similarly `x % 100` yields the last two digits.

{% hint style="info" %}
The modulus operator is very useful in determining if a integer `x` is an even number or an odd number. If `x%2` is equal to `0` then `x` is an even number, odd otherwise.
{% endhint %}

## String operations

In general, you cannot perform mathematical operations on strings, even if the strings look like numbers, so the following are illegal:

{% code lineNumbers="true" %}
```python
'2'-'1' 
'eggs'/'easy' 
'third'*'a charm'
```
{% endcode %}

The `+` operator works with strings, but it might not do what you expect: it performs **concatenation**, which means joining the strings by linking them end-to-end. For example:

```python
first = 'throat' 
second = 'warbler' 
print(first + second) 
```

The output of this program is `throatwarbler`.

The `*` operator also works on strings; it performs repetition. For example, `'Spam'*3` is `'SpamSpamSpam'`. If one of the operands is a string, the other has to be an integer. This use of `+` and `*` \_\_ makes sense by analogy with addition and multiplication. Just as `4*3`} is equivalent to `4+4+4`, we expect `'Spam'*3` to be the same as `'Spam'+'Spam'+'Spam'`, and it is.

On the other hand, there is a significant way in which string concatenation is different from integer addition. Concatenation is not commutative, which means that `'spam'+'sandwich'` is not the same as `'sandwich'+'spam'`, whereas `3+4` is the same as `4+3`.
