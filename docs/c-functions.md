# Functions

## What are functions?  

C and nearly all languages developed since allow us to write functions, sometimes also known as procedures, methods, or subroutines.  

A function is a *black box* with a set of 0+ inputs and 1 output.  

For example:
```c
add(a, b, c)
// or
mult(a, b)
```
The `#!c add` function takes the input from `#!c a, b, c` and will have a single output.  
The `#!c mult` function takes the input from `#!c a, b` and will have a single output.  

Why call it a *black box*?  
If we aren't writing the functions ourselves, we don't need to know the underlying implementation.  

`#!c mult(a, b):` can be implemented in many different ways, including:

* output a * b

Or

* set counter to 0
* repeat b times (ex. 3)
	- add a to counter (ex. 5)
* output counter (counter will add 3 five times with the same output as a * b)  

That's part of the contract of using functions.  The behavior is typically predictable based on the name.  That's why most functions have clear, obvious(ish) names, and are well-documented.  

## Why us functions?  

**Organization**  

* Functions help break up a complicated problem into more manageable subparts.  

**Simplification**  

* Smaller components tend to be easier to design, implement, and debug.  

**Reusability**  

* Functions can be recycled; you only need to write them once, but can use them as often as you need!  

## Function Declarations  

The first step to creating a function is to declare it.  This gives the compiler a heads-up that a user-written function appears in the code.  

Function declarations should always go atop your code, before you begin writing the `#!c main()`. 

There is a standard form that every function declaration follows:  

``` c
return-type name(argument-list);
```  
The `#!c return-type` is what kind of variable the function will output.  
The `#!c name` is what you want to call your function.  
The `#!c argument-list` is the comma-separated set of inputs to your function, each of which has a type and a name.  

Here is an example of a function declaration for a function that would add two integers together:  

``` c
int add_two_ints(int a, int b);
```
The sum of the two integers is going to be an integer as well.  
Given what this function does, make sure to give it an appropriate name (like `#!c add_two_ints`).  
There are two inputs to this function (each of which is an integer), and we need to give a name to each of them for purposes of the function.  There's nothing important about these inputs as far as we know, so giving them a simple name is okay (`#!c a` and `#!c b`).  

Another example for floating point numbers could be:  
``` c
float mult_two_floats(float x, float y);
```  
The product of two floating point numbers is also a floating point number.  

## Function Definitions  

The second step to creating a function is to define it.  This allows for predictable behavior when the function is called with inputs.  

Let's try to define the `#!c mult_two_floats` from above.  

```c
float mult_two_floats(float x, float y);

float mult_two_floats(float x, float y)
{
	float product = x * y;
	return product;
}

```  
Or more simply:  

```c
float mult_two_floats(float x, float y);

float mult_two_floats(float x, float y)
{
	return x * y;
}
```  

Now lets define `#!c add_two_ints()` from earlier:  

```c
int add_two_ints(int a, int b);

int add_two_ints(int a, int b)
{
	int sum;		//declare variable
	sum = a + b;	//calculate the sume
	retruen sum;	//give result back
}
```  

## Function Calls  

To call a function, simply pass it appropriate arguments and assign its return value to something of the correct type.  

Here is an example with a file called `adder.c`:  

```c
// includes
#include <cs50.h>
#include <stdio.h>

// declare function prototype
int add_two_ints(int a, int b);

int main(void)
{
    // ask user for input
    int x = get_int("Give me an integer: ");
    int y = get_int("Give me another integer: ");

    // add the two numbers together via a function call
    int z = add_two_ints(x, y);

    // output the result
    printf("The sum of %i and %i is %i!\n", x, y, z);

}

int add_two_ints(int a, int b)
{
    int sum = a + b;
    return sum;
}
```  
## Function Miscellany 

Recall from our discussion of data types that functions can sometimes take no inputs.  In that case, we declare the function as having a `#!c void` argument list.  An example of this would be `#!c int main(void)`.  

Recall also that functions sometimes do not have an output.  In that case, we declare the function as having a `#!c void` return type.  

## Practice Problem  

We will declare and write a function called `#!c valid_triangle` that takes three real numbers representing the lengths of the three sides of a triangle as its arguments, and outputs either `#!c true` or `#!c false`, depending on whether those three lengths are capable of making a triangle.  

Note the following rules about triangles:

* A triangle may only have sides with positive length.  

* The sum of the lengths of any two sides of the triangle must be greater than the length of the third side.  

```c
bool valid_triangle(float x, float y, float z);

bool valid_triangle(float x, float y, float z)
{
	//check for all positive sizes
		if (x <= 0 || y <= 0 || z <= 0)
		{
			return false;
		}

		//check that the sum of any two sides is greater than the third
		if ((x + y <= z) || (x + z <= y) || (y + z <= x))
		{
            return false;	
		}

		//if both checks pass, we output true!
        return true;	
}


```  

Now lets make one that takes in user input for fun!
``` c
#include <cs50.h>
#include <stdio.h>

int main(void)
{	
	bool valid_triangle();
		float x = get_float("Give me the size of the first side of the triangle: ");
		float y = get_float("Give me the size of the second size of the triangle: ");
		float z = get_float("Give me the size of the third side of the triange: ");

		//check that all floats are positive
		if (x <= 0 || y <= 0 || z <= 0)
		{
			printf("Not a valid triangle.\n");
			return false;
		}

		//check that the sum of any two sides is greater than the third
		if ((x + y <= z) || (x + z <= y) || (y + z <= x))
		{
			printf("Not a valid triangle.\n");
            return false;	
		}

		//if both checks pass, we output true!
		printf("That is a valid triangle!\n");
        return true;	
}
```



