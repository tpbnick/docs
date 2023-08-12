# Arrays

## What are arrays?

Organizing and storing data is a foundational concept of programming.

One way we organize data in real life is by making lists. Let's make one here:

```
New Year's 2022 Resolutions

1. Keep a journal
2. Take a falconry class
3. Learn to juggle
```

Let's now write this list in JavaScript, as an _array_:

```js
let newYearsResolutions = [
    "Keep a journal",
    "Take a falconry class",
    "Learn to juggle",
];
```

Arrays are JavaScript's way of making lists. Arrays can store any data types
(including strings, numbers, and booleans). Like lists, arrays are ordered,
meaning each item has a numbered position.

Here's an array of the concepts we'll cover in these notes:

```js
let concepts = ["creating arrays", "array structures", "array manipulation"];
```

## Creating Arrays

One way we can create an array is to use an _array literal_. An array literal
creates an array by wrapping items in square brackets `[]`. Remember, arrays can
store any data type - we can also have an array that holds all the same data
types or an array that holds different data types. For example:

```js
let arrayExample = ["array example", 10, true];
```

Let's take a closer look at the syntax in the array above:

-   The array is represented by the square brackets `[]` and the content inside

-   Each content item inside an array is called an _element_

-   There are three different elements inside the array

-   Each element inside the array is a different data type (string, number, and
    boolean)

-   The array is saved to a variable (`arrayExample`), which can be referenced
    later in our code

## Accessing ELements

Each element in an array has a numbered position known as its _index_. We can
access individual items using their index, which is similar to referencing an
item in a list based on that item's position.

Arrays in JavaScript are _zero-indexed_, which means the positions start
counting from `0`, rather than `1`. Therefore, the first item in an array will
be at position `0`. Let's see how we could access an element in an array:

```js linenums="1"
let cities = ["Baltimore", "Annapolis", "Columbia"];

console.log(cities[1]); // Annapolis
```

In the code snippet above:

-   `cities` is an array that has three elements

-   We're using bracket notation, `[]` with the index after the name of the
    array to access the element (see `#!js cities[1]`)

You are also able to access individual characters in a string using bracket
notation and the index. For example, you can write:

```js linenums="1"
const hello = "Hello World";
console.log(hello[6]); // Output: W
```

## Update Elements

Once you have access to an element in an array, you can also update its value.

```js linenums="1"
let seasons = ["Winter", "Spring", "Summer", "Fall"];

seasons[3] = "Autumn";
console.log(seasons); // Output: ['Winter', 'Spring', 'Summer', 'Autumn']
```

In the example above, the `seasons` array contained the names of the four
seasons.

However, we decided that we preferred to say `'Autumn'` instead of `'fall'`.

The line, `#!js seasons[3] = 'Autumn';` tells our program to change the item at
index 3 of the `seasons` array to be `'Autumn'` instead of what is already
there.

### Arrays with `let` and `const`

In JavaScript we can declare variables with both the `let` and `const` keywords.
Variables with `let` can be reassigned.

Variables declared with the `const` keyword cannot be changed or reassigned.
However, elements in an array declared with `const` remain mutable. This means
that we can change the contens of a `const` array, but cannot reassign a new
array or a different value.

For example:

```js linenums="1"
let condiments = ["Ketchup", "Mustard", "Soy Sauce", "Sriracha"];

const utensils = ["Fork", "Knife", "Chopsticks", "Spork"];

condiments[0] = "Mayo";
console.log(condiments); // Output: [ 'Mayo', 'Mustard', 'Soy Sauce', 'Sriracha' ]
condiments = ["Mayo"];
console.log(condiments); // Output: ['Mayo']

utensils[3] = "Spoon";
console.log(utensils); // Output: [ 'Fork', 'Knife', 'Chopsticks', 'Spoon' ]
utensils = ["Spoon"]; // Output: TypeError: Assignment to constant variable
```

As you can see above, we are able to change the content and the entire array
when we use `let`. We are only able to change elements inside an array declared
with `const` and will get an error if we try to change the entire array.

## The `.length` Property

One of an array’s built-in properties is `length` and it returns the number of
items in the array. We access the `.length` property just like we do with
strings. Check the example below:

```js linenums="1"
const newYearsResolutions = ["Keep a journal", "Take a falconry class"];

console.log(newYearsResolutions.length);
// Output: 2
```

In the example above, we log `newYearsResolutions.length` to the console using
the following steps:

-   We use dot notation, chaining a period with the property name to the array,
    to access the `length` property of the `newYearsResolutions` array.

-   Then we log the `length` of `newYearsResolution` to the console.

-   Since `newYearsResolution` has two elements, so `2` would be logged to the
    console.

When we want to know how many elements are in an array, we can access the
`.length` property.

## The `.push()` Method

JavaScript has many built-in methods that make working with arrays easier. These
methods are specifically called on arrays to make common tasks, like adding and
removing elements, more straightforward.

One method, `.push()` allows us to add items to the end of an array. Here we
have an example of how it is used:

```js linenums="1"
const itemTracker = ["item 0", "item 1", "item 2"];

itemTracker.push("item 3", "item 4");

console.log(itemTracker);
// Output: ['item 0', 'item 1', 'item 2', 'item 3', 'item 4'];
```

So how does `.push()` work?

-   We access the `push` method by using dot notation, connecting `push` to
    `itemTracker` with a period

-   Then we call it like a function. That's because `.push()` is a function and
    on that JS allows us to use right on an array

-   `.push()` can take a single argument or multiple arguments separated by
    commas. In this case, we're adding two elements: `'item 3'` and `'item 4'`
    to `itemTracker`

-   Notice that `.push()` changes, or _mutates_, `itemTracker`. You might also
    see `.push()` referred to as a _destructive_ array method since it changes
    the initial array.

## The `.pop()` Method

Another array method, `.pop()`, removes the last item of an array.

```js linenums="1"
const newItemTracker = ["item 0", "item 1", "item 2"];

const removed = newItemTracker.pop();

console.log(newItemTracker);
// Output: [ 'item 0', 'item 1' ]
console.log(removed);
// Output: item 2
```

-   In the example above, calling `.pop()` on the `newItemTracker` array removed
    `'item 2'` from the end

-   `.pop()` does not take any arguments, it simply removes the last element of
    an array

-   `.pop()` returns the value of the last element. In this example, we store
    the returned value in a variable `removed` to be used later

-   `.pop()` is a method that mutates the intitial array

## Additional Array Methods

There are many more array methods than just `.push()` and `.pop()`. You can read
about all of the array methods that exist on the
[Mozilla Developer Network (MDN) array documentation](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array).

`.pop()` and `.push()` mutate the array on which they’re called. However, there
are times that we don’t want to mutate the original array and we can use
non-mutating array methods. Be sure to check MDN to understand the behavior of
the method you are using.

Some arrays methods that are available to JavaScript developers include:
`.join()`, `.slice()`, `.splice()`, `.shift()`, `.unshift()`, and `.concat()`
amongst many others. Using these built-in methods make it easier to do some
common tasks when working with arrays.

## Arrays and Functions

Throughout these notes we have gone over arrays being mutable, or changeable.
Well what happens if we try to change an array inside a function? Does the array
keep the change after the function call or is it scoped to inside the function?

Take a look at the following example where we call `.push()` on an array inside
a function. Recall, the `.push()` method mutates, or changes, an array:

```js linenums="1"
const flowers = ["peony", "daffodil", "marigold"];

function addFlower(arr) {
    arr.push("lily");
}

addFlower(flowers);

console.log(flowers); // Output: ['peony', 'daffodil', 'marigold', 'lily']
```

Let's go over what happened in the code above:

-   The `flowers` array has 3 elements

-   The function `addFlower()` has a parameter of `arr` that uses `.push()` to
    add a `'lily'` element into `arr`

-   We call `addFlower()` with an argument of `flowers` which will execute the
    code inside `addFlower`

-   We check the value of `flowers` and it now includes the `'lily'` element!
    The array was mutated (changed)!

In conclusion, when you pass an array into a function, if the array is mutated
inside the function, that change will be maintained outside the function as
well. You might also see this concept explained as _pass-by-reference_ since
what we're actually passing to the function is a reference to where the variable
memory is stored and changing the memory.

## Nested Arrays

Earlier we noted that arrays can store other arrays. When an array contains
another array it is known as a _nested array_. Examine the example below:

```js
const nestedArray = [[1], [2, 3]];
```

To access the nested arrays, we can use the bracket notation with the index
value, just like we did to access any other element:

```js linenums="1"
const nestedArray = [[1], [2, 3]];

console.log(nestedArray[1]); // Output [2, 3]
```

Notice that `nestedArray[1]` will grab the element in index 1, which is the
array `[2, 3]`. Then, if we wanted to access the elements within the nested
array we can _chain_, or add on, more bracket notation with index values.

```js linenums="1"
const nestedArray = [[1], [2, 3]];

console.log(nestedArray[1]); // Output: [2, 3]
console.log(nestedArray[1][0]); // Output: 2
```

In the second `console.log()` statement, we have two bracket notations chained
to `nestedArray`. We know that `nestedArray[1]` is the array `[2, 3]`. Then to
grab the first element from that array, we use `nestedArray[1][0]` and we get
the value of 2.

## Arrays Review

-   Arrays are lists that store data in JavaScript.

-   Arrays are created with brackets `[]`.

-   Each item inside of an array is at a numbered position, or index, starting
    at `0`.

-   We can access one item in an array using its index, with syntax like:
    `#!js myArray[0]`.

-   We can also change an item in an array using its index, with syntax like
    `#!js myArray[0] = 'new string';`.

-   Arrays have a `length` property, which allows you to see how many items are
    in an array.

-   Arrays have their own methods, including `.push()` and `.pop()`, which add
    and remove items from an array, respectively.

-   Arrays have many methods that perform different tasks, such as `.slice()`
    and `.shift()`, you can find documentation at the
    [Mozilla Developer Network website](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array).

-   Some built-in methods are mutating, meaning the method will change the
    array, while others are not mutating. You can always check the
    documentation.

-   Variables that contain arrays can be declared with `let` or `const`. Even
    when declared with `const`, arrays are still mutable. However, a variable
    declared with `const` cannot be reassigned.

-   Arrays mutated inside of a function will keep that change even outside the
    function.

-   Arrays can be nested inside other arrays.

-   To access elements in nested arrays chain indices using bracket notation.
