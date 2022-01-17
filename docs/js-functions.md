# Functions
## What are Functions?
When first learning how to calculate the area of a rectangle, there’s a sequence of steps to calculate the correct answer:

- Measure the width of the rectangle.  

- Measure the height of the rectangle.  

- Multiply the width and height of the rectangle.  

With practice, you can calculate the area of the rectangle without being instructed with these three steps every time.

We can calculate the area of one rectangle with the following code:
```js linenums="1"
const width = 10;
const height = 6;
const area =  width * height;
console.log(area); // Output: 60
```
Imagine being asked to calculate the area of three different rectangles:
```js linenums="1"
// Area of the first rectangle
const width1 = 10;
const height1 = 6;
const area1 =  width1 * height1;
 
// Area of the second rectangle
const width2 = 4;
const height2 = 9;
const area2 =  width2 * height2;
 
// Area of the third rectangle
const width3 = 10;
const height3 = 10;
const area3 =  width3 * height3;
```  
In programming, we often use code to perform a specific task multiple times. Instead of rewriting the same code, we can group a block of code together and associate it with one task, then we can reuse that block of code whenever we need to perform the task again. We achieve this by creating a *function*. A function is a reusable block of code that groups together a sequence of statements to perform a specific task.  

In these notes, we will learn how to create and use functions, and how they can be used to create clearer and more concise code.

In JS, there are many was to create a function.  One way to create a unction is by using a *function declaration*.   Just like how a variable declaration binds a function to a name, or an *identifier*.  Take a look at the anatomy of a function declaration below:
```js
function greetWorld(){
    console.log("Hello, World!");
}
```
A function declaration consists of:  

* The `#!js function` keyword.  

* The name of the function, or its identifier, followed by parentheses.  

* A function body, or the block of statements required to perform a specific task, enclosed in the function's curly brackets, `{}`.

## Parameters and Arguments
Some functions can take inputs and use the inputs to perform a task.  When declaring a function, we can specify its *parameters*.  Parameters allow functions to accept input(s) and perform a task using the input(s).  We use parameters as placeholders for information that will be passed to the function when it is called.  

Let's observe how to specify parametes in our function declaration:

```js
function calculateArea(width, height) {
    console.log(width * height);
}
```
In the code above, `calculateArea()` computes the area of a rectangle based on two inputs, `width` and `height`.  The parameters are specified between the parenthesis as `width` and `height`, and inside the function body, they act like regular variables.  `width` and `height` act as placeholders for values that will be multiplied together.  

When calling a function that has parameters, we specify the values in the parentheses that follow the function name (in the example above: `calculateArea()`).  The values that are passed to the function when it is called are called *arguments*.  Arguments can be passed to the function as values or variables.  

```js  
calculateArea(10, 6);
```
In the function above, the number `10` is passed as the `width` and `6` is passed as the `height`.  Notice that the order in which arguments are passed and assigned follows the order that the parameters are declared.  

```js
const rectWidth = 10;
const rectHeight = 6;

calculateArea(rectWidth, rectHeight);
```
The variables `rectWidth` and `rectHeight` are initialized with the values for the height and width of the rectangle before being used in the function call.  

By using parameters, `calculateArea()` can be reused to compute the area of any rectangle!

Let's create an example function that takes an argument and prints out a message using the argument:

```js
function sayHello(name) {
    console.log("Hello, " + name + "!");
}

sayHello("Nick");
```
This code would have the output `Hello, Nick!`.  We can pass any name as the argument for the `sayHello()` function and it would print accordingly.

### Default Parameters
We can also set default parameters for arguments in a function.  Default parameters allow parameters to have a predetermined value in case there is no argument passed into the function or if the argument is `undefined` when called.

```js
function greeting (name = 'stranger') {
  console.log(`Hello, ${name}!`);
}
 
greeting('Nick'); // Output: Hello, Nick!
greeting(); // Output: Hello, stranger!
```
In the code above, we set a default parameter by using a `=` operator to assign the string `'stranger'`.  This ensures that if a argument is not passed to the function, the function will display the default message instead of erroring out.

## Return
When a function is called, the computer will run through the function's code and evaluate the result of calling the function.  By default that resulting value is `undefined`.  
```js
function rectangleArea(width, height) {
  let area = width * height;
}
console.log(rectangleArea(5, 7)); // Prints undefined 
```
In the code example above, we defined our function to calculate the `area` of the `width` and `height` parameter.  Then `rectangleArea()` is invoked with eh arguments `5` and `7`.  But when we went to print the results we got `undefined`.  Did we write our function wrong?  No!  In fact, the function worked fine, and the computer did compute the area as `35`, but we didn't capture it.  We are able to capture it with the `return` keyword!  

```js
function rectangleArea(width, height) {
  let area = width * height;
  return area;
}
```
To pass back information from the return call, we use a `return` statement.  To create a `return` statement, we use the `return` keyword followed by the value that we wish to return.  Like we saw above, if the value is omitted, `undefined` is returned instead.  

When a `return` statement is used in a function body, the execution of the function is stopped and the code that follows it will not be executed. Look at the example below:
```js
function rectangleArea(width, height) {
  if (width < 0 || height < 0) {
    return 'You need positive integers to calculate area!';
  }
  return width * height;
}
```
If an argument for `width` or `height` is less than `0`, then `rectangleArea()` will return `'You need positive integers to calculate area!'`. The second return statement `width * height` will not run.

The `return` keyword is powerful because it allows functions to produce an output. We can then save the output to a variable for later use.

## Helper Functions
We can also use the return value of a function inside another function. These functions being called within another function are often referred to as *helper functions*. Since each function is carrying out a specific task, it makes our code easier to read and debug if necessary.  

If we wanted to define a function that converts the temperature from Celsius to Fahrenheit, we could write two functions like:

```js
function multiplyByNineFifths(number) {
  return number * (9/5);
};
 
function getFahrenheit(celsius) {
  return multiplyByNineFifths(celsius) + 32;
};
 
getFahrenheit(15); // Returns 59
```
In the example above:

- `getFahrenheit()` is called and `15` is passed as an argument.  

- The code block inside of `getFahrenheit()` calls `multiplyByNineFifths()` and passes `15` as an argument.  

- `multiplyByNineFifths()` takes the argument of `15` for the `number` parameter.  

- The code block inside of `multiplyByNineFifths()` function multiplies `15` by `(9/5)`, which evaluates to `27`.  

- `27` is returned back to the function call in `getFahrenheit()`.  

- `getFahrenheit()` continues to execute. It adds `32` to `27`, which evaluates to `59`.  

- Finally, `59` is returned back to the function call `getFahrenheit(15)`.  

We can use functions to section off small bits of logic or tasks, then use them when we need to. Writing helper functions can help take large and difficult tasks and break them into smaller and more manageable tasks.
