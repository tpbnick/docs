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
This dictionary stores one piece of information about `alien_0`, namely the alien's color.  The string `'color'` is a key in this dictionary, and its associated value is `'green'`.  

### Accessing Values in a Dictionary
To get the value associated with a key, give the name of the dictionary and then place the key inside a set of square brackets, as shown here:  
```py linenums="1"
alien_0 = {'color': 'green'}
print(alien_0['color'])
```
This returns the value associated with the key `'color'` from the dictionary `alien_0`:
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