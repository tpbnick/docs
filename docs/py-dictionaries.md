# Dictionaries
Understanding dictionaries allows you to model a variety of real-world objects more accurately.  For example, we could create a dictionary representing a person and then store as much information as we want about that person.  You can store their name, location, age, profession, and any other aspect of a person you can describe.  We can store any two kinds of information that can be matched up, such as a list of words and their meanings, a list of people's names and their favorite numbers, a list of mountains and their elevations, etc.  

## A Simple Dictionary
Consider a game featuring aliens that can have different colors and point values.  This simple dictionary stores information about a particular alien:  
```py linenums="1"
alien_0 = {'color': 'green', 'points': 5}

print(alien_0['color'])
print(alien_0['points'])
```
The dictionary `alien_0` stores the alien's color and point value.  The last two lines access and display that information, as shown here:  
```
green
5
```
As with most new programming concepts, using dictionaries takes practice.  Once you've worked with dictionaries for a bit, you'll soon see how effectively they can model real-world situations.  

## Working with Dictionaries
A *dictionary* in Python is a collection of *key-value pairs*.  Each *key* is connected to a value, and you can use a key to access the value associated with that key.  A key's value can be a number, a string, a list, or even another dictionary.  In fact, you can use any object that you can create in Python as a value in a dictionary.  

In Python, a dictionary is wrapped in braces, { }, with a series of key-value pairs inside the braces, as shown in the earlier example:  
```py
alien_0 = {'color': 'green', 'points': 5}
```
A *key-value pair* is a set of values associated with each other.  When you provide a key, Python returns the value associated with that key.  Every key is connected to its value by a colon, and individual key-value pairs are separated by commas.  You can store as many key-value pairs as you want in a dictionary.  

The simplest dictionary has exactly one key-value pair, as shown in this modified version of the `alien_0` dictionary:  
```py
alien_0 = {'color': 'green'}
```
This dictionary stores one piece of information about `alien_0`, namely the alien's color.  The string `#!py 'color'` is a key in this dictionary, and its associated value is `#!py 'green'`.  

### Accessing Values in a Dictionary
To get the value associated with a key, give the name of the dictionary and then place the key inside a set of square brackets, as shown here:  
```py linenums="1"
alien_0 = {'color': 'green'}
print(alien_0['color'])
```
This returns the value associated with the key `#!py 'color'` from the dictionary `alien_0`:
```
green
```
You can have an ulimited number of key-value pairs in a dictionary.  For example, here's the original `alien_0` dictionary with two key-value pairs: 
```py
alien_0 = {'color': 'green', 'points': 5}
```
Now you can access either the color or the point value of `alien_0`.  If a player shoots down this alien, you can look up how many points they should earn using code like this:  
```py linenums="1"
alien_0 = {'color': 'green', 'points': 5}

new_points = alien_0['points']
print(f"You just earned {new_points} points!")
```
Once the dictionary has been defined, the code on line 3 pulls the value associated with the key `#!py 'points'` from the dictionary.  This value is then assigned to the variable `#!py 'new_points'`.  The code on line 4 then prints a statement about how many points the player just earned.  

### Adding New Key-Value Pairs
Dictionaries are dynamic structures, and you can add new key-value pairs to a dictionary at any time.  For example, to add a new key-value pair, you would give the name of the dictionary followed by the new key in square brackets along with the new value.  

Let's add two new pieces to the `alien_0` dictionary: the alien's x- and y- coordinates, which will help us display the alien in a particular position on the screen.  Let's place the alien on the left edge of the screen, 25 pixels down from the top.  Because screen coordinates usually start at the upper-left corner of the screen, we'll place the alien on the left edge of the screen by setting the x-coordinate to 0 and 25 pixels from the top by setting the y-coordinate to positive 25:  
```py linenums="1"
alien_0 = {'color': 'green', 'points': '5'}
print(alien_0)

alien_0['x_position'] = 0
alien_0['y_position'] = 25
print(alien_0)
```
We start by defining the same dictionary that we have been working with.  We then print this dictionary, displaying a snapshot of its information.  On line 4, we add a new key-value pair to the dictionary: key `#!py 'x_position'` and a value of `0`.  We do the same for key `#!py 'y_position'` on the next line.  Finally, when we print the modified dictionary, we see the two additional key-value pairs:  
```
{'color': 'green', 'points': '5'}
{'color': 'green', 'points': '5', 'x_position': 0, 'y_position': 25}
```
The final version of the dictionary contains four key-value pairs.

### Starting with an Empty Dictionary
It's sometimes convenient, or even necessary, to start with an empty dictionary and then add each new item to it.  To start filling an empty dictionary, define a dictionary with an empty set of braces and then add each key-value pair on its own line.  For example, here's how to build the `alien_0` dictionary using this approach:
```py linenums="1"
alien_0 = {}

alien_0['color'] = 'green'
alien_0['points'] = '5'

print(alien_0)
```
Here we define an empty `alien_0` dictionary, and then add color and point values to it.  The result is the dictionary we have been usinging in previous examples:  
```
{'color': 'green', 'points': '5'}
```
Typically, you'll use empty dictionaries when storing user-supplied data in a dictionary or when you write code that generates a large number of key-value pairs automatically.  

### Modifying Values ina  Dictionary
To modify a value in a dictionary, give the name of the dictionary with the key in square brackets and then the new value you want associated with that key.  For example, consider an alien that changes from green to yellow as a game progresses: 
```py linenums="1"
alien_0 = {'color': 'green'}
print(f"The alien is {alien_0['color']}.")

alien_0['color'] = 'yellow'
print(f"The alien is now {alien_0['color']}.")
```
We first define a dictionary for `alien_0` that contains only the aliens color; then we change the value associated with the key `#!py 'color'` to `#!py 'yellow'`.  The output shows that the alien has indeed changed from green to yellow:  
```
The alien is green.
The alien is now yellow.
```
For a more interesting example, let's track the position of an alien that can move at different speeds.  We'll sotre a value representing the alien's current speed and then use it to determine how far to the right the alien should move:  
```py linenums="1"
alien_0 = {'x_position': 0, 'y_position': 25, 'speed': 'medium'}
print(f"Original position: {alien_0['x_position']}")
# Move the alien to the right.
# Determine how far to move the alien based on its current speed.
if alien_0['speed'] == 'slow':
	x_increment = 1
elif alien_0['speed'] == 'medium':
	x_increment = 2
else:
	# This must be a fast alien.
	x_increment = 3
# The new position is the old position plus the increment.
alien_0['x_position'] = alien_0['x_position'] + x_increment
print(f"New position: {alien_0['x_position']}")
```
We start by defining an alien with an initial *x* and *y* position, and a speed of `#!py 'medium'`.  We also print the original value of `x_position` to see how far the alien moves to the right.  

On line 5, an `#!py if-elif-else` chain determins how far the alien should move to the right and assigns this value to the variable `x_increment`.  If the alien's speed is `#!py 'slow'`, it moves one unit, if it is `#!py 'medium'`, it moves two, and if it is `#!py 'fast'`, it moves three.  Once the increment has been calculated, it is added to the value of `x_position` on line 13 and the result is stored in the dictionary's `x_position`.  

Because this is a medium-speed alien, its position shifts two units to the right:
```
Original position: 0
New position: 2
```
This technique is pretty cool: by changing one value in the alien's dictionary, you can change the overall behavior of the alien.  For example, to turn this medium-speed alien into a fast alien, you would add the line:  
```py
alien_0['speed'] = 'fast'
```
The `if-elif-else block` would then assign a larger value to `x_increment`
the next time the code runs.

### Removing Key-Value Pairs
When you no longer need a piece of information that is stored ina  dictionary, you can you the `#!py del` statement to completely remove a key-value pair.  All `#!py del` needs is the name of the dictionary and the key  that you want to remove.  

For example, let's remove the key `#!py 'points'` from the `alien_0` dictionary along with its value: 
```py linenums="1"
alien_0 = {'color': 'green', 'points': 5}
print(alien_0)

del alien_0['points']
print(alien_0)
```
The code on line 4 tells Python to delete the key `#!py 'points'` from the dictionary `alien_0` and to remove the value associated with that key as well.  The output shows that the key `#!py 'points'` and its value of 5 are deleted from the dictionary, and the rest is unaffected:  
```
{'color': 'green', 'points': 5}
{'color': 'green'}
```
### A Dictionary of Similar Objects
The previous example involved storing different kinds of information about one object, an alien in a game.  You can also use a dictionary to store one kind of information about many objects.  For example, a dictionary of a group of people's favorite programming language.  A dictionary for this could look like:  
```py linenums="1"
favorite_languages = {
	'jen': 'python',
	'sarah': 'c',
	'edward': 'ruby',
	'phil': 'python',
}
```
As you can see, we've broken a larger dictionary into several lines (mainly for better readability).  Each key is the name of a person and each value is their favorite language.  When you know you'll need more than one line to define a dictionary, press `ENTER` after the opening brace.  Then indent the next line one tab, and write your first key-value pair, followed by a comma.  

Once you have finished defining the dictionary, add a closing brace on a new line after the last key-value pair and indent it one level so it aligns with the keys in the dictionary.  It's good practice to include a comma after the last key-value pair, just in case you want to add more in the future.  

To use this dictionary, given the name of a person, you can easily look up their favorite language:  
```py linenums="1"
favorite_languages = {
	'jen': 'python',
	'sarah': 'c',
	'edward': 'ruby',
	'phil': 'python',
}

language = favorite_languages['sarah'].title()
print(f"Sarah's favorite langugage is {language}.")
```
To see which language Sarah chose, we ask for the value at:
```py
favorite_languages['sarah']
```
We use this syntax to pull Sarah's favorite language from the dictionary (line 8) and assign it to the variable `language`.  Creating a new variable here makes for a much cleaner `#!py print()` call.  The output shows Sarah's favorite Language:
```
Sarah's favorite langugage is C.
```

### Using `#!py get()` to Access Values  

Using keys in square brackets to retrieve the value you're interested in from a dictionary might cause one potential problem: if the key you ask for doesn't exist, you'll get an error.  

Let's see what happens when you ask for the point value of an alien that doesn't have a point value set:
```py linenums="1"
alien_0 = {'color': 'green', 'speed': 'slow'}
print(alien_0['points'])
```
This results in a traceback, showing a KeyError:  
```
KeyError                                  Traceback (most recent call last)
<ipython-input-9-3914d637e9f3> in <module>
      1 alien_0 = {'color': 'green', 'speed': 'slow'}
----> 2 print(alien_0['points'])

KeyError: 'points'
```
For dictionaries, we can use the `#!py get()` method to set a default value that will be returned if the requested key doesn't exist.  

The `#!py get()` method requires a key as a first argument.  As a second optional argument, you can pass the value to be returned if the key doesn't exist: 
```py linenums="1"
alien_0 = {'color': 'green', 'speed': 'slow'}

point_value = alien_0.get('points', 'No point value assigned.')
print(point_value)
```
If the key `#!py 'points'` exists in the dictionary, you'll get corresponding value.  If it doesn't, you get the default value.  In this case, `points` doesn't exist, and we get a clean message instead of an error: 
```
No point value assigned.
```
If there's a chance the key you're asking for might not exist, consider using the `#!py get()` method instead of the square bracket notation.  

## Looping Through a Dictionary
A single Python dictionary can contain just a few key-value pairs or millions of pairs.  Because a dictionary can contain large amounts of data, Python lets you loop through a dictionary.  Dictionaries can be used to store information in a variety of ways; therefore, several different ways exist to loop through them.  You can loop through all of a dictionary's key-value pairs, through its keys, or its values.  

### Looping Through All Key-Value Pairs
Before we explore the different approaches to looping, let's consider a new dictionary designed to store information about a user on website.  The following dictionary would store one person's username, first name, and last name:
```py linenums="1"
user_0 = {
	'username': 'efermi'
	'first': 'enrico'
	'last': 'fermi'
}
```
You can access any single piece of information about `user_0` based on what you've already learned in this chapter.  But what if you wanted to see everything stored in this user's dictionary?  To do so, you could loop through the dictionary using a `#!py for` loop.
```py linenums="1"
user_0 = {
	'username': 'efermi',
	'first': 'enrico',
	'last': 'fermi',
	}

for key, value in user_0.items():
	print(f"\nKey: {key}")
	print(f"Value: {value}")
```
As shown on line 7, to write a `#!py for` loop for a dictionary, you create names for the two variables that will hold the key and value in each key-value pair.  You can choose any names you want for these two variables.  This code would work just as well if you had used abbreviated for the variable names, like this:
```py
for k, v in user_0.items()
```
The second half of the `#!py for` statement on line 7 includes the name of the dictionary followed by the method `items()`, which returns a list of key-value pairs.  The `#!py for` loop then assigns each of these pairs to the two vairbales provided.  In the preceding example, we use the variables to print each key (line 8), followed by the associated value (line 9).  The "\n" in the first `#!py print()` call ensures that a blank line is inserted bfore each key-value pair in the output:  
```
Key: username
Value: efermi

Key: first
Value: enrico

Key: last
Value: fermi
```
Looping through all key-value pairs works particularly well for dictionaries like the *`favorite_languages`* example from [above](https://docs.nicklyss.com/py-dictionaries/#a-dictionary-of-similar-objects), which stores the same kind of information for many different keys.  If you loop through the *`favorite_languages`* dictionary, you get the name of each person in the dictionary and their favorite programming language.  Because the keys always refer to a person's name and the value is always language, we'll use the variables `name` and `language` in the loop, instead of `key` and `value`.  This will make it easier to follow what's happening inside the loop:  
```py linenums="1"
favorite_languages = {
	'jen': 'python',
	'sarah': 'c',
	'edward': 'ruby',
	'phil': 'python',
}

for name, language in favorite_languages.items():
	print(f"{name.title()}'s favorite language is {language.title()}!")
```
The code on line 8 tells Python to loop through each key-value pair in the dictionary.  As it works through each pair the key is assigned to the variable `name`, and the value is assigned to the variable `language`.  These descriptive names make it much easier to see what the `#!py print()` call on line 9 is doing.  

Now, in just a few lines of code, we can display all the information from the poll:  
```
Jen's favorite language is Python!
Sarah's favorite language is C!
Edward's favorite language is Ruby!
Phil's favorite language is Python!
```
This type of looping would work just as well if our dictionary stored the results from polling a thousand or even a million people.  

### Looping Through All The Keys in a Dictionary
The `keys()` method is useful when you don't need to work with all of the values in a dictionary.  Let's loop through the *`favorite_languages`* dictionary and print the names of everyone who answered: 
```py linenums="1"
favorite_languages = {
	'jen': 'python',
	'sarah': 'c',
	'edward': 'ruby',
	'phil': 'python',
}

for name in favorite_languages.keys():
	print(name.title())
```
The code on line 8 tells Python to pull all the keys from the dictionary `favorite_languages` and assign them one at a time to the variable `name`.  The output shows the names of everyone who answered:  
```
Jen
Sarah
Edward
Phil
```
Looping through the keys is actually the default behavior when looping through a dictionary, so this code would have exactly the same output if you wrote:
```py
for name in favorite_languages:
```
rather than:
```py
for name in favorite_languages.keys():
```
You can choose to use the `keys()` method explicitly if it makes your code easier to read, or you can omit it if you wish.  

You can access the value associated with any key you care about inside the loop by using the current key.  Let's print a message to a couple of friends about the languages they chose.  We'll loop through the names in the dictionary as we did previously, but when the name matches on of our friends, we'll display a message about their favorite language:
```py linenums="1"
favorite_languages = {
	'jen': 'python',
	'sarah': 'c',
	'edward': 'ruby',
	'phil': 'python',
}

friends = ['phil', 'sarah']
for name in favorite_languages.keys():
	print(f"Hi, {name.title()}.")

	if name in friends:
		language = favorite_languages[name].title()
		print(f"\t{name.title()}, I see you love {language}!")
```
On line 8 we make a list of friends that we want to print a message to.  Inside the loop, we print each person's name.  Then on line 12 we check whether the `name` we're working with is in the list `friends`.  If it is, we determine the person's favorite language using the name of the dictionary and the current value of `name` as the key (line 13).  We then print a special greeting, including a reference to their language of choice.  

Everyone's name is printed, but our friends receive a special message:
```
Hi, Jen.
Hi, Sarah.
	Sarah, I see you love C!
Hi, Edward.
Hi, Phil.
	Phil, I see you love Python!
```
You can also use the `keys()` method to find out if a particular person was polled.  This time, let's find out if Erin took the poll:
```py linenums="1"
favorite_languages = {
	'jen': 'python',
	'sarah': 'c',
	'edward': 'ruby',
	'phil': 'python',
}

if 'erin' not in favorite_languages.keys():
	print("Erin, please take our poll!")
```
The `keys()` method isn't just for looping: it actually returns a list of all the keys, and the code on line 8 simply checks if `#!py 'erin'` is in the list.  Because she is not, a message is printed inviting her to take the poll.

### Looping Through a Dictionary's Keys in a Particular Order
Starting in Python 3.7, looping through a dictionary returns the items in the same order they were inserted.  Sometimes, though, you'll want to loop through a dictionary in a different order.  

One way to do this is to sort the keys as they're retunred in the `#!py for` loop.  You can use the `#!py sorted()` function to get a copy of the keys in order:  
```py linenums="1"
favorite_languages = {
	'jen': 'python',
	'sarah': 'c',
	'edward': 'ruby',
	'phil': 'python',
}

for name in sorted(favorite_languages.keys()):
	print(f"{name.title()}, thank you for taking the poll.")
```
This `#!py for` statement is like other `#!py for` statements except that we've wrapped the `#!py sorted()` function around the `#!py dictionary.keys()` method.  This tells Python to list all keys in the dictionary and sort that list before looping through it.  The output shows everyone who took the poll, with the names displayed in order:  
```
Edward, thank you for taking the poll.
Jen, thank you for taking the poll.
Phil, thank you for taking the poll.
Sarah, thank you for taking the poll.
```
### Looping Through All Values in a Dictionary
If you are primarily interested in the values that a dictionary contains, you can use the `#!py values()` method to return a list of values without any keys.  For example, say we simply want a list of all languages chosen in our programming language poll without the name of the person who chose each language:
```py linenums="1"
favorite_languages = {
	'jen': 'python',
	'sarah': 'c',
	'edward': 'ruby',
	'phil': 'python',
}

print("The following languages have been mentioned:")
for language in favorite_languages.values():
	print(language.title())
```
The `#!py for` statement here pulls each value from the dictionary and assigns it to the variable `language`.  When these values are printed, we get a list of all chosen languages:
```
The following languages have been mentioned:
Python
C
Ruby
Python
```
This approach pulls all the values from the dictionary without checking for repeats.  That might work fine with a small number of values, but in a poll with a large number of respondents, this would result in a very repetitive list.  To see each language chosen without repitionm we can use a set.  A *set* is a collection in which each item must be unique.  We can use the following `#!py for` loop in place of the one used above:  
```py
for language in set(favorite_languages.values()):
```
When you wrap `#!py set()` around a list that contains duplicate items, Python identifies the unique items in the list and build a set from those items.  The result is a nonrepetitive list of languages that have been menetioned:  
```
The following languages have been mentioned:
C
Ruby
Python
```
## Nesting
Sometimes you'll want to store multiple dictionaries in a list, or a list of items as a value in a dictionary.  This is called *nesting*.  You can nest dictionaries inside a list, a list of items inside a dictionary, or even a dictionary inside another dictionary.  Nesting is a powerful feature, as the following examples will demonstrate.

### A List of Dictionaries
The `alien_0` dictionary contains a variety of information about one alien, but it has no room to store information about a second alien, much less a full screen of aliens.  How can you managae a fleet of aliens?  One way is to make a list of aliens in which each alien is a dictionary of information about that alien.  For example, the following code builds a list of three aliens:  
```py linenums="1"
alien_0 = {'color': 'green', 'points': 5}
alien_1 = {'color': 'yellow', 'points': 10}
alien_2 = {'color': 'red', 'points': 15}

aliens = [alien_0, alien_1, alien_2]

for alien in aliens:
	print(alien)
```
We first create three dictionaries, each representing a different alien.  On line 5 we store each of these dictionaries in a list called `aliens`.  Finally, we loop through the list and print out each alien:
```
{'color': 'green', 'points': 5}
{'color': 'yellow', 'points': 10}
{'color': 'red', 'points': 15}
```
A more realistic example would involve more than three alies with code that automatically generates each alien.  In the following example we use `#!py range()` to create a fleet of 30 aliens:
```py linenums="1"
# Make an empty list for storing aliens
aliens = []

# Make 30 green aliens.
for alien_number in range(30):
	new_alien = {'color': 'green', 'points': 5, 'speed': 'slow'}
	aliens.append(new_alien)

# Show the first 5 aliens.
for alien in aliens[:5]:
	print(alien)
print("...")

# Show how many aliens have been created.
print(f"Total number of aliens: {len(aliens)}")
```	
This example befins with an empty list to hold all of the aliens that will created.  At line 5 `#!py range()` returns a series of numbers, which just tells Python how many times we want the loop to repeat.  Each time the loop runs we create a new alien (line 6) and then append each new alien to the list `aliens` (line 7).  On line 10 we us a slice to print the first five aliens, and then on line 15 we print the length of the list to prove we've actually generated the full fleet of 30 aliens:
```
{'color': 'green', 'points': 5, 'speed': 'slow'}
{'color': 'green', 'points': 5, 'speed': 'slow'}
{'color': 'green', 'points': 5, 'speed': 'slow'}
{'color': 'green', 'points': 5, 'speed': 'slow'}
{'color': 'green', 'points': 5, 'speed': 'slow'}
...
Total number of aliens: 30
```
These aliens all have the same characteristics, but Python considers each one a separate object, which allows us to modify each alien individually.  

How might you work with a group of aliens like this?  Imagine that one aspect of a game has some aliens changing color and moving faster as the game progress.  When it's time to change colors, we can use a `#!py for` loop and an `#!py if` statement to change the color of the aliens.  For example, to change the first three aliens to yellow, medium-speed aliens worth 10 points each, we could do this:  
```py linenums="1"
# Make an empty list for storing aliens
aliens = []

# Make 30 green aliens.
for alien_number in range(30):
	new_alien = {'color': 'green', 'points': 5, 'speed': 'slow'}
	aliens.append(new_alien)

for alien in aliens[:3]:
	if alien['color'] == 'green':
		alien['color'] = 'yellow'
		alien['speed'] = 'medium'
		alien['points'] = '10'

# Show the first 5 aliens.
for alien in aliens[:5]:
	print(alien)
print("...")
```
Because we want to modify the first three aliens, we loop through a slice that includes only the first three aliens.  All of the aliens are green now but that won't always be the case, so we write an `#!py if` statement to make sure we're only modifying green aliens.  If the alien is green, we change the color to `#!py 'yellow'`, the speed to `#!py 'medium'`, and the point value to `10`, as shown in the following output:
```
{'color': 'yellow', 'points': '10', 'speed': 'medium'}
{'color': 'yellow', 'points': '10', 'speed': 'medium'}
{'color': 'yellow', 'points': '10', 'speed': 'medium'}
{'color': 'green', 'points': 5, 'speed': 'slow'}
{'color': 'green', 'points': 5, 'speed': 'slow'}
...
```
You could expand this loop by adding an `#!py elif` block that turns yellow aliens into red, fast-moving ones worth 15 points each.  Without showing the entire program again, that loop would look like this:
```py linenums="1"
for alien in aliens[:3]:
	if alien['color'] == 'green':
		alien['color'] = 'yellow'
		alien['speed'] = 'medium'
		alien['points'] = '10'
	elif alien['color'] == 'yellow':
		alien['color'] = 'red'
		alien['speed'] = 'fast'
		alien['points'] = 15
```
It's common to store a number of dictionaries in a list when each dictionary contains many kinds of information about one subject.  For example, you might create a dictionary for each user on a website and store the individual dictionaries in a list called `users`.  All of the dictionaries in the list should have an identical structure so you can loop through the list and work with each dictionary object in the same way.  

### A List in a Dictionary
Rather than putting a dictionary inside a list, it's sometimes useful to put a list inside a dictionary.  For example, consider how you might describe a pizza that someone is ordering.  If you were to use only a list, all you could really store is a list of the pizza's toppings.  With a dictionary, a list of toppings can be just one aspect of the pizza you're describing.  

In the following example, two kinds of information are stored for each pizza: a type of crust and a list of toppings.  The list of toppings is a value associated with the key `#!py 'toppings'`.  To use the items in the list, we give the name of the dictionary and the key `#!py 'toppings'`, as we would any value in the dictionary.  Instead of returning a single value, we get a list of toppings:  
```py linenums="1"
# Store information about a pizza being ordered.  
pizza = {
	'crust': 'thick',
	'toppings': ['mushrooms', 'extra cheese'],
}

# Summarize the order.
print(f"You ordered a {pizza['crust']}-crust pizza "
	"with the following toppings:")

for topping in pizza['toppings']:
	print("\t" + topping)
```
We begin on line 2 with a dictionary that holds information about a pizza that has been ordered.  One key in the dictionary is `#!py 'crust'`, and the associated value is the string `#!py 'thick'`.  The next key, `#!py 'toppings'`, has a list as its value that stores all the requested toppings.  On line 8 we summarize the order before building the pizza.  When you need to break up a long ling in a `#!py print()` call, choose an appropriate point at which to break the line being printed and quotation mark.  Indent the next line, add an opening quotation mark, and continue the string.  Python will automatically combine all of the strings it finds inside the parentheses.  To print the toppings, we write a `#!py for` loop on line 10.  To access the list of toppings, we use the key `#!py 'toppings'`, and Python grabs the list of toppings from the dictionary.  

The following output summarizes the pizza that we plan to build:  
```
You ordered a thick-crust pizza with the following toppings:
	mushrooms
	extra cheese
```
You can nest a list inside a dictionary any time you want more than one value to be associated with a single key in a dictionary.  In the earlier example of favorite programming languages, if we were to store each person's responses in a list, people could choose more than one favorite language.  When we loop through the dictionary, the value associated with each person would be a list of languages rather than a single language.  Inside the dictionary's `for` loop, we use another `for` loop to run through the list of languages associated with each person:  
```py linenums="1"
favorite_languages = {
	'jen': ['python', 'ruby'],
	'sarah': ['c'],
	'edward': ['ruby', 'go'],
	'phil': ['python', 'haskell'],
}

for name, languages in favorite_languages.items():
	print(f"\n{name.title()}'s favorite languages are:")
	for language in languages:
		print(f"\t{language.title()}")
```
As you can see on line 1, the value associated with each name is now a list.  Notice that some people have one favorite language and others have multiple favorites.  When we loop through the dictionary on line 8, we use the variable name `languages` to hold each value from the dictionary, because we know that each value will be a list.  Inside the main dictionary loop, we use another `#!py for` loop (line 10) to run through each persons list of favorite languages.  

Now each person can list as many favorite languages as they like:  
```
Jen's favorite languages are:
	Python
	Ruby

Sarah's favorite languages are:
	C

Edward's favorite languages are:
	Ruby
	Go

Phil's favorite languages are:
	Python
	Haskell
```
To refine this program even further, you can ad an `#!py if` statement at the beginning of the dictionary's `#!py for` loop to see whether each person has more than one favorite language by examining the value of `#!py len(languages)`.  If a person has more than one favoriem the output would stay the same.  If the person has only one favorite language, you could change the wording to reflect that.  For example, you could say "Sarah's favorite language is C."

### A Dictionary in a Dictionary
You can nest a dictionary inside another dictionary, b ut your code can get complicated quickly when you do.  For example, if you have several users for a website, each with a unique username, you can use the usernames as the keys in a dictionary.  You can then store information about each user by using a dictionary as the value associated with their username.  In the following listing, we store three pieces of information about each user: their first name, last name, and location.  We'll access this information by looping through the usernames and the dictionary of information associated with each username:  
```py linenums="1"
users = {
	'aeinstein': {
		'first': 'albert',
		'last': 'einstein',
		'location': 'princeton',
	},
	'mcurie': {
		'first': 'marie',
		'last': 'curie',
		'location': 'paris',
	},
}

for username, user_info in users.items():
	print(f"\nUsername: {username}")
	full_name = f"{user_info['first']} {user_info['last']}"
	location = user_info['location']

	print(f"\tFull name: {full_name.title()}")
	print(f"\tLocation: {location.title()}")
```
We first define a dictionary called `users` with two keys: one each for the usernames `#!py 'aeinstein'` and `#!py 'mcurie'`.  The value associated with each key is a dictionary that includes each user's first name, last name, and location.  On line 14 we loop through the `users` dictionary.  Python assigns each key to the variable `username`, and the dictionary associated with each username is assigned to the variable `user_info`.  Once inside the main dictionary loop, we print the user-name at line 15.  

On line 16 we start accessing the inner dictionary.  The variable `user_info`, which contains the dictionary of user information, has three keys: `#!py 'first'`, `#!py 'last'`, and `#!py 'location'`.  We use each key to generate a neatly formated full name and location for each person, and then print a summary of what we know about each user:
```
Username: aeinstein
	Full name: Albert Einstein
	Location: Princeton

Username: mcurie
	Full name: Marie Curie
	Location: Paris
```
Notice that the structure of each user's dictionary is identical.  Although not required by Python, this structure makes nested dictionaries easier to work with.  If each user's dictionary had different keys, the code inside the `#!py for` loop would be more complicated.  