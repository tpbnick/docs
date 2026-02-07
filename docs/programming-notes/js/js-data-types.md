# Variables and Simple Data Types

## Variables

Variables are a JavaScript developer's bread and butter. They make it really
easy to write complex programs with lots and lots of instructions, and keep
everything organized and straight. Often times when you're writing a program in
JavaScript, there will be several pieces of data that you need to keep track of.
Think for example of Facebook. Facebook keeps track of tons of information and
displays it on their websites and apps. Things like names, birthdays, status',
etc. In order for us to write more complex programs like these, that do more
than print text out onto the screen, we'll need to learn how to manage all of
the information in our programs and use variables.

Variables are essentially containers which allow a program to store different
pieces of information inside of them. Once the information is stored inside the
variable, that information can then be accessed throughout the program simply by
referring to the variable's name. Using variables is a great way to keep track
of and organize your data. When creating variables, make sure to use descriptive
names! For example, if we were creating a variable to hold someones age, using
`#!js var age` is much better than `#!js var a`. This can save time trying to
figure out what each variable is defining!

Let's make some variables in JS:

```js
var phrase = "To be or not to be";

document.write(phrase);
```

`#!js var` is a special word in JS, which tells JS that a variable is being
created. Now we can call the variable within the `#!js document.write();`
command instead of having to type out the string. This can be very powerful and
save programmers a ton of time! We can also change the variable after defining
it originally:

```js
var phrase = "To be or not to be";

document.write(phrase);
phrase = "Apple";
document.write(phrase);
```

Now it should print out `To be or not to be` and `apple`.

We are not limited to only storing strings of text within a variable. We can
also store numbers (whole numbers or decimals), boolean variables, undefined,
and Null:

```js
var name = "Nick";
var age = 25;
var gpa = 3.8;
var isMale = true;
var flaws = null;
var description = undefined;

document.write(`${name} is ${age} years old.`);
if ((isMale = true)) {
    document.write(`He has a ${gpa} GPA.`);
} else {
    document.write(`She has a ${gpa} GPA.`);
}
```

The above code should have the following output:

```
Nick is 25 years old.He has a 3.8 GPA.
```

`#!js null` and `#!js undefined` are different because when you use `#!js null`,
you are saying that there is no value, but `#!js undefined` says that there is
no value _yet_. You will probably not use `#!js null` or `#!js undefined` much
as a developer, but they are still good to know/understand.

The `$` used above is called _interpolation_. This allows us to insert, or
_interpolate_, variables into strings using _template literals_.

Notice that:

-   A template literal is wrapped by backticks ``` (this key is usually located
    on the top of your keyboard, left of the 1 key).

-   Inside the template literal, you’ll see a placeholder, `#!js ${myPet}`. The
    value of `myPet` is inserted into the template literal.

-   When we interpolate `#!js I own a pet ${myPet}.`, the output we print is the
    string: `'I own a pet armadillo.'`

One of the biggest benefits to using template literals is the readability of the
code. Using template literals, you can more easily tell what the new string will
be. You also don't have to worry about escaping double quotes or single quotes.

Remember to **use descriptive variable names**! Think of a variable as a moving
box. When you fill up the box it is common to write on the outside of the box
what it contains. Use similar logic when it comes to naming variables.

### Create a Variable: `#!js let`

The `#!js let` keyword signlas that the variable can be reassigned a different
value. Take a look at the example:

```js linenums="1"
let meal = "Enchiladas";
console.log(meal); // prints Enchiladas
meal = "Burrito";
console.log(meal); // prints Burrito
```

Another concept that we should be aware of when using `#!js let` (and even
`#!js var`) is that we can declare a variable without assigning the vairable a
value. In such a case, the variable will be automatically initialized with a
value of `undefined`:

```js linenums="1"
let price;
console.log(price); // prints undefined
price = 350;
console.log(price); // prints 350
```

### Create a Variable: `#!js const`

The `#!js const` keyword is short for the word constant, which means that it
cannot be reassigned. Just like `#!js var` and `#!js let`, you can store any
value in a `#!js const` variable (it also follows the same structure!). Take a
look at the following example:

```js linenums="1"
const myName = "Nick";
console.log(myName); // prints Nick
```

As you can see, we created a `#!js const` variable named `myName`, which should
never have to change. If you try to reassign a `#!js const` variable, you'll get
a `TypeError`.

Constant variables _must_ be assigned a value when declared. If you try to
declare a `#!js const` variable without a value, you'll get a `TypeError`.

If you're trying to decide between which keyword to use, `#!js let` or
`#!js const`, think about whether you'll need to reassign the variable later on.

### `#!js typeof` Operator

While writing code, it can be useful to keep track of the data types of the
variables in your program. If you need to check the data type of a variable's
value, you can use the `#!js typeof` operator.

The `#!js typeof` operator checks the value to its right and _returns_, or
passes back, a string of the data type.

```js linenums="1"
const unknown1 = "foo";
console.log(typeof unknown1); // prints string

const unknown2 = 10;
console.log(typeof unknown2); // prints number

const unknown3 = true;
console.log(typeof unknown3); // prints boolean
```

## Strings

<<<<<<< HEAD Strings are any grouping of characters on your keyboard (letters,
numbers, space, symbolsm etc.) surrounded by single quotes `#!js ' ... '` or
double quotes `#!js " ... "`. Though we prefer single quotes. Some people like
to think of string as a fancy word for text.

```js linenums="1"
"This is Nick's Docs!";
"Single quotes work too!";
"JS is fun!";
```

Strings cannot be divided, multiplied, or subtracted, but the + operator _can_
be used on them. It does not add, but it _concatenates_ - it glues two strings
together.

The following line will produced the string "`concatenate`":

```js
"con" + "cat" + "e" + "nate";
```

We cab also concatenate variables with additional strings:

```js linenums="1"
let myName = "Nick";
console.log("Hello, my name is " + myName + "!");
// prints Hello, my name is Nick!
```

## Booleans

Booleans have only two possible values - either `#!js true` or `#!js false`. It
is helpful to think of booleans as on and off switches or as the answers to a
"yes" or "no" question.

Here is one way to produce Boolean values:

```js linenums="1"
console.log(3 > 2);
// true
console.log(3 < 2);
// false
```

Strings can be compared in the same way:

```js linenums="1"
console.log("Aardvark" < "Zoroaster");
// true
```

The way strings are ordered is roughly alphabetic but not really what you'd
expect to see in a dictionary: uppercase letters are always "less" than
lowercase ones, so "Z" < "a", and nonalphabetic characters (!, -, and so on) are
also include in the ordering. When comparing strings, JavaScript goves over the
characters from left to right, comparing the Unicode codes one by one.

Other similar operators are `>=` (greater than or equal to), `<=` (less than or
equal to), `==` (equal to), and `!=` (not equal to).

```js linenums="1"
console.log("Itchy" != "Scratchy");
// true
console.log("Apple" == "Orange");
// false
```

## Numbers

Values of the _number_ type are, unsurprisingly, numeric values. In a JavaScript
program, they are written as follow:

```js
44;
12.34;
```

JavaScript uses a fixed number of bits, 64 of them, to store a single number
value. There are only so many patterns you can make with 64 bits, which means
that the number of different numbers that can be represented is limited. With
_N_ decimal digits, you can represent 10<sup>N</sup> numbers. Similarly, given
64 binary digits, you can represent 2<sup>64</sup> number, which is about 18
quintillion. That's a lot.

Fractional numbers are simply written by using a dot (`12.34`). For very big or
very small numbers, you may also use scientific notation by adding an _e_ (for
exponent), followed by the exponent of the number:

```js
2.998e8; // this is 2.998 x 10^8 = 299,800,000
```

## Arithmetic Operators

Basic arithmetic operators often come in handy when programming.

An _operator_ is a character that performs a task in our code. JavaScript has
several built-in _arithmetic operators_, that allow us to perform mathematical
calculations on numbers. These include the following operators and their
corresponding symbols:

1. Add: `+`

2. Subtract: `-`

3. Multiply: `*`

4. Divide: `/`

5. Remainder: `%`

The first four might work how you guess:

```js linenums="1"
console.log(3 + 4); // prints 7
console.log(5 - 1); // prints 4
console.log(4 * 2); // prints 8
console.log(9 / 3); // prints 3
```

Note that when we `#!js console.log()` the computer will evaluate the expression
inside the parentheses and print that result to the console. If we wanted to
print the characters `#!js 3+4`, we would wrap them in quotes and print them as
a string.

The remainder operator, sometimes known as _modulo_, returns the number that
remains after the right-hand number divides into the left-hand number as many
times as it can.

```js linenums="1"
console.log(11 % 3); // prints 2
console.log(12 % 3); // prints 0
```

`#!js 11 % 3` equals 2 because 3 fits into 11 three times, leaving two as the
remainder.

### The Increment and Decrement Operator

Other mathematical assignment operators include the _increment operator_ (`++`)
and _decrement operator_ (`--`).

The increment operator will increase the value of the variable by 1. The
decrement operator will decrease the value of the variable by 1. For example:

```js linenums="1"
let a = 10;
a++;
console.log(a); // prints 11
```

```js linenums="1"
let b = 20;
b--;
console.log(b); // prints 19
```

Just like the other simple operators (`+=`, `-=`, `*=`, `/=`), the variable's
value is updated and _assigned_ as the new value of that variable.

## Properties

When you introduce a new piece of data into a JavaScript program, the browser
saves it as an instance of the data type. Every string instance has a property
called `length` that stores the number of characters in that string. You can
retrieve property information by appending the string with a period and the
property name:

```js
console.log("Hello".length); // prints 5
```

The `.` is another operator! We call it the _dot operator_.

In the example above, the value saved to the `length` property is retrieved from
the instance of the string, `#!js "Hello"`. The program prints `5` to the
console, because `Hello` has five characters in it.

## Methods

Remember that methods are actions we can perfrom. JavaScript provides a number
of string methods. We _call_, or use, these methods by appending an instance
with:

-   a period `.` (the dot operator)

-   the name of the method

-   opening and closing parentheses

E.g. `#!js 'example string'.methodName();`.

Does that syntax look a little familiar? When we use `#!js console.log();` we're
calling the `#!js .log()` method on the `console` object. Let's see
`#!js console.log()` and some real string methods in action!

```js linenums="1"
console.log("hello".toUpperCase()); // prints HELLO
console.log("Hey".startsWith("H")); // prints true
```
