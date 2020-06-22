# If Statements

Python often involves examining a set of conditions and deciding which action to take based on those conditions.  Python's `if` statement allows you to examine the current state of a program and respond appropriately to that state.  

## A Simple Example
The following short example shows how `if` tests let you respond to special situations correctly.  Imagine you have a list of cars and you want to print out the name of each car.  Car names are proper names, so the names of most cars should be printed in title case.  However, the value `'bmw'` should be printed in all uppercase.  The following code loops through a list of car names and looks for the value `'bmw'`.  Whenever the value is `'bmw'`, it's printed in uppercase instead of title case.  

```py linenums="1"
cars = ['audi', 'bmw', 'subaru', 'toyota']

for car in cars:
	if car == 'bmw':
		print(car.upper())
	else:
		print(car.title())
```
The loop in this example first checks to see if the current value of `car` is `'bmw'`.  If it is, the value is printed in all uppercase.  If the value of `car` is anything other than `'bmw'`, it's printed in title case:  

```
Audi
BMW
Subaru
Toyota
```

## Conditional Tests
At the heart of every `if` statement is an expression that canbe evaluated as `True` or `False` and is called a *conditional test*.  Python uses the values `True` and `False` to decide whether the code in an `if` statement should be executed.  If a conditional test evaluates to `True`, Python executes the code following the `if` statement.  If the test evaluates to `False`, Python ignores the code following the `if` statement.  

### Checking for Equality 
Most conditional tests compare the current value of a variable to a specific value of interest.  The simplest conditional test checks whether the value of a variable is equal to the value of interest:  

```py linenums="1"
car = 'bmw'
car == 'bmw'
```
```
True
```
The code at line 1 sets the value of car to 'bmw' using a single equal sign, as you've seen many times already.  The code at line 2 checks whether the value of `car` is `'bmw'` using a double equal sign (`==`).  This *equality operator* returns `True` if the values on the left and right side of the operator match, and `False` if they don't match.  The values in this example match, so Python returns `True`.  

When the value of `car` is anything other than `'bmw'`, this test returns `False`.  

```py linenums="1"
car = 'audi'
car == 'bmw'
```
```
False
```
A single equal sign is really a statment; you might read the code at line one as "Set the value of `car` equal to `'audi'`".  On the other side, a double equal sign, like the one on line 2, asks a question: "Is the vale of `car` equal to `'bmw'`?"  Most programming languages use equal signs in this way.  

### Ignoring Case When Checking for Equality
Testing for equality is case sensitive in Python.  For example, ywo values with different capitalization are not considered equal: 

```py linenums="1"
car = 'Audi'
car == 'audi'
```
```
False
```
If case matters, this behavior is advantageous.  But if case doesn't matter and instead you just want to test the value of a variable, you can convert the variable's value to lowercase before doing the comparison:  

```py linenums="1"
car = 'Audi'
car.lower() == 'audi'
```
```
True
```
This test would return `True` no matter how the value `'Audi'` is formatted because the test is now case insensitive.  The `lower()` function doesn't change the value that was originally stored in `car`, so you can do this kind of comparison without affecting the original variable: 

```py linenums="1"
car = 'Audi'
car.lower() == 'audi'
```
```
True
```
```py linenums="1"
car
```
```
'Audi'
```
At the first line 1, we assigned the capitalized string `'Audi'` to the variable `car`.  At line 2, we convert the value of `car` to lowercase and compare the lowercase value to the string `'audi'`.  The two strings match, so Python returns `True`.  When we check what is stored in `car` again, we can see that it has not been affected by the `lower()` method.  

Websites enforce certain rules for the data that users enter in a manner similar to this.  For example, a site might use a conditional test like this to ensure that every user has a truly unique username, not just a variation on the capitalization of another person's username.  When someone submits a username, that new username is converted to lowercase and compared to the lowercase versions of all existing usernames.  During this check, a username like `'John'` will be rejected if any variation of `'john'` is already in use.  

### Checking for Inequality 
When you want to determine whether two values are not equal, you can combine an exclamation point and an equal sign (!=).  The exclamation point represents *not*, as it does in many programming languages.  

Let's use another `if` statement to examine how to use the inequality operator.  We'll store a requested pizza topping in a variable and then print a message if the person did not order anchovies:  

```py linenums="1"
requested_topping = 'mushrooms'

if requested_topping != 'anchovies':
	print("Hold the anchovies!")
``` 
The code on line 3 compares the value of `requested_topping` to the value `anchovies`.  If these two values do not match, Python returns `True` and executes the code following the `if` statement.  If the two values match, Python returns `False` and does not run the code following the `if` statement.  

Because the value of `requested_topping` is not `anchovies`, the `print()` function is executed: 

```
Hold the anchovies!
```
Most of the conditional expressions you write will test for equality, but sometimes you'll find it more efficient to test for inequality.  

### Numerical Comparisons 
Testing numerical values is pretty straightforward.  For example, the following code checks whether a person is 18 years old: 

```py linenums="1"
age = '18'
age == '18'
```
```
True
```
You can also test to see if two numbers are not equal.  For example, the following code prints a message if the given answer is not correct:
```py linenums="1"
answer = 17

if answer != 42:
	print("That is not the correct answer.  Please try again!")
```
The conditional test at line 3 passes, because the value of `answer` (17) is not equal to 42.  Because the test passes, the indented code block is executed.  

You can include various mathematical comparisons in your conditional statements as well, such as less than, less than or equal to, greater than, and greater than or equal to.  

### Checking Multiple Conditions
You may want to check multiple conditions at the same time.  For example, sometimes you might need two conditions to be `True` to take an action.  Other times you might be satisfied with just one condition being `True`.  The keywords `and` and `or` can help you in these situations. 

#### Using `and` to Check Multiple Conditions
To check whether two conditions are both `True` simultaneously, use the keyword `and` to combine the two conditional tests; if each test passes, the overall expression evaluates to `True`.  If either test fails or if both tests fail, the expression evaluates to `False`.  

For example, you can check whether two people are both over 21 using the following test:  

```py linenums="1"
age_0 = 22
age_1 = 18
age_0 >= 21 and age_1 >= 21
```
```
False
```
On line 1, we define two ages, `age_0` and `age_1`.  On line 3, we check whether both ages are 21 or older.  The test on the left passes, but the one on the right fails, so the overall conditional expression evaluates to `False`. 
```py linenums="1"
age_1 = 22
age_0 >= 21 and age_1 >= 21
```
```
True
```
On line 1, we change `age_1` to 22. The value of `age_1` is now greater than 21, so both individual tests pass, causing the overal conditional expression to evaluate as `True`.  

To improve readability, you can use parentheses around the individual tests, but they are not required.  If you use parentheses, your test would look like this:  
```py linenums="1"
(age_0 >= 21) and (age_1 >= 21)
``` 

#### Using `or` to Check Multiple Conditions  
The keyword `or` allows you to check multiple conditions as well, but it passes when either or both of the individual test pass.  As `or` expression fails onl when both individual tests fail.  

Let's consider two ages again, but this time we'll look for only one person to be over 21:  

```py
age_0 = 22
age_1 = 18
age_0 >= 21 or age_1 >=21
```
```
True
```
We start with two variables again at line 1.  Because the test for `age_0` at line 3 passes, the overall expression evaluates to `True`.  
```py
age_0 = 18
age_0 >= 21 or age_1 >= 21
```
We now lowe `age_0` to 18.  In the test at line 2, both tests now fail and the overall expression evaluates to `False`.  

### Checking Whether a Value Is in a List  
Sometimes it is important to check whether a list contains a certain value before taking an action.  For example, you might want to check whether a new username already exists in a list of current usernames before completeing someone's registration on a webstie.  In a mapping project, you might want to check whether a submitted location already exists in a list of known locations.  

To find out whether a particular value is already in a list, use the keyword `in`.  Let's consider some code you might write for a pizzeria.  We'll make a list of toppings a customer has requested for a pizza and then check whether certain toppings are in the list.  

```py
requested_toppings = ['mushrooms', 'onions', 'pineapple']
'mushrooms' in requested_toppings
```
```
True
```
```py
'pepperoni' in requested_toppings
```
```
False
```
We told Python to check for the existence of `'mushrooms'` and `'pepperoni'` in the list `requested_toppings`.  This technique is quite powerful because you can create a list of essential values, and then easily check whether the value you're testing matches one of the values in the list.  

### Checking Whether a Value is Not in a List
Other times, it's important to know if a value does not appear in a list.  You can use the keyword `not` in this situation.  For example, consider a list of users who are banned from commenting in a forum.  You can check whether a user has been banned before allowing that user to submit a comment:  

```py linenums="1"
banned_users = ['andrew', 'carolina', 'david']
user = 'marie'

if user not in banned_users:
	print(f"{user.title()}, you can post a response if you wish.")
```

The code on line 4 reads quite clearly.  If the value of `user` is not in the list of `banned_users`, Python returns `True` and execites the indented line.  

The user `'marie'` is not in the list `banned_users`, so she sees a message inviting her to post a response: 

```
Marie, you can post a response if you wish.
```  

### Boolean Expressions
A Boolean expression is just another name for a condtitional test.  A *Boolean value* is either `True` or `False`, just like the value of a conditional expression after it has been evaluated.  

Boolean values are often used to keep track of certain conditions, such as whether a game is running or whether a user can edit certain content on a website.  

```py
game_active = True
can_edit = False
```