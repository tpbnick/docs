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

## Passing Arguments
Because a function definition can have multiple parameters, a function call may need multiple arguments.  You can pass arguments to your functions in a number of ways.  You can use [*positional arguments*](https://docs.nicklyss.com/py-functions/#positional-arguements), which need to be in the same order as the parameters were written; *keyword arguements*, where each argument consists of a variable name and a value; and lists and dictionaries of values.  

### Positional Arguments
When you call a function, Python must match each argument in the function call with a parameter in the function definition.  The simplest way to do this is baased on the order of the arguments provided.  Values matched up this way are called *positional arguments*.  

To see how this works, consider a function that displays information about pets.  The function tells us what kind of animal each pet is and the pet's name, as shown here:  
```py linenums="1"
def describe_pet(animal_type, pet_name):
	"""Display information about a pet."""
	print(f"\nI have a {animal_type}.")
	print(f"My {animal_type}'s name is {pet_name.title()}.")

describe_pet('hamster', 'harry')
```
The definition shows that this function needs a type of animal and the animal's name (line 1).  When we call `describe_pet()`, we need to provide an animal type and a name, in that order.  For example, in the function call, the argument `'hamster'` is assigned to the parameter `animal_type` and the argument `'harry'` is assigned to the parameter `pet_name` (line 6).  In the function body, these two parameters are used to display information about the pet being described.  

The output describes a hamster named Harry:
```
I have a hamster.
My hamster's name is Harry.
```
#### Multiple Function Calls
You can call a function as many times as needed.  Describing a second, different pet requires just one more call to `describe_pet()`:
```py linenums="1"
def describe_pet(animal_type, pet_name):
	"""Display information about a pet."""
	print(f"\nI have a {animal_type}.")
	print(f"My {animal_type}'s name is {pet_name.title()}.")

describe_pet('hamster', 'harry')
describe_pet('dog', 'willie')
```
The only change above was to line 7.  In the second function call, we pass `describe_pet()` the arguments `'dog'` and `'willie'`.  As with the previous set of arguments we used, Python matches `'dog'` with the parameter `animal_type` and `'willie'` with the parameter `pet_name`.  As before, the function does its job, but this time it also prints the values for a Dog named Willie:
```
I have a hamster.
My hamster's name is Harry.

I have a dog.
My dog's name is Willie.
```
Calling a function multiple times is a very efficient way to work.  The code describing a pet is written once in the function.  Then, anytime you want to describe a new pet, you call the function with the new pet's information.  Even if the code for describing a pet were to expand to ten lines, you could still describe a new pet in just one line by calling the function again.  

You can use as many positional arguments as you need in your functions.  Python works through the arguments you provide when calling the function and matches each one with the corresponding parameter in the function's definition.  

#### Order Matters in Positional Arguments
You can get unexpected results if you mix up the order of the arguments in a function call when using positional arguments:
```py linenums="1"
def describe_pet(animal_type, pet_name):
	"""Display information about a pet."""
	print(f"\nI have a {animal_type}.")
	print(f"My {animal_type}'s name is {pet_name.title()}.")

describe_pet('harry', 'hamster')
```
In the above function, we list the name first and the type of animal second.  Because the argument `'harry'` is listed first this time, that value is assigned to the parameter `animal_type`.  Likewise, `'hamster'` is assigned to `pet_name`.  Now we have a "harry" named "Hamster":
```
I have a harry.
My harry's name is Hamster.
```
If you get funny results like this, check to make sure the order of the arguments in your function call matches the order of the parameters in the function's definition. 

### Keyword Arguments
A *keyword argument* is a name-value pair that you pass to a function.  You directly associate the name of the value within the argument, so when you pass the argument to the function, there's no confusion (you won't end up with a harry named Hamster).  Keyword arguments free you from having to worry about correctly ordering your arguments in the function call, and they clarify the role of each value in the function call.  

Let's rewrite the program from above using keyword arguments to call `describe_pet()`:
```py linenums="1"
def describe_pet(animal_type, pet_name):
	"""Display information about a pet."""
	print(f"\nI have a {animal_type}.")
	print(f"My {animal_type}'s name is {pet_name.title()}.")

describe_pet(animal_type='hamster', pet_name='harry')
```
The function `describe_pet()` hasn't changed, but when we call the function, we explicitly tell Python which parameter each argument should be matched with.  When Python reads the function call, it knows to assign the argument `'hamster'` to the parameter `animal_type` and the argument `'harry'` to `pet_name`.  The output correctly shows that we have a hamster named Harry.  

The order of keyword arguments doesn't matter because Python knows where each value should go.  The following two function calls are equivalent:  
```py linenums="1"
describe_pet(animal_type='hamster', pet_name='harry')
describe_pet(pet_name='harry', animal_type='hamster')
```
### Default Values
When writing a function, you can define a *default value* for each parameter.  If an argument for a parameter is proivided in the function call, Python uses the argument value.  If not, it uses the parameter's default value.  So when you define a default value for a parameter, you can exclude the corresponding argument you'd usually write in the function call.  Using default values can simplify your function calls and clarify the ways in which your functions are typically used.  

For example, if you notice that most of the calls to `describe_pet()` are being used to describe dogs, you can set the default value of `animal_type` to `'dog'`.  Now anyone calling `describe_pet()` for a dog can omit that information:  
```py linenums="1"
def describe_pet(pet_name, animal_type='dog'):
	"""Display information about a pet."""
	print(f"\nI have a {animal_type}.")
	print(f"My {animal_type}'s name is {pet_name.title()}.")

describe_pet(pet_name='willie')
```
We changed the definition of `describe_pet()` to include a default value, `'dog'`, for `animal_type`.  Now when the function is called with no `animal_type` specified, Python knows to use the value `'dog'` for this parameter:  
```
I have a dog.
My dog's name is Willie.
```
