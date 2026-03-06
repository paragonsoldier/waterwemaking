## Flow Control


### Boolean Values

A Boolean value is either True or False. 

*Note: Neither True nor False can be used as variable names.*


### Assignment vs. Comparison

A Single Equals will assign the value on the right to the value on the left. 

```python
a = 1 # a is assigned the value of 1
```

A Double Equals will evaluate whether two values are the same. 

```python
"a" == 1 # False, The letter 'a' isn't equal to the value of 1
```


### Comparison Operators

| Operator | Description |
| --- | --- |
| `==` | Equal To |
| `!=` | Not Equal To |
| `<` | Less Than |
| `>` | Greater Than |
| `<=` | Less Than or Equal To |
| `>=` | Greater Than or Equal To |

*Note: Integers and Floating-Point Values can be equal to each other, but neither will ever be equal to a string. 

```python
2 == 2.0 # True
2 == "2" # False
```

*Note: `0`, `0.0`, and `''` all evaluate to False*


### Binary Operators

Binary Operators (e.g. and, or) evaluate on 2 Boolean Values. 

**AND Truth Table**
```python
True and True # True
True and False # False
False and True # False
False and False # False
```

**OR Truth Table**
```python
True or True # True
True or False # True
False or True # False
False or False # False
```


### Unary Operators

Unary Operators (e.g. not) evaluate on 1 Boolean Value. 

**NOT Truth Table**
```python
Not T # False
Not F # True
```


### Flow Control

Flow control is a statement with a condition that evaluates down to a single Boolean Value, that executes a clause if that Boolean Value is True (e.g. IF Statements, While Loops).

Lines of code grouped together are called a block (i.e. block of code).

In Python, Blocks
1. Begin with an indentation increase
2. Can contain other blocks
3. End when the indentation decreases to zero or to a containing block's indentation


### IF Statements

An IF Statement executes a clause if the condition evaluates to `True`.

```python
if name == "John":
	print("Hello, John.")
```


### IF, ELSE Statements

An IF, ELSE Statement executes the `if` clause if the condition evaluates to `True`, otherwise the `else` clause is executed. 

```python
if name == "John":
	print("Hello, John.")
else: 
	print("Hello, Stranger.")
```


### IF, ELIF, ELSE Statements

An IF, ELSE Statement executes the `if` clause if the condition evaluates to `True`, otherwise the next `elif` clause that evaluates to `True` is executed. If no `elif` clauses evaluate to `True`, then the `else` clause is executed. 

```python
if name == "John":
	print("Hello, John.")
elif name == "Jane":
	print("Hello, Jane.")
else: 
	print("Hello, Stranger.")
```

*Note: If there are multiple elif statements, only one will be executed. Therefore, the order of the elif statements matter.*


### WHILE Loops

The code in a `while` clause will execute as long as the while statement's condition evaluates to `True`.

```python
name = ""
while not name:
	print("Please Enter your name: ")
	name = input()
print("Hello, " + name)
```

*Note: When running while loops, it's possible for the program's execution to get stuck in an endless loop. Pressing `CTRL + C` will stop a program's execution immediately.*


### BREAK Statements

A `break` statement is used to break out of a `while` loop's clause early. 

```python
name = ''
while True:
	print("Please Enter your name: ")
	name = input()
	if name:
		break
print("Hello, " + name)
```


### CONTINUE Statements

`continue` statements are used inside loops. When a program's execution reaches a `continue` statement, the program's execution immediately jumps back to the start of the loop and re-evaluates the loop's condition. 

```python
# In this example, program execution will only continue if the user inputs the name 'John'. 
while True:
    print("Please Enter your name: ")
    name = input()
    if name != "John":
        continue
    print("Hello, John. What is your password?")
    password = input()
    if password == "password":
        break
print("Access granted.")
```

### RANGE function

The `range()` function returns a sequence of number based on the start, stop, and step values specified. 

`range(start, stop, step)`
- `start` (*optional*): an integer specifying a start position (default = 0)
- `stop`: an integer specifying at which position to stop
- `step` (*optional*): an integer specifying the incrementation (default = 1)


### FOR Loops

`for` loops are used to execute a block of code a certain number of times.

```python
for i in range(4):
	print(i)
	
# Output: 0 1 2 3
```


---

## Modules

Python has a set of built-in functions that are available in all Python programs. Python also has a standard library that includes a set of modules. Each module contains a group of related functions that can be embedded into Python programs. To use a module, it must be imported first. 

*Note: Do NOT name a Python script using the same name as a Python module.*

```python
# randint(start, stop) returns a random value between the start and stop parameters (inclusive). 
import random
print(random.randint(1, 10)) # Prints a random value 1-10 (inclusive). 
```


#### Multiple Modules
Multiple modules can be imported using a single import statement by separating each module using a comma. 

```python
import random, sys, os, math
```

#### Import a Specific Function from a Module

A specific function can be imported from a module using a `from` statement. 

When a specific function is imported in this fashion, calling the function won't require the module name. 

```python
from random import randint
print(randint(1, 10))
```


---

## Program Termination

A program terminates automatically if the program's execution reaches the bottom of the instructions. 

To terminate a program early, use the `sys.exit()` function. 

```python
import sys
while True: 
	print("Type exit to exit.")
	response = input()
	if response == "exit":
		sys.exit()
	print("You typed " + response + ".")
```