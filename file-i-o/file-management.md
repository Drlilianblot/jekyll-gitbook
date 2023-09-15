# File management

## Filenames and paths

Files are organized into **directories** (also called **folders**). Every running program has a current directory, which is the default directory for most operations. For example, when you open a file for reading, Python looks for it in the current directory.

The `os` module provides functions for working with files and directories (`os` stands for operating system''). `os.getcwd()` returns the name of the current directory:

```bash
>>> import os 
>>> cwd = os.getcwd()
>>> print(cwd) 
 /home/lblot
>>>
```

`cwd` stands for "current working directory". The result in this example `/home/lblot`, which is the home directory of a user named `lblot`.

A string like `cwd` that identifies a file is called a **path**. A **relative path** starts from the current directory; an **absolute path** starts from the topmost directory in the file system. The paths we have seen so far are simple filenames, so they are relative to the current directory. To find the absolute path to a file, you can use `os.path.abspath`:

```bash
>>> os.path.abspath('memo.txt')
 '/home/dinsdale/memo.txt' 
>>>
```

`os.path.exists` checks whether a file or directory exists:

```bash
>>> os.path.exists('memo.txt') 
 True 
>>>
```

If it exists, `os.path.isdir` checks whether it's a directory:

```bash
>>> os.path.isdir('memo.txt') 
 False 
>>> os.path.isdir('music')
 True 
>>> os.path.isfile('memo.txt') 
 True 
>>> 
```

Similarly, `os.path.isfile` checks whether it's a file.

&#x20;os.listdir returns a list of the files (and other directories) in the given directory:

```bash
>>> os.listdir(cwd)
 ['music', 'photos', 'memo.txt'] 
>>> 
```

To demonstrate these functions, the following example "walks" through a directory, prints the names of all the files, and calls itself recursively on all the directories.

{% code lineNumbers="true" %}
```python
import os

def walk(dir): 
    for name in os.listdir(dir): 
        path = os.path.join(dir, name)
        if os.path.isfile(path):
            print(path)    
        else:
            walk(path)
```
{% endcode %}

`os.path.join` takes a directory and a file name and joins them into a complete path.

**Exercise:** Modify `walk` so that instead of printing the names of the files, it returns a list of names.&#x20;

<details>

<summary>Answer</summary>



</details>

**Exercise:** The `os` module provides a function called `walk` that is similar to this one but more versatile. Read the documentation and use it to print the names of the files in a given directory and its subdirectories.
