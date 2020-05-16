# C Basics

## Basic Data Types
* **`#!c int`** – used for variables that store integers (numbers).  
* **`#!c char`** – used for variables that will store single characters. These us single quotes (Ex. 'A').   
* **`#!c float`** – used for variables that will store floating point-values (real numbers) (numbers with decimal point) (32 bits).  
* **`#!c double`** – like `#!c float` but are double precision (64 bits).  
* **`#!c void`** – not a data type – is a type. Void return type does not return a value and does not take arguments.  printf is a void function because it returns nothing, just shows a result.  
* **`#!c bool`** – used for variables that will store a Boolean value (`true` or `false`).  
* **`#!c string`** – used for variables that will store a series of characters (words, sentences, paragraphs).  These use double quotes (Ex. "Hi!").  


## Creating a Variable

To create a variable, you need to simply specify the data type of the variable and give it a name.  

&emsp;&emsp;`#!c int number;` -> number is the name of the integer.  
&emsp;&emsp;`#!c char letter;` -> letter is the name of the character.  

To create multiple variables of the same type, you specify the variable type once and then list as many variables as needed (separated by a comma).  

&emsp;&emsp;`#!c int height, width;`  

## Using a Variable

After a variable has been declared, it is no longer necessary to specify that variable’s type.  

&emsp;&emsp;`#!c int number;` // declaration  
&emsp;&emsp;`#!c number = 17;` // assignment  
&emsp;&emsp;`#!c char letter;` // declaration  
&emsp;&emsp;`#!c letter = 'H'` // assignment  

## Operators

In order to manipulate and work with variables and values in C, operators must be used.  

**Arithmetic Operators**  

In C we can add (`#!c +`), subtract (`#!c -`), multiply (`#!c *`) and divide (`#!c /`) numbers.  
&emsp;&emsp;`#!c int x = y + 1;`  
&emsp;&emsp;`#!c x = x * 5;`  

We also have the modulus operator (`#!c %`), which gives us the remainder when the number on the left of the operator is divided by the number on the right.  

&emsp;&emsp;`#!c int m = 13 % 4` // m is now 1 because after division there was a remainder of 1 (13/4=3 with one left over).  

There is also a shorthand way to apply an arithmetic operator to a single variable.  

&emsp;&emsp;`#!c x = x * 5;` is the same as `#!c x *= 5;`  

Incrementing or decrementing a variable by 1 is very simple:  

&emsp;&emsp;`#!c x++;` or `#!c x--;`  

**Boolean Expressions**

Boolean expressions are used in C for comparing values.  

All Boolean expressions evaluate to one of two possible values - `#!c true` or `#!c false.`  

Boolean expression results can be used to decide which branch in a *conditional* (if true/if false fork) to take, or determine whether a *loop* should continue to run.  

Sometimes when working with Boolean expressions we will use the variables of type `#!c bool`, but we don’t have to.  

In C, every nonzero value is equivalent to `#!c true`, and zero is `#!c false`.  

There are two main types of Boolean expressions: *logical operators* and *relational operators.*  

**Logical Operators**  

Logical **AND (&&)** is true if and only if both operands are true, otherwise false.

| X     | Y     | (X && Y) |
|-------|-------|----------|
| true  | true  | true     |
| true  | false | false    |
| false | true  | false    |
| false | false | false    |  

Logical **OR (||)** is true if and only if at least one operand is true, otherwise false.  

| X     | Y     | (X \|\| Y) |
|-------|-------|------------|
| true  | true  | true       |
| true  | false | true       |
| false | true  | true       |
| false | false | false      |  

Logical **NOT (!)** inverts the value of its operand.  

| X     | !X    |
|-------|-------|
| true  | false |
| false | true  |  

**Relational Operators**  
These behave as you would expect them to, and appear syntactically similar to how you may recall them from elementary arithmetic.  

&emsp;&emsp;Less than (x < y)  
&emsp;&emsp;Less than or equal to (x <= y)  
&emsp;&emsp;Greater than (x > y)  
&emsp;&emsp;Greater than or equal to (x >= y)  

C can also test two variables for equality and inequality.  

&emsp;&emsp;Equality (x == y)  
&emsp;&emsp;Inequality (x != y)  

Be careful with equality!  It is a common mistake to use the assignment operator (=) when you intend to use the equality operator (==).  

## Conditional Statements

Conditional expressions allow your programs to make decisions and take different forks in the road, depending on the values of variables or user input.  

C Provides a few different ways to implement conditional expressions (also known as branches) in your programs.  

**`#!c if (boolean-expression){}`**  

If the boolean-expression evaluates to `#!c true`, all lines of code between the {} will execute in order from top-to-bottom.  
If the boolean-expression evaluates to `#!c false`, those lines of code will not execute.  

**`#!c if (boolean-expression){} else{}`**  

If the boolean-expression evaluates to `#!c true`, all lines of code between the {} will execute in order from top-to-bottom.  
If the boolean-expression evaluates to `#!c false`, all lines of code between the second set of {} will execute in order from top-to-bottom.  

It is possible in C to have an `#!c if-else if-else` chain.  

```c
if (boolean-expr1){
}
else if (boolean-expr2){
}
else if (boolean-expr3){
}
else{
}
```  

Note: The final `#!c else` will only link to the final `#!c if`.  

**`#!c switch`**  
C’s `#!c switch()` statement is a conditional statement that permits enumeration of discrete cases, instead of relying on Boolean expressions.  

It is important to break between each case, or you will “fall through” each case (unless that is intended)

```c
int x = GetInt();
switch(x)
	{
		case 1:
			printf(“One!\n”);
			break;  
		case 2:
			printf(“Two!\n”);
			break;
		case 3:
			printf(“Three!\n”);
			break;
		default:  
			printf(“Sorry!\n”);
	}
```

## Loops
Loops allow your program to execute lines of code repeatedly, saving you from needing to copy/paste or otherwise repeat lines of code.  

**Infinite Loop**  
```c
while (true)
{
}
```
The lines of code between the {} will execute repeatedly from top to bottom, until and unless we break out of it (as with a `break;` statement) or otherwise kill the program.  

**While Loop**
```c
while (boolean-expr)
{
}
```

If the boolean-expr evaluates to `#!c true`, all lines of code between the {} will execute repeatedly, in order from top-to-bottom, until boolean-expr evaluates to `#!c false`.  

Use when you want a loop to repeat an unknown number of times, and possibly not at all.  

**Do While Loop**  
```c
do
{
}
while (boolean-expr);
```

This loop will execute all lines of code between {} once, and then, if the boolean-expr evaluates to `#!c true`, will go back and repeat that process until the boolean-expr evaluates to `#!c false`.  

Use when you want a loop to repeat an unknown number of times, but at least once.  

**For Loop**  
```c
for (int i = 0; i < 10; i++)
{
} 
```

Syntactically unattractive, but `#!c for` loops are used to repeat the body of a loop a specified number of times (in the above example - 10 times).  

The process undertaken in a for loop is:  

* The counter variable(s) (here, i) is set.  
* The Boolean expression is checked.  
	- If it evaluates to `#!c true`, the body of the loop executes.  
	- If it evaluates to `#!c false`, the body of the loop does not execute.  
* The counter variable is incremented, and then the Boolean Expression is checked again, etc.  

Use for when you want a loop to repeat a discrete number of times, though you may not know the number at the moment the program is compiled.  

## First Code
```c
#include <stdio.h>
int main(void)
{  
	printf("Hello, World!\n"); 
} 
```
**Source code -> compiler -> machine code**

`clang hello.c` (clang is the c language compiler) 
This compiles the hello world source code.

`./a.out` (a.out is the compiled machine code from the hello world source code).

To rename a.out simply put a `-o *filename*` before the file that needs to be compiled (Ex. `clang -o hello hello.c`).

To see a list of files in a directory – type `ls`
Files with * means it is executable (has been compiled).

To remove a file in a directory – type `rm *filename*`

## `Hello, *name*!`

Now lets create a "Hello World"-like program that allows input from the user.  

We will now include a string prompt that asks the user for their name.  

`#!c string answer = get_string(“What’s your name?\n”);`
(answer is the variable in the string).

`#!c printf(“Hello, %s\n”, answer);`

`#!c %s` is a placeholder for a string which is defined by the comma and string name.
A string is a sequence (variable) of zero or more characters in double quotes (“”);
```c
#include <cs50.h>
#include <stdio.h>
int main(void)
{
	string answer = get_string("What’s your name?\n");
	printf("Hello, %s.\n", answer);
}
```

## Mario Problem Set

Toward the end of World 1-1 in Super Mario Bros, Mario must ascend a right-alighned pyramid of blocks.  We are going to recreate this in C (Using #'s instead of blocks), but allow the user to choose the block height while setting limits.  

If a user inputs a height of `4`, this is how the program should work:  

```c
   #
  ##
 ###
####
```
To begin, we need to import some libraries:  
```c
#include <cs50.h>
#include <stdio.h> 
```
Before writing the code, we should look at the loop type we want to use.  The best option in this case would be a `#!c do while` loop, like the code that follows:  
```c
int n;  
do
{  
	n = get_int("Positive Number: ");
}
while (n < 1);
```
The code above will continue to prompt the user for a number until it is positive.  

For our Mario blocks, we will make the options only positive integers ranging from 1 to 8.  

Using a `#!c do while` loop we will begin with a prompt for user input:  

```c
int main(void)
{ 
	int n;
	do
	{
		n = get int("Height (1-8): ");
	}
	while(n < 1 || n > 8)
}
```

Next, we will need to add a `#!c for` loop.  

We will add the following:  

```c
for(int i = 0; i < n; i++)
{
	printf("#\n"); 
}
```

Making this right aligned is a more difficult task.  Looking at the problem as a box with rows and columns helps.  Imagine that the 8X8 grid prints the following. (Note that we start counting at 0)  

|   | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 |
|---|---|---|---|---|---|---|---|---|
| 0 |   |   |   |   |   |   |   | # |
| 1 |   |   |   |   |   |   | # | # |
| 2 |   |   |   |   |   | # | # | # |
| 3 |   |   |   |   | # | # | # | # |
| 4 |   |   |   | # | # | # | # | # |
| 5 |   |   | # | # | # | # | # | # |
| 6 |   | # | # | # | # | # | # | # |
| 7 | # | # | # | # | # | # | # | # |  


We will rename `#!c int i` from earlier to `#!c int rows` and create `#!c int columns` to be the columns.  (These can be named whatever you want).  

From here we can create the following code to create the right-aligned blocks.  

```c
#include <stdio.h>
#include <cs50.h>  

int main(void)
{
	int n;
	do
	{
		n = get_int("Height (1-8): ");
	}
	// user input 1-8
	while (n < 1 || n > 8); 
    
	for (int rows = 0; rows < n; rows++)
	{
	for (int columns = 0; columns <= n - 1; columns++)
	{
		if (rows + columns < n -1) 
			printf(" ");
		else
			printf("#");  
	}
	printf("\n");
	}
} 
```

## Cash Problem Set  

When a cashier gives change to a customer they give the biggest denomination they can and go until they must use a less valuable denomination.  For example, if someone is owed $0.47, they will be given 1 quarter (.25), 2 dimes (2 * .10), and 2 pennies (2 * .01).  For this problem set we will create a program that asks how much change is owed and then prints out the fewest number of coins that can be used.  

The easiest way to do this, which requires some copy/pasting, is to create a `#!c while` loop for the different denominations.  It should also be noted that we must use a `#!c float` instead of a `#!c int`, as we have previously, because money will not always be a whole number.  

The code works as the following:

```c
#include <stdio.h>  
#include <cs50.h>
#include <math.h>  
  
int main(void)
{ 
	loat dollars;
      
	do
	{
		dollars = get_float("How much change is owed?\n");
	} 
	while (dollars < 0);

	int cents = round(dollars * 100);  
	int coins = 0;  

	while (cents >= 25)
	{
		cents -= 25;
		coins++;
	} 
	while (cents >= 10)
	{
		cents -= 10;
		coins++;
	}  
	while (cents >= 5)
	{
		cents -= 5;  
		coins++;
	}
	while (cents >= 1)
	{
		cents -= 1;
		coins++;
	}

	printf("%i\n", coins);
}  
```