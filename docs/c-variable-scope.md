# Variables and Scope

## Variable Scope

**Scope** is a characteristic of a variable that defines from which functions that variable may be accessed.  There are two primary scopes in C:  

* **Local Variables** can only be accessed within the functions in which they are created.  
* **Global Variables** can be accessed by any funtion in the program.  These are declared outside of all functions.  

So far in the CS50 course, we have almost always been working with local variables.  

```c
	int main(void)
	{
		int result = triple(5);
	}

	int triple(int x)
	{
		return x * 3;
	}
```
Here, `x` is **local** to the function `#!c triple()`.  No other function can refer to that variable, not even `#!c main()`.  `#!c result` is **local** to `#!c main()`.  

Global variables exist too.  If a variable is declared outside of all functions, **any** function may refer to it.  

```c
	#include <stdio.h>

	float global = 0.5050;  // variable is named global for ease of explanation

	int main(void)
	{
		triple();
		printf("%f\n", global); // global is referred to here inside a function
	}

	void triple(void)
	{
		global *= 3;
	}
```  

## Why do local and global distinctions matter?  

For the most part, local variables in C are **passed by value** in function calls.  

When a variable is passed by value, the **callee** (the function receiving the variable) receives a copy of the passed variable, not the variable itself.  

That means that the variable in the **caller** (the function making the function call) is unchanged unless overwritten.  

For example, the following has no effect on `#!c foo`:  

```c
	int main(void)
	{
		int foo = 4;
		triple(foo);
	}

	int triple(int x)
	{
		return x *= 3;
	}
```  
The following code **does** effect `#!c foo` by overwritting it:  

```c
		int main(void)
	{
		int foo = 4;
		foo = triple(foo); // the call for triple here overwrites foo after the function call
	}

	int triple(int x)
	{
		return x *= 3;
	}
```
Things can get particularly insidious if the same variable name appears in multiple functions, which is perfectly ok as long as the variables exist in different scopes.  For example:  

```c
	int increment(int x);

	int main(void)
	{
		int x = 1; // x(m) - m is local to main
		int y;
		y = increment(x); // x(m)
		printf("x is %i, y is %i\n", x, y); // x(m)
	}

	int increment(int x) // x(i) - i is local to increment
	{
		x++; // x(i)
		return x; // x(i)
	}
```

The above has the variable `#!c x` stored locally in both `#!c int main(void)` and `#!c int increment(int x)`.  

The output of the program above would be "x is 1, y is 2".  