# Writing modules

Any file that contains Python code can be imported as a module. For example, suppose you have a file named `wc.py` with the following code:&#x20;

{% code lineNumbers="true" %}
```python
def linecount(filename): 
    count = 0 
    for line in open(filename): 
        count += 1 
    return count
    
print(linecount('wc.py')) 
```
{% endcode %}

If you run this program, it reads itself and prints the number of lines in the file, which is 7. You can also import it like this:

```bash
>>> import wc
 7 
>>>
```

&#x20;Now you have a module object `wc`:

```bash
>>> print(wc)
 <module 'wc' from 'wc.py'> 
>>>
```

That provides a function called `linecount`:

```
>>> wc.linecount('wc.py')
 7
>>>
```

So that's how you write modules in Python.

The only problem with this example is that when you import the module it executes the test code at the bottom. Normally when you import a module, it defines new functions but it doesn't execute them.

Programs that will be imported as modules often use the following idiom:

{% code lineNumbers="true" %}
```python
if __name__ == 'main': 
    print(linecount('wc.py'))
```
{% endcode %}

**`__name`** is a built-in variable that is set when the program starts. If the program is running as a script, **`__name__`** has the value **`main`**; in that case, the test code is executed. Otherwise, if the module is being imported, the test code is skipped.

**Exercise:** Type this example into a file named `wc.py` and run it as a script. Then run the Python interpreter and `import wc`. What is the value of **`__name__`** when the module is being imported?

{% hint style="info" %}
**Warning:** If you import a module that has already been imported, Python does nothing. It does not re-read the file, even if it has changed. If you want to reload a module, you can use the built-in function **`reload`**, but it can be tricky, so the safest thing to do is restart the interpreter and then import the module again.&#x20;
{% endhint %}

<details>

<summary>Answer</summary>



</details>
