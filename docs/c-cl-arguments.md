# Command Line Arugments Overview

## Command Line Arguments

So far, all of our programs have begun pretty much the same way:

```c
	int main(void)
	{
```

Since we've been collecting user input through in-program prompts, we haven't
needed to modify this declaration of `#!c main`.

If we want the user to provide data to our program before the program starts
running, we need a new form.

To collect so called **command-line arguments** from the user, declare main as:

```c
	int main(int argc, string argv[]) // the first parameter (argument/input) is an integer argc and the second is an array of strings.
	{
```

These two special arguments enable you to know what data the user provided at
the command line and how much data they provided.

**`#!c argc`(argument count)**

-   This integer-type variable will store the **number** of command-line
    arguments the user typed when the program was executed.

| command            | argc |
| ------------------ | ---- |
| ./greedy           | 1    |
| ./greedy 1024 cs50 | 3    |

-   (greedy is the name of the program in the above example)

**`#!c argv` (argument vector)**

-   This array of strings stores, one string per element, the actual text the
    user typed at the command-line when the program was executed.

-   The first element of `#!c argv` is always found at `#!c argv[0]` (first
    index of the `#!c argv` array). The last element of `#!c argv` is always
    found at `#!c argv[argc-1]` (this is because the number of elements that
    exist in the array are `#!c argc` number of elements).

Let's assume the user executes the greedy program as follows:

`./greedy 1024 cs50`

| argv indices  | argv contents                              |
| ------------- | ------------------------------------------ |
| `#!c argv[0]` | "./greedy"                                 |
| `#!c argv[1]` | "1024" (stored as a string NOT an integer) |
| `#!c argv[2]` | "cs50"                                     |
| `#!c argv[3]` | ??? (often leads to segmentation fault)    |
