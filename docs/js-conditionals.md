# Conditional Statements
## What are Conditional Statements?
In life, we make decisions based on circumstances.  *If* we are tired, we go to sleep, *else*, we stay awake.  

These if-else decisions can be modeled in code by creating *conditional statements*.  A conditional statement checks a specific condition(s) and performs a task based on the condition(s).  

In these notes, we will explore how programs make decisions by evaluating conditions and introduce logic into our code.  

## If Statement
We often perform a task based on a condition. For example, if the weather is nice today, then we will go outside. If the alarm clock rings, then we’ll shut it off. If we’re tired, then we’ll go to sleep.

In programming, we can also perform a task based on a condition using an `if` statement:
```js linenums="1"
if (true) {
	console.log("This message will print!");
}
// prints: This message will print!
```
Notice in the example above, we have an `if` statement.  The `if` statment is composed of:

- The `if` keyword followed by a set of parentheses `()` which is followed by a *code block*, or *block statement*, indicated by a set of curly braces `{}`.  

- Inside the parentheses `()`, a condition is provided that evaluates to `#!js true` or `#!js false`.  

- If the condition evaluates to `#!js true`, the code inside the curly braces `{}` runs, or *executes*.  

- If the condition evaluates to `#!js false`, the block won't execute.  

## If-Else Statements
In the previous section, we used an `if` statement that checked a condition to decide whether or not to run a block of code.  In many cases, we'll have code we want to run if our condition evaluates to `#!js false`.  

If we wanted to add some default behavior to the `if` statement, we can add an `else` statement to run a block of code when the condition evaluates to `false`.  Take a look at the inclusion of an `else` statement:
```js linenums="1"
if (false) {
	console.log("The code in this block will not run.");
} else { 
	console.log("But the code in this block will!");
}
// prints: but the code in this block will!
```
An `else` statement must be paired with an `if` statement, and together they are referred to as an `if...else` statement.  

In the example above, the `else` statement:

- Uses the `else` keyword following the code block of an `if` statement.  

- Has a code block that is wrapped by a set of curly braces `{}`.  

- The code inside the `else` statement code block will execute when the `if` statement's condition evaluates to `false`.  

`if...else` statements allow us to automate solutions to yes-or-no questions, also known as *binary decisions*.  

## Comparison Operators
When writing conditional statements, sometimes we need to use different types of operators to compare values.  These operators are called *comparison operators*.  

Here is a list of some handy comparison operators and their syntax:

- Less than: `<`  

- Greater than: `>`  

- Less than or equal to: `<=`  

- Greater than or equal to: `>=`  

- Is equal to: `===`  

- Is not equal to: `!==`  

Comparison operators compare the value on the left on the value on the right.  For instance:
```js 
10 < 12 // evalutates to true
```
It can be helpful to think of comparison statements as questions.  When the answer is "yes", the statement evaluates to `tru`, and when the answer is "no", the statement evaluates to `#!js false`.  The code above would be asking: "Is 10 less than 12?" Yes! So `10 < 12` evaluates to `#!js true`.  

We can also use comparison operators on different data types like strings:
```js
"apples" === "oranges" // false
```
In the example above, we're using the *identity operator* (`===`) to check if the string `"apples"` is the same as the string `"oranges"`.  Since the two strings are not the same, the comparison statement evaluates to `#!js false`.  

All comparison statements evaluate to either `#!js true` or `#!js false` and are made up of:  

- Two values that will be compared.  

- An opeartor that separates the values and compares them accordingly (`<`, `>`, `<=`, `>=`, `===`, `!==`).  

## Logical Operators
Working with conditionals means that we will be using booleans, `#!js true` or `#!js false` values.  In JavaScript, there are operators that work with boolean values known as *logical operators*.  We can use logical operators to add more sophisticated logic to our conditionals.  There are three logical operators:  

- the *and* operator (`&&`)  

- the *or* operator (`||`)  

- the *not* operator, otherwise known as the *bang* operator (`!`)  

When we use the `&&` operator, we are checking that the two things are `#!js true`:  
```js linenums="1"
if (stopLight === 'green' && pedestrians === 0) {
	console.log('Go!');
} else {
	console.log('Stop!');
}
```
When using the `&&` operator, both conditions *must* evaluate to `#!js true` for the entire condition to evaluate to `#!js true` and execute.  Otherwise, if either condition is `#!js false`, the `&&` condition will evaluate to `#!js false` and the `else` block will execute.  

If we only care about either condition being `#!js true`, we can use the `||` operator:
```js linenums="1"
if (day === "Saturday" || day = "Sunday"){
	console.log("Enjoy the weekend!");
} else {
	console.log("Do some work!");
}
```
When using the `||` operator, onlly one of the conditions must evaluate to `#!js true` for the overal statement to evaluate to `#!js true`.  In the code example above, if either `#!js day === "Saturday"` or `#!js dat === "Sunday"` evaluates to `#!js true` the `if`'s condition will evaluate to `#!js true` and its code block will execute.  If the first condition in an `||` statement evaluates to `#!js true`, the second condition won't even be checked.  Only if `#!js day === "Saturday"` evaluates to `#!js false` will `#!js day === "Sunday"` be evaluated.  The code in the `#!js else` statement above will execute only if both comparisons evaluate to `#!js false`.  

The `!` *not operator* reverses, or *negates*, the value of a boolean: 
```js linenums="1"
let excited = true;
console.log(!excited); // prints false

let sleepy = false;
console.log(!sleepy); // prints true
```
Essentially, the `!` operator will either take a `#!js true` value and pass back a `#!js false`, or take a `#!js false` value and pass back a `#!js true`.  

Logical operators are often used in conditional statements to add another layer of logic to our code.  

## Truthy and Falsy
Let's consider how non-boolean data types, like strings or numbers, are evaluated when checked inside a condition.  

Sometimes, you'll want to check if a variable exists and you won't necessarily want it to equal a specific value - you'll only want to see if the variable has been assigned a value.  

Here is an example:
```js linenums="1"
let myVariable = "I exist!";

if (myVariable) {
	console.log(myVariable);
} else {
	console.log("The variable does not exist");
}
```
The code block in the `if` statement will run because `myVariable` has a *truthy* value; even though the value of `myVariable` is not explicitly the value `#!js true`, when used in a boolean or conditional context, it evaluates to `#!js true` because it has been assigned a non-falsy value.   

So which values are *falsy* - or evaluate to `#!js false` when checked as a condition?  The list of falsy values include:

- `0`  

- Empty strings like `""` or `''`  

- `null` which represents when there is no value at all  

- `undefined` which represents when a declared variable lacks a value  

- `NaN`, or Not a Number

Here is an example with numbers:
```js linenums="1"
let numberOfApples = 0;
 
if (numberOfApples){
   console.log('Let us eat apples!');
} else {
   console.log('No apples left!');
}
 
// prints 'No apples left!'
```

The condition evaluates to `#!js false` because the value of the `numberOfApples` is `0`. Since `0` is a falsy value, the code block in the `else` statement will run.