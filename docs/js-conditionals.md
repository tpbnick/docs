# Conditional Statements

## What are Conditional Statements?

In life, we make decisions based on circumstances. _If_ we are tired, we go to
sleep, _else_, we stay awake.

These if-else decisions can be modeled in code by creating _conditional
statements_. A conditional statement checks a specific condition(s) and performs
a task based on the condition(s).

In these notes, we will explore how programs make decisions by evaluating
conditions and introduce logic into our code.

## If Statement

We often perform a task based on a condition. For example, if the weather is
nice today, then we will go outside. If the alarm clock rings, then we’ll shut
it off. If we’re tired, then we’ll go to sleep.

In programming, we can also perform a task based on a condition using an `if`
statement:

```js linenums="1"
if (true) {
    console.log("This message will print!");
}
// prints: This message will print!
```

Notice in the example above, we have an `if` statement. The `if` statment is
composed of:

-   The `if` keyword followed by a set of parentheses `()` which is followed by
    a _code block_, or _block statement_, indicated by a set of curly braces
    `{}`.

-   Inside the parentheses `()`, a condition is provided that evaluates to
    `#!js true` or `#!js false`.

-   If the condition evaluates to `#!js true`, the code inside the curly braces
    `{}` runs, or _executes_.

-   If the condition evaluates to `#!js false`, the block won't execute.

## If-Else Statements

In the previous section, we used an `if` statement that checked a condition to
decide whether or not to run a block of code. In many cases, we'll have code we
want to run if our condition evaluates to `#!js false`.

If we wanted to add some default behavior to the `if` statement, we can add an
`else` statement to run a block of code when the condition evaluates to `false`.
Take a look at the inclusion of an `else` statement:

```js linenums="1"
if (false) {
    console.log("The code in this block will not run.");
} else {
    console.log("But the code in this block will!");
}
// prints: but the code in this block will!
```

An `else` statement must be paired with an `if` statement, and together they are
referred to as an `if...else` statement.

In the example above, the `else` statement:

-   Uses the `else` keyword following the code block of an `if` statement.

-   Has a code block that is wrapped by a set of curly braces `{}`.

-   The code inside the `else` statement code block will execute when the `if`
    statement's condition evaluates to `false`.

`if...else` statements allow us to automate solutions to yes-or-no questions,
also known as _binary decisions_.

## Comparison Operators

When writing conditional statements, sometimes we need to use different types of
operators to compare values. These operators are called _comparison operators_.

Here is a list of some handy comparison operators and their syntax:

-   Less than: `<`

-   Greater than: `>`

-   Less than or equal to: `<=`

-   Greater than or equal to: `>=`

-   Is equal to: `===`

-   Is not equal to: `!==`

Comparison operators compare the value on the left on the value on the right.
For instance:

```js
10 < 12; // evalutates to true
```

It can be helpful to think of comparison statements as questions. When the
answer is "yes", the statement evaluates to `tru`, and when the answer is "no",
the statement evaluates to `#!js false`. The code above would be asking: "Is 10
less than 12?" Yes! So `10 < 12` evaluates to `#!js true`.

We can also use comparison operators on different data types like strings:

```js
"apples" === "oranges"; // false
```

In the example above, we're using the _identity operator_ (`===`) to check if
the string `"apples"` is the same as the string `"oranges"`. Since the two
strings are not the same, the comparison statement evaluates to `#!js false`.

All comparison statements evaluate to either `#!js true` or `#!js false` and are
made up of:

-   Two values that will be compared.

-   An opeartor that separates the values and compares them accordingly (`<`,
    `>`, `<=`, `>=`, `===`, `!==`).

## Logical Operators

Working with conditionals means that we will be using booleans, `#!js true` or
`#!js false` values. In JavaScript, there are operators that work with boolean
values known as _logical operators_. We can use logical operators to add more
sophisticated logic to our conditionals. There are three logical operators:

-   the _and_ operator (`&&`)

-   the _or_ operator (`||`)

-   the _not_ operator, otherwise known as the _bang_ operator (`!`)

When we use the `&&` operator, we are checking that the two things are
`#!js true`:

```js linenums="1"
if (stopLight === "green" && pedestrians === 0) {
    console.log("Go!");
} else {
    console.log("Stop!");
}
```

When using the `&&` operator, both conditions _must_ evaluate to `#!js true` for
the entire condition to evaluate to `#!js true` and execute. Otherwise, if
either condition is `#!js false`, the `&&` condition will evaluate to
`#!js false` and the `else` block will execute.

If we only care about either condition being `#!js true`, we can use the `||`
operator:

```js linenums="1"
if (day === "Saturday" || day = "Sunday"){
	console.log("Enjoy the weekend!");
} else {
	console.log("Do some work!");
}
```

When using the `||` operator, onlly one of the conditions must evaluate to
`#!js true` for the overal statement to evaluate to `#!js true`. In the code
example above, if either `#!js day === "Saturday"` or `#!js dat === "Sunday"`
evaluates to `#!js true` the `if`'s condition will evaluate to `#!js true` and
its code block will execute. If the first condition in an `||` statement
evaluates to `#!js true`, the second condition won't even be checked. Only if
`#!js day === "Saturday"` evaluates to `#!js false` will `#!js day === "Sunday"`
be evaluated. The code in the `#!js else` statement above will execute only if
both comparisons evaluate to `#!js false`.

The `!` _not operator_ reverses, or _negates_, the value of a boolean:

```js linenums="1"
let excited = true;
console.log(!excited); // prints false

let sleepy = false;
console.log(!sleepy); // prints true
```

Essentially, the `!` operator will either take a `#!js true` value and pass back
a `#!js false`, or take a `#!js false` value and pass back a `#!js true`.

Logical operators are often used in conditional statements to add another layer
of logic to our code.

## Truthy and Falsy

Let's consider how non-boolean data types, like strings or numbers, are
evaluated when checked inside a condition.

Sometimes, you'll want to check if a variable exists and you won't necessarily
want it to equal a specific value - you'll only want to see if the variable has
been assigned a value.

Here is an example:

```js linenums="1"
let myVariable = "I exist!";

if (myVariable) {
    console.log(myVariable);
} else {
    console.log("The variable does not exist");
}
```

The code block in the `if` statement will run because `myVariable` has a
_truthy_ value; even though the value of `myVariable` is not explicitly the
value `#!js true`, when used in a boolean or conditional context, it evaluates
to `#!js true` because it has been assigned a non-falsy value.

So which values are _falsy_ - or evaluate to `#!js false` when checked as a
condition? The list of falsy values include:

-   `0`

-   Empty strings like `""` or `''`

-   `null` which represents when there is no value at all

-   `undefined` which represents when a declared variable lacks a value

-   `NaN`, or Not a Number

Here is an example with numbers:

```js linenums="1"
let numberOfApples = 0;

if (numberOfApples) {
    console.log("Let us eat apples!");
} else {
    console.log("No apples left!");
}

// prints 'No apples left!'
```

The condition evaluates to `#!js false` because the value of the
`numberOfApples` is `0`. Since `0` is a falsy value, the code block in the
`else` statement will run.

### Truthy and Falsy Assignment

Truthy and falsy evaluations open a world of short-hand possibilities!

Say you have a website and want to take a user's username to make a personalized
greeting. Sometimes, the user does not have an account, making the `username`
variable falsy. The code below checks if `username` is defined and assigns a
default string if it is not:

```js linenums="1"
let defaultName;
if (username) {
    defaultName = username;
} else {
    defaultName = "Stranger";
}
```

If you compine your knowledge of logical operators you can use a short-hand for
the code above. In a boolean condition, JavaScript assigns the truthy value to a
variable if you use the `||` operator in your assignment:

```js
let defaultName = username || "Stranger";
```

Because `||` or statements check the left-hand condition first, te variable
`defaultName` will be assigned the value of `username` if it is truthy, and it
will be assigned the value of `"Stranger"` if it is falsy. This concept is also
referred to as _short-circuit evaluation_.

## Ternary Operator

In the spirit of using short-hand syntax, we can use a _ternary operator_ to
simplify an `if-else` statement.

Take a look at the `if-else` example below:

```js linenums="1"
let isNightTime = true;

if (isNightTime) {
    console.log("Turn on the lights!");
} else {
    console.log("Turn off the lights!");
}
```

We can use a _ternary operator_ to perform the same functionality:

```js
isNightTime
    ? console.log("Turn on the lights!")
    : console.log("Turn off the lights!");
```

In the example above:

-   The condition, `isNightTime`, is provided before the `?`

-   Two expressions follow the `?` and are separated by a colon `:`

-   If the condition evaluates to `#!js true`, the first expression executes

-   If the condition evaluates to `#!js false`, the second expression executes

Like `if-else` statements, ternary operators can be used for conditions which
evaluate to `#!js true` or `#!js false`.

## Else If Statements

We can add more conditionals to our `if-else` with an `else if` statement. The
`else if` statement allows for more than two possible outcomes. You can add as
many `else if` statements as you'd like, to make more complex conditionals.

The `else if` statement always comes after the `if` statement and before the
`else` statement. The `else if` statement also takes a condition. Let's look at
the syntax:

```js linenums="1"
let stopLight = "yellow";

if (stopLight === "red") {
    console.log("Stop!");
} else if (stopLight === "yellow") {
    console.log("Slow down.");
} else if (stopLight === "green") {
    console.log("Go!");
} else {
    console.log("Caution, unknown!");
}
```

The `else-if` statements allow you to have multiple possible outcomes.
`if`/`else if`/`else` statements are read from top to bottom, so the first
condition that evaluates to `true` from the top to bottom is the block that gets
executed.

In the example above, since `#!js stopLight === 'red'` evaluates to `false` and
`#!js stopLight === 'yellow'` evaluates to `true`, the code inside the first
`else if` statement is executed. The rest of the conditions are not evaluated.
If none of the conditions evaluated to `true`, then the code in the `else`
statement would have executed.

## The `#!js switch` Keyword

`else-if` statements are a great tool if we need to check multiple conditions.
In programming, we often find ourselves needing to check multiple values and
handling each of them differently. For example:

```js linenums="1"
let groceryItem = "papaya";

if (groceryItem === "tomato") {
    console.log("Tomatoes are $0.49");
} else if (groceryItem === "papaya") {
    console.log("Papayas are $1.29");
} else {
    console.log("Invalid item");
}
```

In the code above, we have a series of conditions checking or a value that
matches a `groceryItem` variable. The code works fine, but imagine if we needed
to check 100 different values! Having to write that many `else if` statements
sounds like a pain!

A `switch` statement provides an alternative syntax that is easier to read and
write. A `switch` statement looks like this:

```js linenums="1"
let groceryItem = "papaya";

switch (groceryItem) {
    case "tomato":
        console.log("Tomatoes are $0.49");
        break;
    case "lime":
        console.log("Limes are $1.49");
        break;
    case "papaya":
        console.log("Papayas are $1.29");
        break;
    default:
        console.log("Invalid item");
        break;
}

// prints 'Papayas are $1.29'
```

-   The `switch` keyword initiates the statement and is followed by `(...)`,
    which contains the value that each `case` will compare. In the example, the
    value or expression of the `switch` statement is `groceryItem`.

-   Inside the block, `{...}`, there are multiple `case` keyword checks if the
    expression matches the specified value that comes after it. The value
    following the first `case` is `'tomato'`. If the value of `groceryItem`
    equalled `'tomato'`, that `case`'s `console.log()` would run.

-   The value of `groceryItem` is `'papaya'`, so the third `case` runs -
    `Papayas are $1.29` is logged to the console.

-   The `break` keyword tells the computer to exit the block and not execute any
    more code or check any other cases inside the code block. Note: without
    `break` keywords, the first matching case will run, but so will every other
    subsequent case regardless of whether or not it matches - including the
    default. This behavior is different from `if`/`else` conditional statements
    that execute only one block of code.

-   At the end of each `switch` statement, there is a `default` statement. If
    none of the `case`s are true, then the code in the `default` statement will
    run.

## Conditional Statements Review

-   An `if` statement checks a condition and will execute a task if that
    condition evaluates to `true`.

-   `if-else` statements make binary decisions and execute different code blocks
    based on a provided condition.

-   We can add more conditions using `else if` statements.

-   Comparison operators, including `<`, `>`, `<=`, `>=`, `===`, and `!==` can
    compare two values.

-   The logical and operator, `&&`, or “and”, checks if both provided
    expressions are truthy.

-   The logical operator `||`, or “or”, checks if either provided expression is
    truthy.

-   The bang operator, `!`, switches the truthiness and falsiness of a value.

-   The ternary operator is shorthand to simplify concise `if-else` statements.

-   A `switch` statement can be used to simplify the process of writing multiple
    `else if` statements. The `break` keyword stops the remaining `case`s from
    being checked and executed in a `switch` statement.
