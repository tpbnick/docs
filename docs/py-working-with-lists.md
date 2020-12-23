# Working with Lists

## Looping Through an Entire List 
You'll often want to run through all entries in a list, performing the same task with each item.  For example, in a game you might want to move every element on the screen by the same amount, or in a list of numbers you might want to perform the same statistical operation on every element.  Or perhaps, you'll want to display each headline from a list of articles on a website.  When you want to do the sam eaction with every item in a list, you can use Python's `#!py for` loop.  

Let's say we have a list of magician's names, and we want to print out each name in the list.  We could do this by retrieving each name from the list individually, but this approach could cause several problems.  For one, it would be repetitive to do this with a long list of names.  Also, we'd have to change our code each time the list's length changed.  A `#!py for` loop avoids both of these issues by letting Python manage these issues internally.  

Let's use a `#!py for` loop to print out each name in a list of magicians:  

```py linenums="1"
magicians = ['alice', 'david', 'carolina']
for magician in magicians:
	print(magician)
```
We begin by defining the list (`magicians`).  Next, we define a `#!py for` loop.  This line tells Python to pull a name from the list `magicians`, and associate it with the variable `magician`.  Finally, we tell Python to print the name that's been assigned to `magician`.  Python then repeats these steps for each name in the list.  

Pseudocode for this may look like: 
```
For every magician in the list of magicians
	print the magician's name
```
The output is a simple printout of each name on the list: 

```
alice
david
carolina
```

### A Closer Look at Looping
The concept of looping is important because it's one of the most common ways a computer automates repetitive tasks.  For example, in a simple look, like the one above in `magicians`, Python initially reads the first line of the loop:  

```py linenums="1"
for magician in magicians
```
This line tells Python to retrieve the first value from the list `magicians` and associate it with the variable `magician`.  The first value is `#!py 'alice'`.  Python then reads the next line: 

```py linenums="1"
print(magician)
```
Python prints the current value of `magician`, which is still `#!py 'alice'`.  Because the list contains more values, Python returns to the first line of the loop:

```py linenums="1"
for magician in magicians
```
Python retrieves the next name in the list, `#!py 'david'`, and associates that value with the variable `magician`.  Python then executes the line:

```py linenums="1"
print(magician)
```
Python prints the current value of `magician` again, which is now `#!py 'david'`.  Python repeats the entire loop once more with the last value in the list `#!py 'carolina'`.  Because no more values are in the list, Python moves on to the next line in the program.  In this case nothing comes after the `#!py for` loop, so the program simply ends.  

When you're using loops for the first time, keep in mind that the set of steps is repeated once for each item in the list, no matter how many items are in the list.  If you have a million items in your list, Python repeats these steps a million times -- and usually very quickly.  

Also keep in mind when writing your own `#!py for` loops that you can choose any name you want for the temporary variable that will be associated with each value in the list.  However, it's helpful to choose a meaningful name that represents a single item from the list.  For example, here's a good way to start a `#!py for` loop for a list of cats, a list of dogs, and a general list of items:  

```py linenums="1"
for cat in cats:
for dog in dogs: 
for item in list_of_items:
```
These naming conventions can help you follow the action being done on each item within a `#!py for` loop.  Using a singular and plural names can help you identify whether a section of code is working with a single element from the list or the entire list.  

### Doing More Work Within a `#!py for` Loop  
You can do just about anything with each item in a `#!py for` loop.  Let's build on the previous example by printing a message to each magician, telling them that they performed a great trick:  

```py linenums="1"
magicians = ['alice', 'david', 'carolina']
for magician in magicians:
	print(f"{magician.title()}, that was a great trick!")
```
The only difference in this code is within the `#!py for` loop, where we compose a message to each magician, starting with their name.  The first time through the loop the value of `magician` is `#!py 'alice'`, so Python starts the first message with the name `#!py 'alice'`.  The seond time through the message begins with the next index in the list (`#!py 'david'`).  The output should look as follows:

```
Alice, that was a great trick!
David, that was a great trick!
Carolina, that was a great trick!
```  

You can also write as many lines of code as you like in the `#!py for` loop.  Every indented line following the line `#!py for magician in magicians` is considered *inside the loop*, and each indented line is executed once for each value in the list.  Therefore, you can do as much work as you like with each value in the list.  

Let's add a second line to our message, telling each magician that we're looking forward to their next trick:  

```py linenums="1"
magicians = ['alice', 'david', 'carolina']
for magician in magicians:
	print(f"{magician.title()}, that was a great trick!")
	print(f"I can't wait to see your next trick, {magician.title()}.\n")
```
Because both calls for `#!py print()` are indented, each line will be executed once for every magician in the list.  This will have the output:  
```
Alice, that was a great trick!
I can't wait to see your next trick, Alice.

David, that was a great trick!
I can't wait to see your next trick, David.

Carolina, that was a great trick!
I can't wait to see your next trick, Carolina.
```  

### Doing Something After a `#!py for` Loop  
What happens once a `#!py for` loop has finished executing?  Usually, you'll want to summarize a block of output or move on to other work that your program must accomplish.  

Any lines of code after the `#!py for` loop that are not indented are executed once without repition.  Let's write a thank you to the group of magicians as a whole for putting on an excellent show.  To display this group message after all the individual messages have been printed, we place the thank you message after the `#!py for` loop without indentation:  

```py linenums="1"
magicians = ['alice', 'david', 'carolina']
for magician in magicians:
	print(f"{magician.title()}, that was a great trick!")
	print(f"I can't wait to see your next trick, {magician.title()}.\n")
print("Thank you, everyone.  That was a great magic show!")
```
The first two calls to `#!py print()` are repeated once for each magician in the list, as you saw earlier.  However, because the final line is not indented, it's printed only once:  

```
Alice, that was a great trick!
I can't wait to see your next trick, Alice.

David, that was a great trick!
I can't wait to see your next trick, David.

Carolina, that was a great trick!
I can't wait to see your next trick, Carolina.

Thank you, everyone.  That was a great magic show!
```
When you're processing data using a `#!py for` loop, you'll find that this is a good way to summarize an operation that was performed on an entire data set.  For example, you might use a `#!py for` loop to initialize a game by running through a list of characters and displaying each character on the screen.  You might then write some additional code after this loop tha displays a *Play Now* button after all the characters have been drawn to the screen.  

## Avoiding Indentation Errors
Python uses indentation to determine how a line, or group of lines, is related to the rest of the program.  In the previous examples, the lines that printed messages to individual magicians were part of the `#!py for` loop because they were indented.  Python's use of indentation makes code very easy to read.  Basically, it uses whitespace to force you to write neatly formatted code indented at a few different levels.  These indentation levels help you gain a general sense of the overall program's organization.  

As you begin to write code that relies on proper indentation, you'll need to watch for a few common *indentation errors*.  For example, people sometimes indent lines of code that don't need to be indented or forget to indent lines that need to be indented.  Seeing examples of these errors now will help you avoid them in the future and correct them when they do appear in your own programs.  Let's examine some of the more common indentation errors:  

### Forgetting to Indent
Always indent the line after the `#!py for` statement in a loop.  If you forget, Python will remind you:  

```py linenums="1"
magicians = ['alice', 'david', 'carolina']
for magician in magicians:
print(magician)
```
The call to `#!py print()` above should be indented, but it is not.  When Python expects an indented block and does not find one, it lets you know which line it had a problem with.  The following is what would be output if you ran the code above:  

```
  File "<filename>", line 3
    print(magician)
        ^
IndentationError: expected an indented block
```
You can usually resolve this kind of indentation error by indenting the line or lines immediately after the `#!py for` statement.  

### Forgetting to Indent Additional Lines  
Sometimes your loop will run without any errors but won't produce the expected result.  This can happen when you're trying to do several tasks in a loop and you forget to indent some of its lines.  

For example, this is what happens when we forget to indent the seconf line in the loop that tells each magician we're looking forward to their next trick:  

```py linenums="1"
magicians = ['alice', 'david', 'carolina']
for magician in magicians:
	print(f"{magician.title()}, that was a great trick!")
print(f"I can't wait to see your next trick, {magician.title()}.\n")
```
The second call to print should also be indented, but because Python finds at least one indented line after the `#!py for` statement, it doen't report an error.  As a result, the first `#!py print()` is executed once for each name in the list, but because the second `#!py print()` call is not indented, it will only run once.  Because the final value associated with `magician` is `#!py 'carolina'`, she is the only one who recieves the "looking forward to the next trick message":  

```
Alice, that was a great trick!
David, that was a great trick!
Carolina, that was a great trick!
I can't wait to see your next trick, Carolina.
``` 
This is a *logical error*.  The syntax is valid Python code, but the code does not produce the desired result because a problem occurs in its logic.  If you expect to see a certain action repeated once for each item in a list and it's only executed once, determine whether you need to simply indent a line or group of lines to remedy the problem.  

### Indenting Unnecessarily 
If you accidentally indent a line that doesn't need to be indented, Python will inform you about the unexpected indent:  

```py linenums="1"
message = "Hello Python World!"
	print(message)
```
We do not need the indent before the `#!py print()` call, because it is not part of a loop.  Python will report the following error:  

```py linenums="1"
  File "<ipython-input-1-2f2b50073239>", line 2
    print(message)
    ^
IndentationError: unexpected indent
```
You can avoid unexpected indentation errors by indenting only when you have a specific reason to do so.  So far, we have only needed to indent when we used a `#!py for` loop.  

### Forgetting the Colon
The colon at the end of a `#!py for` statement tells Python to interpret the next line as the start of a loop:

```py linenums="1"
magicians = ['alice', 'david', 'carolina']
for magician in magicians
	print(magician)
```
Notice that we are missing the colon at the end of line 2.  This will cause a syntax error in Python because it will not be able to interpret what we are trying to do.  The above code will give you the following error:  

```py linenums="1"
  File "<ipython-input-2-082d5f15acfa>", line 2
    for magician in magicians
                             ^
SyntaxError: invalid syntax
```

## Making Numerical Lists  
Many reasons exist to store a set of numbers.  For example, you'll need to keep track of the positions of each character in a game, and you might want to keep track of a player's high scores as well.  In data visualizations, you'll almost always work with sets of numbers, such as termperatures, distances, population sizes, or latitude and logitude values, among other types of numerical sets.  

Lists are ideal for storing sets of numbers, and Python provides a vairety of tools to help you work effeciently with lists of numbers.  Once you understand how to use these tools effectively, your code will work well even when your lists contain millions of items.  

### Using the `#!py range()` function  
Python's `#!py range()` function makes it easy to generate a series of numbers.  For example, you can use the `#!py range()` function to print a series of numbers like this:  

```py linenums="1"
for value in range(1, 5):
	print(value)
```
Although this code looks like it should print numbers from 1 to 5, it does not print the number 5:

```
1
2
3
4
```
In this example, `#!py range()` only prints the numbers 1 through 4.  This is another result of the *off-by-one behavior* you'll often see in programming languages.  The `#!py range()` function causes Python to start counting at the first value you give it, and stops when it reaches the second value you provide.  Because it stops at the second value, the output never contains the end value, which would have been 5 in this case.  

To print the numbers 1 to 5, you would use `#!py range(1,6)`.  

If your output is different than what you expect when you're using `#!py range()`, try adjusting your end value by 1.  

### Using `#!py range()` to Make a List of Numbers  
If you want to make a list of numbers you can conver the results of `#!py range()` directly into a list using the `#!py list()` function.  When you wrap `#!py list()` around a call to the `#!py range()` function, the output will be a list of numbers.  

In the example in the previous section, we simply printed out a series of numbers.  We can use the `#!py list()` function to convert that same set of numbers into a list: 

```py linenums="1"
numbers = list(range(1, 6))
print(numbers)
```
And this is the result:

```
[1, 2, 3, 4, 5]
```
We can also use the `#!py range()` function to tell Python to skip numbers in a given range.  If you pass a third argument to `#!py range()`, Python uses that value as a step size when generating numbers.  

For example, here's how to list the even numbers between 1 and 10:  

```py linenums="1"
even_numbers = list(range(2, 11, 2))
print(even_numbers)
```
In this example, the `#!py range()` function starts with the value 2 and then adds 2 to that value, until it reaches index 11 (the number 10).  This will produce the following result: 

```
[2, 4, 6, 8, 10]
```
You can create almost any set of numbers you want to using the `#!py range()` function.  For example, consider how you might make a list of the first 10 square numbers (that is, the square of each integer from 1 through 10).  In Python, two asterisks (`**`) represent exponents.  Here's how you might put the first 10 square numbers into a list:  

```py linenums="1"
squares = []
for value in range(1, 11):
	square = value ** 2
	squares.append(square)
print(squares)
```
We start with an empty list called `squares`.  Next, we tell Python to loop through each value from 1 to 10 using the `#!py range()` function.  Inside the loop, the current value is raised to the second power and assigned to the variable `square`.  Finally, when the loop has finished running, the list of squares is printed:  

```
[1, 4, 9, 16, 25, 36, 49, 64, 81, 100]
```
To write this code even more precisely, omit the temporary variable `square` and append each new value directly to the list: 

```py linenums="1"
squares = []
for value in range(1, 11):
	squares.append(value**2)
print(squares)
```
Sometimes using a temporary value makes our code easier to read; other times it makes the code unecessarily long.  

### Simple Statistics with a List of Numbers 
A few Python functions are helpful when working with lists of numbers.  For example, you can easily find the minimum, maximum, and sum of a list of numbers:

```py linenums="1"
digits = [1, 2, 3, 4, 5, 6, 7, 8, 9, 0]
print(min(digits))
print(max(digits))
print(sum(digits))
```
The above code will give you the following result:
```
0
9
45
```
### List Comprehensions 
The approach described earlier for generating the list `squares` consisted of using three or four lines of code.  A list comprehension combines the `#!py for` loop and the creating of new elements into one line, and automatically appends each new element.  

The following example builds the same list of square numbers you saw earlier but uses a list comprehension: 

```py linenums="1"
squares = [value**2 for value in range(1, 11)]
print(squares)
```
To use this syntax, begin with a descriptive name for the list, such as `squares`.  Next open a set of square brackets and define the expression for the values you want to store in the new list.  In this example, the expression `#!py value**2`, which raises the value to the second power.  Then, write a `#!py for` loop to generate the numbers you want to feed into the expression, and close the square brackets.  The `#!py for` loop in this example is `#!py for value in range(1, 11)`, which feeds the values 1 through 10 into the expression `#!py value**2`.  Notice that no colon is used at the end of the `#!py for` statement.  The result is the same list of square numbers you saw earlier:

```
[1, 4, 9, 16, 25, 36, 49, 64, 81, 100]
```
### Extra Problems

**Use a `#!py for` loop to print the numbers 1 to 20**

```py linenums="1"
numbers = list(range(1, 21))

for number in numbers:
    print(number)
```
**Make a list from one to one million, and then use `#!py min()` and `#!py max()` to make sure your list is complete.  Also use the `#!py sum()` function**
```py linenums="1"
numbers = list(range(1, 1000001))

print(min(numbers))
print(max(numbers))
print(sum(numbers))
```
**Use the third argument of the `#!py range()` function to make a list of the odd numbers from 1 to 20.  Use a `#!py for()` loop to print each number**
```py linenums="1"
odd_numbers = list(range(1, 21, 2))

for numbers in odd_numbers:
	print(numbers)
```
**Make a list of the multiples of 3 from 3 to 30.  Use a `#!py for()` loop to print the numbers in your list**
```py linenums="1"
multiples = list(range(3, 31, 3))

for numbers in multiples:
	print(numbers)
```
**Make a list of the first 10 cubes and use a `#!py for` loop to print out each value of each cube**
```py linenums="1"
cubes = []
for value in range(1, 11):
	cubes.append(value**3)
print(cubes)
```
**Use a list comprehension to generate a list of the first 10 cubes**
```py linenums="1"
cubes = [value**3 for value in range(1, 11)]
print(cubes)
```

## Working with Part of a List
You are able to work with a specific group of items in a list, which Python calls a *slice*.  

### Slicing a List 
To make a slice, you specify the index of the first and last elements you want to work with. As with the `#!py range()` function, Python stops one item before the second index you specify.  To output the first three elements in a list, you would request indices 0 through 3, which would return elements 0, 1, and 2.  

The following example involves a list of players on a team: 

```py linenums="1"
players = ['charles', 'martina', 'florence', 'eli']
print(players[0:3])
```
The code on line 2 prints a slice of that list, including just the values at index 0 - 2.  
If you omit the first index in a slice, Python automaticaly starts your slice at the beginning of the list.  Similarly, if you omit the second index, Python will go from the set starting index through the end of the list.  

You can also include a third value in the slice brackets, telling Python how many items to skip through while going through the specified range.

### Looping Through a Slice
You can use a slice in a `#!py for` loop if you want to loop through s subset of the elements in a list.  In the next example, we loop through the first three players and print their names as part of a simple roster:

```py linenums="1"
players = ['charles', 'martina', 'michael', 'florence', 'eli']

print("Here are the first three players on my team:")
for player in players[:3]:
	print(player.title())
```
Instead of looping through the entire list of players, Python loops through only the first three names. 

Slices are very useful in a number of situations.  For instance, when you're building a web application, you could use slices to display information in a series of pages with an appropriate ammount of information on each page.  

### Copying a List
Often, you'll want to start with an existing list and make an entirely new list based on the first one.  Let's explore how copying a list works and examine one situation in which copying a list is useful.  

To copy a list, you can make a slice that include the entire original list by omitting the first and the second index ([:]).  This tells Python to make a slice that starts at the first item and ends with the last item, producing a copy of the entire list.  

Let's copy a list using slice:  

```py linenums="1"
my_foods = ['pizza', 'burgers', 'steak']
friend_foods = my_foods[:]

print("My favorite foods are:")
print(my_foods)

print("\nMy friend's favorite foods are:")
print(friend_foods)
```
On the first line we created a list of our favorite foods called `my_foods`.  Next, we made a copy of `my_foods` in a new list called `friend_foods`.  We created the copy by asking for a slice without specifying an index ([:]).  When we print each list, we see that they both contain the same foods:  

```
My favorite foods are:
['pizza', 'burgers', 'steak']

My friend's favorite foods are:
['pizza', 'burgers', 'steak']
```
To prove that we actually have two seperate lists, we'll add a new food to each list and show that each list keeps track of the appropriate person's favorite foods:  

```py linenums="1"
my_foods = ['pizza', 'burgers', 'steak']
friend_foods = my_foods[:]

my_foods.append('canoli')
friend_foods.append('ice cream')

print("My favorite foods are:")
print(my_foods)

print("\nMy friend's favorite foods are:")
print(friend_foods)
```
Now we get the result:
```
My favorite foods are:
['pizza', 'burgers', 'steak', 'canoli']

My friend's favorite foods are:
['pizza', 'burgers', 'steak', 'ice cream']
```

## Tuples
Lists work well for storing collections of items that can change throughout the life of a program.  The ability to modify lists is particularly important when you're working with a list of users on a website or a list of characters in a game.  However, sometimes you'll want to create a list of items that cannot change.  Tuples allow you to do just that.  Python refers to values that cannot change as *immutable*, and an immutable list is called a *tuple*.  

### Defining a Tuple
A tuple looks just like a list except you use parentheses instead of square brackets.  Once you define a tuple, you can access individual elements by using each item's index, just as you would for a list.  

For example, if we have a rectangle that should always be a certain size, we can ensure that its size doesn't change by putting the dimensions into a tuple:  

```py linenums="1"
dimensions = (200, 50)
print(dimensions[0])
print(dimensions[1])
``` 
We define a tuple `dimensions` in line 1, using parentheses instead of square brackets.  Next, we print each element in the tuple individually, using the same syntax we've been using to access elements in a list:  

```
200
50
```
Let's see what happens if we try to change one of the items in the tuples dimensions: 

```py linenums="1"
dimensions = (200, 50)
dimensions[0] = 250
``` 
Wehn we try to run the above code we get a "tuple error":

```py linenums="1"
TypeError                                 Traceback (most recent call last)
<ipython-input-13-258c8b06eee2> in <module>
      1 dimensions = (200, 50)
----> 2 dimensions[0] = 250

TypeError: 'tuple' object does not support item assignment
```
??? warning "Note on Tuples"
	Tuples are technically defined by the presence of a comma; the parenthes make them look neater and more readable.  If you want to define a tuple with one element, you need to include a trailing comma:
	```py linenums="1"
	my_t = (3,)
	```
	It doesn't often make sense to build a tuple with one element, but this can happen when tuples are generated automatically.  

### Looping Through All Values in a Tuple
You can loop over all the values in a tuple using a `#!py for` loop, just as you did with a list:  

```py linenums="1"
dimensions = (200,50)
for dimension in dimensions:
	print(dimension)
```
Python will then return all the elements in the tuple, just as it would for a list.

### Writing over a Tuple
Although you cannot modify a tuple, you can assign a new value to a variable that represents a tuple.  So if we wanted to change our dimensions, we could redefine an entire tuple:

```py linenums="1" 
dimensions = (200, 50)
print("Original dimensions:")
for dimension in dimensions:
	print(dimension)

dimensions = (400, 100)
print("\nModified dimensions:")
for dimension in dimensions:
	print(dimension)
```
The code at line 1 defines the original tuple and print the initial dimensions.  At line 6, we associate a new tuple with the variable `dimensions`.  We then print the new dimensions at line 7.  Python does not return any erros this time, because reassigning a variable is valid:  

```
Original dimensions:
200
50

Modified dimensions:
400
100
```
When compared with lists, tuples are simple data structures.  Use them when you want to store a set of values that should not be changed throughout the life of a program.  