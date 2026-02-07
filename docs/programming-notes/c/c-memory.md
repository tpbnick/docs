# Memory

In previous weeks, we have discussed binary. We have also covered how each byte
has an address, or identifier, so we can refer to where our variables are
actually stored. It turns out, by convention, the addresses for memory use the
counting system **hexadecimal**, where there are 16 digits (0-9 and A-F).

In binary (_base-2_), each digit stood for a power of 2:

| 128 | 64  | 32  | 16  | 8   | 4   | 2   | 1   |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 1   | 1   | 1   | 1   | 1   | 1   | 1   | 1   |

With 8 bits, we can count up to 255.

Hexadecimal (_base-16_) is a much more concise way to express the data on a
computer's system. Hexadecimal is displayed as follows:
`0 1 2 3 4 5 6 7 8 9 A B C D E F`.

Just like binary has place values (1, 2, 4, 8...) and decimal has place values
(1, 10, 100, 1000...), hexadecimal does too. Hexadecimal's place values are by
the power of 16. For example, if we were to look at the hex number 0x397, it
would be as follows:

|     | 256 (16<sup>2</sup>) | 16 (16<sup>1</sup>) | 1 (16<sup>0</sup>) |
| --- | -------------------- | ------------------- | ------------------ |
| 0x  | 3                    | 9                   | 7                  |

So the above number would be (3 x 256) + (9 x 16) + 7 = 919.

Another example that uses alphanumeric hex characters:

|     | 256 (16<sup>2</sup>) | 16 (16<sup>1</sup>) | 1 (16<sup>0</sup>) |
| --- | -------------------- | ------------------- | ------------------ |
| 0x  | A                    | D                   | C                  |

This would look like (10 x 256) + (13 x 16) + 12 = 2780 in decimal form.

Here, the `F` is a value of 15 in decimal, and each place is a power of 16, so
the first `F` is 16^1 _ 15 = 240, plus the second `F` with the value of 16^0 _
15 = 15, for a total of 255.

Here is a quick chart to compare decimal, hexadecimal, and binary:

![!number table](https://cdn.nickplatt.dev/Docs/numbertable.png)

The RGB color system also conventionally uses hexadecimal to describe the amount
of each color. For example, `000000` in hexadecimal means 0 of each red, green,
and blue, for a color of black. And `FF0000` would be 255, or the highest
possible, amount of red. With different values for each color, we can represent
millions of different colors.

In writing, we can also indicate a value is in hexadecimal by prefixing it with
`0x`, as in `0x10`, where the value is equal to 16 in decimal, as opposed to 10.
`0x` means nothing to a computer, this is simply to help humans see when
hexadecimal will be used.

## Pointers

**Pointers** provide an alternative way to pass data between functions.

- Up until this point we have passed all data by value, which means we have only
  passed a copy of that data.

If we use pointers instead, we have the power to pass the actual variable
itself. That means that if a change is made in one function, it can impact what
happens in other functions.

Let's create a small program that prints out a value of `n`:

```c linenums="1"
#include <stdio.h>

int main(void)
{
    int n = 50;
    printf("%i\n", n);
}
```

In our computer's memory, there are now 4 bytes somewhere that have the binary
value of 50, labeled `n`.

The bytes for the variable `n` will start at a unique address and may look
something like `0x12345678`. In C, we can actually see the address with the `&`
operator, which means "get the address of this variable":

```c linenums="1"
#include <stdio.h>

int main(void)
{
    int n = 50;
    printf("%p\n", &n); // notice the %p and & here
}
```

When this program was run, I received the result `0x7ffe5878a42c`.

The address of a variable is called a **pointer**, which we can think of as a
value that "points" to a location in the memory. The `*` operator lets us "go
to" the location that a pointer is point to. For example, we can print `*&n`,
where we "go to" the address of `n` and print out the value of `n`, `50`.

The `*` is known as the **deference operator**. It "goes to the reference" and
access that data at that location, allowing you to manipulate it at will.

```c linenums="1"
#include <stdio.h>

int main(void)
{
    int n = 50;
    printf("%i\n", *&n); // notice the *&n here
}
```

We also have to use the `*` operator (in an unfortunately confusing way) to
declare a variable that we want to be a pointer:

```c linenums="1"
#include <stdio.h>

int main(void)
{
   int n = 50;
   int *p = &n; // declaring the pointer variable
   printf("%p\n", p);
}
```

Here, we use int `*p` to declare a variable, `p`, that has the type of `*`, a
pointer, to a value of type `int`, an integer. Then, we can print its value
(something like `0x12345678`), or print the value at its location with
`printf("%i\n", *p);`.

In our computer’s memory, the variables might look like this (each square
representing a byte of memory):

![!memory](https://cdn.nickplatt.dev/Docs/memory.png)

We have a pointer, `p`, with the address of some variable.

We can abstract away the actual value of the addresses now, since they’ll be
different as we declare variables in our programs, and simply think of `p` as
“pointing at” some value:

![!pointing](https://cdn.nickplatt.dev/Docs/pointing.png)

An easier way to look at this is if we have a mailbox labeled "123", with the
number "50" inside it. The mailbox would be `int n`, since it stores an integer.
We might have another mailbox with the address “456”, inside of which is the
value “123”, which is the address of our other mailbox. This would be `int *p`,
since it’s a pointer to an integer. A **pointer**, then, is a data item whose

- _value_ is a memory address

- _type_ describes the data located at that memory address

The simplest pointer available to us in C is the NULL pointer. As you might
expect, this pointer points to nothing (a fact which can actually come in
handy). When you create a pointer and you don't set its value immediately, you
should **always** set the value of the pointer to NULL.

## string

Let's use a variable `string s` for a name like `EMMA` for an example. We should
be able to access each character in `EMMA` with `s[0] - s[4]`:

![!array](https://cdn.nickplatt.dev/Docs/s_array.png)

It actually turns out that each character is stored in memory at a byte with
some address, and `s` is actually just a pointer with the address of the first
character:

![!pointer](https://cdn.nickplatt.dev/Docs/s_pointer.png)

Because `s` is just a pointer to the beginning, only the `\0` indicates the end
of the string.

In fact, the CS50 Library defines a `string` with `typedef char *string`, which
just says that we want to name a new type, `string`, as a `char *`, or a pointer
to a character.

```c linenums="1"
#include <stdio.h>

int main(void)
{
    char *s = "EMMA"; // notice how we are no longer using string, we are using char *s
    printf("%s\n", s);
}
```

## Compare and Copy

Let's create a quick program to compare integers:

```c linenums="1"
#include <cs50.h>
#include <stdio.h>

int main(void)
{
    // Get two integers
    int i = get_int("i: ");
    int j = get_int("j: ");

    // Compare integers
    if (i == j)
    {
        printf("Same\n");
    }
    else
    {
        printf("Different\n");
    }
}
```

We can compile and run this, and our program works as we’d expect, with the same
values of the two integers giving us “Same” and different values “Different”.

Now let's try the same thing, but using strings instead of integers:

```c linenums="1"
#include <cs50.h>
#include <stdio.h>

int main(void)
{
    // Get two strings
    string s = get_string("s: ");
    string t = get_string("t: ");

    // Compare strings' addresses
    if (s == t)
    {
        printf("Same\n");
    }
    else
    {
        printf("Different\n");
    }
}
```

If we run the above program we will see that it will give us the result
"Different" each time, even when the strings are identical. Why does this
happen? Simply, this is caused by how C stores strings in memory. When these are
compared, C looks at the addresses of the stings, not the user input data. The
strings are stored in different places of memory (pointers), which will return
different hexadecimal results when compared.

Now let's look at how we can copy strings. Let's make a simple program:

```c linenums="1"
#include <cs50.h>
#include <ctype.h>
#include <stdio.h>

int main(void)
{
    string s = get_string("s: ");

    string t = s; // copies string s to string t (but only as an address)

    t[0] = toupper(t[0]); // capitalizes string t

    // Print string twice
    printf("s: %s\n", s);
    printf("t: %s\n", t);
}
```

- We get a string `s`, and copy the value of `s` into `t`. Then, we capitalize
  the first letter in `t`.

- But when we run our program, we see that both `s` and `t` are now capitalized.

- Since we set `s` and `t` to the same values, they’re actually pointers to the
  same character, and so we capitalized the same character!

To actually make a copy of a string, we have to do a little more work:

```c linenums="1"
#include <cs50.h>
#include <ctype.h>
#include <stdio.h>
#include <string.h> // needed for strlen (string length)

int main(void)
{
    char *s = get_string("s: ");

    char *t = malloc(strlen(s) + 1); // malloc is "memory allocate" to store the copy

    for (int i = 0, n = strlen(s); i < n + 1; i++) // we need n+1 for the null character in a string
    {
        t[i] = s[i]; // copies strings
    }

    t[0] = toupper(t[0]); // capitalizes the first character of the string

    printf("s: %s\n", s);
    printf("t: %s\n", t);
}
```

- We create a new variable, `t`, of the type `char *`, with `char *t`. Now, we
  want to point it to a new chunk of memory that’s large enough to store the
  copy of the string. With `malloc`, we can allocate some number of bytes in
  memory (that aren’t already used to store other values), and we pass in the
  number of bytes we’d like. We already know the length of `s`, so we add 1 to
  that for the terminating null character. So, our final line of code is
  `char *t = malloc(strlen(s) + 1);`.

- Then, we copy each character, one at a time, and now we can capitalize just
  the first letter of `t`. And we use `i < n + 1`, since we actually want to go
  up to `n`, to ensure we copy the terminating character in the string.

- We can actually also use the `strcpy` library function with `strcpy(t, s)`
  instead of our loop, to copy the string `s` into `t`. To be clear, the concept
  of a “string” is from the C language and well-supported; the only training
  wheels from CS50 are the type string instead of `char *`, and the `get_string`
  function.

If we didn’t copy the null terminating character, `\0`, and tried to print out
our string `t`, printf will continue and print out the unknown, or garbage,
values that we have in memory, until it happens to reach a `\0`, or crashes
entirely, since our program might end up trying to read memory that doesn’t
belong to it!

## valgrind

It turns out that, after we’re done with memory that we’ve allocated with
`malloc`, we should call `free` (as in `free(t)`), which tells our computer that
those bytes are no longer useful to our program, so those bytes in memory can be
reused again.

If we kept running our program and allocating memory with `malloc`, but never
freed the memory after we were done using it, we would have a **memory leak**,
which will slow down our computer and use up more and more memory until our
computer runs out.

`valgrind` is a command-line tool that we can use to run our program and see if
it has any memory leaks. We can run valgrind on our program above with
`help50 valgrind ./*program*` and see, from the error message, that line 10, we
allocated memory that we never freed (or “lost”).

So at the end, we can add a line `free(t)`, which won’t change how our program
runs, but no errors from valgrind.

Let's look at an example program provided from valgrind's official
documentation:

```c linenums="1"
// http://valgrind.org/docs/manual/quick-start.html#quick-start.prepare

#include <stdlib.h>

void f(void)
{
    int *x = malloc(10 * sizeof(int));
    x[10] = 0; // this int [10] is not in the correct range (0-9) and will result in a buffer overflow
}

int main(void)
{
    f();
    return 0;
}
```

- The function `f` allocates enough memory for 10 integers, and stores the
  address in a pointer called `x`. Then we try to set the 11th value of `x` with
  `x[10]` to `0`, which goes past the array of memory we’ve allocated for our
  program. This is called **buffer overflow**, where we go past the boundaries
  of our buffer, or array, and into unknown memory.

- valgrind will also tell us there’s an “Invalid write of size 4” for line 8,
  where we are indeed trying to change the value of an integer (of size 4
  bytes).

## Swap

We have two colored drinks, purple and green, each of which is in a cup. We want
to swap the drinks between the two cups, but we can’t do that without a third
cup (temporary variable) to pour one of the drink into first.

Now, let’s say we wanted to swap the values of two integers.

```c linenums="1"
void swap(int a, int b)
{
    int tmp = a;
    a = b;
    b = tmp;
}
```

- With a third variable to use as temporary storage space, we can do this pretty
  easily, by putting `a` into `tmp`, and then `b` to `a`, and finally the
  original value of `a`, now in `tmp`, into `b`.

But, if we tried to use that function in a program, we don’t see any changes:

```c linenums="1"
#include <stdio.h>

void swap(int a, int b);

int main(void)
{
    int x = 1;
    int y = 2;

    printf("x is %i, y is %i\n", x, y);
    swap(x, y);
    printf("x is %i, y is %i\n", x, y);
}

void swap(int a, int b)
{
    int tmp = a;
    a = b;
    b = tmp;
}
```

This does not work because the `swap` function successfully swaps `int a` and
`int b`, but these are simply copies of `int x` and `int y`. When `x` and `y`
are printed, the copies used by the `swap` funciton do not alter the actual `x`
and `y` integers in the `main` function.

## Memory Layout

Within our computer’s memory, the different types of data that need to be stored
for our program are organized into different sections:

![!memory layout](https://cdn.nickplatt.dev/Docs/memory_layout.png)

- The ** _machine code_ ** section is our compiled program’s binary code. When
  we run our program, that code is loaded into the “top” of memory.

- ** _Globals_ ** are global variables we declare in our program or other shared
  variables that our entire program can access.

- The ** _heap_ ** section is an empty area where `malloc` can get free memory
  from, for our program to use.

- The ** _stack_ ** section is used by functions in our program as they are
  called. For example, our `main` function is at the very bottom of the stack,
  and has the local variables `x` and `y`. The `swap` function, when it’s
  called, has its own frame, or slice, of memory that’s on top of `main`’s, with
  the local variables `a`, `b`, and `tmp`:
  ![!stack](https://cdn.nickplatt.dev/Docs/stack.png)

- Once the function `swap` returns, the memory it was using is freed for the
  next function call, and we lose anything we did, other than the return values,
  and our program goes back to the function that called `swap`.

- So by passing in the addresses of `x` and `y` from `main` to `swap`, we can
  actually change the values of `x` and `y`:
  ![!pointers](https://cdn.nickplatt.dev/Docs/pointers.png)

By passing in the address of `x` and `y`, our `swap` function from above can
actually work:

```c linenums="1"
#include <stdio.h>

void swap(int *a, int *b); // we use * throughout to point to the real integer, not the copy

int main(void)
{
    int x = 1;
    int y = 2;

    printf("x is %i, y is %i\n", x, y);
    swap(&x, &y); // address of x and y
    printf("x is %i, y is %i\n", x, y);
}

void swap(int *a, int *b)
{
    int tmp = *a;
    *a = *b;
    *b = tmp;
}
```

- The addresses of `x` and `y` are passed in from `main` to `swap`, and we use
  the `int *a` syntax to declare that our `swap` function takes in pointers. We
  save the value of `x` to `tmp` by following the pointer `a`, and then take the
  value of `y` by following the pointer `b`, and store that to the location `a`
  is pointing to (`x`). Finally, we store the value of `tmp` to the location
  pointed to by `b` (`y`), and we’re done.

If we call `malloc` too many times, we will have a **heap overflow**, where we
end up going past our heap. Or, if we have too many functions being called, we
will have a **stack overflow**, where our stack has too many frames of memory
allocated as well. And these two types of overflow are generally known as buffer
overflows, after which our program (or entire computer) might crash.

## get_int

We can implement `get_int` ourselve with a C library function, `scanf`:

```c linenums="1"
#include <stdio.h>

int main(void)
{
    int x;
    printf("x: ");
    scanf("%i", &x);
    printf("x: %i\n", x);
}
```

- `scanf` takes a format, `%i`, so the input is “scanned” for that format, and
  the address in memory where we want that input to go. But `scanf` doesn’t have
  much error checking, so we might not get an integer.

We can try to get a string the same way:

```c linenums="1"
#include <stdio.h>

int main(void)
{
    char *s = NULL;
    printf("s: ");
    scanf("%s", s);
    printf("s: %s\n", s);
}
```

- But we haven’t actually allocated any memory for `s` (`s` is `NULL`, or not
  pointing to anything), so we might want to call `char s[5]` to allocate an
  array of 5 characters for our string. Then, `s` will be treated as a pointer
  in `scanf` and `printf`.

- Now, if the user types in a string of length 4 or less, our program will work
  safely. But if the user types in a longer string, `scanf` might be trying to
  write past the end of our array into unknown memory, causing our program to
  crash.

## File Pointers

The ability to read data from and write data to files is the primary means of
storing **persistent data**, data that does not disappear when your program
stops running.

The abstraction of files that C provides is implemented in a data structure
known as a `FILE`. Almost universally when working with files, we will be using
pointers to them, `FILE*`.

Some of the most common file input/output (I/O) functions that we will be
working with are: `fopen()`, `fclose()`, `fgetc()`, `fputc()`, `fread()`, and
`fwrite()`.

- **`fopen()`** opens a file and returns a file pointer to it. It always checks
  the return value to make sure you don't get back NULL.

- **`fclose()`** closes the file pointed to by the given file pointer.

- **`fgetc()`** reads and returns the next character from the file pointed to.
  Note: the operation of the file pointer passed in as a parameter must be "r"
  for read, or you will have an error.

- **`fputc()`** writes or appends the specified character to the pointed-to
  file. Note: the operation of the file pointer must be "w" for write or "a" for
  append, or you will have an error.

- **`fread()`** reads `<qty>` units of size `<size>` from the file pointed to
  and stores them in memory in a buffer (usually an array) pointed to by
  `<buffer>`. Note: the operation of the file pointer passed in as a parameter
  must be "r" for read, or you will have an error.

- **`fwrite()`** writes `<qty>` units of size `<size>` to the file pointed to by
  reading them from a buffer (usually an array) pointed to by `<buffer>`. Note:
  the operation of the file pointer passed in as a parameter must be "w" for
  write or "a" for append, or you will suffer an error.

With the ability to use pointers, we can also open files:

```c linenums="1"
#include <cs50.h>
#include <stdio.h>
#include <string.h>

int main(void)
{
    // Open file
    FILE *file = fopen("phonebook.csv", "a");

    // Get strings from user
    char *name = get_string("Name: ");
    char *number = get_string("Number: ");

    // Print (write) strings to file
    fprintf(file, "%s,%s\n", name, number);

    // Close file
    fclose(file);
}
```

- `fopen` is a new function we can use to open a file. It will return a pointer
  to a new type, `FILE`, that we can read from and write to. The first argument
  is the name of the file, and the second argument is the mode we want to open
  the file in (`r` for read, `w` for write, and `a` for append, or adding to).

- After we get some strings, we can use `fprintf` to print to a file.

- Finally, we close the file with `fclose`.

Now we can create our own CSV files, files of comma-separated values (like a
mini-spreadsheet), programmatically.

## JPEG

We can also write a program that opens a file and tells us if it’s a JPEG
(image) file:

```c linenums="1"
#include <stdio.h>

int main(int argc, char *argv[])
{
    // Check usage
    if (argc != 2)
    {
        return 1;
    }

    // Open file
    FILE *file = fopen(argv[1], "r");
    if (!file)
    {
        return 1;
    }

    // Read first three bytes
    unsigned char bytes[3];
    fread(bytes, 3, 1, file);

    // Check first three bytes
    if (bytes[0] == 0xff && bytes[1] == 0xd8 && bytes[2] == 0xff)
    {
        printf("Maybe\n");
    }
    else
    {
        printf("No\n");
    }

    // Close file
    fclose(file);
}
```

- Now, if we run this program with `./jpeg brian.jpg`, our program will try to
  open the file we specify (checking that we indeed get a non-NULL file back),
  and read the first three bytes from the file with `fread`.

- We can compare the first three bytes (in hexadecimal) to the three bytes
  required to begin a JPEG file. If they’re the same, then our file is likely to
  be a JPEG file (though, other types of files may still begin with those
  bytes). But if they’re not the same, we know it’s definitely not a JPEG file.

We can use these abilities to read and write files, in particular images, and
modify them by changing the bytes in them, in this week’s problem set!
