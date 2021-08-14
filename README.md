# Map

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
