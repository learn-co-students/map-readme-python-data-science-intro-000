
# Map in Python

### Introduction

In the last section, we saw how we select a subset of a list by iterating through a list of elements to select only those that match a certain criteria.  In this lesson, we learn how to use the `map` function not to return a subset of elements, but to alter each element in a similar manner.

### First Solve For One Element

Imagine that we have a list of names. 


```python
names = ['Homer', 'Marge', 'Bart', 'Maggie', 'Lisa']
```

We would like to add the name `Simpson` to the end of each name.  Just as we did with `filter`, we can start by writing a function that solves the problem for one element.


```python
def add_simpson(name):
    return name + " Simpson"
```


```python
add_simpson("Homer")
```




    'Homer Simpson'



Great, our method `add_simpson` successfully takes in a string, `name`, and returns that string with the added last name, `Simpson`.

### Then Solve For All

Now we can iterate through the names one by one, and for each name we perform the same operation -- add the last name `"Simpson"`.


```python
def add_simpsons(elements):
    altered = []
    for element in elements:
        altered.append(add_simpson(element))
    return altered
```


```python
simpsons = add_simpsons(names)
simpsons
```




    ['Homer Simpson',
     'Marge Simpson',
     'Bart Simpson',
     'Maggie Simpson',
     'Lisa Simpson']



So notice that unlike what we saw in filtering for elements, there is no `if` statement in this `for` loop.  Instead, the number of elements in our output list is the same as the number of elements in our input list.  However, each one of those elements has been altered.

### Finding what's common

As you may have guessed, using a for loop to alter each element by applying some operation is a common procedure in programming.  Let's write a function that derives the initials of each person's name.


```python
def find_initial(name):
    names = name.split(' ')
    first_name = names[0]
    last_name = names[1]
    return first_name[0] + last_name[0]
```


```python
homer = simpsons[0]
find_initial(homer)
```




    'HS'




```python
def find_initials(elements):    
    altered = []
    for element in elements:
        altered.append(find_initial(element))
    return altered

find_initials(simpsons)
```




    ['HS', 'MS', 'BS', 'MS', 'LS']



Our two functions, are quite similar.

```python

def add_simpsons(elements):
#     altered = []
#     for element in elements:
        altered.append(add_simpson(element))
#     return altered

def find_initials(elements):    
#     altered = []
#     for element in elements:
        altered.append(find_initial(element))
#     return altered
```

The map function, allows us to apply the same operation to each element and return a new list of elements receiving the modified elements from this operation. 


```python
map(add_simpson, names)
```




    <map at 0x1114ca7f0>



However, just as the `filter` function returns a filter object, the `map` function returns a map object. So, in order to get our desired list back, we need to coerce the map object to a list:


```python
list(map(add_simpson, names))
```




    ['Homer Simpson',
     'Marge Simpson',
     'Bart Simpson',
     'Maggie Simpson',
     'Lisa Simpson']




```python
list(map(find_initial, simpsons))
```




    ['HS', 'MS', 'BS', 'MS', 'LS']



So the map function goes through each element and executes the altering function on the current element. Then the return value of the altering function is added as an element to the new list, which is then returned after we coerce the map object to a list.

### Lambda functions

Our functions like `add_simpson` and `find_initial` may work well as stand alone functions to alter a single name.  But Python recognizes that sometimes a programmer wishes to perform an operation once and almost throw it away.  The operation doesn't even need a named function.  Wrapping the operation in a function adds some degree of indirection.

For that reason, we can use `lambda` functions. Let's use the `lambda` function to have all of the names say `"hi"`.


```python
list(map(lambda name: name + ' Simpson says hi.', names))
```




    ['Homer Simpson says hi.',
     'Marge Simpson says hi.',
     'Bart Simpson says hi.',
     'Maggie Simpson says hi.',
     'Lisa Simpson says hi.']



So notice that using a lambda function in python works just like using a normal named function.  However, we can write the function on one line.  A lambda function is declared by writing the keyword `lambda` followed by the argument then the colon to mark the start of the function's body.  The end of the function body is indicated with a comma.


```python
list(map(lambda name: name + ' Simpson says bye.', names))
```




    ['Homer Simpson says bye.',
     'Marge Simpson says bye.',
     'Bart Simpson says bye.',
     'Maggie Simpson says bye.',
     'Lisa Simpson says bye.']



Note that `lambda` functions can also be used with `filter`.  That's another case where we may only need a function once, and then can almost throw it away.


```python
list(filter(lambda name: name.startswith('M'),names))
```




    ['Marge', 'Maggie']



With `filter`, an element is returned so long as the `lambda` function returns a truthy value.


```python
list(filter(lambda name: True,names))
```




    ['Homer', 'Marge', 'Bart', 'Maggie', 'Lisa']



So if the function, or the lambda function always returns `True` then the `filter` function does not return a subset of the collection but the entire collection.

### Summary

In this section, we learned about the `map` function which takes in two arguments. The first argument is the altering function, which operates on each element by passing through the element as an argument and returning a value. The second argument is the list of elements to be iterated through and operated on. The return values of the altering function are appended to a new list, which is returned after we coerce our map object into a list.

Then we finished by learning about lambda functions. Lambda functions can be used with iterators like `filter` and `map` and can be defined in just one line.  We declare a lambda function with the keyword `lambda` followed by the argument, and then a colon to indicate the beginning of the body of the lambda function. 
