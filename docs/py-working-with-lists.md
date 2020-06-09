# Working with Lists

## Looping Through an Entire List 

You'll often want to run through all entries in a list, performing the same task with each item.  For example, in a game you might want to move every element on the screen by the same amount, or in a list of numbers you might want to perform the same statistical operation on every element.  Or perhaps, you'll want to display each headline from a list of articles on a website.  When you want to do the sam eaction with every item in a list, you can use Python's `for` loop.  

Let's say we have a list of magician's names, and we want to print out each name in the list.  We could do this by retrieving each name from the list individually, but this approach could cause several problems.  For one, it would be repetitive to do this with a long list of names.  Also, we'd have to change our code each time the list's length changed.  A `for` loop avoids both of these issues by letting Python manage these issues internally.  

Let's use a `for` loop to print out each name in a list of magicians:  

```py
magicians = ['alice', 'david', 'carolina']
for magician in magicians:
	print(magician)
```
We begin by defining the list (`magicians`).  Next, we define a `for` loop.  This line tells Python to pull a name from the list `magicians`, and associate it with the variable `magician`.  Finally, we tell Python to print the name that's been assigned to `magician`.  Python then repeats these steps for each name in the list.  

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

```py
for magician in magicians
```
This line tells Python to retrieve the first value from the list `magicians` and associate it with the variable `magician`.  The first value is `'alice'`.  Python then reads the next line: 

```py
print(magician)
```
Python prints the current value of `magician`, which is still `'alice'`.  Because the list contains more values, Python returns to the first line of the loop:

```py
for magician in magicians
```
Python retrieves the next name in the list, `'david'`, and associates that value with the variable `magician`.  Python then executes the line:

```py
print(magician)
```
Python prints the current value of `magician` again, which is now `'david'`.  Python repeats the entire loop once more with the last value in the list `'carolina'`.  Because no more values are in the list, Python moves on to the next line in the program.  In this case nothing comes after the `for` loop, so the program simply ends.  

When you're using loops for the first time, keep in mind that the set of steps is repeated once for each item in the list, no matter how many items are in the list.  If you have a million items in your list, Python repeats these steps a million times -- and usually very quickly.  

Also keep in mind when writing your own `for` loops that you can choose any name you want for the temporary variable that will be associated with each value in the list.  However, it's helpful to choose a meaningful name that represents a single item from the list.  For example, here's a good way to start a `for` loop for a list of cats, a list of dogs, and a general list of items:  

```py
for cat in cats:
for dog in dogs: 
for item in list_of_items:
```
These naming conventions can help you follow the action being done on each item within a `for` loop.  Using a singular and plural names can help you identify whether a section of code is working with a single element from the list or the entire list.  

### Doing More Work Within a `for` Loop  

You can do just about anything with each item in a `for` loop.  Let's build on the previous example by printing a message to each magician, telling them that they performed a great trick:  

```py
magicians = ['alice', 'david', 'carolina']
for magician in magicians:
	print(f"{magician.title()}, that was a great trick!")
```
The only difference in this code is within the `for` loop, where we compose a message to each magician, starting with their name.  The first time through the loop the value of `magician` is `'alice'`, so Python starts the first message with the name `'alice'`.  The seond time through the message begins with the next index in the list (`'david'`).  The output should look as follows:

```
Alice, that was a great trick!
David, that was a great trick!
Carolina, that was a great trick!
```  

You can also write as many lines of code as you like in the `for` loop.  Every indented line following the line `for magician in magicians` is considered *inside the loop*, and each indented line is executed once for each value in the list.  Therefore, you can do as much work as you like with each value in the list.  

Let's add a second line to our message, telling each magician that we're looking forward to their next trick:  

```py
magicians = ['alice', 'david', 'carolina']
for magician in magicians:
	print(f"{magician.title()}, that was a great trick!")
	print(f"I can't wait to see your next trick, {magician.title()}.\n")
```
Because both calls for `print()` are indented, each line will be executed once for every magician in the list.  This will have the output:  
```
Alice, that was a great trick!
I can't wait to see your next trick, Alice.

David, that was a great trick!
I can't wait to see your next trick, David.

Carolina, that was a great trick!
I can't wait to see your next trick, Carolina.
```  

### Doing Something After a `for` Loop  

What happens once a `for` loop has finished executing?  Usually, you'll want to summarize a block of output or move on to other work that your program must accomplish.  

Any lines of code after the `for` loop that are not indented are executed once without repition.  Let's write a thank you to the group of magicians as a whole for putting on an excellent show.  To display this group message after all the individual messages have been printed, we place the thank you message after the `for` loop without indentation:  

```py
magicians = ['alice', 'david', 'carolina']
for magician in magicians:
	print(f"{magician.title()}, that was a great trick!")
	print(f"I can't wait to see your next trick, {magician.title()}.\n")
print("Thank you, everyone.  That was a great magic show!")
```
The first two calls to `print()` are repeated once for each magician in the list, as you saw earlier.  However, because the final line is not indented, it's printed only once:  

```
Alice, that was a great trick!
I can't wait to see your next trick, Alice.

David, that was a great trick!
I can't wait to see your next trick, David.

Carolina, that was a great trick!
I can't wait to see your next trick, Carolina.

Thank you, everyone.  That was a great magic show!
```
When you're processing data using a `for` loop, you'll find that this is a good way to summarize an operation that was performed on an entire data set.  For example, you might use a `for` loop to initialize a game by running through a list of characters and displaying each character on the screen.  You might then write some additional code after this loop tha displays a *Play Now* button after all the characters have been drawn to the screen.  

## Avoiding Indentation Errors

Python uses indentation to determine how a line, or group of lines, is related to the rest of the program.  In the previous examples, the lines that printed messages to individual magicians were part of the `for` loop because they were indented.  Python's use of indentation makes code very easy to read.  Basically, it uses whitespace to force you to write neatly formatted code indented at a few different levels.  These indentation levels help you gain a general sense of the overall program's organization.  

As you begin to write code that relies on proper indentation, you'll need to watch for a few common *indentation errors*.  For example, people sometimes indent lines of code that don't need to be indented or forget to indent lines that need to be indented.  Seeing examples of these errors now will help you avoid them in the future and correct them when they do appear in your own programs.  Let's examine some of the more common indentation errors:  

### Forgetting to Indent

Always indent the line after the `for` statement in a loop.  If you forget, Python will remind you:  

```py
magicians = ['alice', 'david', 'carolina']
for magician in magicians:
print(magician)
```
The call to `print()` above should be indented, but it is not.  When Python expects an indented block and does not find one, it lets you know which line it had a problem with.  The following is what would be output if you ran the code above:  

```
  File "<filename>", line 3
    print(magician)
        ^
IndentationError: expected an indented block
```
You can usually resolve this kind of indentation error by indenting the line or lines immediately after the `for` statement.  

### Forgetting to Indent Additional Lines  

Sometimes your loop will run without any errors but won't produce the expected result.  This can happen when you're trying to do several tasks in a loop and you forget to indent some of its lines.  

For example, this is what happens when we forget to indent the seconf line in the loop that tells each magician we're looking forward to their next trick:  

```py
magicians = ['alice', 'david', 'carolina']
for magician in magicians:
	print(f"{magician.title()}, that was a great trick!")
print(f"I can't wait to see your next trick, {magician.title()}.\n")
```
The second call to print should also be indented, but because Python finds at least one indented line after the `for` statement, it doen't report an error.  As a result, the first `print()` is executed once for each name in the list, but because the second `print()` call is not indented, it will only run once.  Because the final value associated with `magician` is `'carolina'`, she is the only one who recieves the "looking forward to the next trick message":  

```
Alice, that was a great trick!
David, that was a great trick!
Carolina, that was a great trick!
I can't wait to see your next trick, Carolina.
``` 
This is a *logical error*.  The syntax is valid Python code, but the code does not produce the desired result because a problem occurs in its logic.  If you expect to see a certain action repeated once for each item in a list and it's only executed once, determine whether you need to simply indent a line or group of lines to remedy the problem.  

