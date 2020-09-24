# Learning notes on Python, Algorithms and Data structure

## 1/Environment setup

```
cd
mkdir pyworkshop
cd pyworkshop
python3.7 -m venv env
source env/bin/activate
```

## Starting REPL (Read, Execute, Print, ...)

Command + Shift + P

## Get list of methode for a given type

Get the variable type with 
type (variable);
This will print the variable type, then
dir (type);

## Recommended Coding convention to follow 

PEP8 --> https://pep8.org


## Variables
There is no need to specify the type of the variable when creating it as Python is a dynamic. It is recommended to have them start with lower case and compose with dash (-)
Variables cannot start with number and we must be careful not to overwrite existing data structures as Python allow things like list = 1, which will turn the list data structure into an integer

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

## Operations

```
x = 5
y = 3.0
x + Y --> 8.0 (notice the result being a float)
```

### String
Can be in single quote or double quote. It is recommended to use double quote as it can wrap single quote that are part of the string

### long string
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

```
variable = "Haja"
f"Hello {variable}" --> Hello Haja
```

## concatation
Use the + symbole

```
"Hello" + "world"
```
Strings and Integers cannot be concatenated


## Function 

Formation `def` `function_name` `()` `:` no braquet. Function uses indentations (tab or space) to define its scope.
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

# Advanced data types

## List

https://www.learnpython.dev/02-introduction-to-python/080-advanced-datatypes/10-lists/#list-cheat-sheet

Can be created with two square braquets `[]` or list()
We use comma to separate the items inside the list. Pretty much like `array` in JS 
Items does not need to be all the same type, but in practice it is better

```
name = ["Haja", "Nina", "John"]
```
Get the length of a list 

```
len(name)
#len is globaly available function
```
List retain the order of the items inside --> Need to use index to access the items. The index start at `0`

```
print(name[1]) --> "Nina"
```
Because the items inside List has an order, then we can sort them. They are different way to sort

### First way to sort --> Take the original list and return the a copy of the list that is sorted with `sorted()` built in function.
It basically returns a copy of the list passed to it sorted (the orifinal list wont change)

```
lottery_numbers = [1,4,3423,78,11]
# sorted() is a built in function
sorted(lottery_numbers) --> [1, 4, 11, 78, 3423]
print(lottery_numbers) --> [1, 4, 3423, 78, 11]
```
Sorted take an optiona argument that define the order 

```
sorted(lottery_numbers, reverse=True) --> [3423, 78, 11, 4, 1]
```

### Second way to sort is to do it in place (mutate the original list). It modifies the original list

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
Note that `.remove("arg")` will remove only the first item that match the `arg`
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

# Tuples
https://www.learnpython.dev/02-introduction-to-python/080-advanced-datatypes/30-tuples/#tuple-cheat-sheet

Tuples are UNMMUTABLE. Once create the items inside cannot be changed. Useful for thing like containing a snapshot of datas.

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
## Tuple unpacking (Similar to deconstruction in JS)

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

If we dont want a specific value in the typle to ne unpacked, we replace with underscore `_`

```
>>> name, _, _, _ = student
>>> name
'Haja'
>>> 
```
## Return a tuple from a function and unpack

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






























