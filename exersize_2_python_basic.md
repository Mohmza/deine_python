# Python Basics
First things, indentation matters in Python. This is not so important
in langauges like `C++` but in Python it won't run if it's not indented
correctly. Indentation basically replaces the functionality of braces like `{}`
in `C++`.
I will assume you know most of the basic programming paradigms and will
just breifly go over them:

### if/else if/else
```Python
number = 3
if number == 2:
    print('Is 2')

elif number == 3:
    print('Is 3')

else:
    print('Is 4')
```
### For loop
```Python
# These are all equivalent
my_list = ['a', 'b', 'c']

for i in [0, 1, 2]:
    item = my_list[i]
    print(item)

for i in range(0, len(my_list)):
    item = my_list[i]
    print(item)

for item in my_list:
    print(item)

## Looping through some more complicated things

# Basic way
for tuple_item in [  ('a', 1), ('b', 2), ('c', 3)  ]:
    character = tuple_item[0]
    number = tuple_item[1]
    print(character + '_' + str(number))

# With tuple inpacking inside the loop
for tuple_item in [  ('a', 1), ('b', 2), ('c', 3)  ]:
    character, number = tuple_item   # This is called `unpacking`
    print(character + '_' + str(number))

# For loops can automaticall unpack items for you
for character, number in [  ('a', 1), ('b', 2), ('c', 3)  ]:
    print(character + '_' + str(number))

```

### Lists

```Python
## Creating Lists
## ---------------
# These are all equivalent
my_list = [0, 1, 2, 3, 4]

number_generator = range(0, 5)
my_list = list(number_generator)

my_list = []
for i in range(0, 5):
    my_list.append(i)

# This is called 'list comprehension'
# ..bit funky at first but it can be super useful later
my_list = [i for i in range(0, 5)] 

## Accessing Lists
## ---------------
# List indices start from 0 as it does in C++
item_3 = my_list[3] 

# ... you can even access items indexing from the end
last_item = my_list[-1] 
second_last_item = my_list[-2]

# You can access a `slice` of lists
# you can read this as 'my_list from 0 to 3'
# this will return you back a list of items in that `slice` of the list
first_second_and_third_items = my_list[0:3]

## Membership of lists
## -------------------
my_list = ['a', 'b', 'c']

if 'a' in my_list:
    print('a is in the list')

if 'e' not in my_list:
    print('e is not in the list')

# You can also phrase the above one differently by switching where the `not`
# appears
if not 'e' in my_list:
    print('e is not in the list')

# Slighty bigger example
for character in ['a', 'd', 'z']:
    if character in my_list:
        print(character + ' is in ' + my_list)
    else:
        print(character + ' is not in ' + my_list)

## Enumerate
my_list = ['a', 'b', 'c']

for i, character in enumerate(my_list):
    print(character ' is at index ' + i)

## Zip
characters = ['a', 'b', 'c'] 
numbers = [420, 69, 42]

for char, num in zip(characters, numbers):
    print(char ' is at the same index as ' num)
```

### Dictionarys
```Python
## Basics
## ---------------

# These are all equivalent
my_dict = {
    'a' : 1,
    'b' : 2,
    'c' : 3
}

print(my_dict['a']) # should print 1
print(my_dict['c']) # should print 3

for value in my_dict.values():
    print(value)  # prints 1, 2, 3

for key in my_dict.keys():
    print(key)  # prints 1, 2, 3

for key, value in my_dict.items():
    print(key + ' has value ' + value)

# the weirdest syntax you'll come across in  Python
del my_dict['a'] # Deletes the key,value pair associated with 'a'

# Creating a dictionary in fancier ways
keys = ['a', 'b', 'c']
values = [1, 2, 3]

my_dict = {} # create a blank Dict
for k, v in zip(keys, values):
    my_dict[k] = v

# ...using dictionary comprehension, similar to list comprehension
my_dict = { key : value for key, value in zip(keys, values) }
```

### Functions
```Python
def my_function(param):
    print(param)

my_function('hello_world')

def my_bad_adding_function(num1, num2):
    return num1 + num2 + 69

my_bad_adding_function(3, 4)
my_bad_adding_function(num2 = 4, num1 = 3) # you can specify the parameter values specifically

def function_with_a_default_value(p1, p2='default_value'):
    print('p1 is ' p1)
    print('p2 is ' p2)

function_with_a_default_value('hello', 'world') # 'p1 is hello' 'p2 is world'
function_with_a_default_value('hello') # 'p1 is hello' 'p2 is default_value'
```

### Classes
```Python
class Person:
    """
    Multiline comments go between triple quotes.
    Normally comments for functions and classes go below like this one is.

    the __init__ is the constructor of a class.

    As you can see in all class `methods`, `self` is the first parameter. This
    is just the Python paradigm. 

    The `self` is equivalent to the keyword `this` in C++ and lets
    you access properties inside methods
    """

    # the __init__ is basically the constructor
    def __init__(self, name, age, gender='female'):
        """
        Params
        ======
        name : str
            the name of the person
        age : int
            the age of the person
        gender : str = 'female'
            the gender of the person
        """
        self.name = name
        self.age = age
        self.gender = gender

    def description(self):
        """ 
        Returns a string description of the person 

        Returns
        =======
        str
            the string description of the person
        """
        desc = self.name + ' is ' + self.age + ' years old and is a ' + self.gender
        return desc

    def as_dict(self):
        """
        Returns a dictionary representation of the person

        Returns
        =======
        dict
            the dictionary description of the person

        """
        dict = {
            'name' : self.name,
            'age' : self.age,
            'gender' : self.gender
        }
        return dict

eddie = Person('eddie', 23, 'male')
hamza = Person('hamza', 23, 'male')

print(eddie.description())
print(hamza.description())

if eddie.gender == hamza.gender:
    print('same gender')

if hamza.age > eddie.age:
    age_difference = hamza.age - eddie.age
    print('hamza is older by ' age_difference)

girl1 = Person('Lea', 33, 'female')
girl2 = Person('Maya', 20)  # don't actually have to specify the gender as 'female' is the default

for key, value in hamza.as_dict():
    print(key + ' ' + value)
```

### Imports
```Python
import sys
print(sys.version_info)

import sys as system
print(system.version_info)

from sys import version_info
print(version_info)

from sys import version_info as vi
print(vi)
```
