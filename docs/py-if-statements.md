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

## `if` Statements
When you understand conditional tests, you can start writing `if` statements.  Several different kinds of `if` statments exist, and your choice of which to use depends on the number of conditions you need to test.  You saw several examples of `if` statments in the discussion about conditional tests, but now let's dif deeper into the topic.  

### Simple `if` Statements
The simplest kind of `if` statment has one test and one action:  
```py
if conditional_test:
	do something
```  

You can put any conditional test in the first line and just about any action in the indented block following the test.  If the condtional test evaluates to `True`, Python executes the code following the `if` statement.  If the test evaluates to `False`, Python ignores the code following the `if` statement.  

Let's say we have a variable representing a person's age, and we want to know if that person is old enough to vote.  The following code tests whether the person can vote:  
```py linenums="1"
age = 19
if age >= 18:
	print("You are old enough to vote!")
```
On line 2, Python checks to see whether the value of age is greater than or equal to 18.  It is, so Python executes the indented `print()` call on line 3:
```
You are old enough to vote!
```

Indentation plays the same role in `if` statements as it did in `for` loops.  All indented lines after an `if` statement will be executed if the test passes, and the entire block if indented lines will be ignored if the test does not pass.  
You can have as many lines of code as you want in the block following the `if` statement.  Let's add another line of output if the person is old enough to vote, asking if the individual has registered to vote yet:
```py linenums="1"
age = 19
if age >= 18:
	print("You are old enough to vote!")
	print("Have you registeredto vote yet?")
```
The conditional test passes, and both `print()` calls are indented, so both lines are printed:
```
You are old enough to vote!
Have you registered to vote yet?
```
If the value of `age` is less than 18, this program would produce no output.  

### `if-else` Statements
Often, you'll want to take one action when a conditional test passes and a different action in all other cases.  Python's `if-else` syntax makes this possible.  An `if-else` block is similar to a simple `if` statement, but the `else` statement allows you to define an action or set of actions that are executed when the conditional test fails.  

We'll display the same message we had previously if the person is old enough to vote, but this time we'll add a message for anyone who is not old enough to vote:
```py linenums="1"
age = 17
if age >= 18:
	print("You are old enough to vote!")
	print("Have you registeredto vote yet?")
else:
	print("Sorry, you are too younng to vote.")
	print("Please register as soon as you turn 18!")
```
If the conditional test on line 2 passes, the first block of indented `print()` calls are executed.  If the test evaluates to `False`, the `else` block on line 5 is executed.  Because age is less than 18 this time, the conditional test fails and the code in the `else` block is executed.  

This code works because it only has two possible situations to evaluate: a person is either old enough to vote or not old enough to vote.  The `if-else` structure works well in situation in which you want Python to always execute one of two possible actions.  In a simple `if-else` chain like this, one of the two actions will always be executed.  

### The `if-elif-else` Chain
Often, you'll need to test more than two possible situations, and to evaluate these you can use Python's `if-elif-else` syntax.  Python executes only one block in an `if-elif-else` chain.  It runs each conditional test in order until one passes.  When a test passes, the code following that test is executed and Python skips the rest of the test.  

Many real-world situations involve more than two possible conditions.  For example, consider an amusement park that charges different rates for different age groups:  

* Admission for anyone under age 4 is free.

* Admission for anyone between the ages of 4 and 18 is $25.  

* Admission for anyone age 18 or older is $40.  

How can we use an `if` statement to determine a person's admission rate?  The following code tests for the age group of a person and then prints an admission price message:  
```py linenums="1"
age = 12

if age < 4:
	print("Your admission cost is $0.")
elif age < 18:
	print("Your admission cost is $25.")
else:
	print("Your admission cost is $40.")
```

The `if` test on line 3 tests whether a person is under 4 years old.  If the test passes, an appropriate message is printed an Python skips the rest of the tests.  The `elif` code on line 5 is really another `if` test, which runs only if the previous test fails.  At this point in the chain, we know the person is at least 4 years old because the first test failed. If the person is under 18, an appropriate message is printed and Python skips the `else` block.  If both the `if` and `elif` tests fail, Python runs the code in the `else` block on line 7.  

In this example, the test on line 3 evaluates to `False`, so its code block is not executed.  However, the second test evaluates to `True` (12 is less than 18) so its code is executed.  The output is one sentence, informing the user of the admission cost:  
```
Your admission cost is $25.
```
Any age greater than 17 would cause the first two tests to fail.  In these situations, the `else` block would be executed and the admission price would be $40.  

Rather than printing the admission price within the `if-elif-else` block, it would be more concise to just set the price inside the `if-elif-else` chain and then have a simple `print()` call that runs after the chain has been evaluated:  

```py linenums="1"
age = 12

if age < 4:
	price = 0
elif age < 18:
	price = 25
else:
	price = 40
print(f"Your admission cost is ${price}.")
```
Lines 4, 6, and 8 set the value of `price` according to the person's age, as in the previous example.  After the price is set by the `if-elif-else` chain, a separate unindented `print()` call line 9 uses this value to display a message reporting the person's admission price.  

This code produces the same output as the previous example, but the
purpose of the `if-elif-else` chain is narrower. Instead of determining a
price and displaying a message, it simply determines the admission price.
In addition to being more efficient, this revised code is easier to modify
than the original approach. To change the text of the output message,
you would need to change only one `print()` call rather than three separate
`print()` calls. 

We can also get user input for age by using a `int(input())` call in line 1 as follows:
```py
age = int(input("What is your age?\n"))
```
**Note**: we must use `int(input)` instead of just `input()` because it will error out when mathematical checks (`<`) are used on a string.  Setting the `input` and an `int` will make the mathematical checks function correctly.  

### Using Multiple `elif` Blocks
You can use as many `elif` blocks in your code as you like.  For example, if the amusement park were to implement a discount for seniors, you could add one more conditional test to the code to determine whether someone qualified for the senior discount.  Let's say anyone 65 or older pays half the regular admission, or $20:  
```py linenums="1"
age = 12

if age < 4:
	price = 0
elif age < 18:
	price = 25
elif age < 65:
	price = 40
else:
	price = 20

print(f"Your admission cost is ${price}.")
```
Most of this code is unchanged.  The second `elif` block on line 7 now checks to make sure a person is less than 65 before assigning them the full admission rate of $40.  Notice that the value assigned in the `else` block on line 9 needs to be changed to $20, because the only ages that make it to this block are people 65 or older.  

### Omitting the `else` Block 
Python does not require an `else` block at the end of an `if-elif` chain.  Sometimes an `else` block is useful; sometimes it is clearer to use an additional `elif` statement that catches the specific condition of interest:  
```py linenums="1"
age = 12

if age < 4:
	price = 0
elif age < 18:
	price = 25
elif age < 65:
	price = 40
elif age >= 65:
	price = 20

print(f"Your admission cost is ${price}.")
```
The extra `elif` block on line 9 assigns a price of $20 when the person is 65 or older, which is a bit clearer than the general `else` block.  With this change, every block of code must pass a specific test in order to be executed.  

The `else` block is a catchall statement.  It matches any condition that wasn't matched by a sepcific `if` or `elif` test, and that can sometimes include invalid or even malicious data.  If you have a specific final confition you are testing for, consider using a file `elif` block and omit the `else` block.  As a result, you'll gain extra confidence that your code will run only under the correct conditions.  

### Testing Multiple Conditions
The `if-elif-else` chain is powerful, but it's only appropriate to use it when you just need one test to pass.  As soon as Python finds one test that passes, it skips the rest of the tests.  This behavior is beneficial, because it's efficient and allows you to test for one specific condition.  

However, sometimes it is important to check all of the conditions of interest.  In this case, you should use a series of simple `if` statments with no `elif` or `else` blocks.  This technique makes sense when more than one condition should be `True`.  

Let's reconsider the pizzeria example.  If someone requests a two-topping pizza, you'll need to be sure to include both toppings on their pizza:  
```py linenums="1"
requested_toppings = ['mushrooms', 'extra cheese']

if 'mushrooms' in requested_toppings:
	print("Adding mushrooms.")
if 'pepperoni' in  requested_toppings:
	print("Adding pepperoni.")
if 'extra cheese' in requested_toppings:
	print("Adding extra cheese.")

print("\nFinished making your pizza!")
```
We start with a list containing the requested toppings.  The `if` statement at line 3 checks to see whether the person requested mushrooms on their pizza.  If so, a message is printed confirming the topping.  The test for pepperoni on like 5 is another simple `if` statement, not an `elif` or `else` statement, so this test runs regardless of whether the previous test passed or not.  The code on like 7 checks whether extra cheese was requested regardless of the results of the first two tests.  These three independent tests are executed every time this program is run.  

Because every condition in this example is evaluated, bot mushrooms and extra cheese are added to the pizza:  

```
Adding mushrooms.
Adding extra cheese.

Finished making your pizza!
```
This code would not work properly if we used an `if-elif-else` block, because the code would stop working after only one test passes.  

In summary, if you want only one block of code to run, use an `if-elif-else` chain.  If more than one code of block needs to run, use a series of independent `if` statements.  

## Using `if` Statements with Lists
You can do some interesting work when you combine lists and `if` statements.  You can watch for special values that need to be treated differently than other values in the list.  You can manage changing conditions efficiently, such as the availability of certain items i a restaurant throughout a shift.  You can also begin to prove that your code works as you expect it to in all possible situations.  

### Checking for Special Items
Earlier, we covered how to handle a special value like 'bmw', which needed to be printed in a different format than other values in the list.  Now that we have a basic understanding of conditional tests and `if` statements, let's take a closer look at how you can watch for special values in a list and handle those values appropriately.  

Let's continue with the pizzeria example.  The pizzeria displays a message whenever a topping is added to your pizza, as it's being made.  The code for this action can be written very efficiently by making a list of toppings the customer has requested and using a loop to announce each topping as it's added to the pizza:  
```py linenums="1"
requested_toppings = ['mushrooms', 'green peppers', 'extra cheese']

for requested_topping in requested_toppings:
	print(f"Adding {requested_topping}.")

print("\nFinished making your pizza!")
```
The output is straightforward because the code is just a simple `for` loop:
```
Adding mushrooms.
Adding green peppers.
Adding extra cheese.

Finished making your pizza!
```
But what if the pizzeria runs out of green peppers?  An `if` statement inside the `for` loop can handle this situation appropriately:
```py linenums="1"
requested_toppings = ['mushrooms', 'green peppers', 'extra cheese']

for requested_topping in requested_toppings:
	if requested_topping == 'green peppers':
		print("Sorry, we are out of green peppers right now.")
	else:
		print(f"Adding {requested_topping}.")

print("\nFinished making your pizza!")
```
This time we check each requested item before adding it to the pizza.  The code at line 4 checks to see if the person requested green peppers.  If so, we display a message that we are out of green peppers.  The `else` block on line 6 ensures that all other toppings are added to the pizza.  

### Checking that a List is Not Empty
We've made a simple assumption about every list we've worked with so far; we've assumed that each list has at least one item in it.  Soon we'll let users provide the information that's stored in a list, so we won't be able to assume that a list has any items in it each time a loop is run.  In this situation, it's useful to check whether a list is empty before running a `for` loop.  

As an example, let's check whether the list of requested toppings is empty before building the pizza.  If the list is empty, we'll prompt the use and make sure they want a plain pizza.  If the list is not empty, we'll build the pizza just as we did in the previous examples:  
```py linenums="1"
requested_toppings = []

if requested_toppings:
	for requested_topping in requested_toppings:
		print(f"Adding {requested_topping}.")
	print("\nFinished making your pizza!")
else:
	print("Are you sure you want a plain pizza?")
```
This time we start out with an empty list.  Instead of jumping right into the `for` loop, we do a quick check on line 3.  When the name of a list is used in an `if` statement, Python returns `True` if the list contains at least one item; an empty list evaluates to `False`.  If `requested_toppings` passes the conditional test, we run the same `for` loop we used in the previous example.  If the conditional test fails, we print a message asking the customer if they really want a plain pizza with no toppings.  

### Using Multiple Lists
People will ask for just about anything, especially when it comes to pizza toppings.  What if a customer wants french fries on their pizza?  You can use lists and `if` statements to make sure your input makes sense before you act on it.  

Let's watch out for unusual topping requests before we build a pizza.  The following example defines two lists.  The first is a list of available toppings at the pizzeria, and the second is the list of toppings that the user has requested.  This time, each item in `requested_toppings` is checked against the list of available toppings before it is added to the pizza:  
```py linenums="1"
available_toppings = ['mushrooms', 'olives', 'green peppers', 'pepperoni', 'pineapple', 'extra cheese']

requested_toppings = ['mushrooms', 'french fries', 'extra cheese']

for requested_topping in requested_toppings:
	if requested_topping in available_toppings:
		print(f"Adding {requested_topping}.")
	else:
		print(f"Sorry, we don't have {requested_topping}.")

print("\nFinished making your pizza!")
```
On line 1, we defined a list of available toppings.  Next, on line 3, we created a list of requested toppings from the customer (Note the unusual request for 'french fries').  On line 5, we loop through the list of requested toppings.  Inside the loop, we first check to see if each requested topping is actually in the list of available toppings.  If it is, we add the topping to the pizza.  If the requested topping is not available, we run the `else` block and print a message saying that the topping is not available.  