# User Input and `while` Loops
Most programs will require a user's input to function.  For a simple example, let's say someone wants to find out whether they're old enough to vote.  If you write a program to answer this question, you need to know the user's age before you can provide an answer.  The program will need to ask the user to enter, or *input*, their age; once the program has this input, it can compare it to the voting age to determine if the user is old enough and then report the result.  

In this chapter you'll learn how to accept user input so your program can then work with it.  When your program needs a name, you'll be able to prompt the user for a name.  When your program needs a list of names, you'll be able to prompt the user for a name.  When your program needs a list of names, you'll be able to prompt the user for a series of names.  To do this, you'll use the `input()` function.  

We'll also learn how to keep programs running as long as users want them to, so they can enter as much information as they need to; then, your program can work with this information.  You'll use Python's `while` loop to keep programs running as long as certain conditons remain `true`.

## How the `input()` Function Works
The `input()` function pauses your program and waits for the user to enter some text.  Once Python receives the user's input, it assigns that input to a variable to make it convenient for you to work with.  

For example, the following program asks the user to enter some text, then displays that message back to the user:  
```py linenums="1"
message = input("Tell me something, and I will repeat it back to you: ")
print(message)
```
The `input()` function takes one argument: the *prompt*, or instructions, that we want to display to the user so they know what to do.  In this example when Python runs the first line, the user sees the prompt `Tell me something, and I will repeat it back to you: `.  The program waits while the user enters their response and continues after the user presses `ENTER`/  The response is assigned to the variable `message`, then `print(message)` displays the input back to the user:  
```
Tell me something, and I will repeat it back to you: Hello Everyone!
Hello Everyone!
```
### Writing Clear Prompts
Each time you use the `input()` function, you should include a clear, easy-to-follow prompt that tells the suer exactly what kind of information you're looking for.  Any statment that tells the user what to enter should work.  For example: 
```py linenums="1"
name = input("Please enter your name: ")
print(f"\nHello, {name}!")
```
Add a space at the end of your prompts (after the colon in the preceding example) to separate the prompt from the user's response and to make it clear to your user where to enter their text.  

Sometimes you'll want to write a prompt that is longer than one line.  For example, you might want to tel the user why you're asking for certain input.  You can assign your prompt to a variable and pass that variable to the `input()` function.  This allows you to build your prompt over several lines, then write a clean `input()` statement.  
```py linenums="1"
prompt = "If you tell us who you are, we can personalize the messages you see."
prompt += "\nWhat is your first name? "

name = input(prompt)
print(f"\nHello, {name}!")
```
This example shows one way to build a multi-line string.  The first line assigns the first part of the message to the variable `prompt`.  In the second line, the operator `=+` takes the string that was assigned to `prompt` and adds the new string onto the end.  

The above prompt now spans two lines, again with space after the question mark for clarity:  
```
If you tell us who you are, we can personalize the messages you see.
What is your first name? Nick

Hello, Nick!
```
### Using `int()` to Accept Numerical Input
When you use the `input()` function, Python interprets everything the user enters as a string.  Consider the following interpreter session, which asks for the user's age:
```
>>> age = input("How old are you? ")
How old are you? 21
>>> age
'21'
```
The user enters the number 21, but when we ask Python for the value of age, it returns `'21'`, the string representation of the numerical value entered.  We know Python interpreted the input as a string because the number is now enclosed in quites.  If all you want to do is print the input, this works well.  But if you try to use the input as a number, you'll get an error:
```
>>> age = input("How old are you? ")
How old are you? 21
>>> age >= 18
Traceback (most recent call last):
	file "<stdin>", line 1, in <module>
TypeError: unorderable types: str() >= int()
```
When you try to use the input to do a numerical comparison, Python produces an error because it can't compare a string to an integer: the string `'21'` that's assigned to age can't be compared to the numerical value `18`.  

We can resolve this by using the `int()` function, which tells Python to treat the input as a numerica value.  We can do this by wrapping the `input()` statement in an `int()`: 
```py
age = int(input("How old are you? "))
```
How do you use the `int()` function in an actual program?  Consider a program that determins whether people are tall enough to ride a roller coaster:  
```py linenums="1"
height = int(input("How tall are you, in inches? "))

if height >= 48:
	print("\nYou're tall enough to ride!")
else:
	print("\nYou're not tall enough to ride!")
```
The program can compare `height` to `48` because the `input()` for the `height` is wrapped in an `int()`.  

### The Modulo Operator
A useful tool for working with numerical information is the *modulo operator (%)*, which divides one number by another and returns the remainder.  For example:
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
The modulo operator doesn't tell you how many times one number fits into another; it just tells you what the remainder is.  

When one number is divisible by another number, the remainder is 0, so the modulo operator always returns 0.  You can use this fact to determine if a number is even or odd:
```py linenums="1"
number = int(input("Enter a number, and I'll tell you if it's even or odd: "))

if number % 2 == 0:
	print(f"\nThe number {number} is even.")
else:
	print(f"\nThe number {number} is odd.")
```
Even numbers are always divisible by two, so if the modulo of a number and two is zero (here, `if number % 2 == 0`) the number is even.  Otherwise, it's odd.  
```
Enter a number, and I'll tell you if it's even or odd: 5

The number 5 is odd.
```

## Introducing `while` Loops
The `for` loop takes a collection of items and executes a block of code once for each item in a collection.  In contrast, the `while` loop runs as lons as, or *while*, a certain condition is true.  

### The `while` Loop in Action
You can use a `while` loop to count up through a series of numbers.  For example, the following `while` loop counts from 1 to 5:
```py linenums="1"
current_number = 1
while current_number <=5:
	print(current_number)
	current_number +=1
```
In the first line, we start counting from 1 by assigning `current_number` to the value `1`.  The `while` loop is then set to keep running as long as the value of `current_number` is less than or equal to 5.  The code inside the loop prints the value of `current_number` and then adds 1 to that value with the `current_number += 1`. (The += operator is shorthand for `current_number = current_number + 1`).  

Python repeats the loop as long as the condition `current_number <= 5` is true.  Each time it loops it will check the value of `current_number` and add 1 (if less than 5), until it reaches 5.
```
1
2
3
4
5
```
The programs you use every day most likely contain `while` loops.  For example, a game needs a `while` loop to keep running as long as you want to keep playing, and so it can stop running as soon as you ask it to quit.  Programs wouldn't be fun to use if they stopped running before we told them to or kept running even after we wanted to quit, so `while` loops are quite useful.  

### Letting the User Choose When to Quit
We can make a program as long as the user wants by putting most of the program inside a `while` loop.  We'll define a *quit value* and then keep the program running as long as the user has not entered the quit value: 
```py linenums="1"
prompt = "\nTell me something, and I will repeat it back to you:"
prompt += "\nEnter 'quit' to end the program."

message = ""
while message != 'quit':
	message = input(prompt)
	print(message)
```
On line 1, we define a prompt that tells the user their two options: entering a message or entering a quit value (in this case, 'quit').  Then we set up a variable `message` (line 4) to keep track of whatever value the user enters.  We define `message` as an empty string, "", so Python has something to check the first time it reaches the `while` line.  The first time the program runs and Python reaches the `while` statementm it needs to compare the value of `message` to `quit`, but no user input has been entered yet.  If Python has nothing to compare, it won't be able to continue running the program.  To solve this provlem, we make sure to give `message` an initial value.  Although it's just an empty string, it will make sense to Python and allow it to perform the comparison that makes the `while` loop work.  This `while` loop (line 5) runs as long as the value of `message` is not `'quit'`.  

The first time through the loop, `message` is just an empty string, so Python enters the loop.  At `message = input(prompt)`, Python displays the prompt and waits for the user to enter their input.  Whatever they enter is assigned to `message` and printed; then, Python reevaluates the condition in the `while` statement.  As long as the user has not entered the word `'quit'`, the prompt is displayed again and Python waits for more input.  When the user finally enters `'quit'`, Python stops executing the `while` loop and the program ends:  
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
The progam works well, except that it prints the word `'quit'` as if it were an actual message.  A simple `if` test fixes this:
```py
if message != 'quit':
	print(message)
```
Now the program will quit immediately after the input, instead of printing 'quit'.

### Using a Flag
In the previous example, we had the program perform certain tasks while a given condition was true.  But what about more complicated programs in which many different events could cause the program to stop running?  

For example, in a game, several different event can end the game.  When the player runs out of ships, their time runs out, or the cities they were supposed to protect are all destroyed, the game should end.  It needs to end if any one of these event happen.  If many possible events might occur to stop the program, trying to test all these conditions in one `while` statement becomes complicated and difficult.  

For a program that should run only as long as many conditions are true, you can define one variable that determines whether or not the entire program is active.  This varibale, called a *flag*, acts as a signal to the program.  We can write our programs so they run while the flag is set to `True` and stop running when any of several events sets the value of the flag to `False`.  As a result, our overall `while` statement needs to check only one condition: whether or not the flag is currently `True`.  Then, all our other tests (to see if an event has occurred that should set the flag to `False`) can be neatly organized in the rest of the program.  

Let's add a flag to the program from the previous section.  This flag, which we'll call active (though you can call it anything), will monitor whether or not the program should continue running:
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
We set the variable `active` to `True` on line 4 so the program starts in an active state.  Doing so makes the `while` statement simpler because no comparison is made in the `while` statement itself; the logic is taken care of in other parts of the program.  As long as the `active` variable remains `True`, the loop will continue running (line 5).  

In the `if` statement inside the `while` loop, we check the value of `message` once the user enters their input.  If the user enters `'quit'` (line 8), we set `active` to `False`, and the `while` loop stops.  If the user enters anything other than `'quit'`, we print the input as a message.  

This program has the same output as the previous example where we placed the conditional test directly in the `while` statement.  But now that we have a flag to indicate whether the overal program is in an active state, it would be easy to add more tests (such as `elif` statements) for events that should cause `active` to become `False`.  This is useful in complicated programs like games in which there may be many evenet that should each make the program stop running.  When any of these events causes the active flag to become `False`, the main loop will exit, a *Game Over* message can be displayed, and the player can be given the option to play again.  

### Using `break` to Exit a Loop
To exit a `while` loop immediately without running any remaining code in the loop, regardless of the results of any conditional test, use the `break` statement.  The `break` statement directs the flow of your program; you can use it to control which lines of code are executed and which aren't, so the program only executes code that you want it to, when you want it to.  

For example, consider a program that asks a user about places they've visited.  We can stop the `while` loop in this program by calling a `break` as soon as the user enters the `'quit'` value:  
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
A loop that starts with a `while True` (line 4) will run forever unless it reaches a `break` statement.  The loop in this program continues asking the user to enter the names of cities they've been to until they enter `'quit'`.  When they enter `'quit'`, the `break` statement runs, causing Python to exit the loop:
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
??? warning "Note on `break`"
	You can use the `break` statement in any of Python's loops.  For example, you could use `break` to quite a `for` loop that's working through a list or a dictionary.  

### Using `continue` in a Loop
Rather than breaking out of a loop entirely without executing the rest of its code, you can use the `continue` statement to return to the beginning of the loop based on the result of a conditional test.  For example, consider a loop that counts from 1 to 10 but prints only the odd numbers in the range: 
```py linenums="1"
current_number = 0
while current_number < 10:
	current_number += 1
	if current_number % 2 == 0:
		continue

	print(current_number)
```
First we set `current_number` to 0.  Because it's less than 10, Python enters the `while` loop.  Once inside the loop, we increment the count by 1 (line 3), so the `current_number` is 1.  The `if` statement then checks the modulo of `current_number` and 2.  If the modulo is 0 (which means `current_number` is divisible by 2), the `continue` statement tells Python to ignore the rest of the loop and return to the beginning.  If the current number is not divisible by 2, the rest of the loop is executed and Python prints the current number:  
```
1
3
5
7
9
```
### Avoiding Infinite Loops
Every `while` loop needs a way to stop running so it won't continue to run forever.  For example, this counting loop should count from 1 to 5:  
```py linenums="1"
x = 1
while x < 5:
	print(x)
	x += 1
```
But if you accidentally omit the line `x += 1` (as shown next), the loop will run forever:
```py linenums="1"
x = 1
while x < 5:
	print(x)
```
Now the value of `x` will start at 1 but never change.  As a result, the conditional test `x <= 5` will always evaluate to `True` and the `while` loop will run forever, printing a series of 1s.  

Every programmer accidentally writes and infinite `while` loop from time to time, especially when a program's loops have subtle exit conditions.  If your program gets stuck in an infinite loop, press `CTRL-C` or just close the terminal window displaying the program's output.  

To avoid writing infinite loops, test every `while` loop and make sure the loop stops when you expect it to.  If you want your program to end when the user enters a certain input value, run the program and enter that value.  If the program doesn't end, scrutinize the way your program handles the value that should cause the loop to exit.  Make sure at least one part of the program can make the loop's condition `False` or cause it to reach a `break` statement.  
