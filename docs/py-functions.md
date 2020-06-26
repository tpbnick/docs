# Functions
On this page we'll learn how to write *functions*, which are named blocks of code that are designed to do one specific job.  When you want to perform a particular task that you've defined in a function, you *call* the function responsible for it.  If you need to perform that task multiple times throughout your program, you don't need to type all the code for the same task again and again; you just call the function dedicated to handling that task, and the call tells Python to run the code inside the function.  You'll find that using functions makes your programs easier to write, read, test, and fix.  

We will also learn ways to pass information to functions.  We will learn how to write certain functions whose primary job is to display information and other functions desinged to process data and return a value or a set of values.  Finally, we will cover how to store functions in separate files called *modules* to help organize our main program files.  

## Defining a Function 
Here is a simple function named `greet_user()` that prints a greeting:
```py linenums="1"
def greet_user():
	"""Display a simple greeting."""
	print("Hello!")
greet_user()
```
This example shows the simplest structure of a function.  The code on line 1 uses the keyword `def` to inform Python that you're defining a function.  This is the *function definition*, which tells Python the name of the function and, if applicable, what kind of information the function needs to do its job.  The parentheses hold that information.  In this case, the name of the function is `greet_user()`, and it needs no information to do its job, so its parentheses are empty.  (Even so, the parentheses are required.)  Finally, the definition ends in a colon.  

An indented lines that follow `def greet_user():` make up the *body* of the function.  The text on line 2 is a comment called a *docstring*, which describes what the function does.  Docstrings are enclosed in triple quotes, which Python looks for when it generates documentaion for the functions in your programs.  

The line `print("Hello!")` on line 3 is the only line of actual code in the body of this function, so `greet_user()` has just one job: `print("Hello!")`.  

When you want to use this function, you call it.  A *function call* tells Python to execute the code in the function.  To *call* a function, you write the name of the function, followed by any necessary information in parentheses, as shown on line 4.  Because no information is needed here, calling our function is as simple as entering `greet_user()`.  As expected, it prints `Hello!`.

### Passing Information to a Function
Modified slightly, the function `greet_user()` can not only tell the user `Hello!` but also greet them by name.  For the function to do this, you enter `username` in the parentheses of the function's definition at `def greet_user()`.  By adding `username` here you allow the function to accept any value of `username` you specify.  The function now expects you to provide a value for `username` each time you call it.  When you call `greet_user()`, you can pass it a name, such as `'jesse'`, inside the parentheses:
```py linenums="1"
def greet_user(username):
	"""Display a simple greeting."""
	print(f"Hello, {username.title()}!")

greet_user('jesse')
```
Entering `greet_user('jesse')` calls `greet_user()` and give the function the information it needs to execute the `print()` call.  The function acceptsthe name you passed it and displays the greeting for that name:
```
Hello, Jesse!
```
### Arguments and Parameters
In the preceding `greet_user()` function, we defined `greet_user()` to require a value for the variable `username`.  Once we called the function and gave it the information (a person's name), it printed the right greeting.  

The variable `username` in the definition of `greet_user()` is an example of a *parameter*, a piece of information the function needs to do its job.  The value `'jesse'` is `greet_user('jesse')` is an example of an *argument*.  An argument is a piece of information that's passed from a function call to a function.  When we call the function, we place the value we want the function to work with in the parenthese.  In this case the argument `'jesse'` was passed to the function `greet_user()`, and the value was assigned to the parameter `username`.  
