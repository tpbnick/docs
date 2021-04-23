# Conditionals and Control Flow

## Intoduction to Control Flow
Imagine we're writing a program that enrolls students in courses.  

- ***If*** a student has completed the prerequisites, ***then*** they can enroll in a course.  

- ***Else***, they need to take the prerequisite courses.  

For example, a student cannot take Physics II without first completing Physics I.  

We represent this kind of decision-making in our program using *conditional* or *control flow* statements.  Before this point, our code runs line-by-line from the top down, but conditional statements allow us to be selective in which portions will run.  

Conditional statements check a `#!java boolean` condition and run a *block* of code depending on the condition.  Curly braces mark the scope of a conditional block similar to a method or class.  

Here's a complete conditional statement:
```java linenums="1"
if (true) {
    System.out.println("Hellow World!");
}
```
If the condition is `#!java true`, then the block is run, which results in `Hello World!` being printed.  

But suppose the condition is different:
```java linenums="1"
if (false) {
    System.out.println("Hello World!");
}
```
If the condition is `#!java false`, then the block does not run.  

This code is also called *if-then* statements: "If `(condition)` is `#!java true`, then do something".  

### If-Then Statement
The *if-then* statement is the most simple control flow we can write.  It tests an expression for truth and executes some code based on it.  

```java linenums="1"
if (flip == 1) {
    System.out.println("Heads!");
}
```  

- the `#!java if` keyword marks the beginning of the conditional statement, followed by parentheses `()`.  

- The parentheses hold a `#!java boolean` datatype.  

For the condition in parentheses we can also use variables that reference a boolean, or comparisons that evaluate to a boolean.  

The boolean condition is followed by opening and closing curly braces that mark a block of code.  This block runs if, and only if, the boolean is `#!java true`.  

```java linenums="1"
boolean isValidPassword = true;

if (isValidPassword) {

    System.out.println("Password Accepted!");
}

// prints "Password accepted!"

int numberOfItemsInCart = 9;

if (numberOfItemsInCart > 12) {
    System.out.println("Express checkout not available");
} 

// nothing is printed
```
If a conditional is brief we can omit the curly braces entirely:
```java linenums="1"
if (true) System.out.println("Brevity is the soul of wit");
```

### If-Then-Else
We've seem how to conditionally execute one block of code, but what if there are two possible blocks of code we'd like to execute?  

Let's say *if* a student has the required prerequisite, *then* they enroll in the selected course, *else* they're enrolled in the prerequisite course instead.  

We create an alternate conditional branch with the `#!java else` keyword:  
```java linenums="1"
if (hasPrerequisite) {
    // enroll in course
} else {
    // enroll in prerequisite
}
```
This conditional statement ensures that exactly one code block will be run.  If the condition `#!java hasPrerequisite`, is `#!java false`, the block after `#!java else` runs.  

There are now two separate code blocks in our conditional statement.  The first block runs if the condition evaluates to `#!java true`, the second block runs if the condition evaluates to `#!java false`.  

This code is also called an *if-then-else* statement:  

- If *condition* is true, then do something.  

- Else, do a different thing.  

### If-Then-Else-If
The conditional structure we've learned can be chained together to check as many conditions as are required by our program.  

Imagine our program is now selecting the appropriate course for a student.  We'll check their submission to find the correct course enrollment.  

The conditional statement now has multiple conditions that are evaluated from the top down:

```java linenums="1"
String course = "Theatre";

if (course.equals("Biology")) {
    // enroll in Biology course
} else if (course.equals("Algebra")) {
    // enroll in Algebra course
} else if (course.equals("Theatre")) {
    // enroll in Theatre course
} else {
    System.out.println("Course not found!");
}
``` 
**The first** condition to evaluate to `#!java true` will have that code block run.  Here's an example demonstrating the order:
```java linenums="1"
int testScore = 72;

if (testScore >= 90){
    System.out.println("A");
} else if (testScore >= 80) {
    System.out.println("B");
} else if (testScore >= 70) {
    System.out.println("C");
} else if (testScore >= 60) {
    System.out.println("D");
} else {
    System.out.println("F");
}
```
This chained conditional statement has two conditions that evaluate to `#!java true`.  Because `#!java testScore >= 70` comes before `#!java testScore >= 60`, only the earlier code block is run.  

**Note:** Only one of the code blocks will run.  

### Nested Conditional Statements
We can create more complex conditional structures by creating *nested contitional statements*, which is created by placing conditional statements inside other conditional statements:
```java linenums="1"
if (outer condition) {
    if (nested condition) {
        // instruction to execute if both conditions are true
    }
}
```
When we implement nested conditional statements, the outer statement is evaluated first.  If the outer condition is `#!java true`, then the inner, nested statement is evaluated.  

Let's create a program that helps us decide what to wear based on the weather:
```java linenums="1"
int temp = 45;
boolean raining = true;

if (temp < 60) {
    System.out.println("Wear a jacket!");
    if (raining == true) {
        System.out.println("Bring your umbrella!");
    } else {
        System.out.println("Leave your umbrella at home.");
    }
}
```
In the code snippet above, our compiler will check the condition in the first `if-then` statement: `#!java temp < 60`.  Since `temp` has a value of `#!java 45`, this condition is `#!java true`; therefore, our program will print `Wear a jacket!`.  

Then, we'll evaluate the condition in the nested `if-then` statement: `#!java raining == true`.  This condition is also `#!java true`, so `Bring your umbrella` is also printed to the screen.  

Note that, if the first condition was `#!java false`, the nested condition would not be evaluated.  

### Switch Statement
An alternative to chaining if-then-else conditions together is to use the `#!java switch` statement.  This conditional will check a given value against any number of conditions and run the code block where there is a match.  

Here's an example of our course selection conditional as a `#!java switch` statement instead:

```java linenums="1"
String course = "History";

switch (course) {
    case "Algebra":
        // Enroll in Algebra
        break;
    case "Biology":
        // Enroll in Biology
        break;
    case "History":
        // Enroll in History
        break;
    case "Theatre":
        // Enroll in Theatre
        break;
    default:
        System.out.println("Course not found");
}
```
This example enrolls the student in History class by checking the value contained in the parentheses, `course`, against each of the `#!java case` labels.  If the value after the case lable matches the value within the parentheses, the *switch block* is run.  

In the above example, `course` references the string `#!java "History"`, which matches `#!java case "History":`.  

When no value matches, the `#!java default` block runs.  Think of this as the `#!java else` equivalent.  

Switch blocks are different than other code blocks because they are not marked by curly braces and we use the `#!java break` keyword to exit the switch statement.  

Without `#!java break`, code below the matching `#!java case` label is run, *including code under other case labels*, which is rareley the desired behavior.  

```java linenums="1"
String course = "Biology"; 

switch (course) {
  case "Algebra": 
    // Enroll in Algebra
  case "Biology": 
    // Enroll in Biology
  case "History": 
    // Enroll in History
  case "Theatre":
    // Enroll in Theatre
  default:
    System.out.println("Course not found");
}
 
// enrolls student in Biology... AND History and Theatre!
```
### Conditional/Control Flow Review
Conditional statements add branching paths to our programs.  We use conditionals to make decisions in the program so that different inputs will produce different results.  

Conditionals have the general structure:
```java linenums="1"
if (condition) {
    // consequent path
} else {
    // alternate path
}
```
Specific conditional statements have the following behavior:

- `if-then`:

    - Code block runs if the condition is true.  

- `if-then-else`:

    - One block runs if condition is true.  

    - Another block runs if condition is false.  

- `if-then-else` chained:

    - Same as `if-then` but an arbitrary number of conditions.  

- `#!java switch`:  

    - Switch block runs if condition matches the `#!java case` value.  

