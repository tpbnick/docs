# Arrays

## Introduction to Arrays

We have seen how to store single pieces of data in variables. What happens when
we need to store a group of data? What if we have a list of students in a
classroom? Or a ranking of the top 10 horses finishing a horse race?

If we were storing 5 lottery ticket numbers, for example, we could create a
different variable for each value:

```java linenums="1"
int firstNumber = 4;
int secondNumber = 8;
int thirdNumber = 12;
int fourthNumber = 16;
int fifthNumber = 20;
```

That is a lot of ungainly repeated code. What if we had 100 lottery numbers? It
is more clean and convenient to use a Java _array_ to stroe the data as a list.

An array hold a fixed number of values of one type. Arrays hold
`#!java double`s, `#!java int`s, `#!java boolean`s, or any other
[primitives](java-variables.md/#introduction-to-variables). Arrays can also
contains `#!java String`s as well as object references!

Each index of an array corresponds with a different value. Here is a diagram of
an array filled with integer values:

| elements | 4   | 8   | 12  | 16  | 20  |
| -------- | --- | --- | --- | --- | --- |
| indices  | 0   | 1   | 2   | 3   | 4   |

Similar to C and Python, the indexes start at 0! The element at index 0 is `4`,
while the element at index 1 is `8`. This array has a length of 5, since it
holds five elements, but the highest index of the array is 4.

### Creating an Array Explicitly

Imagine that we're using a program to keep track of the prices of different
items we want to buy. We would want a list of the prices and a list of the items
they correspond to. To create an array, we first declare the type of data it
holds.

```java
double[] prices;
```

Then, we can explicitly initialize the array to contain the data we want to
store:

```java
prices = {13.15, 15.87, 14.22, 16.55};
```

Just like with simple variables, we can declare and initialize in the same line:

```java
double[] prices = {13.15, 15.87, 14.22, 16.55};
```

We can use arrays to hold `#!java String`s and other objects as well as
primitives:

```java
String[] clothingItems = {"Tank Top", "Beanie", "Funny Socks", "Pants"};
```

### Importing Arrays

If we want to have a descriptive printout of an array, we need a
`#!java toString()` method that is provided by the `Arrays` _package_ in Java.

```java
import java.util.Arrays;
```

We put this line at the top of the file, before we even define the class!

When we import a package in Java, we are making all of the methods of that
package available in our code.

The `Arrays` package has many useful methods, including
`#!java Arrays.toString()`. When we pass an array into
`#!java Arrays.toString()`, we can see the contents of the array printed out.

```java linenums="1"
import java.util.Arrays;

public class Lottery(){

    public static void main(String[] args){
        int[] lotteryNumbers = {4, 8, 12, 16, 20};
        String betterPrintout = Arrays.toString(lotteryNumbers);
        System.out.println(betterPrintout);
    }
}
```

This code will print:

```
[4, 8, 12, 16, 20]
```

### Get Element By Index

Now that we have an array declared and intitialized, we want to be able to get
values out of it.

We use square brackets `[]` to access data at a certain index:

```java linenums="1"
double[] prices = {13.1, 15.87, 14.22, 16.55}

System.out.println(prices[1]);
```

This command will print out `15.87`.

This happens because `15.87` is the item at the `1` index of the array.

If we try to access an element outside of its appropriate index range, we will
receive an `ArrayIndexOutOfBoundsException` error.

For example, if we were to run the command
`#!java System.out.println(prices[5])`, we would get the following output:

```
java.lang.ArrayIndexOutOfBoundsException: 5
```

### Creating an Empty Array

We can also create empty arrays and then fill the items one by one. Empty arrays
have to be intitialized with a fixed size:

```java
String[] menuItems = new String[5];
```

Once you declare this size, it cannot be changed! This array will always be of
size `5`.

After declaring and intializing, we can set each index of the array to be a
different item:

```java linenums="1"
menuItems[0] = "Veggie hot Dog";
menuItems[1] = "Potato salad";
menuItems[2] = "Cornbread";
menuItems[3] = "Roasted broccoli";
menuItems[4] = "Coffee ice cream";
```

This group of commands has the same effect as assigning the entire array at
once:

```java linenums="1"
String[] menuItems = {"Veggie hot dog", "Potato salad", "Cornbread", "Roasted broccoli", "Coffee ice cream"};
```

We can also change an item after it has been assigned! Let's say this restaurant
is changing its broccoli dish to a cauliflower one:

```java
menuItems[3] = "Baked cauliflower";
```

Now the array looks like:

```
["Veggie hot dog", "Potato salad", "Cornbread", "Baked cauliflower", "Coffee ice cream"]
```

### Array Length

What if we have an array storing all the usernames for our program, and we want
to quickly see how many users we have? To get the length of an array, we can
access the `length` field of the array object:

```java linenums="1"
String[] menuItems = new String[5];
System.out.println(menuItems.length);
```

This command would print `5`, since the `menuItems` array has `5` slots, even
though they are all empty.

If we print out the length of the `prices` array:

```java linenums="1"
double[] prices = {13.1, 15.87, 14.22, 16.55};

System.out.println(prices.length);
```

We would see `4`, since there are four items in the `prices` array!

### `#!java String[] args`

When we write `#!java main()` methods for our programs, we use the parameter
`#!java String[] args`. Now that we know about array syntax, we can start to
parse what that means.

A `#!java String[]` is an array made up of `#!java String`s. Examples of
`#!java String` arrays:

```java linenums="1"
String[] humans = {"Nick", "Alyssa", "Matt", "Nathan"};
String[] robots = {"R2D2", "Marvin", "Wall-E", "Bender"};
```

The `#!java args` parameter is another example of a `#!java String` array. In
this case, the array `#!java args` contains the arguments that we pass in from
the terminal when we run the class file. (So far `#!java args` has been empty.)

So how can you pass arguments to `#!java main()`> Let's say we have this class
`HelloYou`:

```java linenums="1"
public class HelloYou {
    public static void main(String[] args){
        System.out.println("Hello " + args[0];)
    }
}
```

When we runn the file `HelloYou` in the terminal with an argument of `"Laura"`:

```
java HelloYou Laura
```

We get the output:

```
Hello Laura
```

The `#!java String[] args` would be interpreted as an array with one element,
`"Laura"`. When we use `#!java args[0]` in the main method, we can access that
element like we did in `HelloYou`.

We can actually create `if-else` statements that run based on the input:

```java linenums="1"
if (args[0].equals("A")){
    // do something
} else if (args[0].equals("B")){
    // do something
} else {
    // do something
}
```

### Arrays Review

We have now seen how to store a list of values in an array. We can use this
knowledge to make organized programs with more complex variables.

Throughout these notes, we have leared about:

-   Creating arrays explicitly, using `{` and `}`.

-   Accessing an index of an array, using `[` and `]`.

-   Creating empty arrays of a certain size, and filling the indices one by one.

-   Getting the length of an array using `.length`.

-   Using the argument `#!java args` that is passed into the `#!java main()`
    method of a class.

Let's create a small program that holds student names and test scores with the
following characteristics:

-   Make an array of strings called `students` with the following names: Sade,
    Alexus, Sam, Koma.

-   Create an empty array of `#!java double`s called `mathScores` of size 4.

-   Sade got a 94.5 on the test. Store this value in the same indice that she is
    listed in the `students` array.

-   Sam got a 76.8. Store this value in the appropriate spot in the `mathScores`
    array.

-   Finally, add a print statement that says: "The number of students in the
    class is `numStudents`." using the `.length` operator.

```java linenums="1"
import java.util.Arrays;

public class Classroom {

    public static void main(String[] args){
        String[] students = {"Sade", "Alexus", "Sam", "Koma"};
        double[] mathScores = new double[4];
        mathScores[0] = 94.5;
        mathScores[2] = 76.8;

        System.out.println("The number of students in the class is " + students.length + ".");
    }
}
```

## Introduction to ArrayLists

When we work with arrays in Java, we've been limited by the fact that once an
array is created, it has a fixed size. We can't add or remove elements.

But what if we needed to add to the book lists, newsfeeds, and other structures
we were using arrays to represent?

To create multiple and dynamic lists, we can use Java's `ArrayList`s.
`ArrayList`s allow us to:

-   Store object references as elements

-   Store elements of the same type (just like arrays)

-   Access elements by index (just like arrays)

-   Add elements

-   Remove elements

Remember how we had to [import `java.util.Arrays`](#importing-arrays) in order
to use additional array methods? To use an `ArrayList` at all, we need to import
them from Java's `util` package as well:

```java
import java.util.ArrayList;
```

### Creating ArrayLists

To create an `ArrayList`, we need to declare the type of object it will hold,
just as we do with arrays:

```java
ArrayList<String> babyNames;
```

We use angle brackets (`<>`) to declare the type of the `ArrayList`. These
symbols are used for _generics_. Generics are a Java construct that allows us to
define classes and objects as parameters of an `ArrayList`. For this reason, we
can't use primitive types in an `ArrayList`:

```java linenums="1"
// This code won't compile:
ArrayList<int> ages;

// This code will compile:
ArrayList<Integer> ages;
```

The `<Integer>` generic has to be used in an `ArrayList` instead. You can also
use `<Double>` and `<Char>` for types you would normally declare as
`#!java double`s or `#!java char`s.

We can intialize to an empty `ArrayList` using the `#!java new` keyword:

```java linenums="1"
// Declaring:
ArrayList<Integer> ages;
// Intializing:
ages = new ArrayList<Integer>();

// Declaring and intializing in one line:
ArrayList<String> babyNames = new ArrayList<String>();
```

#### Adding Items to an ArrayList

Now we have an empty `ArrayList`, but how do we get it to store values?

`ArrayList` comes with an `add()` method which inserts an element into the
structure. There are two ways we can use `add()`.

If we want to add an element to the end of the `ArrayList`, we'll call `add()`
using only one arguement that represents the value we are inserting. In this
example, we'll add objects from the `Car` class to an `ArrayList` called
`carShow`:

```java linenums="1"
ArrayList<Car> carShow = new ArrayList<Car>();

carShow.add(ferrari);
// carShow now holds [ferrari]
carShow.add(thunderbird);
// carShow now holds [ferrari, thunderbird]
carShow.add(volkswagen);
// carShow now holds [ferrari, thunderbird, volkswagen]
```

If we want to add an element at a specific index of our `ArrayList`, we'll need
two arguments in our method call: the first arguement will define the index of
the new element while the second argument defines the value of the new element:

```java linenums="1"
// Insert object corvette at index 1
carShow.add(1, corvette);
// carShow now holds [ferrari, corvette, thunderbird, volkswagen]

// Insert object porsche at index 2
carShow.add(2, porsche);
// carShow now holds [ferrari, corvette, porsche, thunderbird, volkswagen]
```

By inserting a value at a specified index, any elements that appear after this
new element will have their index shift over by 1.

Also, note that an error will occur if we try to insert a value at an index that
does not exist.

You are able to add multiple data types to the same array using `add()`:

```java linenums="1"
ArrayList assortment = new ArrayList<>();
assortment.add("Hello"); // String
assortment.add(12); // Integer
assortment.add(ferrari); // reference to Car
// assortment holds ["Hello", 12, ferrari]
```

In this case, the items stored in this `ArrayList` will be considered `Objects`.
As a result, they won’t have access to some of their methods without doing some
fancy casting. Although this type of `ArrayList` is allowed, using an
`ArrayList` that specifies its type is preferred.

### ArrayList Size

Let's say we have an `ArrayList` that stores items in a user's online shopping
cart. As the user navigates through the site and adds items, their cart grows
bigger and bigger.

If we wanted to display the number of items in the cart, we could find the size
of it using the `size()` method:

```java linenums="1"
ArrayList<String> shoppingCart = new ArrayList<String>();

shoppingCart.add("Goofy socks");
System.out.println(shoppingCart.size());
// 1 is printed
shoppingCart.add("Funny tie");
System.out.println(shoppingCart.size());
// 2 is printed
shoppingCart.add("HK-416 Assault Rifle");
System.out.println(shoppingCart.size());
// 3 is printed
```

In dynamic objects like `ArrayList`s, it's important to know how to access the
amount of objects we have stored.

### Accessing an Index

With arrays, we can use bracket notation to access a value at a particular
index:

```java linenums="1"
double[] ratings = {3.2, 5.5, 1.6};

System.out.println(ratings[1]);
// this will print 5.5
```

This code prints `5.5`, the value at index `1` of the array.

For `ArrayList`s, bracket notation won't work. Instead we use the method `get()`
to access an index:

```java linenums="1"
ArrayList<String> shoopingCart = new ArrayList<String>();

shoppingCart.add("Goofy Socks");
shoppingCart.add("Funny tie");
shoppingCart.add("HK-416 Assault Rifle");

System.out.println(shoppingCart.get(2));
```

This code prints `"HK-416 Assault Rifle"`, which is the value at index 2 of the
`ArrayList`.

### Changing a Value

When we were using arrays, we could rewrite entries by using bracket notation to
reassign values:

```java linenums="1"
String[] shoppingCart = {"Goofy Socks", "Funny tie", "HK-416 Assault Rifle"};

shoppingCart[0] = "Serious Socks";
// This overwrites the "Goofy Socks" string with "Serious Socks"
```

`ArrayList` has a slightly different way of doing this, using the `set()`
method:

```java linenums="1"
ArrayList<String> shoppingCart = new ArrayList<shoppingCart>();

shoppingCart.add("Goofy Socks");
shoppingCart.add("Funny tie");
shoppingCart.add("HK-416 Assault Rifle");

shoppingCart.set(0, "Serious Socks");

// shoppingCart now holds ["Serious Socks", "Funny tie", "HK-416 Assault Rifle"]
```

### Removing an Item

What if we wanted to get rid of an entry alltogether? For arrays, we would have
to make a completely new array without the value.

Luckily, `ArrayList`s allow us to remove an item by specifying the index to
remove:

```java linenums="1"
ArrayList<String> shoppingCart = new ArrayList<shoppingCart>();

shoppingCart.add("Goofy Socks");
shoppingCart.add("Funny tie");
shoppingCart.add("HK-416 Assault Rifle");

shoppingCart.remove(1);
// shoppingCart now holds ["Goofy Socks", "HK-416 Assault Rifle"]
```

We can also remove an item by specifying the value to remove:

```java linenums="1"
ArrayList<String> shoppingCart = new ArrayList<shoppingCart>();

shoppingCart.add("Goofy Socks");
shoppingCart.add("Funny tie");
shoppingCart.add("HK-416 Assault Rifle");

shoppingCart.remove("Funny tie");
// shoppingCart now holds ["Goofy Socks", "HK-416 Assault Rifle"]
```

**Note**: This command removes the FIRST instance of the value "Funny tie".

### Getting an Item's Index

What if we had a really large list and wanted to know the position of a certain
element in it? For instance, what if we had an `ArrayList` `detectives` with the
names of fictional detectives in chronological order, and we wanted to know what
position `"Flecther"` was.

```java linenums="1"
// detectives holds ["Holmes", "Poirot", "Marple", "Spade", "Fletcher", "Conan", "Ramotswe"];
System.out.println(detectives.indexOf("Fletcher"));
```

This code would print `4`, since `"Fletcher"` is at index `4` of the
`detectives` `ArrayList`.

### ArrayLists Review

Some crucial methods in `ArrayList`s:

-   Adding a new ArrayList item using `add()`.

-   Accessing the size of an ArrayList using `size()`.

-   Finding an item by index using `get()`.

-   Changing the value of an ArrayList item using `set()`.

-   Removing an item with a specific value using `remove()`.

-   Retrieving the index of an item with a specific value using `indexOf()`.
