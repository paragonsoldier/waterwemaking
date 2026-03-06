## Functions 


### Function Basics

A function is, essentially, a mini-program inside of a program. The primary purpose of a function is to group code blocks that execute multiple times. 


#### The DRY Principle

Functions support the DRY (*Don't Repeat Yourself*) principle. If the same code blocks are used multiple time throughout a program, place those code blocks inside a function, then call the function when needed. This way, if the code block needs updates, it'll only need updated in a single location.


#### Defining a Function

Functions are defined using a `def` statement.

```python
def printHello():
	print("Hello")
```


#### Calling a Function

Typing the function name, without the `def` statement, calls the function. 

```python
printHello() # "Hello"
```


#### Function Arguments

Functions can optionally accept arguments. Arguments are values passed to a function. 

For a function to accept arguments they must be written as parameters (i.e. variables that contain arguments) inside a function's parentheses. 

```python
def printHelloName(name):
	print("Hello, " + name)
printHelloName("John") # 'Hello, John'
```

*Note: Most arguments passed to a function are positional (i.e. the order the arguments are passed matters). Keyword arguments are arguments identified by a keyword. Parameters can also be optional.*


#### RETURN Statements

Rather then performing an action, a function can also return a value. This is done using the `return` keyword, followed by a value, or expression, to be returned. 

```python
def add(a, b):
	return a + b
print(str(add(1, 2))) # '3'
```

*Note: All functions evaluate to a return value. Python automatically adds `return None` to the end of any function definition that doesn't include a return statement. Functions without a return statement are of the `NoneType` data type.*

#### Summary

*Defining a Function*: a `def` statement defines (i.e. creates) a function

*Argument*: a value that's passed to the function

*Parameter*: function variables that have arguments passed to them

*RETURN Statement*: the `return` keyword, followed by the value or express the function should return

*Return Value*: the value a function call evaluates to

*Call a Function*: A function is called by typing the function name without the `def` statement. Calling a function sends the program's execution to the top of the function's code. 


### Built-In Functions

#### print()

The `print()` function outputs the provides argument(s). 

```python
print("Hello, World!") # "Hello, World!"
```

By default `print()` adds a newline character to the end of the print statement. `end` is an optional keyword argument that augments the trailing character at the end of a print statement. 

```python
print("Hello", end="")
print("World") # 'HelloWorld'
```

By default `print()` automatically separates multiple string values with a single space. `sep` is an optional keyword argument that can overwrite this behavior.

```python
print("bacon", "eggs", "sausage", sep="") # 'baconeggssausage'
```


#### abs()

The `abs()` function returns the absolute value of the parameter. 

```python
abs(-7.25) # 7.25
```


#### input()

The `input()` function waits for the user to enter text, then returns the text the user typed. 

```python
print('Please Enter your name: ')
name = input()
```


#### len()
The `len()` function returns the number of characters in a string. 

```python
len("Hello, World!") #13
```


### The Call Stack

The *Call Stack* is a stack Python uses to remembers which line of code called a function, so that execution returns to that location when it encounters the function's return statement. 

Each *Frame Object* stores the line number of the original function call


### Function Scope

Python variables exist is one of two scopes, either local or global. 

*local variable*: a variable that exists in a local scope

Variables that are assigned when a function is called exist in that function's local scope. When the scope is destroyed (e.g. a function's return statement is executed), the variables in that scope are forgotten. Code in a local scope can't access variables from a different local scope. 

*global variable*: a variable that exists in the global scope

Variables that are assigned outside of all functions exist in the global scope. Code in the global scope can't access local variables, but code in a local scope can access global variables. 

*Note: It's bad practice for local variable names to match global variable names, as this can lead to difficulties when troubleshooting.*

A `global` statement, inside a function, tells Python to modify a global variable from within that function. 

```python
def spam():
	global eggs
	eggs='spam'
eggs = 'global'
spam()
print(eggs) # prints 'spam'
```

In a function, a variable with either ALWAYS be global, or ALWAYS be local.
- If there's a `global` statement for that variable in a function, then its a global variable. 
- If the variable is used in an assignment statement in the function, then it's a local variable. 
- If the variable is not used in an assignment statement, then it's a global variable.
- If a variable is being used in the global scope, then its a global variable. 

```python
def spam():
	global eggs
	eggs = 'spam' # this is the global

def bacon():
	eggs = 'bacon' # this is a local

def ham():
	print(eggs) #this is the global
```


### Exception/Error Handling

By default, if a program returns an error, then the program crashes. To prevent crashes, code that could potentially have an error should be placed in a `try` clause. If an error occurs when using a `try` clause, then the program's execution will move to the start of the following `except` clause.  After an `except` clause is ran, the program's execution will continue as normal. 

```python
def spam(divideBy):
	try:
		return 42 / divideBy
	except ZeroDivisionError:
		print('Error: Invalid argument.')
```