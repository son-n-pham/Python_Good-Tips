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
- It functionality is not as our expectation
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
