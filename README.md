# lamda
lambda is used to replace simple function

Example:
```Python
# Normal function
def double(x):
  return x*2
  
# Re-write by using lambda
double = lambda x: x*2
```
```Python
# Normal function
def double_or_square(x):
  if x%2 == 0:
    return x*2
  else:
    return x**2
  
# Re-write by using lambda
double = lambda x: x*2 if x%2==0 else x**2
```

# map() higher-order function

maps() are higher-order function with below syntax:

```Python
returned_map_object = map(function, iterable)
```

map() returns a map object, which can be converted into a list by ***list(returned_map_object)

![Map()-Function](https://user-images.githubusercontent.com/79841341/129447756-46aba022-f828-40f4-9a0a-410756fbb131.gif)

map() can be used with lambda.

Below is the an example of map with another function and with lambda function:

```Python
# double function to double the input:
def double(x):
  return x*2

# input list of integer int_list
int_list = [3, 6, 9]

# map() with double function
doubled = map(double, int_list)

# print out the result
print(list(doubled)

################################
# Combine map() and lambda
doubled_1 = map(lambda x: x*2, int_list)
```

# filter() higher-order function

It is similar to map by taking 2 arguments, which is a function and a list

![image](https://user-images.githubusercontent.com/79841341/129448975-865f27a1-1b13-4dfc-a96d-638cf5316d75.png)

![Filter()-Function (1)](https://user-images.githubusercontent.com/79841341/129448997-24ea6dcf-54bf-4c0d-8d07-91475e26e6cb.gif)

# reduce() higher-order function

This function is different from map() and filter():
- It needs to be import from ***functools*** module
![Reduce()-Function](https://user-images.githubusercontent.com/79841341/129449142-50872890-8347-43ad-9593-2fdee4dca8a7.gif)

Example:

```Python
letters = ['r', 'e', 'd', 'u', 'c', 'e']

# remember to import the reduce function
from functools import reduce

# store the result of your reduce function in the variable word
word = reduce(lambda x,y: x+y, letters)

# print word
print(word)

# The result should be "reduce" in the console
```

# Decorator

```Python
# 1. Functions are objects
def add_five(num):
  return num+5

print(add_five)

# RESULT
# <function add_five at 0x7f07b9bc8dd0>

#####################################

# 2. Functions within functions
def add_five(num):
  def add_two(num):
    return num+2

  num_plus_two = add_two(num)
  print(num_plus_two + 3)

add_five(10)

# RESULT
# 15

#####################################

# 3. Returning functions from functions
def get_math_function(operation): # + or -
  def add(n1, n2):
    return n1 + n2
  def sub(n1, n2):
    return n1 - n2

  if operation == '+':
    return add
  elif operation == '-':
    return sub

add_function = get_math_function('+')
print(add_function)
print(add_function(1,2))

# RESULT:
# <function get_math_function.<locals>.add at 0x7f07b9bb1170>
# 3

#####################################

# 4. Decorating a function
# We call it as decorated function as it is decorating print_my_name() function
# with print("Professor:") above. This is done by putting the target function
# into a wrapper function.

def title_decorator(print_name_function):
  def wrapper():
    print("Professor:")
    print_name_function()
  return wrapper

def print_my_name():
  print("Mike")

decorated_function = title_decorator(print_my_name)

decorated_function()

# RESULT:
# Professor:
# Mike

#####################################

# 5. Decorators
# Instead of calling decorated_function = title_decorator(print_my_name)
# We just use @title_decorator just before the targeted function, then
# we can that targeted function directly and it will be decorated.

def title_decorator(print_name_function):
  def wrapper():
    print("Professor:")
    print_name_function()
  return wrapper

@title_decorator
def print_my_name():
  print("Mike")

print_my_name()

# RESULT:
# Professor:
# Mike

#####################################

# 6. Decorators with Parameters
# Targeted function can have parameter, which can be passed to wrapper
# by adding *args, **kargs. *args for positional parameters as a list
# and *kargs for position paramters as dictionary

def title_decorator(print_name_function):
  def wrapper(*args, **kargs):
    print("Professor:")
    print_name_function(*args, **kargs)
  return wrapper

@title_decorator
def print_my_name(first_name, last_name):
  print(f"{first_name} {last_name}")

print_my_name("Son", "Pham")

# RESULT:
# Professor:
# Son Pham
```
