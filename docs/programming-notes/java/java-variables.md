# Variables

## Introduction to Variables

Let's say we need a program that connects a user with new jobs. We need the
user's name, their salary, and they current employment status. All of these
pieces of information are stored in our program.

We store information in _variables_, which are named locations in memory.

Naming a piece of information allows us to use that name later, accessing the
information we stored. Variables also give context and meaning to the data we're
storing. The value `42` could be someone's age, a weight in pounds, or the
number of orders placed. With a name, we **know** the value of `42` is `age`,
`weightInPounds`, or `numOrdersPlaced`.

In Java, we specify the type of information we're storing. _Primitive datatypes_
are types of data built-in to the Java system. The three main primitive types we
will cover in these notes are:

-   [`#!java int`](#int) - Stores whole numbers

-   [`#!java double`](#double) - Stores bigger whole numbers and decimal numbers

-   [`#!java boolean`](#boolean) - Stores `true` and `false`

-   [`#!java char`](#char) - Stores single characters using single quotes (`''`)

-   [`#!java String`](#string) - Stores multiple characters using double quotes
    (`""`)

We must _declare_ a variable to reference it within our program. Declaring a
variable requires that we specify the type and name:

```java linenums="1"
// datatype variableName
int age;
double salaryRequirement;
boolean isEmployed;
```

The names of the variables above are `age`, `salaryRequirement`, and
`isEmployed`.

These variables don't have any associated value. To assign a value to a
variable, we use the assignment operator `=`:

```java linenums="1"
age = 85;
```

Now, `age` has a value of `85`. When code is used to represent a fixed value,
like `85`, it is referred to as a _literal_.

For example, to assign `2013` to a variable named `yearNickGraduatedHighSchool`
of type `int`, we write:

```java linenums="1"
int yearNickGraduatedHighSchool = 2013;
```

Using this logic towards the `#!java System.out.println()` statements we used
from [Java Basics](java-basics.md), instead of putting text within parenthesis,
we could print a variable:

```java linenums="1"
public class Nick {
	public static void main(String[] args) {
    String name = "Nick";
    int yearBorn = 1995;
    System.out.println(name);
    System.out.println(yearBorn);
	}
}
```

This would have the output:

```
Nick
1995
```

## `#!java int`

The first type of data we will store is the whole number. Whole numbers are very
common in programming. You often see them stored as ages, maximum sizes, or the
number of times some code has been run, among many other uses.

In Java, whole numbers are stored in the _`#!java int`_ primitive data type.

`#!java int`s hold positive numbers, negative numbers, and zero. They do not
store fractions or numbers with decimals in them.

The `#!java int` data type allows values between -2,147,483,648 and
2,147,483,647, inclusive.

To declare a variable of type `#!java int`, we use the `#!java int` keyword
before the variable name:

```java linenums="1"
// int variable declaration
int yearJavaWasCreated;
// assignment
yearJavaWasCreated = 1996;
// declaration and assignment
int numOfPrimitiveTypes = 8;
```

## `#!java double`

Whole numbers don't accomplish what we need for every program. What if we wanted
to store the price of stomething? We need a decimal point. What if we need to
store the world's population? That number would be larger than the `#!java int`
type can hold.

The `#!java double` primitive data type can help. `#!java double` can hold
decimals as well as very small/large numbers. The maximum value is
1.797,693,134,862,315,7 E+308, which is approximately 17 followed by 307 zeros.
The minimum value is 4.9 E-324, which is 324 decimal places!

To declare a variable of type `#!java double`, we use the `#!java double`
keyword in the declaration:

```java linenums="1"
// doubles can have decimal places:
double price = 8.99;
// doubles can have values bigger than an int can hold:
double gdp = 12237700000;
```

## `#!java boolean`

Often our programs face questions that can only be answered with yes or no.
These questions could be: is the oven on? Is the light green? Did I eat
breakfast?

These questions are answered with a _boolean_, a type that references on of two
values: `#!java true` or `#!java false`.

We declare boolean variables by using the keyword `#!java boolean` before the
variable name:

```java linenums="1"
boolean javaIsACompiledLanguage = true;
boolean javaIsACupOfCoffee = false;
```

## `#!java char`

How do we answer questions like: What grade did you get on the test? What letter
does your name start with?

The `#!java char` data type can hold any character, like a letter, space, or
punctuation mark. It must be surrounded by single quotes, `'`.

For example:

```java linenums="1"
char grade = 'A';
char firstLetter = 'p';
char punctuation = '!';
```

## `#!java String`

So far, we have learned about primitive data types, which are the simplest types
of data with no built-in behavior. Our programs will also use `#!java String`s,
which are _objects_, instead of primitives. Objects have built-in behavior.

`#!java String`s hold sequnces of characters. We've already seen instances of a
`#!java String`, for example, when we printed out `"Hello World!"`. There are
two ways to create a `#!java String` object, using a `#!java String` literal or
calling the `#!java String` class to create a new `#!java String` object.

A _`#!java String` literal_ is any sequence of characters enclosed in
double-quotes (`""`). Like primitive-type variables, we declare a
`#!java String` variable by specifying the type first:

```java linenums="1"
String greeting = "Hello World!";
```

We could also create a _new `#!java String` object_ by calling the
`#!java String` class when declaring a `#!java String` like so:

```java linenums="1"
String salutations = new String("Hello World!");
```

There are subtle differences in behavior depending on whether you create a
`#!java String` using a `#!java String` literal or a new `#!java String` object.
For these notes, we will almost always be using `#!java String` literals.

## Static Checking

The Java programming language has _static typing_. Java programs will not
compile if a variable is assigned a value of an incorrect type. This is a _bug_,
specifically a type declaration bug.

Bugs are dangerous! They cause our code to crash, or produce incorrect results.
Static typing helps because bugs are caught during programming rather than
during the execution of code.

The program will not compile if the declared type of the variable does not match
the type of the assigned value:

```java linenums="1"
int greeting = "Hellow World!";
```

The `#!java String` `"Hello World!"` cannot be held in a variable of type
`#!java int`.

For the example above, we see an error in the console at compilation:

```
error: incompatible types: String cannot be converted to int
    int greeting = "Hello World";
```

When bugs are not caught at compilation, they interrupt execution of the code by
causing _runtime errors_. The program will crash.

Java's static typing helps programmers avoid runtime errors, and thus have much
safer code that is free from bugs.

## Naming

Let's imagine that we are storing a user's name for their profile. Which of the
following code is better named?

```java
String data = "Manfred";
```

or

```java
String nameOfUser = "Manfred";
```

While both of these will compile, the second example is easier to understand.
Readers of the code will know the purpose of the value: `Manfred`.

Naming variables according to convention leads to clear, readable, and
maintainable code. When someone else, or our future self, reads the code, there
is no confusion about the purpose of the variable.

In Java, variable names are case-sensitive. `myHeight` is a different variable
from `myheight`. Then length of a variable name is unlimited, but we should keep
it concise while keeping the meaning clear.

A variable starts with a valid letter, or a `$`, or a `_`. No other symbol or
numbers can begin a variable name. `1stPlace` and `*Gazer` are not valid names.

Variable names of only one word are spelling in all lowercase letters. Variable
names of more than one word have the first letter lowercase while the beginning
letter of each subsequent word is capitalized. This style of capitalization is
called _camelCase_.

```java linenums="1"
// good style
boolean isHuman;

// bad styles
// no capitalization for new word
boolean ishuman;
// first word should be lowercase
boolean IsHuman;
//underscores don't separate words
boolean is_human;
```

## Quick Review

Below is a program that contains all of the above concepts:

```java linenums="1"
public class NickProfile {
	public static void main(String[] args) {
    String name = "Nick";
    int age = 26;
    double desiredSalary = 110000.00;
    char gender = 'm';
    boolean lookingForJob = true;
	}
}
```

**Tips**

-   Addition and subtraction, using `+` and `-`

-   Multiplication and division, using `*` and `/`

-   The modulo operator for finding remainders, `%`

-   Compound assignment operators `+=`, `-=`, `*=`, `/=`, and `%=`.

-   The order of operations: parentheses -> multiplication -> division -> modulo
    -> addition -> subtraction

-   Greater than, `>`, and less than, `<`

-   Equal to, ==, and not equal to, `!=`

-   Greater than or equal to, `>=`, and less than or equal to, `<=`

-   `equals()` for comparing `String`s and other objects

-   Using `+` to concatenate `String`s

-   The `final` keyword which makes variables unchangeable
