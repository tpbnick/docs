# User Input and `#!py while` Loops

Most programs will require a user's input to function. For a simple example,
let's say someone wants to find out whether they're old enough to vote. If you
write a program to answer this question, you need to know the user's age before
you can provide an answer. The program will need to ask the user to enter, or
_input_, their age; once the program has this input, it can compare it to the
voting age to determine if the user is old enough and then report the result.

In this chapter you'll learn how to accept user input so your program can then
work with it. When your program needs a name, you'll be able to prompt the user
for a name. When your program needs a list of names, you'll be able to prompt
the user for a name. When your program needs a list of names, you'll be able to
prompt the user for a series of names. To do this, you'll use the `#!py input()`
function.

We'll also learn how to keep programs running as long as users want them to, so
they can enter as much information as they need to; then, your program can work
with this information. You'll use Python's `#!py while` loop to keep programs
running as long as certain conditons remain `#!py true`.

## How the `#!py input()` Function Works

The `#!py input()` function pauses your program and waits for the user to enter
some text. Once Python receives the user's input, it assigns that input to a
variable to make it convenient for you to work with.

For example, the following program asks the user to enter some text, then
displays that message back to the user:

```py linenums="1"
message = input("Tell me something, and I will repeat it back to you: ")
print(message)
```

The `#!py input()` function takes one argument: the _prompt_, or instructions,
that we want to display to the user so they know what to do. In this example
when Python runs the first line, the user sees the prompt
`Tell me something, and I will repeat it back to you: `. The program waits while
the user enters their response and continues after the user presses `ENTER`/ The
response is assigned to the variable `message`, then `#!py print(message)`
displays the input back to the user:

```
Tell me something, and I will repeat it back to you: Hello Everyone!
Hello Everyone!
```

### Writing Clear Prompts

Each time you use the `#!py input()` function, you should include a clear,
easy-to-follow prompt that tells the suer exactly what kind of information
you're looking for. Any statment that tells the user what to enter should work.
For example:

```py linenums="1"
name = input("Please enter your name: ")
print(f"\nHello, {name}!")
```

Add a space at the end of your prompts (after the colon in the preceding
example) to separate the prompt from the user's response and to make it clear to
your user where to enter their text.

Sometimes you'll want to write a prompt that is longer than one line. For
example, you might want to tel the user why you're asking for certain input. You
can assign your prompt to a variable and pass that variable to the
`#!py input()` function. This allows you to build your prompt over several
lines, then write a clean `#!py input()` statement.

```py linenums="1"
prompt = "If you tell us who you are, we can personalize the messages you see."
prompt += "\nWhat is your first name? "

name = input(prompt)
print(f"\nHello, {name}!")
```

This example shows one way to build a multi-line string. The first line assigns
the first part of the message to the variable `prompt`. In the second line, the
operator `#!py =+` takes the string that was assigned to `prompt` and adds the
new string onto the end.

The above prompt now spans two lines, again with space after the question mark
for clarity:

```
If you tell us who you are, we can personalize the messages you see.
What is your first name? Nick

Hello, Nick!
```

### Using `#!py int()` to Accept Numerical Input

When you use the `#!py input()` function, Python interprets everything the user
enters as a string. Consider the following interpreter session, which asks for
the user's age:

```
>>> age = input("How old are you? ")
How old are you? 21
>>> age
'21'
```

The user enters the number 21, but when we ask Python for the value of age, it
returns `#!py '21'`, the string representation of the numerical value entered.
We know Python interpreted the input as a string because the number is now
enclosed in quites. If all you want to do is print the input, this works well.
But if you try to use the input as a number, you'll get an error:

```
>>> age = input("How old are you? ")
How old are you? 21
>>> age >= 18
Traceback (most recent call last):
	file "<stdin>", line 1, in <module>
TypeError: unorderable types: str() >= int()
```

When you try to use the input to do a numerical comparison, Python produces an
error because it can't compare a string to an integer: the string `#!py '21'`
that's assigned to age can't be compared to the numerical value `18`.

We can resolve this by using the `#!py int()` function, which tells Python to
treat the input as a numerica value. We can do this by wrapping the
`#!py input()` statement in an `#!py int()`:

```py
age = int(input("How old are you? "))
```

How do you use the `#!py int()` function in an actual program? Consider a
program that determins whether people are tall enough to ride a roller coaster:

```py linenums="1"
height = int(input("How tall are you, in inches? "))

if height >= 48:
	print("\nYou're tall enough to ride!")
else:
	print("\nYou're not tall enough to ride!")
```

The program can compare `height` to `48` because the `#!py input()` for the
`height` is wrapped in an `#!py int()`.

### The Modulo Operator

A useful tool for working with numerical information is the _modulo operator
(%)_, which divides one number by another and returns the remainder. For
example:

```py
4 % 3
```

```
1
```

or

```py
6 % 3
```

```
0
```

The modulo operator doesn't tell you how many times one number fits into
another; it just tells you what the remainder is.

When one number is divisible by another number, the remainder is 0, so the
modulo operator always returns 0. You can use this fact to determine if a number
is even or odd:

```py linenums="1"
number = int(input("Enter a number, and I'll tell you if it's even or odd: "))

if number % 2 == 0:
	print(f"\nThe number {number} is even.")
else:
	print(f"\nThe number {number} is odd.")
```

Even numbers are always divisible by two, so if the modulo of a number and two
is zero (here, `#!py if number % 2 == 0`) the number is even. Otherwise, it's
odd.

```
Enter a number, and I'll tell you if it's even or odd: 5

The number 5 is odd.
```

## Introducing `#!py while` Loops

The `#!py for` loop takes a collection of items and executes a block of code
once for each item in a collection. In contrast, the `#!py while` loop runs as
lons as, or _while_, a certain condition is true.

### The `#!py while` Loop in Action

You can use a `#!py while` loop to count up through a series of numbers. For
example, the following `#!py while` loop counts from 1 to 5:

```py linenums="1"
current_number = 1
while current_number <=5:
	print(current_number)
	current_number +=1
```

In the first line, we start counting from 1 by assigning `current_number` to the
value `1`. The `#!py while` loop is then set to keep running as long as the
value of `current_number` is less than or equal to 5. The code inside the loop
prints the value of `current_number` and then adds 1 to that value with the
`#!py current_number += 1`. (The += operator is shorthand for
`#!py current_number = current_number + 1`).

Python repeats the loop as long as the condition `#!py current_number <= 5` is
true. Each time it loops it will check the value of `current_number` and add 1
(if less than 5), until it reaches 5.

```
1
2
3
4
5
```

The programs you use every day most likely contain `#!py while` loops. For
example, a game needs a `#!py while` loop to keep running as long as you want to
keep playing, and so it can stop running as soon as you ask it to quit. Programs
wouldn't be fun to use if they stopped running before we told them to or kept
running even after we wanted to quit, so `#!py while` loops are quite useful.

### Letting the User Choose When to Quit

We can make a program as long as the user wants by putting most of the program
inside a `#!py while` loop. We'll define a _quit value_ and then keep the
program running as long as the user has not entered the quit value:

```py linenums="1"
prompt = "\nTell me something, and I will repeat it back to you:"
prompt += "\nEnter 'quit' to end the program."

message = ""
while message != 'quit':
	message = input(prompt)
	print(message)
```

On line 1, we define a prompt that tells the user their two options: entering a
message or entering a quit value (in this case, 'quit'). Then we set up a
variable `message` (line 4) to keep track of whatever value the user enters. We
define `message` as an empty string, "", so Python has something to check the
first time it reaches the `#!py while` line. The first time the program runs and
Python reaches the `#!py while` statementm it needs to compare the value of
`message` to `quit`, but no user input has been entered yet. If Python has
nothing to compare, it won't be able to continue running the program. To solve
this provlem, we make sure to give `message` an initial value. Although it's
just an empty string, it will make sense to Python and allow it to perform the
comparison that makes the `#!py while` loop work. This `#!py while` loop
(line 5) runs as long as the value of `message` is not `#!py 'quit'`.

The first time through the loop, `message` is just an empty string, so Python
enters the loop. At `#!py message = input(prompt)`, Python displays the prompt
and waits for the user to enter their input. Whatever they enter is assigned to
`message` and printed; then, Python reevaluates the condition in the
`#!py while` statement. As long as the user has not entered the word
`#!py 'quit'`, the prompt is displayed again and Python waits for more input.
When the user finally enters `#!py 'quit'`, Python stops executing the
`#!py while` loop and the program ends:

```
Tell me something, and I will repeat it back to you:
Enter 'quit' to end the program. Hello everyone!
Hello everyone!

Tell me something, and I will repeat it back to you:
Enter 'quit' to end the program. Hello again.
Hello again.

Tell me something, and I will repeat it back to you:
Enter 'quit' to end the program. quit
quit
```

The progam works well, except that it prints the word `#!py 'quit'` as if it
were an actual message. A simple `#!py if` test fixes this:

```py
if message != 'quit':
	print(message)
```

Now the program will quit immediately after the input, instead of printing
`#!py 'quit'`.

### Using a Flag

In the previous example, we had the program perform certain tasks while a given
condition was true. But what about more complicated programs in which many
different events could cause the program to stop running?

For example, in a game, several different event can end the game. When the
player runs out of ships, their time runs out, or the cities they were supposed
to protect are all destroyed, the game should end. It needs to end if any one of
these event happen. If many possible events might occur to stop the program,
trying to test all these conditions in one `#!py while` statement becomes
complicated and difficult.

For a program that should run only as long as many conditions are true, you can
define one variable that determines whether or not the entire program is active.
This varibale, called a _flag_, acts as a signal to the program. We can write
our programs so they run while the flag is set to `#!py True` and stop running
when any of several events sets the value of the flag to `#!py False`. As a
result, our overall `#!py while` statement needs to check only one condition:
whether or not the flag is currently `#!py True`. Then, all our other tests (to
see if an event has occurred that should set the flag to `#!py False`) can be
neatly organized in the rest of the program.

Let's add a flag to the program from the previous section. This flag, which
we'll call active (though you can call it anything), will monitor whether or not
the program should continue running:

```py linenums="1"
prompt = "\nTell me something, and I will repeat it back to you:"
prompt += "\nEnter 'quit' to end the program."

active = True
while active:
	message = input(prompt)

	if message == 'quit':
		active = False
	else:
		print(message)
```

We set the variable `#!py active` to `#!py True` on line 4 so the program starts
in an active state. Doing so makes the `#!py while` statement simpler because no
comparison is made in the `#!py while` statement itself; the logic is taken care
of in other parts of the program. As long as the `#!py active` variable remains
`#!py True`, the loop will continue running (line 5).

In the `#!py if` statement inside the `#!py while` loop, we check the value of
`#!py message` once the user enters their input. If the user enters
`#!py 'quit'` (line 8), we set `#!py active` to `#!py False`, and the
`#!py while` loop stops. If the user enters anything other than `#!py 'quit'`,
we print the input as a message.

This program has the same output as the previous example where we placed the
conditional test directly in the `#!py while` statement. But now that we have a
flag to indicate whether the overal program is in an active state, it would be
easy to add more tests (such as `#!py elif` statements) for events that should
cause `#!py active` to become `#!py False`. This is useful in complicated
programs like games in which there may be many evenet that should each make the
program stop running. When any of these events causes the active flag to become
`#!py False`, the main loop will exit, a _Game Over_ message can be displayed,
and the player can be given the option to play again.

### Using `#!py break` to Exit a Loop

To exit a `#!py while` loop immediately without running any remaining code in
the loop, regardless of the results of any conditional test, use the
`#!py break` statement. The `#!py break` statement directs the flow of your
program; you can use it to control which lines of code are executed and which
aren't, so the program only executes code that you want it to, when you want it
to.

For example, consider a program that asks a user about places they've visited.
We can stop the `#!py while` loop in this program by calling a `#!py break` as
soon as the user enters the `#!py 'quit'` value:

```py linenums="1"
prompt = "\nPlease enter the name of a city you have visited:"
prompt += "\n(Enter 'quit' when you are finished.) "

while True:
	city = input(prompt)

	if city == 'quit':
		break
	else:
		print(f"I'd love to go to {city.title()}!")
```

A loop that starts with a `#!py while True` (line 4) will run forever unless it
reaches a `#!py break` statement. The loop in this program continues asking the
user to enter the names of cities they've been to until they enter
`#!py 'quit'`. When they enter `#!py 'quit'`, the `#!py break` statement runs,
causing Python to exit the loop:

```
Please enter the name of a city you have visited:
(Enter 'quit' when you are finished.) San Francisco
I'd love to go to San Francisco!

Please enter the name of a city you have visited:
(Enter 'quit' when you are finished.) Los Angeles
I'd love to go to Los Angeles!

Please enter the name of a city you have visited:
(Enter 'quit' when you are finished.) quit
```

??? warning "Note on `#!py break`"

    You can use the `#!py break` statement in any of Python's loops. For example,
    you could use `#!py break` to quite a `#!py for` loop that's working through
    a list or a dictionary.

### Using `#!py continue` in a Loop

Rather than breaking out of a loop entirely without executing the rest of its
code, you can use the `#!py continue` statement to return to the beginning of
the loop based on the result of a conditional test. For example, consider a loop
that counts from 1 to 10 but prints only the odd numbers in the range:

```py linenums="1"
current_number = 0
while current_number < 10:
	current_number += 1
	if current_number % 2 == 0:
		continue

	print(current_number)
```

First we set `current_number` to 0. Because it's less than 10, Python enters the
`#!py while` loop. Once inside the loop, we increment the count by 1 (line 3),
so the `current_number` is 1. The `#!py if` statement then checks the modulo of
`current_number` and 2. If the modulo is 0 (which means `current_number` is
divisible by 2), the `#!py continue` statement tells Python to ignore the rest
of the loop and return to the beginning. If the current number is not divisible
by 2, the rest of the loop is executed and Python prints the current number:

```
1
3
5
7
9
```

### Avoiding Infinite Loops

Every `#!py while` loop needs a way to stop running so it won't continue to run
forever. For example, this counting loop should count from 1 to 5:

```py linenums="1"
x = 1
while x < 5:
	print(x)
	x += 1
```

But if you accidentally omit the line `x += 1` (as shown next), the loop will
run forever:

```py linenums="1"
x = 1
while x < 5:
	print(x)
```

Now the value of `x` will start at 1 but never change. As a result, the
conditional test `#!py x <= 5` will always evaluate to `#!py True` and the
`#!py while` loop will run forever, printing a series of 1s.

Every programmer accidentally writes and infinite `#!py while` loop from time to
time, especially when a program's loops have subtle exit conditions. If your
program gets stuck in an infinite loop, press `CTRL-C` or just close the
terminal window displaying the program's output.

To avoid writing infinite loops, test every `#!py while` loop and make sure the
loop stops when you expect it to. If you want your program to end when the user
enters a certain input value, run the program and enter that value. If the
program doesn't end, scrutinize the way your program handles the value that
should cause the loop to exit. Make sure at least one part of the program can
make the loop's condition `#!py False` or cause it to reach a `#!py break`
statement.

## Using a `#!py while` Loop with Lists and Dicitonaries

So far, we've worked with only one piece of user information at a time. We
received the user's input and then printed the input or a response to it. The
next time through the `#!py while` loop, we'd receive another input value and
respond to that. But to keep track of many users and pieces of information,
we'll need to use lists and dictionaries with our `#!py while` loops.

A `#!py for` loop is effective for looping through a lsit, but you shouldn't
modify a list inside a `#!py for` loop because Python will have trouble keeping
track of the items in the list. To modify a list as you work through it, use a
`#!py while` loop. Using `#!py while` loops with lists and dictionaries allow
you to collect, store, and organize lots of input to examine and report on
later.

### Moving Items from One List to Another

Consider a list of newly registered but unverified users of a website. After we
verify these users, how can we move them to a separate list of confirmed users?
One way would be to use a `#!py while` loop to pull users from the list of
unconfirmed users as we verify them and then add them to a separate list of
confirmed users. Here's what that code might look like:

```py linenums="1"
# Start with users that need to be verified,
# and an empty list to hold confirmed users.
unconfirmed_users = ['alice', 'brian', 'candace']
confirmed_users = []

# Verify each user until there are no more unconfirmed users.
# Move each verified user into the list of confirmed users.
while unconfirmed_users:
	current_user = unconfirmed_users.pop()

	print(f"Verifying user: {current_user.title()}")
	confirmed_users.append(current_user)

#Display all confirmed users.
print("\nThe following users have been confirmed:")
for confirmed_user in confirmed_users:
	print(confirmed_user.title())
```

We begin with a list of unconfirmed users on line 3 (Alice, Brian, and Candace)
and an empty list to hold confirmed users. The `#!py while` loop on line 8 runs
as long as the list `unconfirmed_users` is not empty. Within this loop, the
`#!py pop()` function (line 9) removes unverified users one at a time from the
end of `unconfirmed_users`. Here, because Candace is te last in the
`unconfirmed_users` list, her name will be the first to be removed, assigned to
`current_user`, and added to the `confirmed_users` list on line 12. Next is
Brian, then Alice.

We simulate confirming each user by printing a verification message then adding
them to the list of confirmed users. As the list of unconfirmed users shrinks,
the list of confirmed users grows. When the list of unconfirmed users is empty,
the loop stops and the list of confirmed users in printed:

```
Verifying user: Candace
Verifying user: Brian
Verifying user: Alice

The following users have been confirmed:
Candace
Brian
Alice
```

### Removing All Instances of Specific Values from a List

In previous notes
([located here](https://docs.nickplatt.dev/programming-notes/python/py-lists/#removing-elements-from-a-list))
we used `#!py remove()` to remove a specific value from a list. The
`#!py remove()` function worked because the value we were interested in appeared
only once in the list. But what if you want to remove all instances of a value
from a list?

Say you have a list of pets with the value `#!py 'cat'` repeated several times.
To remove all instances of that value, you can run a `#!py while` loop until
`#!py 'cat'` is no longer in the list, as shown here:

```py linenums="1"
pets = ['dog', 'cat', 'dog', 'goldfish', 'cat', 'rabbit', 'cat']
print(pets)

while 'cat' in pets:
	pets.remove('cat')

print(pets)
```

We start with a list containing multiple instances of `#!py 'cat'`. After
printing the list, Python enters the `#!py while` loop because it finds the
value `#!py 'cat'` in the list at least once. Once insidethe loop, Python
removes the first instance of `#!py 'cat'`, returns to the `#!py while` line,
and then reenters the loop when it finds that `#!py 'cat'` is still in the list.
It removes each instance of `#!py 'cat'` until the value is no longer in the
list, at which point Python exits the loop and prints the list again:

```
['dog', 'cat', 'dog', 'goldfish', 'cat', 'rabbit', 'cat']
['dog', 'dog', 'goldfish', 'rabbit']
```

### Filling a Dictionary with User Input

You can prompt for as much input as you need in each pass through a `#!py while`
loop. Let's make a polling program in which each pass through the loop prompts
for the participant's name and response. We'll store the data we gather in a
dictionary, because we want to connect each response with a particular user:

```py linenums="1"
responses = {}

# Set a flag to indicate that polling is active
polling_active = True

while polling_active:
	# Prompt for the person's name and response.
	name = input("\nWhat is your name? ")
	response = input("Which mountain would you like to climb someday? ")

	# Store the response in the dictionary
	responses[name] = response

	# Find out if anyone else if going to take the poll.
	repeat = input("Would you like to let another person respond? (yes/no) ")
	if repeat == 'no':
		polling_active = False

# Polling is complete.  Show the results.
print("\n--- Poll Results ---")
for name, response in responses.items():
	print(f"{name} would like to climb {response}.")
```

The program first defines an empty dictionary (`responses`) and sets a flag
(`polling_active`) to indicate that polling is active. As long as
`polling_active` is `#!py True`, Python will run the code in the `#!py while`
loop.

Within the loop, the user is prompted to enter their name and a mountain they'd
like to climb (line 8). That information is stored in the `responses` dictionary
(line 12), and the user is asked whether or not to keep the poll running (line
15). If they enter yes, the program enters the `#!py while` loop again. If they
enter no, the `polling_active` flag is set to `#!py False`, the `#!py while`
loop stops running, and the final code block at line 20 displays the results of
the poll.

If you run this program and enter sample resonses, you should see output like
this:

```
What is your name? Eric
Which mountain would you like to climb someday? Denali
Would you like to let another person respond? (yes/ no) yes

What is your name? Lynn
Which mountain would you like to climb someday? Devil's Thumb
Would you like to let another person respond? (yes/ no) no

--- Poll Results ---
Lynn would like to climb Devil's Thumb.
Eric would like to climb Denali.
```
