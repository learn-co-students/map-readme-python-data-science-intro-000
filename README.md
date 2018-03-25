
# Map in Python

### Introduction

In the last section, we saw how we select a subset of a list by iterating through a list of elements to select only those that match a certain criteria.  In this lesson, we learn how to use the `map` function not to select a subset of elements, but to alter each element in a similar manner.

### First solve it for one element

Imagine that we have a list of names. 


```python
names = ['Homer', 'Marge', 'Bart', 'Maggie', 'Lisa']
```

We would like to add the name `Simpson` to the end of each name.  Just like as we did with `filter`, we can start by writing a function that solves the problem for one element.


```python
def add_simpson(name):
    return name + " Simpson"
```


```python
add_simpson("Homer")
```




    'Homer Simpson'



### Then solve for all

So now we can iterate through the names one by one, and for each name perform the same operation -- add the last name of `"Simpson"`.


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



So notice that unlike what we saw in filtering for elements, there is no `if` statement in this `for` loop.  Instead, the number of element in our output list is the same as the number of elements in our input list.  However, each one of those elements have been altered.

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
find_initial(simpsons[0])
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

The map function, allows us to apply the same operation to each element and return the list of elements receiving this operation. 


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



So the map function goes through each element, and executes the altering function on the current element, the return value of the altering function is added as an element to the returned list.

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



Just like filter returns each element for which the first function returns a truthy value.

### Summary

In this section, we learned about the `map` function.  The `map` function takes two arguments.  The second argument is the list of elements to be iterated through and operated on.  The first argument is an altering function that operates each element one by one by passing through the element as an argument and returning a value.  The return values of the altering function comprises of the elements of the newly returned list.    

Then we ended by learning about lambda functions.  Lambda functions can be used with iterators like `filter` and `map` and can be defined in just one line.  We declare a lambda function with the keyword `lambda` followed by the argument, and then a colon to indicate the beginning of the body of the lambda function. 
