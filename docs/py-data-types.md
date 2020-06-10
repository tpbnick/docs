# Variables and Simple Data Types  

## Variables 

Let's go back to the [first program](https://docs.nicklyss.com/py#first-program) and use a variable.  To do this, we simply add a new line at the beginning of the file and modify the second line:  

```py linenums="1"
message = "Hello Python World!"
print(message)
```
We have now created a *variable* named `message`.  Every variable is connected to a *value*, which is the information associated with that variable.  In this case the value is the `Hello Python World!` text.  

Adding a variable makes a little more work for the Python interpreter.  When it processes the first line, it associates the variable `message` with the `Hello Puthon World!` text. When it reaches the second line, it prints the value associated with `message` to the screen.  

### Naming and Using Variables 

When you're using variables in Python, you need to adhere to a few rules and guidelines.  breaking some of these rules will cause errors; other guidelines just help you write code that's easier to read and understand.  Be sure to keep the following variable rules in mind:  

* Variable names can contain only letters, numbers and underscores.  They can start with a letter or underscore, but not with a number.

* Spaces are not allowed in variable names, underscores should be used instead.

* Avoid using Python keywords and function names as variable names that serve a particular programmatic purpose.  This could cause many different problems. 

* Variable names should be short but descripitve.  For example, `name` is better than `n`.

* Be careful when using the lowercase *l* and the uppercase letter *O* because they could be confused with the numbers *1* and *0*.  

## Strings  

Because most programs define and gather some sort of data, and then do something useful with it, it helps to classify different types of data.  The first data type we'll look at is the *string*.  Strings are quite simple at first glance, but you can use them in many different ways.  

A *string* is a series of characters.  Anything inside quotes is considered a string in Python, and you can use single or double quotes around your strings like this: 

```py linenums="1"
"This is a string"
'This is also a string'
```

This flexibility allows you to use quotes and apostrophes within your strings:

```py linenums="1"
'I told my friend, "Python is my favorite language!"'
``` 

### Changing Case in a String with Methods 

One of the simplest tasks you can do with strings is change the case of the words in a string:  

```py linenums="1"
name = "ada lovelace"
print(name.title())
```

In the above example, the variable `name` refers to the lowercase string `ada lovelace`/  The method `title()` appears after the variable in the `print()` call.  A *method* is an action that Python can perform on a piece of data.  The dot (.) after `name` in `name.title()` tells Python to make the `title()` method act on the variable `name`.  

The `title()` method changes each word to title case, where each word begins with a capital letter.  This is useful because you'll often want to think of a name as a piece of information.  For example, you might want to program the input values of `Ada`. `ADA`, and `ada` as the same name, and display them all as `Ada`.  

Several other useful methods are available for dealing with case as well.  For example, you can change a string to all uppercase or all lowercase letters like this:  

```py linenums="1"
name = "Ada Lovelace"
print(name.upper())
print(name.lower())
``` 

This will display the following: 

```
ADA LOVELACE
ada lovelace
``` 

### Using Variables in Strings

In some situations, you may want to use a variable's name inside a string.  For example, you might want two variables to represent a first name and a last name respectively, and then want to combine those values to display someone's full name:

```py linenums="1"
first_name = "ada"
last_name = "lovelace"
full_name = f"{first_name} {last_name}"
print(full_name)
``` 

To insert a variable's value into a string, place the letter `f` immediately before the opening quoatation mark. Put braces around the name or names of any variable you want to use inside the string.  Python will replace each variable with its value when the string is displayed.  

These strings are called *f-strings*.  The *f* is for *format*, because Python formats the string by replaceing the name of any variable in braces with its value.  

You can do a lot with f-strings.  For example, you can use f-strings to compose complete messages using the information associated with a variable:  

```py linenums="1"
first_name = "ada"
last_name = "lovelace"
full_name = f"{first_name} {last_name}"
print(f"Hello, {full_name.title()}!")
```
The above code would display the following:  

```
Hello, Ada Lovelace!
```  

We can actually make this even simpler, by assigning the entire message to a variable:  

```py linenums="1"
first_name = "ada"
last_name = "lovelace"
full_name = f"{first_name} {last_name}"
message = f"Hello, {full_name.title()}!"
print(message)
```
The final `print()` call is much simpler in this case.  

??? warning "f-string compatibility"
	f-strings were first introduced in Python 3.6.  If you are using Python 3.5 or earlier, you must use the `format()` method rather than the above `f` syntax. To use format(), list the variables you want to use in the string inside the parentheses following format.  Each variable is referred to by a set of braces; the braces will be filled by the values listed in parentheses in the order provided: 

	```py linenums="1"
	full_name = "{} {}".format(first_name, last_name)
	```

### Adding Whitespace to Strings with Tabs or Newlines  

In programming, *whitespace* refers to any nonprinting character, such as spaces, tabs, and end-of-line symbols.  You can use whitespace to organize your output so it's easier for users to read.  

* To add a tab to your text, use the character combination `\t`.

* To add a newline in a string, use the character combination `\n`.  

* You can also combine tabs and newlines in a single string.  The string `\n\t` tells Python to move to a new line and start the next line with a tab.  

### Stripping Whitespace  

Extra whitespace can be confusing in your programs.  To programmers, `'python'` and `'python '` look pretty much the same, but to a program, they are two different strings.  Puthon detects the extra space in `'python '` and considers it significant unless you tell it otherwise.  

It is important to think about whitespace, because often you'll want to compare two strings to determine whether they are the same.  For example, one important instance might involve checking people's usernames when they login to a website.  Extra whitespace can be confusing in much simpler situations as well.  Fortunately, Python makes it simple to eliminate extraneous whitespace from data that people enter.  

Python can look for extra whitespace on the right and left sides of a string.  To ensure that no whitespace exists at the right end of a string, use the `rstrip()` method.  

```py linenums="1"
favorite_language = 'python '

favorite_language
>>> 'python '

favorite_language.rstrip()
>>>'python'
```

Running the above code with the `rstrip()` method does not permanently remove the whitespace at the end of the string.  If the code was run again without the `rstrip()`, the extra whitespace would appear again.  

### Avoiding Syntax Errors with Strings  

One kind of error that you mught see with some regularity is a syntax error.  A *syntax error* occurs when Python doesn't recognize a section of your program as valid Python code.  For example, if you use an apostrophe within single quotes, you will produce an error.  This happens because Python interprets everything between the first single quote and the apostrophe as a string.  

Luckily, Python will let you know where the error is located and will try it's best to say what the problem is.  Sometimes, the error is straight forward, but sometimes, it will require additional research to find a solution.  

## Numbers  

Numbers are used quite often in programming to keep score in games, represent data in visualizations, store information in web applications, and so on.  Python treats numbers in several different ways.  Let's first take a look at how Python manages integers, because they are the simplest to work with:  

You can add (`+`), subtract (`-`), multiply (`*`) and divide (`/`) integers in Python.

```py linenums="1" 
>>> 2 + 3
5

>>> 3 - 2
1

>>> 2 * 3
6

>>> 3 / 2
1.5
```

In a terminal session, Python simply returns the result of the operation.  Python uses two multiplication symbols to represent exponents: 

```py linenums="1"
>>> 3 ** 2 
9

>>> 3 ** 3
27

>>> 10 ** 6
1000000
```  

Python supports the order of operations too, so you can use multiple operations in one expression.  You can also use parentheses to modify the order of operations so Python can evaluate your expression in the order you specify.  For example:

```py linenums="1"
>>> 2 + 3*4
14

>>> (2 + 3) * 4
20
```

### Floats

Python calls any number with a decimal point a *float*. This term is used in most programming languages (like in [C](https://docs.nicklyss.com/c)), and it refers to the fact that a decimal point can appear at any position in a number.  Every programming language must be carefully designed to properly manage decimal numbers so numbers behave appropriately no matter where the decimal point appears.  

For the most part, you can use decimals without worrying how they behave.  Simply enter the numbers you want to use, and Python will most likely do what you expect:  

```py linenums="1"
>>> 0.1 + 0.1
0.2

>>> 0.2 * 0.2
0.4
``` 

But beware, sometimes you will get an arbitrary number of decimals in your answer:  

```py linenums="1"
>>> 0.2 + 0.1
0.3000000000000004

>>> 0.3 * 0.1
0.3000000000000004
``` 
This happens in all languages and is of little concern.  Python tries to find a way to represent the result as precisely as possible, which is sometimes difficult given how computers have to represent numbers internally.  

### Integers and Floats  

When you divide any two numbers, even if they are integers that result in a whole number, you'll always get a float: 

```py linenums="1"
>>> 4/2
2.0
```
If you mix an integer and a float in any operation, you'll get a float as well.  Python defaults to a float in any operation that uses a float, even if the output is a whole number.  

### Underscores in Numbers  

When you're writing long numbers, you can group digits using underscores to make large numbers more readable in code: 

```py linenums="1"
universe_age = 14_000_000_000
```
When you print a number that was defined with underscores, Python only prints the digits.  Even if the numbers are not grouped in threes, Python will still ignore the underscores.  This feature works for both integers and floats, but only in Python 3.6 and later.  

### Multiple Assignment 

You can assign values to more than one variable using just a single line.  This can help shorten your programs and make them easier to read; you'll use this technique most often when initializing a set of number.  

For example, here is how you can initialize the variables `x`, `y`, and `z` to zero: 

```py linenums="1"
x, y, z = 0, 0, 0
```

You need to separate the variable names with commas, and do the same with the values, and Python will assign each value to its respectively positioned variable.  As long as the number of values matches the number of variables, Python will match them up correctly.  

### Constants

A *constant* is like a variable whose value stays the same throughout the life of a program.  Python doesn't have built-in constant types, but Python programmers use all capital letters to indicate a variable should be treated as a constant and never be changed: 

```py linenums="1"
MAX_CONNECTIONS = 5000
```

## Comments

Comments are an extremely useful feature in most programming languages.  Adding a hash mark (#) indicates a comment.  Anything following a hash mark in your code is ignored by the Python interpreter until a new line of code is detected.  

Comments should be written throughout your program to help whoever is reading it understand what does what.  