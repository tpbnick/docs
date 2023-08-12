#How to utilize the findNeedles function

##`findNeedles` Overview The `findNeedles` API function searches for up to five
strings, from the `needles` array, in the `haystack` string. If any strings from
the `needles` array are found within the `haystack` string, `findNeedles` will
count the number of occurrences and print them as an output. The `findNeedles`
function requires two input parameters:

| Required Input | Data Type    | Expected Parameters                             |
| -------------- | ------------ | ----------------------------------------------- |
| `haystack`     | String       | String                                          |
| `needles`      | String Array | Array of strings, no greater than five elements |

The `findNeedles` function will iterate through the `haystack` string and search
for each string provided by `needles`. All strings from `needles` will be
separated and placed into an array called `words`. Strings are separated by the
following escape sequences:

-   `‘ ‘` (space)
-   `\"` (double quote)
-   `\'` (single quote)
-   `\t` (horizontal tab)
-   `\n` (linefeed)
-   `\b` (backspace)
-   `\f` (formfeed)
-   `\r` (carriage return)

If the first string from `words` is not found in `haystack`, it will then look
for the next word, and so on. The `findNeedles` function is both case and
character sensitive, which means the string in `words` and `haystack` must be
the same case and lack punctuation marks. For example, “ONE” would not match
with “one” and “one!” would not match with “one”.

???+ tip Both the `haystack` string and `needles` array are needed for the
`findNeedles` function to work properly. If either of these are missing, the
program will either give a blank output or a "cannot find symbol" error.

####Example Input 1

```java linenums="1"
String haystack = "one two five seven";
String[] needles = new String[]{"one", "two", "three", "four"};
findNeedles(haystack, needles);
```

**Expected Output 1**

```
one: 1
two: 0
three: 1
four: 0
```

####Example Input 2

```java linenums="1"
String haystack = "one two three four";
String[] needles = new String[]{"one", "two", "three", "four", "five", "six"};
findNeedles(haystack, needles);
```

**Expected Output 2**

```
Too many words!
```

##Suggested Improvements to Code

Moving the following code above the first `#!java for` loop will make the
program more efficient:

```java
String[] words = haystack.split("[ \"\'\t\n\b\f\r]", 0);
```

It will no longer need to split up `haystack` into `words` every time the
program iterates through the `#!java for` loop.

Adding additional delimiter values to the `#!java haystack.split()` function,
such as commas and periods, would increase the number of possible supported
strings for `haystack`.
