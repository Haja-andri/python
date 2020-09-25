# Learning notes on Python, Algorithms and Data structure

## 1/ Environment setup

```
cd
mkdir pyworkshop
cd pyworkshop
python3.7 -m venv env
source env/bin/activate
```

### Starting REPL (Read, Evaluate, Print, Loop)

Command + Shift + P

### Get list of methode for a given type

Get the variable type with  `type (variable);`
This will print the variable type, then `dir (type)`

### Recommended Coding convention to follow 

PEP8 --> https://pep8.org


## 2/ Variables
There is no need to specify the type of the variable when creating it, since Python is a dynamically typed. It is recommended to have them start with lower case and compose with dash (-) or lowdash (_)
Variables cannot start with number and we must be careful not to overwrite existing data types as Python allow things like `list = 1`, which will turn the list data type into an integer

### Integers
```
x = 4
y = -4673
z = 0
```

### Float
```
x = 5.0
y = -3494.5
z= 0.0
```
Integers an simple data types are just object under the hood

### Operations

```
x = 5
y = 3.0
x + Y --> 8.0 (notice the result being a float)
```

### String
Can be in single quote or double quote. It is recommended to use double quote as it can wrap single quote that are part of the string

### long string on REPL
Use triple double quote

``` 
long_string = """
... 12342
...noer
... andihsr
..."""

long_string -> \n12342\nnoer\nandihsr (\n --> new line)
```
### fstring
fprint allow combining variables directly into the string 

```
variable = "Haja"
f"Hello {variable}" --> Hello Haja
```

### concatation
Use the + symbole

```
"Hello" + "world"
```
Strings and Integers cannot be concatenated


## 3/ Function 

Formation: `def` `function_name` `()` `:` no braquet. Function uses indentations (tab or space) to define its scope.
If a function returns a value, it can be assigned to another variable

When a function argument have a default value, it has to be last in the function definition 
```
def fun_name(arg_1, arg_2="default_value"):
  print f"{arg_1} and {arg_2}"
```

Never use mutable type (like `list`, `dict`, `set`) as default argument... because they get created the first time the function is called and then memorized and not reinitialised the next time the function is called

### Don't do this
```
def foo(a, b=[]):
  b.append(a)
  print("B is: ", b)

foo(5) --> "B is: [5]"
foo(6) --> "B is: [5,6]"
```

Instead do
```
def foo(a, b=None):
  if b is None:
    b=[]
  b.append(a)
  print("B is: ", b)
```

### Scope
Scope are defined by indentations

## 4/ Advanced data types

### List

https://www.learnpython.dev/02-introduction-to-python/080-advanced-datatypes/10-lists/#list-cheat-sheet

List can be created with two square braquets `[]` or ` variable = list()`
We use comma to separate the items inside the list. Pretty much like `array` in JS 
Items does not need to be all the same type, but in practice it is better.

```
name = ["Haja", "Nina", "John"]
```

Get the length of a list 
```
len(name) --> 2
#len is globaly available function
```
List retain the order of the items inside it --> We use index to access the items. The index start at `0`

```
print(name[1]) --> "Nina"
```
Because the items inside List has an order, then we can sort them. They are different way to sort

### First way to sort --> Take the original list and return the a copy of the list that is sorted with `sorted(my_list)` built in function.
It basically returns a copy of the list passed to it sorted (the orifinal list wont change)

```
lottery_numbers = [1,4,3423,78,11]
# sorted() is a built in function
sorted(lottery_numbers) --> [1, 4, 11, 78, 3423]
print(lottery_numbers) --> [1, 4, 3423, 78, 11]
```
Sorted take an optional argument that define the order 

```
sorted(lottery_numbers, reverse=True) --> [3423, 78, 11, 4, 1]
```

### Second way to sort is to do it in place but unlike sorted(), .sort() modifies the original list

`.sort()` and `.reverse()` will mutate the list and has NO return

```
lottery_numbers.sort()
print(lottery_numbers)
>>> [1, 4, 11, 78, 3423]
lottery_numbers.reverse()
print(lottery_numbers)
>>> [3423, 78, 11, 4, 1]
```

### Searching in a list
Its a very slow operations because under the hood, each value is checked ...
`my_list.index(item)` or `item in my_list`
`.index()` will return the position of the item, it there are several items with the same name at differents index, it will return the first one

```
names = ["Nina","Richy","Dan","Nina"]
>>> names = ["Nina","Richy","Dan","Nina"]
>>> "Richy" in names
True
>>> "Yolo" in names
False
>>> 
>>> names.index("Richy")
1
>>> names.index("Nina")
0
```

### Find out how many times an item appear in a list with count()
```
>>> names.count("Richy")
1
>>> names.count("Nina")
2
>>> 
```

### Find an item position and change it

```
>>> pos = names.index("Richy")
>>> names[pos] = "Gab"
>>> names
['Nina', 'Gab', 'Dan', 'Nina']
```

### Add items to the list
`my_list.append("new_item")` will add `new_item` to `my_list` at the end of the list.

We also have `.insert()` will insert an item at a specified position
```
my_list.insert(index_where_to_insert, item_to_insert)
```

### Combine 2 lists with extend()
```
names = ["Nina", "Max"]
colors = ["red", "bleu"]
names.extend(colors)
print(names) --> ["Nina", "Max","red", "bleu"]
```

### Remove item form list with 

#### .remove()
Note that `.remove("item_to_remove")` will remove only the first item that match the `arg`
```
>>> names.remove("Gab")
>>> names
['Nina', 'Dan', 'Nina']
```

#### .pop()
Remove the item at the given index (last item in the list by default), and return the item.

```
>>> names
['Dan', 'Nina']
>>> names.append("Jack")
>>> names
['Dan', 'Nina', 'Jack']
>>> names.pop()
'Jack'
>>> names
['Dan', 'Nina']
>>> names.append("Bro")
>>> names
['Dan', 'Nina', 'Bro']
>>> names.pop(1)
'Nina'
>>> names
['Dan', 'Bro']
>>> 
```

#### del

```
>>> my_list
['zero', 'one', 'two', 'two_and_half', 'tree']
>>> del my_list[3]
>>> my_list
['zero', 'one', 'two', 'tree']
>>> 
```


### Inserting

Insert take the position at which it needs value needs to be inserted

```
>>> my_list
['zero', 'one', 'two', 'tree']
>>> my_list.insert(3, "two_and_half")
>>> my_list
['zero', 'one', 'two', 'two_and_half', 'tree']
>>> 
```


#### List slicing getting items on specific range

```
>>> my_list = ["zero", "one", "two", "tree"]
>>> my_list
['zero', 'one', 'two', 'tree']
>>> my_list[0]
'zero'
>>> my_list[0:2]
['zero', 'one']
# Same result below without specifying
>>> my_list[:2]
['zero', 'one']
# The last item in the list
>>> my_list[-1]
'tree'
>>> my_list[1:3]
['one', 'two']
>>> 
```

## Tuples
https://www.learnpython.dev/02-introduction-to-python/080-advanced-datatypes/30-tuples/#tuple-cheat-sheet

Tuples are UNMMUTABLE. Once create the items inside cannot be changed. Useful for thing like containing a snapshot of datas e.g spreadsheets.

Make a tuple with empty parenthesis. If a value is provided inside the parenthesis, then it is not a tuple anymore. We have to add a commat at the end to make it a tuple

```
>>> a = ()
>>> type(a)
<class 'tuple'>
>>> b = (1)
>>> type(b)
<class 'int'>
>>> b = (1,)
>>> type(b)
<class 'tuple'>
>>> b = (1,3,4)
>>> type(b)
<class 'tuple'>
```

In fact the parenthesis are optional as long as we have the commas
```
>>> x = 1,2,3,4
>>> type(x)
<class 'tuple'>
```

This will work also for an empty one
`tuple()`



Tuples are practical to store datas that together discribe something e.g a Student. Each item can be accessed by its index just like list.

```
>>> student = ("Haja", "26", "Physics", 9.0)
>>> student[1]
'26'
>>> 
```
### Tuple unpacking (Similar to deconstruction in JS)

```
>>> student
('Haja', '26', 'Physics', 9.0)
>>> name, age, subject, gpa = student
>>> name
'Haja'
>>> age
'26'
>>> subject
'Physics'
>>> gpa
9.0
```

If we want only some specific value (not all) in the tuple, we can unpack, we replace with underscore `_` at the position that we dont need/want. Note that the orders matters

```
>>> name, _, _, _ = student
>>> name
'Haja'
>>> 
```
### Return a tuple from a function and unpack

```
>>> def http_status_code():
...     return 200, "OK"
... 
>>> http_status_code()
(200, 'OK')
>>> code, name = http_status_code()
>>> code
200
>>> name
'OK'
>>> 
```

## Sets

https://www.learnpython.dev/02-introduction-to-python/080-advanced-datatypes/50-sets/#set-cheat-sheet

Datatype that allow to store other immutables types (string, number, all simple data types) in an unsorted way.
Item can be set only once (no duplicate is allowed). Its a collection, therefore there is no other. Which make it very fast to search (use Hash system).

### Create Set
Note. curly braces `{}` are used by both `Set` and `Dictionary` . Therefore we have to be explicite as so `set()` for an empty set

```
>>> set()
set()
>>> {1}
{1}
>>> type({1})
<class 'set'>
>>> 
```

### Duplicated items
The duplicated items will be ignored

```
>>> names = {"Nina", "Max", "Nina"}
>>> names
{'Max', 'Nina'}
>>> len(names)
2
>>> 
```

### Sets cannot take mutable data types like such as List 

Set use a builting `hash` function to reference its items. Hash can be performed only on immutable data type (string, number, ....)

```
>>> {[]}
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: unhashable type: 'list'
>>> 
```

Set can be use to remove duplicate in a list by passing the list as an argument to create the set

```
>>> names = ["Nina", "Haja", "Nina"]
>>> set(names)
{'Haja', 'Nina'}
>>> 
```

Set has length (but no order) and is mutable

### Add from set

Use the `.add(item_to_add)`. Tak eonly one argument

```
>>> colors = {"red", "green", "blue"}
>>> colors.add("yellow")
>>> colors
{'green', 'blue', 'red', 'yellow'}
>>> 
```

### Discard and Remove
Remove from a set with `.discard(item_to_discard)`. It does not throw an error if `item_to_discard` does not 

```
>>> colors
{'green', 'blue', 'red', 'yellow'}
>>> colors.discard("yellow")
>>> colors
{'green', 'blue', 'red'}
>>> 
```

We also have `.remove(item_to_remove)` which does the same thin as discard but will throw an error if `item_to_remove` does not exist in the set

### Update a set (like a merge)

With `.update(sequence_to_add)` will combine `sequence_to_add` to the set. Please note that `.update()` expect a sequence as an argument

```
>>> numbers = {3,4,5}
>>> colors.update(numbers)
>>> colors
{'blue', 3, 4, 5, 'green', 'red'}
>>> 
```
And because a `string` is actually a sequence. The operation would work but the result is not necessary what would one expect

```
>>> colors.update("string")
>>> colors
{'blue', 3, 4, 5, 's', 'r', 'n', 'green', 'g', 't', 'i', 'red'}
>>> 
```

### Operation

#### Search

Check the presence of an item. Same as list and tuple but faster
```
>>> colors = {"red", "black", "green"}
>>> "green" in colors
True
>>> 
```

#### Union

Combine the items of two sets

with `myset.union(other_set)` or `my_set | other_set`

```
>>> rainbow_colors = {"red", "yello", "blue"}
>>> favorite_colors = {"orange","black"}
>>> rainbow_colors.union(favorite_colors)
{'yello', 'blue', 'black', 'orange', 'red'}
>>> more_colors = {"pink", "black", "brown"}
>>> rainbow_colors | more_colors
# Note that pink was picked up only once
{'yello', 'blue', 'black', 'brown', 'pink', 'red'}
>>> 
```
#### Intersection

Intersection create a new set with only items that appears on both sets. Will return empty set if there is no similar items

```
>>> intersection_colors = set()
>>> rainbow_colors
{'yello', 'blue', 'red'}
>>> intersection_colors.add("blue")
>>> new_intersection = rainbow_colors & intersection_colors
>>> new_intersection
{'blue'}
>>> 
```
#### Difference

Return the difference of two or more sets as a new set. (i.e. all elements that are in this set but not the others.)

```
>>> colors_one = {"blue", "red", "pink"}
>>> colors_two = {"brown", "black", "red", "pink"}
>>> diff_colors = colors_one ^ colors_two
>>> diff_colors
{'blue', 'black', 'brown'}
>>> more_colors = {"black", "yello"}
>>> diff_colors = diff_colors.difference(more_colors)
>>> diff_colors
{'blue', 'brown'}
>>> 
```

#### Sort

Since sets have no orders, they are therefore not sortable. One way would be to pass the set to a list that will return a list that can be sorted 

```
>>> not_sortable = {1,2,44,87,16}
>>> not_sortable
{1, 2, 44, 16, 87}
>>> sortable = list(not_sortable)
>>> sortable
[1, 2, 44, 16, 87]
>>> sortable.sort()
>>> sortable
[1, 2, 16, 44, 87]
>>> 
```

## Dictionaries (object?)

https://www.learnpython.dev/02-introduction-to-python/080-advanced-datatypes/60-dictionaries/#dict-ionary-cheat-sheet

Allow to store data in key/value pairs. Dictionnaries are mutable but Keys used must be immutable data types because it uses hash function. 
Checking is a key is in a dictionnary is a very fast operation.

### Creation

for an empty dictionnary `dict()` or `{}`

With some data : 

```
>>> dict()
{}
>>> number = {1: "one", 2: "two"}
>>> number
{1: 'one', 2: 'two'}
>>> 
```
Values can take mutable data type, but not the key because of the hash function it uses to reference its contents
```
>>> {["one"]:1}
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: unhashable type: 'list'
>>> 
```

### Access

There is no order, we access items with the keys

```
>>> my_dic = {"one" : 1, "two" : 2}
>>> my_dic["two"]
2
>>> 
```

With Get. While access with `["key"]` throw an error it the `key` is not listed in the dictionnary, the `.get("key")` methode will return the value if found, otherwise nothing.

```
>>> my_dic.get("four")
>>> my_dic.get("two")
2
>>> 
```

We can return a default value if a `key` is not present by passing a second argument to `.get()`.

```
>>> my_dic
{'one': 1, 'two': 2}
>>> my_dic.get("one")
1
>>> my_dic.get("four")
>>> my_dic.get("four", "default value")
'default value'
>>> 
```


#### Add

Dictionnaries are mutable. Use the square braquets with the key inside and assign with the value

```
>>> my_dic[4] = "Four"
>>> my_dic
{'one': 1, 'two': 2, 4: 'Four'}
>>> my_dic[4] = "New Four"
>>> my_dic
{'one': 1, 'two': 2, 4: 'New Four'}
>>> 
```

### Search

Same as Set and tuples with the key work `in`

```
>>> my_dic
{'one': 1, 'two': 2, 4: 'New Four'}
>>> "one" in my_dic
True
>>> "tree" in my_dic
False
>>> 
```
### combining with update

```
>>> colors = {"p": "pink"}
>>> numbers = {1: "one"}
>>> colors
{'p': 'pink'}
>>> numbers
{1: 'one'}
>>> colors.update(numbers)
>>> colors
{'p': 'pink', 1: 'one'}
>>> 
```

Since the values can be mutable data type we can have list as value for a specific key. Therefore we can apply methodes that mutates data on the value stored at specific key

```
>>> vegetables = {"green": ["spinach"]}
>>> vegetables
{'green': ['spinach']}
>>> vegetables["green"]
['spinach']
>>> vegetables["green"].append("apple")
>>> vegetables["green"]
['spinach', 'apple']
>>>
```

### Get the keys or the values list of a dictionnary 

```
>>> my_dictionary = {"one": 1, "two":2}
>>> keys = my_dictionary.keys()
>>> keys
dict_keys(['one', 'two'])
>>> values = my_dictionary.values()
>>> values
dict_values([1, 2])
>>> 
```

The `.items()` methode will return a list of tuples of the key/value pair

```
>>> items = my_dictionary.items()
>>> items
dict_items([('one', 1), ('two', 2)])
>>> 
```

## 5/ Mutability

https://www.learnpython.dev/02-introduction-to-python/080-advanced-datatypes/65-mutability/#mutability

### Not mutable

`int`, `float`, `decimal`, `str`, `bool` are all not mutable. `tuple` despite being a container type is immutable

### Mutable 

`set`, `list`, `dict` are all mutables


## Booleans

https://www.learnpython.dev/02-introduction-to-python/090-boolean-logic/10-truthiness/#cheat-sheet

### The integer

 0 is falsy. Any other integer are True even negatvie numvers


```
>>> bool(0)
False
>>> bool(10)
True
>>> bool(-10)
True
>>> 
```
### List, Tuple, Set, Dictionary

Empty list, Tuple, Set and Dictionnaries are all falsy unless they have at least a value in it

```
>>> bool({})
False
>>> bool(())
False
>>> bool([])
False
>>> bool(set())
False
```

### String

Empty string is falsy. Becomes true once has at least one characters

## Comparaison

### Less and greater, Less or and greater or

`<` and `>`
`<=` and `>=`

Hint : Upper case string is lower than its lower case

```
>>> "T" < "t"
True
>>> 
```
### Equality

`==`

### Key word `is`

The key wor is check for identity by checking reference in memory 

```
>>> a = [0,1,2]
>>> b = [0,1,2]
# a and be are equal (same items values)
>>> a == b
True

# a is not be: Do not point to the same reference in memory
>>> a is b
False
>>> 
```
### Key word `is not`

Reverse of `is`

```
>>> a = [0,1,2]
>>> b = [0,1,2]
>>> a == b
True
>>> a is b
False
>>> a is not b
True
>>> 
```

### And, Or and Not

https://www.learnpython.dev/02-introduction-to-python/090-boolean-logic/30-and-or-not/#and-or-not-cheat-sheet


#### Or
The or statement will return the thrufty value of the comparaison. If both are True it will return the first one (left side of the comparaison)

```
>>> [] or [1]
[1]
>>> [1] or []
[1]
>>> [1] or [1]
[1]
>>> [1] or [2]
[1]
>>> [2] or [1]
[2]
>>> 
```

#### And

Will return the first `false` value unless both are `true`. If both are true the right side of the comparaison will be returned

```
>>> [] and [1]
[]
>>> [1] and []
[]
>>> [1] and [2]
[2]
>>> [2] and [1]
[1]
>>> 
```

#### Not

Return the reverse

```
>>> not []
True
>>> not True
False
>>> 
```

## Loops and Control

### Looping in a list with For

For item in items list do something

```
>>> colors = ["red", "pink", "blue"]
>>> for color in colors:
...     print(color)
... 
red
pink
blue
>>> 
```
Note, since the for is not a function,`color` will persist in the scope of the function that contain the for loop. Here, `color` will have `blue` as value (the last assigment in the for loop)

```
>>> colors = ["red", "pink", "blue"]
>>> for color in colors:
...     print(color)
... 
red
pink
blue
>>> color
'blue'
>>> 
```

To access the index we have to use the enumerate function applied on the list

```
>>> colors = ["pink", "red", "blue"]
>>> for index, color in enumerate(colors):
...     print(f"Current index is {index} with color {color}")
... 
Current index is 0 with color pink
Current index is 1 with color red
Current index is 2 with color blue
>>> 
```


### Range

We can provide a range to the for loop


### Loop over a dictionary

This loop will return only the keys of the dictionary

```
>>> my_dictionnary = {1: "one", 2:"two", 3:"tree"}
>>> my_dictionnary
{1: 'one', 2: 'two', 3: 'tree'}
>>> for item in my_dictionary:
...     print(item)
... 
one
two
>>> 
```

If we want to access the value. We can use the `.items()` methode on the dictionary. This will return a tuple of key/pair value that can be unpacked to specific variables

```
>>> for number_rep, string_rep in my_dictionnary.items():
...     print(f"The number representation is {number_rep} and the string is {string_rep}")
... 
The number representation is 1 and the string is one
The number representation is 2 and the string is two
The number representation is 3 and the string is tree
>>> 
```

### While loop

Run forever until a condition is match

```
>>> counter = 0
>>> max = 4
>>> while counter < max:
...     print(f"counter {counter}")
...     counter = counter + 1
... 
counter 0
counter 1
counter 2
counter 3
>>> 
```
We can control loops with Break Continue and Return

#### Break 

It will break completly the current loop execution

```
>>> names = ["Jimmy", "Rose", "Max", "Nina", "Phillip"]
>>> for name in names:
...     print(f"Hello {name}")
...     if name == "Nina":
...             break
... 
Hello Jimmy
Hello Rose
Hello Max
Hello Nina
>>> 
```

If we are in a nested loop. The break method will break only the currentl level of the loop and jump back to the parent loop
The `return` key word would also break the loop

#### Continue

This will skip the remaining of the loop and go back to the bigginning of the loop until its condition is met

```
>>> names
['Jimmy', 'Rose', 'Max', 'Nina', 'Phillip']
>>> for name in names:
...     if name != "Nina":
...             continue
...     print(f"Hello, {name}")
... 
Hello, Nina
>>> 
```


## Re-using function from other files.

If the file that contain the function we want to use is in the same directory. We can just import it with with the file name

`import file_that_host_needed_function.py`

Then in the current script, we call call the needed function by callin the file imported concataned with a `.needed_function_name(argument)`

```
output = file_that_host_needed_function.needed_function_name("argument")
```

However, if `needed_function_name` do some print inside his body but we dont want to see the print from the calling script, We have to put a condition in the called function that say that we print only if we are in the `Main` thread. We can do so by wrapping the code in an `if` statement by checking if we are in the main thread

```
if __name__ == "__main___":
  # The following print will print only if we are in the main
  print("We are in the main")
```

## Handling ecxeption to continue a program usin try + except
We must specify the type of `except` we want to handle

```
try:
  int("a") # this is not allowed setting a strin =g as an integer
except ValueError as error:
  print(f"Oops not permitted {error}")
print("We reached the end despite the error") 

>>>Oops not permitted invalid literal for int() with base 10: 'a'
>>>We reached the end despite the error
```

## Import request library 
Install the `requests` library

```
python -m pip install request
```

The request library allow to interaction with APIs. Most API calls will return a JSON file and the request library with turn it into a dictionary

```
import requests
api_repo_search_url = "https://api.github.com/search/repositories"
response = requests.get(api_repo_search_url)
response_json = response.json()
return response_json
```
