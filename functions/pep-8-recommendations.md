# PEP 8 Recommendations

## Function Names

Function names should be lowercase, with words separated by underscores as necessary to improve readability.

mixedCase is allowed only in contexts where that's already the prevailing style (for example `threading.py`), to retain backwards compatibility.

## Function Arguments

If a function argument's name clashes with a reserved keyword, it is generally better to append a single trailing underscore rather than use an abbreviation or spelling corruption. Thus `class_` is better than `clss`. An even better solution is to avoid such clashes by using a synonym.

Don't use spaces around the `=` sign when used to indicate a keyword argument or a default parameter value.

{% code lineNumbers="true" %}
```python
#Yes: 
def complex(real, imag=0.0): 
    return magic(r=real, i=imag) 
```
{% endcode %}

{% code lineNumbers="true" %}
```python
#No: 
def complex(real, imag = 0.0): 
    return magic(r = real, i = imag)
```
{% endcode %}

## Return statement

Be consistent in return statements. Either all return statements in a function should return an expression, or none of them should. If any return statement returns an expression, any return statements where no value is returned should explicitly state this as return `None`, and an explicit return statement should be present at the end of the function (if reachable).

{% code overflow="wrap" lineNumbers="true" %}
```python
#Yes: 
def foo(x): 
    if x >= 0: 
        return math.sqrt(x) 
    else: 
        return None
        
def bar(x): 
    if x < 0: 
        return None 
    return math.sqrt(x) 
```
{% endcode %}

{% code lineNumbers="true" %}
```python
#No: 
def foo(x): 
    if x >= 0: 
        return math.sqrt(x)

def bar(x): 
    if x < 0: 
        return 
    return math.sqrt(x) \end{pycode}
```
{% endcode %}

## Indentation

Continuation lines should align wrapped elements either vertically using Python's implicit line joining inside parentheses, brackets and braces, or using a hanging indent. When using a hanging indent the following should be considered; there should be no arguments on the first line and further indentation should be used to clearly distinguish itself as a continuation line.

{% code lineNumbers="true" %}
```python
#Yes:
# Aligned with opening delimiter.
foo = long_function_name(var_one, var_two, 
                         var_three, var_four)
                         
# More indentation included to distinguish this from the rest.
def long_function_name( 
        var_one, var_two, var_three, 
        var_four): 
    print(var_one)
    
# Hanging indents should add a level.
foo = long_function_name( 
    var_one, var_two, 
    var_three, var_four)
```
{% endcode %}

{% code lineNumbers="true" %}
```python
#No:
# Arguments on first line forbidden when not using vertical alignment.
foo = long_function_name(var_one, var_two, 
    var_three, var_four)
    
# Further indentation required as indentation is not distinguishable.
def long_function_name( 
    var_one, var_two, 
    var_three, var_four): 
    print(var_one)
```
{% endcode %}

{% hint style="info" %}
The 4-space rule is optional for continuation lines.
{% endhint %}

## Blank lines and White Spaces

* Avoid extraneous white spaces immediately before the open parenthesis that starts the argument list of a function call:

```
#Yes: 
spam(1)
```

```
#No:
spam (1)
```

* Surround top-level function and class definitions with two blank lines.
* Extra blank lines may be used (sparingly) to separate groups of related functions. Blank lines may be omitted between a bunch of related one-liners (e.g. a set of dummy implementations).
* Use blank lines in functions, sparingly, to indicate logical sections.
