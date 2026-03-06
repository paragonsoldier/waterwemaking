## Python Basics

### Comments

Comments are lines of code that aren't compiled nor executed when the program runs. They're used as a way to annotate the source code to provide explanations on how areas of the code work. 

#### Single-Line Comments

Single-Line comments are written using a hash symbol (`#`) prefix. 

```python
# This is a single-line comment. 
```

#### Multi-Line Comments

 Multi-Line comments are written using triple single ( `'''`) or triple double quotes (`"""`). 
 
 ```python
 '''This is a 
multi-line comment.'''
```


### Expressions

A Python expression consists of values and operators that evaluate down to a single value. 


### Math Operators

| Operator | Description |
| --- | --- |
| `**` | Exponent          |
| `//` | Integer Division  |
| `%`  | Modulus/Remainder |
| `*`  | Multiplication    |
| `/`  | Division          |
| `+`  | Addition          |
| `-`  | Subtraction       |


### Order of Operations

Python follows the mathematical order of operations which can be summarized using the acronym PEMDAS (Parentheses, Exponents, Multiplication/Division, Addition/Subtraction). 


### Data Types

| Data Type                      | Example          |
| ------------------------------ | ---------------- |
| Integers (int)                 | -1, 0, 1, 2      |
| Floating-Point Numbers (float) | -1.25, 0.5, 1.75 |
| Strings                        | 'Hello, World!'  |


### Type Conversion

`str()` is used to convert a value to the string type. 
`int()` converts a value to the integer type. 
`float()` converts a value to the floating-point type.

```python
str(42) # "42"
int("42") # 42
float("42") # 42.0
```




### Variables

Variables are a way of storing data. A variable is initialized the first time a value is stored in it. 

Variables are initialized using an assignment statement, which uses a single equals sign. 

```python
spam = 'Hello, World!'
```

Variable can be used in expressions. 

A variable can be overwritten, by storing a new value. 

The following rules must be followed when declaring variable names: 
1) Use only one word, with no spaces.
2) Only use letters, numbers, and underscores.
3) Variable name can't begin with a number