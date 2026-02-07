# Conditionals and Control Flow

## Intoduction to Control Flow

Imagine we're writing a program that enrolls students in courses.

-   **_If_** a student has completed the prerequisites, **_then_** they can
    enroll in a course.

-   **_Else_**, they need to take the prerequisite courses.

For example, a student cannot take Physics II without first completing Physics
I.

We represent this kind of decision-making in our program using _conditional_ or
_control flow_ statements. Before this point, our code runs line-by-line from
the top down, but conditional statements allow us to be selective in which
portions will run.

Conditional statements check a `#!java boolean` condition and run a _block_ of
code depending on the condition. Curly braces mark the scope of a conditional
block similar to a method or class.

Here's a complete conditional statement:

```java linenums="1"
if (true) {
    System.out.println("Hellow World!");
}
```

If the condition is `#!java true`, then the block is run, which results in
`Hello World!` being printed.

But suppose the condition is different:

```java linenums="1"
if (false) {
    System.out.println("Hello World!");
}
```

If the condition is `#!java false`, then the block does not run.

This code is also called _if-then_ statements: "If `(condition)` is
`#!java true`, then do something".

### If-Then Statement

The _if-then_ statement is the most simple control flow we can write. It tests
an expression for truth and executes some code based on it.

```java linenums="1"
if (flip == 1) {
    System.out.println("Heads!");
}
```

-   the `#!java if` keyword marks the beginning of the conditional statement,
    followed by parentheses `()`.

-   The parentheses hold a `#!java boolean` datatype.

For the condition in parentheses we can also use variables that reference a
boolean, or comparisons that evaluate to a boolean.

The boolean condition is followed by opening and closing curly braces that mark
a block of code. This block runs if, and only if, the boolean is `#!java true`.

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

We've seem how to conditionally execute one block of code, but what if there are
two possible blocks of code we'd like to execute?

Let's say _if_ a student has the required prerequisite, _then_ they enroll in
the selected course, _else_ they're enrolled in the prerequisite course instead.

We create an alternate conditional branch with the `#!java else` keyword:

```java linenums="1"
if (hasPrerequisite) {
    // enroll in course
} else {
    // enroll in prerequisite
}
```

This conditional statement ensures that exactly one code block will be run. If
the condition `#!java hasPrerequisite`, is `#!java false`, the block after
`#!java else` runs.

There are now two separate code blocks in our conditional statement. The first
block runs if the condition evaluates to `#!java true`, the second block runs if
the condition evaluates to `#!java false`.

This code is also called an _if-then-else_ statement:

-   If _condition_ is true, then do something.

-   Else, do a different thing.

### If-Then-Else-If

The conditional structure we've learned can be chained together to check as many
conditions as are required by our program.

Imagine our program is now selecting the appropriate course for a student. We'll
check their submission to find the correct course enrollment.

The conditional statement now has multiple conditions that are evaluated from
the top down:

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

**The first** condition to evaluate to `#!java true` will have that code block
run. Here's an example demonstrating the order:

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

This chained conditional statement has two conditions that evaluate to
`#!java true`. Because `#!java testScore >= 70` comes before
`#!java testScore >= 60`, only the earlier code block is run.

**Note:** Only one of the code blocks will run.

### Nested Conditional Statements

We can create more complex conditional structures by creating _nested
contitional statements_, which is created by placing conditional statements
inside other conditional statements:

```java linenums="1"
if (outer condition) {
    if (nested condition) {
        // instruction to execute if both conditions are true
    }
}
```

When we implement nested conditional statements, the outer statement is
evaluated first. If the outer condition is `#!java true`, then the inner, nested
statement is evaluated.

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

In the code snippet above, our compiler will check the condition in the first
`if-then` statement: `#!java temp < 60`. Since `temp` has a value of
`#!java 45`, this condition is `#!java true`; therefore, our program will print
`Wear a jacket!`.

Then, we'll evaluate the condition in the nested `if-then` statement:
`#!java raining == true`. This condition is also `#!java true`, so
`Bring your umbrella` is also printed to the screen.

Note that, if the first condition was `#!java false`, the nested condition would
not be evaluated.

### Switch Statement

An alternative to chaining if-then-else conditions together is to use the
`#!java switch` statement. This conditional will check a given value against any
number of conditions and run the code block where there is a match.

Here's an example of our course selection conditional as a `#!java switch`
statement instead:

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

This example enrolls the student in History class by checking the value
contained in the parentheses, `course`, against each of the `#!java case`
labels. If the value after the case lable matches the value within the
parentheses, the _switch block_ is run.

In the above example, `course` references the string `#!java "History"`, which
matches `#!java case "History":`.

When no value matches, the `#!java default` block runs. Think of this as the
`#!java else` equivalent.

Switch blocks are different than other code blocks because they are not marked
by curly braces and we use the `#!java break` keyword to exit the switch
statement.

Without `#!java break`, code below the matching `#!java case` label is run,
_including code under other case labels_, which is rareley the desired behavior.

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

Conditional statements add branching paths to our programs. We use conditionals
to make decisions in the program so that different inputs will produce different
results.

Conditionals have the general structure:

```java linenums="1"
if (condition) {
    // consequent path
} else {
    // alternate path
}
```

Specific conditional statements have the following behavior:

-   `if-then`:

    -   Code block runs if the condition is true.

-   `if-then-else`:

    -   One block runs if condition is true.

    -   Another block runs if condition is false.

-   `if-then-else` chained:

    -   Same as `if-then` but an arbitrary number of conditions.

-   `#!java switch`:

    -   Switch block runs if condition matches the `#!java case` value.

## Introduction to Conditional Operators

Java includes operators that only use boolean values. These _conditional
operators_ help simplify expressions containing complex boolean relationships by
reducing multiple boolean values to a single use: `#!java true` or
`#!java false`.

For example, what if we want to run a code block only if _multiple_ conditions
are true. We could use the _AND_ operator: `#!java &&`.

Or, we want to run a code block if _at least one_ of two conditions are
`#!java true`. We could use the _OR_ operator: `#!java ||`.

Finally, we can produce the opposite value, where `#!java true` becomes
`#!java false` and `#!java false` becomes `#!java true`, with the _NOT_
operator: `#!java !`.

In the following notes, we'll go over each of these conditional operators to see
how they can be implemented into our conditional statements.

**AND**

| A     | B     | A&&B  |
| ----- | ----- | ----- |
| true  | true  | true  |
| true  | false | false |
| false | true  | false |
| false | false | false |

**OR**

| A     | B     | A\|\|B |
| ----- | ----- | ------ |
| true  | true  | true   |
| true  | false | true   |
| false | true  | true   |
| false | false | false  |

**NOT**

| A     | !A    |
| ----- | ----- |
| true  | false |
| false | true  |

### Conditional-AND: `#!java &&`

Let's return to our student enrollment program. We've added an additional
requirement: not only must students have the prerequisite, but their tuition
must be paid up as well. We have _two_ conditionals that must be `#!java true`
before we enroll the student.

Here is one way we can write the code:

```java linenums="1"
if (tuitionPaid) {
    if (hasPrerequisite){
        // enroll student
    }
}
```

We've nested two `#!java if-then` statements. This does the job but we can be
more concise with the _AND_ operator:

```java linenums="1"
if (tuitionPaid && hasPrerequisite){
    // enroll student
}
```

The AND operator, `#!java &&`, is used between two boolean values and evaluates
to a single boolean value. If the values **on both sides** are `#!java true`,
then the resulting value is `#!java true`, otherwise the resulting value is
`#!java false`.

This code illustrates every combination:

```java
true && true
// true
false && true
// false
true && false
// false
false && false
// false
```

### Conditional-OR: `#!java ||`

The requirements of our enrollment program have changed again. Certain courses
have prerequisites that are satisfied by multiple courses. As long as students
have taken **at least one** prerequisite, they should be allowed to enroll.

Here's one way we could write the code:

```java linenums="1"
if (hasAlgebraPrerequisite){
    // enroll student
}

if (hasGeometryPrerequisite){
    // enroll student
}
```

We're using two `#!java if-then` statements with **the same code block**. We can
be more concise with the _OR_ operator:

```java linenums="1"
if (hasAlgebraPrerequisite || hasGeometryPrerequisite){
    // enroll student
}
```

The OR operator, `#!java ||`, is used between two boolean values and evaluates
to a single boolean value. If **either of the two values** are `#!java true`,
then the resulting value is `#!java true`, otherwise the resulting value is
`#!java false`.

This code illustrates every combination:

```java
true || false
// true
true || false
// true
false || true
// true
false || false
// false
```

### Logical NOT: `#!java !`

The _unary_ operator NOT, `#!java !`, works on a **single** value. This operator
evaluates to the opposite boolean to which it is applied:

```java
!false
// true
!true
// false
```

NOT is useful for expressing our intent clearly in programs. For example
sometimes we need the opposite behavior of an `#!java if-then`: run a code block
**only if** the condition is `#!java false`.

```java linenums="1"
boolean hasPrerequisite = false;

if (hasPrerequisite) {
    // do nothing
} else {
    System.out.println("Must complete prerequisite course!");
}
```

This code does what we want but it's strange to have a code block that does
nothing!

The logical NOT operator cleans up our example:

```java linenums="1"
boolean hasPrerequisite = false;

if (!hasPrerequisite){
    System.out.println("Must complete prerequisite course!");
}
```

We can write a succint conditional statement without an empty code block.

### Combining Conditional Operators

We have the ability to expand our boolean expressions by using multiple
conditional operators in a single expression.

For example:

```java
boolean foo = true && !(false || !true)
```

How does an expression like this get evaluated by the compiler? The order of
evaluation when it comes to conditional operators is as follows:

1. Conditions placed in parentheses - `#!java {}`

2. NOT - `#!java !`

3. AND - `#!java &&`

4. OR - `#!java ||`

Using this information, let's dissect the expression above to find the value of
`foo`:

```java
true && !(false || !true)
```

First, we'll evaluate the `#!java (false || !true)` because it is enclosed
within parentheses. Following the order of evaluation, we will evaluate
`#!java !true`, which equals `#!java false`:

```java
true && !(false || false)
```

Then, we'll evaluate `#!java (false || false)` which equals `#!java false`. Now
our expression looks like this:

```
true && !false
```

Next, we'll evaluate `#!java !false` because it uses the NOT operator. This
expression equals `#!java true` making our expression the following:

```java
true && true
```

`#!java true && true` evaluates to `#!java true`; therefore, the value of `foo`
is `#!java true`.

## Conditional Operators Review

Conditional Operators work on boolean values to simplify our code. They're often
combined with conditional statements to consolidate the branching logic.

Conditional-AND, `#!java &&`, evaluates to `#!java true` if the booleans on
_both sides_ are `#!java true`.

Conditional-OR, `#!java ||`, evaluates to `#!java true` if one or both oif the
booleans on either side is `#!java true`.

Conditional-NOT, `#!java !`, evaluates to the opposite boolean value to which it
is applied.
