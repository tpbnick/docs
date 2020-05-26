# Memory

In previous weeks, we have discussed binary.  We have also covered how each byte has an address, or identifier, so we can refer to where our variables are actually stored.  It turns out, by convention, the addresses for memory use the counting system **hexadecimal**, where there are 16 digits (0-9 and A-F).  

In binary, each digit stood for a power of 2:  

| 128 | 64 | 32 | 16 | 8 | 4 | 2 | 1 |
|-----|----|----|----|---|---|---|---|
| 1   | 1  | 1  | 1  | 1 | 1 | 1 | 1 |  

With 8 bits, we can count up to 255.  

In hexadecimal, we are able to count up to 8 bits with just 2 digits:  

```
16^1 16^0
   F    F
```  

Here, the `F` is a value of 15 in decimal, and each place is a power of 16, so the first `F` is 16^1 * 15 = 240, plus the second `F` with the value of 16^0 * 15 = 15, for a total of 255.

Here is a quick chart to compare decimal, hexadecimal, and binary:  

![number table](https://nicklyss.com/wp-content/uploads/2020/05/numbertable.png)

The RGB color system also conventionally uses hexadecimal to describe the amount of each color. For example, `000000` in hexadecimal means 0 of each red, green, and blue, for a color of black. And `FF0000` would be 255, or the highest possible, amount of red. With different values for each color, we can represent millions of different colors.  

In writing, we can also indicate a value is in hexadecimal by prefixing it with `0x`, as in `0x10`, where the value is equal to 16 in decimal, as opposed to 10.

## Pointers  

Let's create a small program that prints out a value of `n`:  

```c
#include <stdio.h>

int main(void)
{
    int n = 50;
    printf("%i\n", n);
}
```  

In our computer's memory, there are now 4 bytes somewhere that have the binary value of 50, labeled `n`.  

The bytes for the variable `n` will start at a unique address and may look something like `0x12345678`.  In C, we can actually see the address with the `&` operator, which means "get the address of this variable":  

```c
#include <stdio.h>

int main(void)
{
    int n = 50;
    printf("%p\n", &n); // notice the %p and & here
}
```

When this program was run, I received the result `0x7ffe5878a42c`.  

The address of a variable is called a **pointer**, which we can think of as a value that "points" to a location in the memory.  The `*` operator lets us "go to" the location that a pointer is point to.  For example, we can print `*&n`, where we "go to" the address of `n` and print out the value of `n`, `50`.  

```c
#include <stdio.h>

int main(void)
{
    int n = 50;
    printf("%i\n", *&n); // notice the *&n here
}
```  
We also have to use the `*` operator (in an unfortunately confusing way) to declare a variable that we want to be a pointer:  

```c
#include <stdio.h>

int main(void)
{
   int n = 50;
   int *p = &n; // declaring the pointer variable
   printf("%p\n", p);
}
```

Here, we use int `*p` to declare a variable, `p`, that has the type of `*`, a pointer, to a value of type `int`, an integer. Then, we can print its value (something like `0x12345678`), or print the value at its location with `printf("%i\n", *p);`.

In our computer’s memory, the variables might look like this (each square representing a byte of memory):  

![memory](https://cs50.harvard.edu/x/2020/notes/4/p.png)

We have a pointer, `p`, with the address of some variable.  

We can abstract away the actual value of the addresses now, since they’ll be different as we declare variables in our programs, and simply think of `p` as “pointing at” some value:

![pointing](https://cs50.harvard.edu/x/2020/notes/4/pointing.png)

An easier way to look at this is if we have a mailbox labeled "123", with the number "50" inside it.  The mailbox would be `int n`, since it stores an integer. We might have another mailbox with the address “456”, inside of which is the value “123”, which is the address of our other mailbox. This would be `int *p`, since it’s a pointer to an integer.  

## string  

Let's use a variable `string s` for a name like `EMMA` for an example.  We should be able to access each character in `EMMA` with `s[0] - s[4]`:  

![array](https://cs50.harvard.edu/x/2020/notes/4/s_array.png)  

It actually turns out that each character is stored in memory at a byte with some address, and `s` is actually just a pointer with the address of the first character:  

![pointer](https://cs50.harvard.edu/x/2020/notes/4/s_pointer.png)

Because `s` is just a pointer to the beginning, only the `\0` indicates the end of the string.  

In fact, the CS50 Library defines a `string` with `typedef char *string`, which just says that we want to name a new type, `string`, as a `char *`, or a pointer to a character.

```c
#include <stdio.h>

int main(void)
{
    char *s = "EMMA"; // notice how we are no longer using string, we are using char *s
    printf("%s\n", s);
}
```  

This allows us to drop the cs50 library.