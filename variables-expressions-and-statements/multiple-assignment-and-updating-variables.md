# Multiple assignment & Updating variables

## Multiple assignment

As you may have discovered, it is legal to make more than one assignment to the same variable. A new assignment makes an existing variable refer to a new value (and stop referring to the old value).

{% code lineNumbers="true" %}
```python
bruce = 5 
print(bruce) 
bruce = 7 
print(bruce)
```
{% endcode %}

&#x20;The output of this program is: &#x20;

```
5 
7 
```

Because the first time `bruce` is printed, its value is 5, and the second time, its value is 7. Here is what **multiple assignment** looks like in a state diagram:

<mark style="background-color:blue;">\beforefig \centerline{\includegraphics{figs/assign2.eps\}} \afterfig</mark>

With multiple assignment it is especially important to distinguish between an assignment operation and a statement of equality. Because Python uses the equal sign (`=`) for assignment, it is tempting to interpret a statement like `a = b` as a statement of equality. **It is not!**

First, equality is a symmetric relation and assignment is not. For example, in mathematics, if $$a = 7$$ then $$7 = a$$. But in Python, the statement `a = 7` is legal and `7 = a` is not.  Furthermore, in mathematics, a statement of equality is either true or false, for all time. If $$a = b$$ now, then $$a$$ will always equal $$b$$. In Python, an assignment statement can make two variables equal, but they don't have to stay that way:

{% code lineNumbers="true" %}
```python
a = 5 
b = a # a and b are now equal 
a = 3 # a and b are no longer equal
```
{% endcode %}

The third line changes the value of `a` but does not change the value of `b`, so they are no longer equal. Although multiple assignment is frequently helpful, you should use it with caution. If the values of variables change frequently, it can make the code difficult to read and debug.

## Updating variables

One of the most common forms of multiple assignment is an `update`, where the new value of the variable depends on the old.

```python
x = x+1 
```

This means "get the current value of `x`, add one, and then update `x` with the new value." If you try to update a variable that doesn't exist, you get an error, because Python evaluates the right side before it assigns a value to `x`:

```
>>> y = y+1 
Traceback (most recent call last): 
 File "<pyshell#49>", line 1, in <module> 
   y = y+1 
NameError: name 'y' is not defined 
```

Before you can update a variable, you have to **initialise** it, usually with a simple assignment:

{% code lineNumbers="true" %}
```python
y = 0 
y = y+1
```
{% endcode %}

Updating a variable by adding 1 is called an **increment**; subtracting 1 is called a **decrement**.
