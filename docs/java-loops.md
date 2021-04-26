# Loops
## Introduction to Loops
In the programming world, we hate repeating ourselves.  There are two reasons for this:  

- Writing the same code over and over is time-consuming.  

- Having less code means having less to debug.  

But we often need to do the same task more than once.  Fortunately, computers are really good (and fast) at doing repetitive tasks.  We do this through loops.  

A *loop* is a programming tool that allows developers to repeat the same block of code until some condition is met.  

The compiler first evaluates a boolean condition.  If the condition is `true`, then the loop body is executed.  When the last line of the loop body is executed, the condition is re-evaluated.  This process continues until the condition is `false`.  If the initial condition is `false`, the loop never gets executed.  

We employ loops to easily scale programs - saving time and minimizing mistatkes.  

We'll go over three types of loops that we'll see everywhere:  

- `while` loops  

- `for` loops  

- for-each loops  

### While Loops
A `while` loop looks a bit like an `if` statement:
```java linenums="1"
while (silliness > 10) {

    // code to run 

}
```
Like an `if` statement, the code inside a `while` loop will only run if the condition is `true`.  However, a `while` loop will continue running the code over and over until the condition evaluates to `false`.  So the above codeblock will continue to repeat until `silliness` is less than or equal to `10`.  
```java linenums="1"
// set attempts to 0
int attempts = 0;

// enter loop if condition is true
while (passcode != -524 && attempts < 4){

    System.out.println("Try again.");
    passcode = getNewPasscode();
    attempts += 1;

    // is the condition still true?  
    // if so, repeat code block
}
// exit when condition is not true
```
`while` loops are extremely useful when you want to run some code until a specific change happens.  However, if you aren't certain that change will occur, beware the infinite loop!  

*Infinite loops* occur when the condition will never evaluate to `false`.  This can cause your entire program to crash.  
```java linenums="1"
int hedgehogs = 5;

// this will cause an infinite loop:
while (hedgehogs < 6){

    System.out.println("Not enough hedgehogs!");
}
```
In the example above, `hedegehogs` remains equal to `5`, which is less than `6`, leading to an infinite loop.  

### Incrementing While Loops  
When looping through code, it's common to use a counter variable.  A *counter* (also known as an *iterator*) is a variable used in the conditional logic of the loop and (usually) incremented in value during each iteration through the code.  For example:  
```java linenums="1"
// counter is initialized
int wishes = 0;

// conditional logic uses counters
while (wishes < 3) {

    System.out.println("Wish granted.");
    // counter is incremented
    wishes++;
}
```
In the above example, the counter `wishes` gets intialized before the loop with a value of `0`, then the program will keep printing `"Wish granted."` and adding `1` to `wishes` as long as `wishes` has a value of less than `3`.  Once `wishes` reaches a value of `3` or more, the program will exit the loop.  

So the output would look like:
```
Wish granted.
Wish granted.
Wish granted. 
```
We can also decrement counters like this: 
```java linenums="1"
int pushupsToDo = 10;

while (pushupsToDo > 0) {
    
    doPushup();
    pushupsToDo--;

}
```
In the code above, the counter, `pushupsToDo`, starts at 10, and increments down one at a time.  When it hits 0, the loop exits.  

## For Loops
Incrementing with loops is actually so common in programming that Java (like many other programming languages) includes syntax specifically to address this pattern: `for` loops.  

A `for` *loop* header is made up of the following three parts, each separated by a semicolon:  

1. The intialization of the loop control variable.  

2. A `boolean` expression.  

3. An increment or decrement statement.  

The opening line might look like this:  
```java linenums="1"
for (int i = 0; i < 5; i++>){

    // code that will run  

}
```
In a `for` loop, an intialization statement is run once in order to intialize the loop control variable.  This variable is modified in every iteration, can be referenced in the loop body, and used to test the boolean condition.  In the example above, `i` is the loop control variable.  

Let's breakdown the above example:  

1. `i = 0`: `i` is intialized to `0`.  

2. `i < 5`: the loop is given a `boolean` confition that relies on the value of `i`.  The loop will continue to execute until `i < 5` is `false`.  

3. `i++`: `i` will be incremented at the end of each loop and before the condition is re-evaluated.  

So the code will run through the loop a total of five times.  

We'll also hear the term "iteration" in reference to loops.  When we *iterate*, it just means that we are repeating the same block of code.  

### Using For Loops 
Even though we can write `while` loops that accomplish the same task, `for` loops are useful because they help us remember to increment our counter - something that is easy to forget when we increment with a `while` loop.  

Leaving out that line of code would cause an infinite loop!  

Fortunately, equipped with our new understanding of `for` loops, we can help prevent infinite loops in our own code.  

It's important to be aware that, if we don't create the correct `for` loop header, we can cause the iteration to loop one too many times or one too few times; this occurance is known as an "off by one" error.  

For example, imagine we wanted to find the sum of the first ten numbers and wrote the following code:  
```java linenums="1"  
int sum = 0;
for (int i=0; i<10; i++){
    sum += i;
}
```
This code would produce an incorrect value of `45`.  We skipped adding `10` to `sum` because our loop control variable started with a value of `0` and stopped the iteration after it had a value of `9`.  We were off by one!  We could fix this by changing the condition of our loop to be `i <= 0;` or `i < 11;`.  

These errors can be tricky because, while they do not always produce an error in the terminal, they can cause some miscalculations in our code.  These are called logical errors - the code runs fine, but it didn't do what you expected it to do.  

### Iterating Over Arrays and ArrayLists
One common pattern we'll encounter as a programmer is *traversing*, or looping, through a list of data and doing something with each item.  In Java, that list would be an array or `ArrayList` and the loop could be a `for` loop.  

In order to traverse an array or `ArrayList` using a loop, we must find a way to access each element via its index.  We may recall that `for` loops are created with a counter variable.  We can use that counter to track the index of the current element as we iterate over the list of data.  

Because the first index in an array or `ArrayList` is `0`, the counter would begin with a value of `0` and increment until the end of the list.  So we can increment through an array or `ArrayList` using its indices.  

For example, if we wanted to add `1` to every `int` in an array `secretCode`, we could do this:  
```java linenums="1"
for (int i = 0; i < secretCode.length; i++){
    // increase value of element value by 1
    secretCode[i] += 1; 
}
```
Notice that our condition in this example is `i < secretCode.length`.  Because arrray indices start at `0`, the length of `secretCode` is 1 larger than its final index.  A loop should stop its traverse before its counter is equal to the length of the list.  

To give a concrete example, if the length of an array is `5`, the last index we want to access is `4`.  If we were to try to access index `5`, we would get an `ArrayIndexOutOfBoundsException` error!  

This is a very common mistake when first starting to traverse arrays.  

Traversing an `ArrayList` looks very similar:
```java linenums="1"  
for (int i = 0; i < secretCode.size(); i++){
    // increase value of element value by 1
    int num = secretCode.get(i);
    secretCode.set(i, num + 1);
}
```
We can also use `while` loops to travers through arrays and `ArrayList`s.  If we use a `while` loop, we need to create our own counter variable to access individual elements.  We'll also set our condition to continue looping until our counter variable equals the list length.  

For example, let's use a `while` loop to travers through an array:
```java linenums="1"
int i = 0; // initialize counter

while (i < secretCode.length) {
    secretCode[i] += 1;
    i++; // increment the while loop
}
```
Traversing through an `ArrayList` with a `while` loop would look like this:  
```java linenums="1"
int i = 0; // intialize counter

while (i < secretCode.size()){
    int num = secretCode.get(i);
    secretCode.set(i, num + 1);
    i++; // increment the while loop
}
```

### break and continue
If we ever want to exit a loop before it finishes all its iterations or want to skip one of the iterations, we can use the `break` and `continue` keywords.  

The `break` keyword is used to exit, or break, a loop.  Once `break` is executed, the loop will stop iterating.  For example:
```java linenums="1"
for (int i = 0; i < 10; i++){
    System.out.println(i);
    if (i == 4) {
        break;
    }
}
```
Even though the loop was set to iterate until the condition `i < 10` is `false`, the above code will output the following because we used `break`:
```
0
1
2
3
4
```
The `continue` keyword can be placed inside of a loop if we want to skip an iteration.  If `continue` is executed, the current loop iteration will immediately end, and the next iteration will begin.  We can use the `continue` keyword to skip any even valued iteration:  
```java linenums="1"
int[] numbers = {1, 2, 3, 4, 5};

for (int i = 0; i < numbers.length; i++){

    if (numbers[i] % 2 == 0) {
        continue;
    }
    System.out.println(numbers[i]);
}
```
This program would output the following:
```
1
3
5
```
In this case, if a number is even, we hit a `continue` statement, which skips the rest of that iteration, so the print statement is skipped.  As a result, we only see odd numbers print.  

### For-Each Loops
Sometimes we need access to the elements' indices or we only want to iterate through a portion of a list.  If that's the case, a regular `for` loop or `while` loop is a great choice.  

For example, we can use a `for` loop to print out each element in an array called `inventoryItems`:
```java linenums="1"
for (int inventoryItem = 0; inventoryItem < inventoryItems.length; inventoryItem++){
    // print element at current index
    System.out.println(inventoryItems[inventoryItem]);
}
```
But sometimes we couldn't care less about the indices; we only care about the element itself.  

At times like this, for-each loops come in handy.  

*For-each loops*, which are also referred to as *enhanced loops*, allow us to directly loop through each item in a list of items (like an array or `ArrayList`) and perform some action with each item.  

If we want to use a for-each loop to rewrite our program above, the syntax looks like this:  
```java linenums="1"
for (String inventoryItem : invenoryItems) {
    // print element value
    System.out.println(inventoryItem);
}
```
Our enhanced loop contains two items: an enhanced `for` loop variable (`inventoryItem`) and a list to traverse through (`inventoryItems`).  

We can read the `:` as "in" like this: for each `inventoryItem` (which should be a `String`) in `inventoryItems`, print `inventoryItem`.  

If we try to assign a new value to the enhanced `for` loop variable, the value stored in the array or `ArrayList` will not change.  This is because, for every iteration in the enhanced loop, the loop variable is assigned a copy of the list element.  

**Note**: we can name the enhanced `for` loop variable whatever we wantl using the singular of a plural is just a convention.  We may also encounter conventions like `String word : sentence`.  

### Removing Elements During Traversal
If we want to remove elements from an `ArrayList` while traversing through one, we can easily run into an error if we aren't careful.  

When an element is removed from an `ArrayList`, all the items that appear after the removed element will have their index value shift by negative one - it's like all elements shifted to the left!  We'll have to be very careful with how we use our counter variable to avoid skipping elements.  

#### Removing an Element Using `while`
When using a `while` loop and removing elements from an `ArrayList`, we should **not** increment the `while` loop's counter whenever we remove an element.  We don't need to increase the counter because all of the other elements have now shifted to the left.  

For example, if we removed the element at index `3`, then the element that was at index `4` will be moved to index `3`.  If we increase our counter to `4`, we'll skip that element.  

Take a look at this block of code that will remove all odd numbers from an `ArrayList`.  Think about what the value of `i` is, when we're increasing the value of `i`, and when `i < lst.size()` becomes `false`. 
```java linenums="1"
int i = 0; // initializing counter

while (i < lst.size()){
    // if value is odd, remove value
    if (lst.get(i) % 2 != 0){
        lst.remove(i);
    } else {
        // if content is even, increment counter
        i++;
    }
}
```
#### Removing an Element Using `for`
We can use a similar strategy when removing elements using a `for` loop.  When using a `while` loop, we decided to not increase our loop control variable whenever we removed an element.  This ensured that we would not skip an element when all of the other elements shifted to the left.  

When using a `for` loop, we, unfortunately, *must* increase our loop control variable - the loop control variable will always change when we reach the end of the loop (and it will usually change by `1` because we often use something like `i++`).  Since we can't avoid increasing our loop control variable, we can take matters into our own hands and decrease the loop control variable whenever we remove an item.  

For example:
```java linenums="1"
for (int i = 0; i < lst.size(); i++){
    if (lst.get(i) == "value to remove"){
        // remove value from ArrayList
        lst.remove(lst.get(i));
        // decrease loop control variable by `
        i--;
    }
}
```
Now whenever we remove an item, we'll decrease `i` by `1`.  Then when we reach the end of the loop, `i` will increase by `1`.  It will be like `i` never changed!  

**Note**: avoid manipulating the size of an `ArrayList` when using an enhanced `for` loop.  Actions like adding or removing elements from an `ArrayList` when using a `for each` loop can cause a `ConcurrentModificationException` error.  

## Loops Review
Quick recap on what the Loops notes cover:

- `while` loops: these are useful to repeat a code block an unknown number of times until some condition is met.  For example:  

```java linenums="1"
int wishes = 0;
 
while (wishes < 3) {
 
  // code that will run
  wishes++;
 
}
```  

- `for` loops: these are ideal for when you are incrementing or decrementing with a counter variable.  For example:  

```java linenums="1"
for (int i = 0; i < 5; i++) {
 
  // code that will run
 
}
```  

- for-each loops: these make it simple to do something with each item in a list.  For example:  

```java linenums="1"
for (String inventoryItem : inventoryItems) {
 
  // do something with each inventoryItem
 
}
```