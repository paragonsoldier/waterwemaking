## Augmented Assignment Operators

Using Augmented Assignment Operators provides a shorthand way to edit a variable, then reassign it back to itself (e.g. Instead of coding `i = i + 1`, an augmented assignment operator can be used to perform the same action using shorthand: `i += 1`.

```python
i += 1
i -= 1
i *= 1
i /= 1
i %= 1
i += ' world!' # Can be used with strings also. 
# Can also be used with list replication. 
person = ['John']
person *= 3 # ['John', 'John', 'John']
```


## Lists

A *list* is a value that contains multiple other values in an ordered sequence. 

When referencing the list itself that's called the *list value*. The values inside a list are called *list items*.  

```python
spam = ['bacon', 'eggs', 'sausage']
```

*Note: Most of the examples on this page will reference this list.*

Indentation doesn't matter inside of lists. The example list can also be written using the following syntax: 

```python
spam = ['bacon', 
        'eggs', 
        'sausage']
```


### Access List Items by Index

Specifying an index from a list will return that value. 

```python
spam[0] # 'bacon'
```

A negative index can also be specified.

```python
spam[-1] # 'sausage'
```


### Slicing

Slicing a list returns a new list with the specified values

`<list>[<start>:<stop>:<step>]`
- **start:** The index to start the slice (inclusive). Defaults to 0 if omitted.
- **stop:** The index to end the slice (exclusive). Defaults to the end of the list if omitted.
- **step:** The increment between indices. Defaults to 1 if omitted.

```python
spam[0:2] # ['bacon', 'eggs']
spam[:2] # ['bacon', 'eggs']
spam[1:] # ['eggs', 'sausage']
spam[:] # returns the whole list, ['bacon', 'eggs', 'sausage']
```


### Length

The `len()` method returns the number of values that are in the list passed. 
```python
len(spam) # 3
```


### Reassign a List Value

To reassign a list value, specify it's index and use the assignment operator. 

```python
spam[1] = 'ham' # ['bacon', 'ham', 'sausage']
spam[1] = spam[0] # ['bacon', 'bacon', sausage']
```


### List Concatenation

The `+` operator can be used to combine lists. 

```python
['A', 'B'] + ['C', 'D'] # ['A', 'B', 'C', 'D']
```


*Python Tip*: a backslash (\) can be used to split instructions across multiple lines. 

```python
['A'] + ['B'] + \
['C'] + ['D'] # ['A', 'B', 'C', 'D']
```


### List Replication

The `*` operator can be used to replicate list values. 

```python
['A', 'B'] * 2 # ['A', 'B', 'A', 'B']
```


### Loop Over a List

 A `for` loop can be used to perform an action over each index in a list. 

```python
for i in range(len(spam)):
	print(spam[i], end='') # baconeggssausage
```


### IN and NOT IN Operators

The `in` and `not in` operators are used to test weather the specified value is located, or not located, within a list. 

```python
'ham' in spam # False
'bacon' in spam # True
'bacon' not in spam # False
```


### Tuple Unpacking

*Tuple Unpacking*, also known as the multiple-assignment trick, is a way to assign multiple variables to the values in a list using a single line of code. 

```python
person = ['John', 42]
name, age = person # name = 'John', age = 42
```


### List Enumeration

An *enumeration* is a complete, ordered listing of all the items in a collection.

*List Enumeration* is useful to access both a list's values and indices from within a loop. 

```python
for index, item in enumerate(spam):
	print('Index: ' + str(index) + ', Item: ' + item)
# Index: 0, Item: bacon
# Index: 1, Item: eggs
# Index: 2, Item: sausage
```


### random.choice()

`random.choice(<list>)` returns a randomly selected item from a list. 

```python
import random
random.choice(spam) # Will randomly return either 'bacon', 'eggs', or 'sausage'
```


### random.shuffle()

`random.shuffle()` reorders the values within a list. 

```python
random.shuffle(spam)
```


### index()

`index()` returns the index of the value if found, returns `ValueError` if not found. 

*Note: If there are multiple instances of the value in the list, only the index of the first instance is returned.*

```python
spam.index('bacon') # 0
```


### Adding Items to a List

#### append()

`append()` is used to add values to the end of a list. 

```python
spam.append('ham') # ['bacon', 'eggs', 'sausage', 'ham']
```


#### insert()

`insert()` is used to add a value to a specific index in a list. 

```python
spam.insert(1, 'ham') # ['bacon', 'ham', 'eggs', 'sausage']
```


### Removing Items from a List

#### remove()

`remove()` removes a value from a list if found, returns `ValueError` if not found. 

*Note: If there are multiple instances of the value in a list, only the first instance is removed.*

```python
spam.remove('eggs') # ['bacon', 'sausage']
```


#### del()

`del()` removes a value from a list at the specified index.

```python
del(spam[1]) # ['bacon', 'sausage']
```


### Sorting a List

`sort()` sorts the contents of a list. 

`reverse` is an optional argument. If set to `True`, then list is sorted in reverse. 

*Note: When sorting, all values in the list must be of the same type, otherwise `TypeError` is returned.*

```python
spam.sort() # ['bacon', 'eggs', 'sausage']
spam.sort(reverse=True) # ['sausage', 'eggs', 'bacon']
```


### Nested lists

Lists can also be nested inside of other lists. 

```python
spam = [['cat', 'bat'], [10, 20, 30]]
spam[0] # ['cat', 'bat']
spam[0][1] #'bat'
spam[1][0] # 10

```

---

## Mutable vs. Immutable

A *mutable* data type allows values to be added, removed, or changed. An *immutable* data type can't be changed. 

Integers (`int`), Floating-Point Numbers (`float`), Boolean Values (`bool`), and Strings (`str`) are all immutable data types. 

```python
spam[1] = 'ham' # ['bacon', 'ham', 'sausage']
name = 'Sam'
name[0] = 'P' # TypeError
```

## Tuples

Tuples are like lists, but are immutable. 

Tuples are coded using parentheses, instead of square brackets. 

```python
person = ('John', 42)
```

*Note: Use a trailing comma for single-value tuples.*

```python
type(('John',)) # class 'tuple'
type(('John')) # class 'str'
```


## List and Tuple Type Conversions

`list()` converts the parameter to the list type.

`tuple()` converts the parameter to tuple type. 


---

## Reference vs. Copy

### IDs

All Python values have a unique identity (i.e. ID). 

The `id()` function returns this identifier. 

```python
id(spam)
spam.append('ham') 
id(spam) # append() modifies the list "in place", so the identifier will remain the same
spam = ['pig', 'chicken', 'cow']
id(spam) # During the reassignment, spam no longer references the original list. A new list was created. Therefore, id now displays a different identifier. 
```

Python's automatic garbage collector frees up memory by deleting any values that aren't being referred to by any variables. 


### References

When a variable is assigned to another variable, the variable becomes a reference to the assigned variable. 

```python
spam # ['bacon', 'eggs', 'sausage']
cheese = spam
cheese[1] = 'ham'
cheese # ['bacon', 'ham', 'sausage']
spam # ['bacon', 'ham', 'sausage']
```

However, when a new value of an immutable data type is assigned, the new variable will no longer reference the original. 

```python
age = 42
newAge = age
newAge # 42
age # 42
age = 43
newAge # 42
age # 43
```


### Passing Reference

When a function is called, the argument values are copied to the parameter variables. This means, with lists and dictionaries, a copy of the reference is used for the parameter. Keep this behavior in mind, as this can lead to confusing bugs.

```python
def eggs(someParameter):
	someParameter.append('Hello')
spam = [1, 2, 3]
eggs(spam)
print(spam) # [1, 2, 3, 'Hello']
```


### copy()

`copy()` is used to make a duplicate copy of a mutable value, such as a list or dictionary, instead of just a reference. 

```python
import copy
id(spam)
cheese = copy.copy(spam)
id(cheese) # cheese is different list with different identity
cheese[1] = 42
spam # ['A', 'B', 'C', 'D']
cheese # ['A', 42, 'C', 'D']
```


### deepcopy()

If the list being copied contains sub-lists, `deepcopy()` will copy the sub-lists also.
