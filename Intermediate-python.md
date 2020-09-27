# Convert between data type

## From string to a list
This is usefull when getting a CSV file and convert into a list

```
>>> my_data = "one,two,tree,four,five"
>>> my_data.split(",")
['one', 'two', 'tree', 'four', 'five']
>>> 
```

It can also be unpacked

```
>>> on,tw,tr,fo,fi = my_data.split(",")
>>> on
'one'
>>> tw
'two'
>>> tr
'tree'
>>> fo
'four'
>>> fi
'five'
>>> 
```
To reverse from list back to string is `.join()`

```
>>> my_list = my_data.split(",")
>>> my_list
['one', 'two', 'tree', 'four', 'five']
>>> ",".join(my_list)
'one,two,tree,four,five'
>>> 
```
## From string to integer or float and vice versa

```
>>> int("5")
5
>>> 

>>> float("5.3")
5.3
>>> 

>>> str(6.7)
'6.7'
>>> 
```

## String to list

String are just sequence in python, the sequence will be split in list item
```
>>> my_str = "Hello"
>>> my_list = list(my_str)
>>> my_list
['H', 'e', 'l', 'l', 'o']
>>>
```

back to a strig with `"".join()`

```
>>> back_to_str = "".join(my_list)
>>> back_to_str
'Hello'
>>> 
```

## Fom list to set

Useful to remove duplicate

```
>>> names = ["Haja", "Bob", "Haja"]
>>> no_duplicates = set(names)
>>> no_duplicates
{'Haja', 'Bob'}
>>> 
```
## From set to list 

Use sorted method on the set to enforce order back to a list

```
>>> names = ["Haja", "Bob", "Haja"]
>>> no_duplicates = set(names)
>>> no_duplicates
{'Haja', 'Bob'}
>>> back_to_list = sorted(no_duplicates)
>>> back_to_list
['Bob', 'Haja']
>>> 
```

#  Comprehension

## List comprehension

Take a for loop and condence it into one statement

Consider this code that convert a list of names to upper case

```
>>> names = ['Haja', 'Bob', 'Indra']
>>> upper_name = []
>>> for name in names:
...     upper_name.append(name.upper())
... 
>>> upper_name
['HAJA', 'BOB', 'INDRA']
>>> 
```
It can be done so : [`action we want to perform` `then the loop`]

```
>>> names = ["Bro", "Bra", "Bri"]
>>> upper = [name.upper() for name in names]
>>> upper
['BRO', 'BRA', 'BRI']
>>> 
```

Get the square of a number in a range (below 0 to 5)

```
>>> [num * num for num in range(6)]
[0, 1, 4, 9, 16, 25]
>>> 
```

The left side of the list comprehension define what we want to obtain and the right side the loop
i.e we wnat to get the list of `tuples` with the length of the names in a list of names 

```
>>> names = ['Haja', 'Bob', 'Indra']
>>> [("lenght", len(name)) for name in names]
[('lenght', 4), ('lenght', 3), ('lenght', 5)]
>>> 
```

### Use conditional statement in List comprehension

We had this 

```
>>> [num * num for num in range(6)]
[0, 1, 4, 9, 16, 25]
>>> 
```

But we want to get only the even number (divisible by 2). We can use `modulo` for that
`modulo` return 0 when a number is divisible by 2

Conditional statements go on the right side 

```
>>> [num * num for num in range(6) if num % 2 == 0]
[0, 4, 16]
>>> 
```

### List operations

##### Sum 

Return the sum of the elements in a list 

```
>>> my_list = [num * num for num in range(6)]
>>> my_list
[0, 1, 4, 9, 16, 25]
>>> list_sum = sum(my_list)
>>> list_sum
55
>>> 

```
#### min & max

```
>>> my_list
[0, 1, 4, 9, 16, 25]
>>> min(my_list)
0
>>> max(my_list)
25
```
#### sorting


```
>>> sorted_list = sorted(my_list)
>>> sorted_list
[0, 1, 4, 9, 16, 25]
>>> 
```

```
>>> sorted_list = sorted(my_list, reverse=True)
>>> sorted_list
[25, 16, 9, 4, 1, 0]
>>> 
```

## Set comprehension

To get a set, we basically use the same syntax/construction as for the list, but we replace the square braquet `[]` with curly braquets `{}`

```
>>> {num * num for num in range(12)}
{0, 1, 64, 121, 4, 36, 100, 9, 16, 49, 81, 25}
>>> 
```

## Dictionary comprehension

Just have to add the column that define keys vs values. Below the actual number is the key and the square is the value

```
>>> {num: num * num for num in range(12)}
{0: 0, 1: 1, 2: 4, 3: 9, 4: 16, 5: 25, 6: 36, 7: 49, 8: 64, 9: 81, 10: 100, 11: 121}
>>>
```

# Generators

List/Set/Dic comprehension build every output in memory, so can be heavy/inneficient on long run ...

As we work with bigger data set

Generators build what we needs on the fly like `range(6)` ... but they cannot be assigned to a variable to access through keys and need to be passed inline or to a loop

## Make a generators comprenhension/expression

By replacing the wrappers `[]` for list, and `{}` for set and dic with `()`. We will get an object called `Generator expression`

```
>>> names
['Haja', 'Bob', 'Indra']
>>> [len(name)for name in names]
[4, 3, 5]
```
Replaced wit `()` as wrapper
```
>>> (len(name)for name in names)
<generator object <genexpr> at 0x107682b50>
>>> 
```
Just like range the value will be calculated as we need them (generaly when we loop over it)

The GC can be passed to other methods. Lets say a set

```
>>> set( (len(name)for name in names) )
{3, 4, 5}
>>> 
```
The above is much more efficient 

### passing a generators expression to methods (sum, max, min)

```
>>> set( (len(name)for name in names) )
{3, 4, 5}
>>> max( (len(name)for name in names) )
5
>>> min( (len(name)for name in names) )
3
>>> sum( (len(name)for name in names) )
12
>>> 
```

### assignment

The only way a generators can be processed outside of an inline procession is to pass it to a loop.
They dont have to have an end because there is no memory assignment. It knows only where it is currently and where to go next.

```
>>> my_gen = (num * num for num in range(2))
>>> for num in my_gen:
...     print(num)
... 
0
1
>>> 
```

Also note that generators are not reusable/persistant. Once consumed it will be freed from the memory


# Slicing
Slice works on all data type that has an order (list, tuple)
Create sub (copy) list/tuple from an list/tuple
## String


```>>> my_list = "Hello, world"
>>> my_list[0]
'H'
>>> my_list[0:4]
'Hell'
>>> my_list[-1]
'd'
>>> my_list[:5]
'Hello'
>>> my_list[6]
' '
>>> my_list[:6]
'Hello,'
>>> my_list[6:]
' world'
>>> 
```

## List

```
>>> names = ["Peter", "Haja", "Bob", "Henry"]
>>> names[1:2]
['Haja']
>>> names[:3]
['Peter', 'Haja', 'Bob']
>>> names[3:]
['Henry']
>>> names[-1]
'Henry'
>>> names[2:-1]
['Bob']
>>> 
```

### List copy vs reference

With the equal operation `=`, we are actualy passing a reference to memory to the variable that receive it.
There for a change on the new variable will actually change what its in memory 

```
>>> names = ["Peter", "Haja", "Bob", "Henry"]
>>> new_names = names
>>> new_names
['Peter', 'Haja', 'Bob', 'Henry']
>>> new_names.append("Tom")
>>> new_names
['Peter', 'Haja', 'Bob', 'Henry', 'Tom']
>>> names
['Peter', 'Haja', 'Bob', 'Henry', 'Tom']
>>> 
```

So to get a copy of a list whitout changing the original data, we have to use slice that will return a copy

```
>>> names
['Peter', 'Haja', 'Bob', 'Henry', 'Tom']
>>> more_names = names[:]
>>> more_names
['Peter', 'Haja', 'Bob', 'Henry', 'Tom']
>>> more_names.append("John")
>>> more_names
['Peter', 'Haja', 'Bob', 'Henry', 'Tom', 'John']
>>> names
['Peter', 'Haja', 'Bob', 'Henry', 'Tom']
>>> 
```
### negative indexing


```
>>> names
['Peter', 'Haja', 'Bob', 'Henry', 'Tom']
>>> names[-1]
'Tom'
>>> names[-3]
'Bob'
>>> names[:-3]
['Peter', 'Haja']
>>> 
```

### Third argument of slicing

The third argument define the step (by default 1) we want to take

```
>>> my_list = list(range(9))
>>> my_list
[0, 1, 2, 3, 4, 5, 6, 7, 8]
# step by 2 (third arg) runing from beginig (first arg) to the end (second)
>>> my_list[::2]
[0, 2, 4, 6, 8]
>>> 
```

# Zip function

Combine the values of two list. Same like generators it will return a loopable object. 

```
>>> players = ["Haja", "Tom", "John"]
>>> scores = [10, 3, 7]
>>> zip(players, scores)
<zip object at 0x1076ba5f0>
>>> for item in zip(players, scores):
...     print(item)
... 
('Haja', 10)
('Tom', 3)
('John', 7)
>>> 
```

Now we want a list of tuple. We can use the unpacking method

```
>>> for name, score in zip(players,scores):
...     print(f"Name: {name} had a scrore of {score}")
... 
Name: Haja had a scrore of 10
Name: Tom had a scrore of 3
Name: John had a scrore of 7

>>> # With a comprehension
>>> [f"Name {name} and score is {score}" for name, score in zip(players, scores)]
['Name Haja and score is 10', 'Name Tom and score is 3', 'Name John and score is 7']
```

To see what is inside the returned object from the zip (this apply to generators as well) we pass it to a list

```
>>> list(zip(players, scores))
[('Haja', 10), ('Tom', 3), ('John', 7)]
>>> 
```

The list must have the same lenght for a balanced output. Otherwise the extra element that did not have correspondance is ignored  

```
>>> list_one = ["a", "b", "c"]
>>> list_two = [1, 2]
>>> list(zip(list_one,list_two))
[('a', 1),
```

## From list of tuple to a dictionnary 

### With list comprehension
```
>>> list(zip(players, scores))
[('Haja', 10), ('Tom', 3), ('John', 7)]
>>> {name: score for name, score in zip(players, scores)}
{'Haja': 10, 'Tom': 3, 'John': 7}
>>> 
```

### with dict()

```
>>> dict(list(zip(players, scores)))
{'Haja': 10, 'Tom': 3, 'John': 7}
>>> 
```


# Object Oriented Program

Everything in Python are objects. We can se them as generic containers to group concept together

## Classes

### Self

If we want to pass an argument to initialise the instance of a classe we use a special notation called constructor

`def` + `__init__` + `(self, arg_for_instance_initialisation)`

```
class Car:
  runs = True

  # the constructor
  def __init__(self, name):
    print(f"New car ! ")
    self.name = name
  
  def start(self):
    if self.runs:
      print(f"Car is started {self.name}")
    else:
      print(f"{self.name} is broken")
```


### Making classes readable/friendly

Add the folowing special methods to the class

```
  # This methode is to help understanding our class
  # by providing a readeable string (friendly) when we print an 
  # instance of the class
  def __str__(self):
    return f"My car the {self.name} currently {self.runs}"

  # this allow to print the class with all of the arguments that is expected
  def __repr__(self):
    return f"Car {self.name}"
```

then

```
new_car = Car("BMW")
print(new_car) --> My car the BMW currently True
print(repr(new_car)) ---> Car BMW
```

## Inheritance

Share properties/attributes between each other
We pass the more generic class as a parameters of the class that inherite from it. 
Then we use the `super` keyword to hook the sub class with the constructor of it more generic

```
## Create a more generic class
class Vehicule:
  
  def __init__(self, make, model, fuel="gas"):
    self.make = make
    self.model = model
    self.fuel = fuel
    
  def is_fuel_efficient(self):
    if self.fuel == "gas":
      return False
    else:
      return True    

# An class that will inherite from vehicule
class Car(Vehicule):
  def __init__(self, make, model, fuel="gas", number_of_wheels=4):
    # the super key word lock with the more generic class
    # it will basically call the constructor of the class Vehicule
    super().__init__(make, model, fuel)
    # parameter that is specific to the Car class (do not exist in vehicule)
    self.number_of_wheels = number_of_wheels
    
four_by_four = Vehicule("Tesla", "S3", "petrol")
my_sub = Car("Subaru", "Flyer")
print(my_sub.is_fuel_efficient()) --> False (defaulted to "gas", since it was not initialised)
 ```

The subclass can access all methodes that are present in the parent class. Here i.e 


# Debugging

In the terminal, add `-i` options to run the file we want to execute. This will automatically open a REPL in wich we can then inspect verious status, type, methode, variables ...

```
python -i path/to/my/file.py
```

# Exceptions



