# Warren Shea's Notes for Python
**Version**: 20191204

```python
#print(f'{x}') VS print("{}".format(x="test"))
#different types (list, tuple, dictionary) : print(f
#def func(*args): #<-- pass in as many tuple args as you want, by convention, always use 'args' # returns tuple
#def func(**kwargs): #<-- pass in a dictionary   # returns dictionary
#lambda expression - one time use/run functions


#Formatted string literals (f-strings) in Python
print(f'{x}')
print("{}".format(x="test"))

#No need to open and close file this way
with open('myfile.txt') as my_new_file:
    contents = my_new_file.read()

for item_name in iteratble:
    print(item_name)

for (a,b) in mylist: #<-- tuple impacting?
    print(a)

for a,b in mylist:
   print (b)

# iterate through dictionary:
# by default, iterating through dictionary only iterates through keys
for key in d.items():
  print(item) <-- prints key and value as tuple
# ^ dictionaries are unordered, no guarantee what you get back is order you put it in

contine, break, pass #<- for loops

for num in range(start,stop[, step])
for num in range(0,10,2) #[0,2,4,6,8]

#https://www.udemy.com/course/complete-python-bootcamp/learn/lecture/9407966#overview
#36. Useful Operators in Python

word = 'abc'
for item in enumerate(word):
    print(item)
(0, 'a')
(1, 'b')
(2, 'c')

word = 'abc'
for index,letter in enumerate(word):
    print(index)
    print(letter)
0
a
1
b
2
c

#zip function
#pairs up lists/combines them

#instring
'a' in 'a world '

#random
from random import shuffle
shuffle(mylist)

from random import randint
randint(0,100)

def name_function():
    '''
    DOCSTRING: Information about the function
    INPUT:
    OUTPUT
    '''
    print()

def func(*args): #<-- pass in as many tuple args as you want, by convention, always use 'args'
    # returns tuple
def func(**kwargs): #<-- pass in a dictionary
    # returns dictionary

#lambda expression - one time use/run functions

#runs the function() on each item of the list, returning the same dimensions of the list, but modified
for item in map(function,list):
    print(item)

#runs the function() on each item of the list where the function returns a value if true or false (e.g. return num%2 = 0)
for n in filter(function,list)
    print(n)

#lambda expression / anonymous function
# instead of
def square(num): return num ** 2
# lamda expression
square = lambda num: num ** 2
square(5) #returns 25

#using lamda and map function
list(map(lambda num: num**2, mynums))

# Scope
# LEGB Rule:
# L: Local - name assigned within a function (def or lambda) and not declared global
# E: Enclosing function local - names in local scope
# G: Global (module) - names assigned at top-level of a module file or declared global in def within file
# B: Built-in (Python) - names preassigned in the built-in names modules

#Changing Global namespace
x = 50
def func():
    global x
    x = 200 #will do it on global level

#A better way:
x = 50
def func(x):
    x = 200
    return x
x = func(x)
```