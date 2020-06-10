# Lists

## What is a List?

A *list* is a collection of items in a particular order.  You can make a list that includes the letters of the alphabet, the digits from 0-9, or the names of people in your family.  You can put anything into a list, and the items in your list don't have to be related in any particular way.  Because a list usually contains more than one element, it's a good idea to make the name of your list plural, such as `letters`, `digits`, or `names`.  

In Python, square brackets ([ ]) indicate a list, and individual elements in the list are separated by commas.  Here is a simple example of a list that contains a few kinds of bicylces:  

```py linenums="1"
bicylces = ['trek', 'cannondale', 'redline', 'specialized']
print(bicylces)
```
If you ask Python to print a list, Python returns its representation of the list, including the square brackets:

```py linenums="1"
['trek', 'cannondale', 'redline', 'specialized']
```  
Because this isn't the output you want your users to see, let's learn how to access the individual items in a list.  

### Accessing Elements in a List  

Lists are ordered collections, so you can access any element in a list by telling Python the position, or *index*, of the item desired.  To access an elemenet in a list, write the name of the list followed by the index of the item enclosed in square brackets.  

For example, let's pull out the first bicycle in the list `bicycles`:

```py linenums="1"
bicylces = ['trek', 'cannondale', 'redline', 'specialized']
print(bicylces[0])
```

??? warning "Index Positions"
	Just like in C, and most other programming languages, **index positions start at 0, not 1**.  This is usually something that takes some time for beginner programmers to commit to memory.  It is also useful to remember that you can count backwards in a list as well, with the last element in a list being located at position [-1].

When you print out a single item from a list, Python will return just that element without square brackets:  

```py linenums="1"
trek
```
We can also use the `.title()` method, discussed in [variables and simple data types](https://docs.nicklyss/py-data-types/#using-variables-in-strings).  This will capitalize the first letter of the element:  

```py linenums="1"
bicylces = ['trek', 'cannondale', 'redline', 'specialized']
print(bicylces[0].title())
```
The above example would print out the first element as follows:  

```py linenums="1"
Trek
```  
### Using Individual Values from a List 

You can use individual values from a list just as you would any other variable. For example, you can use f-strings to create a message based on a value from a list.  

Let's try pulling the first bicycly from the list and composing a message using that value:  

```py linenums="1"
bicylces = ['trek', 'cannondale', 'redline', 'specialized']
message = f"My first bicycle was a {bicycles[0].title()}."
print(message)
``` 

This code would have the following output:  

```
My first bicycles was a Trek.
``` 

## Changing, Adding, and Removing Elements  

Most lists you create will be dynamic, meaning you'll build a list and then add and remove elements from it as your program runs its course.  For example, you might create a game in which a player has to shoot aliens out of the sky.  You could store the initial set of aliens in a list and then remove an alien from the list each time one is shot down.  Each time a new alien appears on the screen, you add it to the list.  Your list of aliens will increase and decrease in length throughout the course of the game.  

### Modifying Elements in a List  

The syntax for modifying an element is similar to the syntax for [accessing an element in a list](https://docs.nicklyss.com/py-lists/#accessing-elements-in-a-list).  To change an element, use the name of the list followed by the index of the element you want to change, and then provide the new value you want that item to have.  

For example, let's say we have a list of motorcycles, and the first item in the list is `'honda'`.  How would we go about changing the value of the first item?  

```py linenums="1"
motorcycles = ['honda', 'yamaha', 'suzuki']
print(motorcycles)

motorcycles[0] = 'ducati'
print(motorcycles)
``` 

The first code set defines the original list, with `'honda'` as the first element.  The second code set changes the value of the first item (`[0]`) to `'ducati'`.  The output shows the first item ahs indeed been changed, and the rest of the list stays the same.  

```
['honda', 'yamaha', 'suzuki']
['ducati', 'yamaha', 'suzuki']
``` 

Note: You can change the value of any item in a list, not just the first.  

### Adding Elements to a List  

You might want to add a new element to a list for many reasons.  For example, you might want to make new aliend appear in a game, add new data to a visualization, or add new registered users to a website you've built.  Python provides several  ways to add new data to existing lists.  

#### Appending Elements to the End of a List  

The simplest way to add a new element to a list is to *append* the item to the list.  When you append an item to a list, the new element is added to the end of the list.  Using the same list we had in the previous example, we'll add the new element `'ducati'` to the end of the list:  

```py linenums="1"
motorcycles = ['honda', 'yamaha', 'suzuki']
print(motorcycles)

motorcycles.append('ducati')
print(motorcycles)
```

The `append()` method adds `'ducati'` to the end of the list without affecting any of the other elements in the list:  

```
['honda', 'yamaha', 'suzuki']
['honda', 'yamaha', 'suzuki', 'ducati']
```  

The `append()` method makes it easy to build lists dynamically. For
example, you can start with an empty list and then add items to the list
using a series of append() calls. Using an empty list, let’s add the elements
`'honda'`, `'yamaha'`, and `'suzuki'` to the list:  

```py linenums="1"
motorcycles = []

motorcycles.append('honda')
motorcycles.append('yamaha')
motorcycles.append('suzuki')

print(motorcycles)
```  

The resulting list looks exactly the same as the lists in previous examples:  

```
['honda', 'yamaha', 'suzuki']
```  
Building lists this way is very common, because you often won’t know
the data your users want to store in a program until after the program is
running. To put your users in control, start by defining an empty list that
will hold the users’ values. Then append each new value provided to the list
you just created.  

#### Inserting Elements into a List  

You can also add a new element at any position in your list by using the `insert()` method.  You do this by specifying the index of the new element and the value of the new item:  

```py linenums="1"
motorcycles = ['honda', 'yamaha', 'suzuki']

motorcycles.insert(0, 'ducati')
print(motorcycles)
```
The above code inserts the value `'ducati'` at position `0`.  So running this program will have the following output:  

```
['ducati', 'honda', 'yamaha', 'suzuki'] 
```
### Removing Elements from a List  

Often, you'll want to remove an item or a set of items from a list.  You can remove an item according to its position in the list or according to its value.  

#### Removing an Item using the `del` Statement  

If you know the position of the item you want to remove from a list, you can use the `del` statement.  

```py linenums="1"
motorcycles = ['honda', 'yamaha', 'suzuki']
print(motorcycles)

del motorcycles[0] 
print(motorcycles)
```
The `del` statement will remove the item at index `[0]` from the list `motorcycles`.  If you were to run the above code you would get the following result:  

```
['honda', 'yamaha', 'suzuki']
['yamaha', 'suzuki']
```
#### Removing an Item using the `pop()` Method

Sometimes you'll want to use the value of an item after you remove it from a list.  For example, you might want to get the *x* and *y* position of an alien that was just shot down, so you can draw an explosion at that position.  In a web application, you might want to remove a user from a list of active member and then add that user to a list of inactive members.  

The `pop()` method removes the last item in a list, but it lets you work with them after removing it.  The term `pop` comes from thinking of a list as a stack of items and popping one item off the top of a stack.  In this analogy, the top of a stack corresponds to the end of a list.  

Let's pop a motorcycle from a list of motorcycles:  

```py linenums="1"
motorcycles = ['honda', 'yamaha', 'suzuki']
print(motorcycles)

popped_motorcycle = motorcycles.pop()
print(motorcycles)
print(popped_motorcycle)
```  

We start by defining and printing the list `motorcycles`.  Next, we pop a value (`suzuki`) from the list and store that value in the variable `popped_motorcycle`.  Finally, we print the lists to show that a value has been successfully removed from the initial list.  Then we print the popped list and prove we still have access to it.  The above code would yield the following result:  

```
['honda', 'yamaha', 'suzuki']
['honda', 'yamaha']
suzuki
```  

How might this `pop()` method be useful?  Imagine that the motorcycles in the list are store in chronological order according to when we owned them.  If this is the case, we can use the `pop()` method to print a statement about the last motorcycle we bought:  

```py linenums="1"
motorcycles = ['honda', 'yamaha', 'suzuki']

last_owned = motorcycles.pop()
print(f"The last motorcycle I owned was a {last_owned.title()}.")
```
The output of the above would be: 

```
The last motorcycle I owned was a Suzuki.
```

#### Popping Items from any Position in a List  

We can use `pop()` to remove an item from any position in a list by including the index of the item you want to remove in parenthese:  

```py linenums="1"
motorcycles = ['honda', 'yamaha', 'suzuki']

first_owned = motorcycles.pop(0)
print(f"The first motorcycle I owned was a {first_owned.title()}.")
```
We start by popping the first motorcycle in the list (located at index `0`), and then we print a message about the motorcycle.  The output is a simple sentence describing the first motorcycle owned: 

```
The first motorcycle I owned was a Honda
``` 
Remember that each time we use `pop()`, the item we were working with is no longer stored in the list.  

??? tip "When to use `del` or `pop()`"
	When you want to delete an item from a list	and not use that item in any way, use the `del` statement; if you want to use an item as you remove it, use the `pop()` method.  

#### Removing an Item by Value

Sometimes you won't know the position of the value you want to remove from a list.  If you only know the value of the item you want to remove, you can use the `remove()` method.  

For example, let's say we want to remove the value `'ducati'` from the list of motorcycles:  

```py linenums="1"
motorcycles = ['honda', 'yamaha', 'suzuki', 'ducati']
print(motorcycles)

motorcycles.remove('ducati')
print(motorcycles)
```
The above code tells Python to find and remove `'ducati'` from within the `motorcycles` list. It would give the following result when ran:  

```
['honda', 'yamaha', 'suzuki', 'ducati']
['honda', 'yamaha', 'suzuki'] 
```  
You can also use the `remove()` method to work with a value that's being removed form a list.  Let's remove the value `'ducati'` and print a reason for removing it from the list: 

```py linenums="1"
motorcycles = ['honda', 'yamaha', 'suzuki', 'ducati']
print(motorcycles)

too_expensive = 'ducati'
motorcycles.remove(too_expensive)
print(motorcycles)
print(f"\nA {too_expensive.title()} is too expensive for me.")
```  
After defining the list on line 1, we assign the value `'ducati'` to a variable called `too_expensive`.  We then use this variable to tell Python which value to remove from the list.  `'ducati'` is removed from the list, but is still accessible through the variable `too_expensive`, allowing us to print a statement about why we removed `'ducati'` from the list of motorcycles.  

The code above would have the following output:  

```
['honda', 'yamaha', 'suzuki', 'ducati']
['honda', 'yamaha', 'suzuki']

A Ducati is too expensive for me.
```

??? warning "Note on `remove()`"
	The `remove()` method deletes only the first occurrence of the value you specify. If there’s a possibility the value appears more than once in the list, you’ll need to use a loop to make sure all occurrences of the value are removed. 

### Organizing a List

Often, your lists will be created in an unpredictable order, because you can't always control the order in which your users provide their data.  Although this is unavoidable in most circumstances, you'll frequently want to present your information in a particular order.  Sometimes you'll want to preserve the original order of your list, and other times you'll want to change the original order.  Python provides a number of different ways to organize your lists, depending on the situation.  

#### Sorting a List Permanently with the `sort()` Method  

Python's `sort()` method makes it relatively easy to sort a list.  Imagine we have a list of cars and want to change the order of the list to store them alphabetically.  To keep the task simple, let's assume that all the values in the list are lowercase:  

```py linenums="1"
cars = ['bmw', 'audi', 'toyota', 'subaru']
cars.sort()
print(cars)
```
The `sort()` method, shown above changes the order of the list permanently.  The cars are now in alphabetical order, and we can never revert to the original order:  

```
['audi', 'bmw', 'subaru', 'toyota'] 
``` 
You can also sort this list in reverse alphabetical order by passing the argument `reverse=True` to the `sort()` method.  The following example sorts the list of cars in reverse alphabetical order: 

```py linenums="1"
cars = ['bmw', 'audi', 'toyota', 'subaru']
cars.sort(reverse=True)
print(cars)
```

#### Sorting a List Temporarily with the `sorted()` Function  

To maintain the original order of a list but present it in a sorted order, you can use the `sorted()` function.  The `sorted()` function lets you display your list in a particular order but doesn't affect the actual order of the list.  Let's try this function on the list of cars:  

```py linenums="1"
cars = ['bmw', 'audi', 'toyota', 'subaru']

print("Here is the orginal list:")
print(cars)

print("\nHere is the sorted list:")
print(sorted(cars))

print("\nHere is the original list again:")
print(cars)
```

This should have the following output:  

```
Here is the orginal list:
['bmw', 'audi', 'toyota', 'subaru']

Here is the sorted list:
['audi', 'bmw', 'subaru', 'toyota']

Here is the original list again:
['bmw', 'audi', 'toyota', 'subaru']
```

??? warning "Note on Sorting"
	Sorting a list alphabetically is a bit more complicated when all the values are not in lowercase. There are several ways to interpret capital letters when determining a sort order, and specifying the exact order can be more complex than we want to deal with at this time. 

#### Printing a List in Reverse Order 

To reverse the original order of a list, we can use the `reverse()` method.  If we originally stored the list of cars in chronological order according to when we owned them, we could easily rearrange the list into reverse chronological order:  

```py linenums="1" 
cars = ['bmw', 'audi', 'toyota', 'subaru']
print(cars)

cars.reverse()
print(cars)
```
After running this code will will get the following result:  

```
['bmw', 'audi', 'toyota', 'subaru']
['subaru', 'toyota', 'audi', 'bmw']
```
The `reverse()` method changes the order of a list permanently, but you can always simply run the `reverse()` function again to get back to the original order.  

#### Finding the Length of a List  

You can quickly find the length of a list by using the `len()` funtion.  The list in this example has four items, so the output will be the integer 4:  

```py linenums="1"
cars = ['bmw', 'audi', 'toyota', 'subaru']
len(cars)
``` 
### Avoiding Index Errors When Working with Lists 

One type of error is common when you're working with lists for the first time.  Let's say we have a list with three items, and you ask for the fourth item:  

```py linenums="1"
motorcycles = ['honda', 'yamaha', 'suzuki']
print(motorcycles[3])
``` 
Running this code results in an *index error*:  

```py linenums="1"
---------------------------------------------------------------------------
IndexError                                Traceback (most recent call last)
<ipython-input-10-9811709cfb18> in <module>
      1 motorcycles = ['honda', 'yamaha', 'suzuki']
----> 2 print(motorcycles[3])

IndexError: list index out of range
```
Python attempts to give you the item at index *3*, but when it searches the list, there is no item in index 3 in `motorcycles`.  You must remember that indexing starts at 0 in Python.  

??? warning "Note on Index Errors"
	If an index error occurs and you can’t figure out how to resolve it, try printing your list or just printing the length of your list. Your list might look much different than you thought it did, especially if it has been managed dynamically by your program. Seeing the actual list, or the exact number of items in your list, can help you sort out such logical errors.  
