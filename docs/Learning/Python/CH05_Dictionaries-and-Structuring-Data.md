## Dictionaries and Structuring Data

A Python *dictionary* is a mutable collection of key-value pairs. A *key* is dictionary index. A *key-value pair* is a key and its associated value. 

Unlike lists, dictionary indices can use many different data types. 

```python
person = {'name': 'John', 'age': 42}
```

*Note: Most of the examples on this page will reference this dictionary.*

Unlike lists, dictionary items are unordered (i.e. the order of dictionary indexes doesn't matter). Because they're unordered, dictionaries can't be sliced. 

```python
spam = ['bacon', 'eggs']
ham = ['eggs', 'bacon']
spam == ham # False

person = {'name': 'John', 'age': 42}
anotherPerson = {'age': 42, 'name': 'John'}
person == anotherPerson # True
```

Specifying a key from a dictionary will return that value. 

*Note: If a key doesn't exist, then `KeyError` will occur.*

```python
person['name'] # 'John'
```


### Dictionary Methods

#### keys()

`keys()` returns a list of data type `dict_keys`. 

```python
person.keys() # dict_keys(['name', 'age'])
```

#### values()

`values()` returns a list of data type `dict_values`.

```python
person.values() # dict_values(['John', 42])
```

#### items()

`items()` returns a list of the key-value pairs as tuples; type `dict_items`. 

```python
person.items() # dict_items([('name', 'John'), ('age', 42)])
```


### Iterating over Dictionaries

 The returns values of `keys()`, `values()`, and `items()` can't be modified, nor do they have an append method, but they can be iterated over. 

Note: The `dict_keys`, `dict_values`, and `dict_items` data types can be converted to iterable lists using the `list()` function. 

### Tuple Unpacking

*Tuple Unpacking* (e.g. the multiple-assignment trick) can also be used with dictionaries. 

*Reminder: Tuple Unpacking is a way to assign multiple variables to the values in a list using a single line of code.*

```python
for k, v in person.items():
	print('Key: ' + k + ', Value: ' + str(v))
```


### IN and NOT IN Operators

The `in` and `not in` operators are used to test weather the specified value is located, or not located, within the given `dict_keys`, `dict_values`, or  `dict_items` data type. 

*Note: If checking key values, you can use shorthand and leave off `.keys()`.*

```python
'name' in spam.keys() # True
'color' in spam.keys() # False
'color' not in spam.keys() # True
'color' in spam # False
```


### get()

The `get()` method can be used to prevent `KeyErrors` when an attempt is made to access a key that doesn't exist. 

`get()` takes 2 arguments: 
1.  the key of the value to retrieve 
2.  a fallback value to return if the key doesn't exist.

```python
picnicItems = {'apples': 5, 'cups': 2}
'I am bringing ' + str(picnicItems.get('eggs', 0)) + ' eggs.' # 'I am bringing 0 eggs.'
```


### setdefault()

`setdefault()` sets the value for a specified key in a dictionary, only if that key doesn't already have a value. 

```python
person.setdefault('job', 'programmer')
person # {'name': 'John', 'age': 42, 'job': 'programmer'}
person.setdefault('job', 'unemployeed')
person # {'name': 'John', 'age': 42, 'job': 'programmer'}
```


### Pretty Printing

#### pprint()

`pprint()` is a method used to print a dictionary with sorted keys. 

To use the pretty printing method, the `pprint` module must be imported. 

```python
import pprint
person = {'name': 'John', 'age': 42, 'favColor': 'blue'}
print(person) # {'name': 'John', 'age': 42}
pprint.pprint(spam) #prints with sorted keys - {'age': 42, 'name': 'John'}
```

If the output of `pprint()` is large, then each key-value pair will print on a new line. 

```python
person = {'name': 'John', 'age': 42, 'favColor': 'blue', 'favSport': 'gymnastics', 'favFood': 'pizza'}
pprint.pprint(person)
# {'age': 42,
#  'favColor': 'blue',
#  'favFood': 'pizza',
#  'favSport': 'gymnastics',
#  'name': 'John'}
```


#### pformat()

`pformat()` can be used to get the prettified text as a string value, instead of displaying it to the screen. 
