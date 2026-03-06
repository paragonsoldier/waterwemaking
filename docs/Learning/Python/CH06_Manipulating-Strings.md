## Manipulating Strings

### String Literals

String Literals begin and end with single quotes, or double quotes.

*Note: When using single quotes to surround a string literal, single quotes can't be used inside without being escaped.*

```python
'I am a string literal.'
```

Using Double Quotes for String Literals allows for use of the single-quote character without escaping. 

```python
"I'm a string literal."
```


### Escape Characters

Escape Characters provide a way to type characters that are otherwise impossible to put into a string. 

```python
'\'' # single quote
'\"' # Double quote
'\t' # Tab
'\n' # Newline (line break)
'\\' # Backslash
```


### Raw Strings

Raw Strings ignore all escape characters. Therefore, Raw Strings are useful for typing file paths. 

Raw Strings are prefixed with the letter `r`.

```python
print(r'C:\Users\localadmin\Desktop')
```


### Multiline Strings

Multiline Strings are a way to preserve white space and line breaks. Escaping single or double quotes inside of multiline strings is optional. 

Multiline Strings are wrapped in either triple single quotes or triple double quotes.

```python
print('''Dear John, 

I ate spam and eggs for breakfast. 

Sincerly, 
Jane''')
```


### Indexing and Slicing

Strings can be indexed and sliced liked lists. 

*Note: Slicing doesn't modify the original string.*

```python
spam[0] = "Hello, World!"
spam[0] # 'H'
spam[:5] # 'Hello'
```


### IN and NOT IN Operators

The `in` and `not in` operators are used to test weather the specified value is located, or not located, within a string. 

*Note: When IN and NOT IN are used with strings, they're case sensitive.*

```python
'Hello' in 'Hello, World' # True
'HELLO' in 'Hello, World' # False
```


### String Concatenation

The `+` operator can be used to combine strings. 

```python
print('Hello, ' + 'World!') # 'Hello, World!'
```

*Note: When concatenating strings, all values must be of the string type.*

### String Replication

The `*` operator can be used with strings to repeat the string the specified number of times. 

```python
'Hello' * 3 # 'HelloHelloHello'
```


### String Interpolation

`%s` can be used to act as a marker, which will be replaced by what comes after the string. 

*Note: Using the `%s` marker means the `str()` method isn't needed convert values to strings.*

```python
age = 42
print('Age: %s' % (age)) # 'Age: 42'
```


### F-Strings

*F-Strings* were introduces in Python 3.6 to allow expressions inside of braces.

F-Strings are prefixed with the letter `f`.

```python
age = 42
print(f'Age: {age}, Age Next Year: {age + 1}') # 'Age: 42, Age Next Year: 43'
```


### String Methods

This example string will be used for the following method examples. 

```python
spam = 'Hello, world!'
```


#### upper()

```python
spam.upper() # 'HELLO, WORLD!'
```


#### lower()

```python
spam.lower() # 'hello, world!'
```


#### isupper()

`isupper()` returns `True` if the string has at least one letter and all the letters are uppercase.

```python
spam.isupper() # False
'HELLO'.isupper() # True
'123'.isupper() # False
```


#### islower()

`islower()` returns `True` if the string has at least one letter and all the letters are lowercase.

```python
spam.islower() # False
'abc123'.islower() # True
```


#### isalpha()

`isalpha()` returns `True` if the string consists only of letters and isn’t blank. 


#### isalnum()

`isalnum()` returns `True` if the string consists only of letters and numbers and isn't blank. 


#### isdecimal()

`isdecimal()` returns `True` if the string consists only of numeric characters and isn't blank. 


#### isspace()

`isspace()` returns `True` if the string consists only of spaces, tabs, and newlines and isn't blank. 


#### istitle()

`istitle()` returns `True` if the string consists only of words that begin with an uppercase letter followed by only lowercase letters. 


#### startswith()

`startswith()` returns `True` if the string begins with the string passed to the method.

```python
'Hello, world!'.startswith('Hello') # True
```


#### endswith()

`endswith()` returns `True` if the string ends with the string passed to the method. 


#### join()

`join()` joins together a list of strings using the character(s) passed.

```python
' '.join(['bacon', 'eggs', 'sausage']) # 'bacon eggs sausage'
', '.join(['bacon', 'eggs', 'sausage']) # 'bacon, eggs, sausage'
'ABC'.join(['bacon', 'eggs', 'sausage']) # 'baconABCeggsABCsausage'
```


#### split()

`split()` does the opposite of `join()`; it returns a list of strings from a string value. 

`split()` splits on whitespace by default. 

```python
'bacon eggs sausage'.split() # ['bacon', 'eggs', 'sausage']
```


#### partition()

`partition()` splits a string into the text before an after a separator string. A tuple of three substrings is returned: before, separator, after. 

```python
'bacon'.partition('c') # ('ba', 'c', 'on')
```

Tuple Unpacking can be used with `partition()`.

```python
before, sep, after = 'bacon'.partition('c')
```


### Text Justification 

Text justification is the process of aligning text with the left and right margins of a paragraph.


#### rjust() and ljust()

`rjust()` and `ljust()` add justification (i.e. padding) to the right or left of text respectively. 

```python
'bacon'.rjust(10) # '          bacon'
```

By default, `rjust()` and `ljust()` use the space character as the padding character. An optional argument can be added to use another character. 

```python
'bacon'.rjust(10, '*') #'**********bacon'
```


#### center()

`center()` works like `rjust()` and `ljust()`, but centers the text instead. 

```python
'bacon'.center(10, '=') # '=====bacon====='
```


### Removing Whitespace

This example string will be used for the following method examples. 

```python
spam = '     bacon     '
```


#### strip()

`strip()` returns a new string without any whitespace characters at the beginning or end. 

```python
spam.strip() # 'bacon'
```

`strip()` strips whitespace by default, but characters can be specified instead. 

*Note: The order of the strip parameters doesn't matter.*

```python
spam = 'bacon'
spam.strip('b') # 'acon'
spam.strip('ba') # 'con'
spam.strip('ab') # 'con'
spam = 'bbcon'
spam.strip('b') # 'con'
```


#### lstrip()

`lstrip()` removes whitespace from only the beginning. 

```python
spam.lstrip() # 'bacon     '
```


#### rstrip()

`rstrip()` removes whitespace from only the end.

```python
spam.rstrip() # '     bacon'
```


### Numerical Values of Characters

Unicode is a text encoding standard designed for the digitization of all of the world's writing systems.  Every text character has a numerical value assigned called a *Unicode Code Point*. 

#### ord()

`ord()` returns the code point of a one-character string.

```python
ord('A') # 65
```


#### chr()

`chr()` returns the one-character string of an integer code point.

```python
chr(65) # 'A'
```


### Copy and Paste with pyperclip

[pyperclip](https://pypi.org/project/pyperclip/) is a 3rd Party module for Python that enables copy and paste clipboard functions. 

*Note: `pyperclip` is a 3rd Party module. Unlike built-in Python modules, 3rd Party modules must be installed manually.* 

`copy()` copies the passed text to the computer's clipboard. 

`paste()` pastes the current value stored in the computer's clipboard. 

*Note: If something outside of the Python program changes the clipboard's contents, the `paste()` function will return it.* 

```python
import pyperclip
pyperclip.copy('bacon')
pyperclip.paste() # 'bacon'
```


---

### Writing Command Line Utilities

Python programs created for the purpose of running as command-line utilities must include a shebang line (`#!`) at the beginning of the script. This line specifies the interpreter/program that should be used to execute the script. 

In Python, a shebang line is typically written as `#!/usr/bin/env python3`

Command Line Arguments are stored in `sys.argv`. 