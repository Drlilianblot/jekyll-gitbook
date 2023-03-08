# PEP 8 Recommendations

## Indentation

When the conditional part of an if-statement is long enough to require that it be written across multiple lines, it's worth noting that the combination of a two character keyword (i.e. if), plus a single space, plus an opening parenthesis creates a natural 4-space indent for the subsequent lines of the multiline conditional. This can produce a visual conflict with the indented suite of code nested inside the if-statement, which would also naturally be indented to 4 spaces. The PEP 8 takes no explicit position on how (or whether) to further visually distinguish such conditional lines from the nested suite inside the if-statement. Acceptable options in this situation include, but are not limited to:

<pre class="language-python" data-line-numbers><code class="lang-python"># No extra indentation.
if (this_is_one_thing and 
    that_is_another_thing): 
    do_something()
    
# Add a comment, which will provide some distinction in editors
<strong># supporting syntax highlighting.
</strong><strong>if (this_is_one_thing and 
</strong><strong>    that_is_another_thing): 
</strong><strong>    # Since both conditions are true, we can frobnicate. 
</strong><strong>    do_something()
</strong><strong>
</strong><strong># Add some extra indentation on the conditional continuation 
</strong><strong># line.
</strong><strong>if (this_is_one_thing 
</strong><strong>        and that_is_another_thing): 
</strong><strong>    do_something()
</strong></code></pre>

## Compound Statements

&#x20;Compound statements (multiple statements on the same line) are generally discouraged.

{% code lineNumbers="true" %}
```python
# Yes:
if foo == 'blah': 
    do_blah_thing() 
do_one() 
do_two() 
do_three()

# Rather not:
if foo == 'blah': do_blah_thing() 
do_one(); do_two(); do_three()
```
{% endcode %}

While sometimes it's okay to put an `if` with a small body on the same line, never do this for multi-clause statements. Also avoid folding such long lines!

{% code lineNumbers="true" %}
```python
# Rather not:
if foo == 'blah': do_blah_thing()

# Definitely not:
if foo == 'blah': do_blah_thing() 
else: do_non_blah_thing()

# Definitely not:
if foo == 'blah': one(); two(); three()
```
{% endcode %}

## Comparisons to singletons

* Comparisons to singletons like `None` should always be done with `is` or `is not`, never the equality operators.
* Beware of writing `if x` when you really mean `if x is not None` - e.g. when testing whether a variable or argument that defaults to `None` was set to some other value. The other value might have a type (such as a container) that could be false in a boolean context!
* Use `is not` operator rather than `not ... is`. While both expressions are functionally identical, the former is more readable and preferred.

{% code lineNumbers="true" %}
```python
# Yes:
if foo is not None:
    do_something()
    
# No:
if not foo is None: 
    do_something()`
```
{% endcode %}

