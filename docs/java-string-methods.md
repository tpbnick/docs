# String Methods
## Introduction to String Methods
As you may recall, a `String`, which is widely used in Java, is an object that represents a sequence of characters.  it is a great way to store information.  

Because character strings are so vital to programming, Java dedicated an entire class to them.  This is great news for us because the `String` class has a lot of useful methods to help us perform operations on `String`s and data manipulation.  We don't have to import anything to use the `String` class because it's apart of the `java.lang` package, which is available by default.  

In these notes, we are going to go over several `String` methods:  

- `length()`  

- `concat()`  

- `equals()`  

- `indexOf()`  

- `charAt()`  

- `substring()`  

- `toUpperCase()`/`toLowerCase()`  

## `length()`  
In Java, the `length()` string method returns the length - total number of characters - of a `String`.  

Suppose we have a `String` called `str`, `str.length()` would return its length.  

Take a look at this code for example:  
```java linenums="1"
String str = "Hello World!";

System.out.println(str.length());
```  

`12` would be printed because `str` has 12 characters:  

`H` `e` `l` `l` `o` `_` `W` `o` `r` `l` `d` `!`  

In theory, the length of a `String` is the same as the [Unicode](https://en.wikipedia.org/wiki/Unicode) units of the `String`.  For example, escape sequences such as `\n` count as only one character.  

## `concat()`  
The `concat()` method concatenates one string to the end of another string.  Concatenation is the operation of joining two strings together.  

Suppose we have a `String` called `str1` and another `String` called `str2`, using `#!java str1.concat(str2)` would return `str1` with `str2` appended to the end of it.  

For example:  
```java linenums="1"  
String name = new String("Nick's ");  

name = name.concat("Docs");

System.out.println(name);
```
`Nick's Docs` would be printed.  

`String`s are immutable objects, which means that `String` methods, like `concat()` do not actually change a `String` object.    

Our variable, `name` holds a reference to the `String` object, `"Nick's "`.  When we use `concat()` on `name`, we changed its value so that it references a new object - `"Nick's "`, combined with the String literal, `"Docs"`.  

Suppose we do something slightly different.  We'll use `concat()` on `name` without reassigning its value:  

```java linenums="1"
String name = new String("Nick's ");  

name.concat("Docs");

System.out.println(name);
```
`Nick's` would be printed instead.  The value of the `String` can't change!  Instead, we create a new object and need to assign that new object some variable.  

## `equals()`  
With objects, such as `String`s, we can't use the primitive equality operator `==` to check for equality between two strings.  To test equality with strings, we use a built-in method called `equals()`.  

For example:
```java linenums="1"
String flavor1 = "Mango";
String flavor2 = "Peach";

System.out.println(flavor1.equals("Mango"));
// prints true
System.out.println(flavor2.equals("Mango"));
// prints false
```
Side note, there's also an `equalsIgnoreCase()` method that compares two strings without considering upper/lower case.  

We can also compare `String` values lexicographically (think dictionary order) using the `.compareTo()` method.  When we call the `.compareTo()` method, each character in the `String` is converted to Unicode; then the Unicode character from each `String` is compared.  

The method will return an `int` that represents the difference between the two `String`s.  

For example:
```java linenums="1"
String flavor1 = "Mango";
String flavor2 = "Peach";

System.out.println(flavor1.compareTo(flavor2));
```
Our program will output `-3`.  

When using a `compareTo()` method, we must pay attention to the return value:

- If the method returns `0`, the two `String`s are equal.  

- If the value is less that `0`, then the `String` object is lexicographically less than the `String` object argument.  

- If the value is greater than `0`, then the `String` object is lexicographically greater than the `String` object argument.  

## `indexOf()`
If we want to know the index of the first occurence of a character in a string, we can use the `indexOf()` method on a string.  

Remember that the indices in Java start with `0`:  
```java linenums="1"
String letters = "ABCDEFGHIJKLMN";

System.out.println(letters.indexOf("C"));
```
This would output `2`.  

Although `C` is the third letter in the English alphabet, it is located in the second index of the string.  

Suppose we want to know the index of the first occurrence of an entire substring.  The `indexOf()` instance method can also return where the substring begins (the index of the first character in the substring):
```java linenums="1"
String letters = "ABCDEFGHIJKLMN";

System.out.println(letters.indexOf("EFG"));
```
This would output `4` because `EFG` starts at index `4`.  

If the `indexOf()` doesn't find what it's looking for, it'll return a `-1`.  

## `charAt()`
The `charAt()` method returns the character located at a `String`'s specified index.  

For example:
```java linenums="1"
String str = "qwer";

System.out.println(str.charAt(2));
```
It would output `e` because that is what is located at index 2.  

Suppose we try to return the character located at index 4.  It would produce an `IndexOutOfBoundsException` error because index 4 is out of `str`'s range.  

## `substring()`  
There may be times when we only want a part of a string.  In such cases, we may want to extract a *substring* from a string.  

The `substring()` method does exactly that.  

For example:  
```java linenums="1"
String line = "The Heav'ns and all the Constellations rung";

System.out.println(line.substring(24));
```
It would output `Constellations rung` because that's what begins at index 24 and ends at the end of `line`.  The substring begins with the character at the specified index and extends the end of the string.  

But suppose we want a substring from the middle of the string.  We can include two arguments with this string method.  For example:  
```java linenums="1"
String line = "The Heav'ns and all the Constellations rung";

System.out.println(line.substring(24, 38));
```
It would output `Constellations` because that's the substring that begins at index 24 and ends at index 38.  

We can use this method to return a single-element substring at a specific index by calling `substring()` with the wanted index value plus one as the second argument.  

For example, we can use this method to output just `C`:  
```java linenums="1"
String line = "The Heav'ns and all the Constellations rung";

System.out.println(line.substring(24, 25));
```  
## `toUpperCase()`/`toLowerCase()`
There will be times when we have a word in a case other than what we need it in.  Luckily, Java has a couple `String` methods to help us out:  

- `toUpperCase()`: returns the string value converted to uppercase.  

- `toLowerCase()`: returns the string value converted to lowercase.  

For example:
```java linenums="1"
String input = "Cricket!";
 
String upper = input.toUpperCase();
// stores "CRICKET!"
 
String lower = input.toLowerCase();
// stores "cricket!"
```  
A good use of this functionality is to ensure consistency of the data you store in a database. Making sure all of the data you get from a user is lowercase before you store it in your database will make your database easier to search through later.  

### String Methods Review  
| String Method   | Value                                   |
|-----------------|-----------------------------------------|
| `length()`      | returns the length                      |
| `concat()`      | concatenates two strings                |
| `equals()`      | checks for equality between two strings |
| `indexOf()`     | returns the index of a substring        |
| `charAt()`      | returns a character                     |
| `substring()`   | returns a substring                     |
| `toUpperCase()` | returns the upper case version          |
| `toLowerCase()` | returns the lower case version          |