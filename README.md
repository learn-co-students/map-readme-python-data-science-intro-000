
# Map in Python

### Objectives

* Understand how `map` works in python for mapping a given function to each element of an iterable.
* Differentiate between map and filter functions and identify suitable uses cases for each

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

### Map Function

The map function, allows us to apply the same operation to each element and return a new list of elements receiving the modified elements from this operation. 

A `map()` function is defined in python like this:

```python
map(Function, Sequence)

```

Let's use the map function with `add_simpson` defined above.


```python
map(add_simpson, names)
```




    <map at 0x10eda6860>



However, just as the `filter` function returns a filter object, the `map` function returns a map object. So, in order to get our desired list back, we need to coerce the map object to a list:


```python
list(map(add_simpson, names))
```




    ['Homer Simpson',
     'Marge Simpson',
     'Bart Simpson',
     'Maggie Simpson',
     'Lisa Simpson']



Similarly, we can pass `simpsons` list with `find_initial` to `map` and get the desired output as shown below.


```python
list(map(find_initial, simpsons))
```




    ['HS', 'MS', 'BS', 'MS', 'LS']



So the map function goes through each element and executes the altering function on the current element. Then the return value of the altering function is added as an element to the new list, which is then returned after we coerce the map object to a list.

`map`, just like `filter`, is built into python is always available. It is also computationally more efficient than a manually coded for loop. 

`map` can be used in more advance ways e.g. given multiple sequence arguments, it sends items taken form sequences in parallel as distinct arguments to the function. Let's see this through an example below.

The `pow` built-in python function takes in two numbers as arguments and calculates the result by setting second number as power of first number. Let's see this in action.


```python
pow(2,4)
```




    16



So 2 to the power 4 is 16 as seen above. `map` allows us to pass `pow` function along with two lists as arguments to calculate the powers of elements from first list to elements of second list as shown below:


```python
list(map(pow, [2, 4, 8], [3, 5, 7]))
```




    [8, 1024, 2097152]



This shows that with multiple sequences, `map` expects an N-argument function for N sequences i.e. `pow` requires two arguments and map uses use two lists for mapping elements. 

### Summary

In this section, we learned about the `map` function which takes in two arguments. The first argument is the altering function, which operates on each element by passing through the element as an argument and returning a value. The second argument is the list of elements to be iterated through and operated on. The return values of the altering function are appended to a new list, which is returned after we coerce our map object into a list.
