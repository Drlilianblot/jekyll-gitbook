# Debugging

## Editor

If you are using a text editor to write your scripts, you might run into problems with spaces and tabs. The best way to avoid these problems is to use spaces exclusively (no tabs). Most text editors that know about Python do this by default, but some don't. Tabs and spaces are usually invisible, which makes them hard to debug, so try to find an editor that manages indentation for you.

Also, don't forget to save your program before you run it. Some development environments do this automatically, but some don't. In that case the program you are looking at in the text editor is not the same as the program you are running.&#x20;

Debugging can take a long time if you keep running the same, incorrect, program over and over! Make sure that the code you are looking at is the code you are running. If you're not sure, put something like `print('hello')` at the beginning of the program and run it again. If you don't see `hello`, you're not running the right program!

## Traceback

&#x20;The traceback Python displays when an error occurs contains a lot of information, but it can be overwhelming, especially when there are many frames on the stack. The most useful parts are usually:

* What kind of error it was, and
* Where it occurred.

Syntax errors are usually easy to find, but there are a few gotchas. Whitespace errors can be tricky because spaces and tabs are invisible and we are used to ignoring them.

```sh
>>> x = 5 
>>>  y = 6 
  File "", line 1 
     y = 6 
     ^ 
SyntaxError: invalid syntax
```

&#x20;In this example, the problem is that the second line is indented by one space. But the error message points to `y`, which is misleading. In general, error messages indicate where the problem was discovered, but the actual error might be earlier in the code, sometimes on a previous line.

The same is true of runtime errors. Suppose you are trying to compute a signal-to-noise ratio in decibels. The formula is $$SNR_{db} = 10 \log_{10} (P_{signal} / P_{noise})$$. In Python, you might write something like this:

{% code lineNumbers="true" %}
```python
import math 
signal_power = 9 
noise_power = 10 
ratio = signal_power // noise_power 
decibels = 10 * math.log10(ratio) 
print(decibels) 
```
{% endcode %}

But when you run it, you get an error message:

```sh
Traceback (most recent call last):
  File "snr.py", line 5, in <module>
    decibels = 10 * math.log10(ratio)
ValueError: math domain error
```

The error message indicates line 5, but there is nothing wrong with that line. To find the real error, it might be useful to print the value of `ratio`, which turns out to be `0`. The problem is in line 4, because using the integer division does floor division. The solution is to use the floating-point division `/` instead.&#x20;

In general, error messages tell you where the problem was discovered, but that is often not where it was caused.
