# Python Basics

## Quick Links  

* [Python Documentation](https://docs.python.org/3.7/search.html)  

* [Python Beginner's Help (PDF)](https://nicklyss.com/wp-content/uploads/2020/06/python_beginner_cheatsheet.pdf)  

* [Python Cheat Sheet](https://www.pythoncheatsheet.org/)  

* [Learning Python - 5th Edition (2014) (PDF)](https://nicklyss.com/wp-content/uploads/2020/06/Learning-Python-5th-Edition-by-Mark-Lutz-z-lib.org_.pdf)

* [Python Crash Course - 2nd Edition (2019) (PDF)](https://nicklyss.com/wp-content/uploads/2020/06/Python-Crash-Course-2nd-Edition-A-Hands-On-Project-Based-Introduction-to-Programming.pdf)

* [Python Crash Course - Basics](https://ehmatthes.github.io/pcc_2e/cheat_sheets/cheat_sheets/)

## Introduction  

Python is a powerful multiparadigm computer programming language, optimized
for programmer productivity, code readability, and software quality.  

Python is a popular open source programming language used for both standalone programs and scripting applications in a wide variety of domains

Python is an excellent and versatile language choice for making complex C operations much simpler:  

* String manipulation 

* Networking  

### Python Syntax  

To start writing Python, open up a file with the .py file extension.  

Unlike a C program, which typically has to be compiled before you run it, a Python program can be run without explicitly compiling it first.  

#### Variables

Python variables have three big differences from C:  

* No type specifier

* Declared by initialization only  

* Python statements do not need to be ended with semicolons  

#### Conditionals 

* All of the old favorites from C are still available for you to use:  

* elif - else if 

* True / False (bool)  

* input() - collects user input  

**Loops** 

Two varieties: while and for 

```py linenums="1"
counter = 0
while counter < 100:
		print(counter)
		counter += 1
```  

```py linenums="1" 
for x in range(100):
	print(x)
```  

#### ~~Arrays~~ Lists

Here is where things really start to get a lot better than C.  

Python arrays (more appropriately known as *lists*) are **not** fixed in size; they can grow or shrink as needed, and you can always tack extra elements onto your array and splce things in and out easily.  

```py linenums="1"
nums = [1, 2, 3, 4]
```  
Instead of square bracket syntax, you can also simply use a function to create a list:  

```py linenums="1"
nums = list()
``` 

#### Tuples  

Tuples are ordered, immutable sets of data; they are great for associating collections of data, sort of like a `struct` in C, but where those values are unlikely to change.  

Here is a list of tuples:  

```py linenums="1"
presidents = [
	("George Washington", 1789),
	("John Adams", 1797),
	("Thomas Jefferson", 1801),
	("James Madison", 1809)
]
```
This list is iterable as well: 

```py linenums="1"
for prez, year in presidents:
	print("In {1}, {0} took office".format(prez, year))
```  

#### Dictionaries  

Python also has built in support for dictionaries, allowing you to specifiy list indices with words or phrases (keys).  

```py linenums="1"
pizzas = {
	"cheese": 9,
	"pepperoni": 10,
	"vegetable": 11,
	"buffalo chicken": 12
}
```  

#### Functions

Python has support fr functions as well.  Like variables, we don't need to specifiy the return type of the function (because it doesn't matter), nor the data types of any parameters.  

All functions are introduced with the `def` keyword.  

```py linenums="1"
def square(x):
	result = 0
	for i in range(0, x):
		result += x
	return result
```  

#### Objects  

Python is an *object-oriented* programming language.  

Objects have properties and *methods*, or functions that are inherent to the object, and mean nothing outside of it.  You must also define methods inside the object.  

```py linenums="1"
object.method()
```  

You define a type of object using the `class` keyword in Python.  

Classes require an initialization function, also more-generally known as a *constructor*, which sets the starting values of the properties of the object.  

In defining each method of an object, `self` should be its first parameter, which stipulates on what object the method is called.  

```py linenums="1"
class Student():

	def __init__(self, name, id):
		self.name = name
		self.id = id

	def changeID(self, id):
		self.id = id

	def print(self):
		print("{} - {}".format(self.name, self.id))
```

#### Style  

If you haven't noticed by now, good style is **crucial** in Python.  

Tabs and indentation actually matter in this language, and things will not work the way you intend for them to if you disregard styling!  

## First Program  

```py linenums="1"
print("Hello Python World!")
```  

If you compare this to C's [first code](https://docs.nicklyss.com/c#first-code), you will notice that we no longer need to create a `main` function or import the `<stdio.h>` library.  

## Troubleshooting in Python  

When a program contains a significant error, Python displays a *trace-back*, which is an error report.  Python looks through the file and tries to identify the problem.  Check the traceback; it might give you a clue as to what the issue is preventing the program from running.  

Remember how important syntax is in Python, and every other programming language, and review your code.  