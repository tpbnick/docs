# Algorithms

## Searching  

In computer science, a search algorithm is any algorithm which solves the search problem, namely, to retrieve information stored within some data structure, or calculates in the search space of a problem domain, either with discrete or continuous values.  

For now, we are going to go over two different types of searches:  

1. **Linear Search**  
2. **Binary Search**  

For the following examples, we are going to be using a row of lockers with numbers inside (an array) and we will look through them to find something, while returning a boolean (`true` or `false`) as a result.

A **linear search** is where we move in a line (usually start to end or end to start).  

Now lets look through the lockers to find one with the number 50 inside.  Some pseudocode for linear search could be written as:  

```
For i from 0 to n–1  // from start (0) to end (n-1)
    If i'th element is 50
        Return true  // if the i'th element is 50 - return true
Return false // if not 50, return false
```
A **binary search** is where we start in the middle and move left or right, depending on what we're looking for.  

Some pseudocode for binary search could be written as:  

```
If no items
    Return false
If middle item is 50
    Return true
Else if 50 < middle item
    Search left half
Else if 50 > middle item
    Search right half
```

## Big O  

Computer scientists have created a way to describe algorithms (how well it is designed), and it's generally called **big O**.  

![Running Time](https://nicklyss.com/wp-content/uploads/2020/05/running_time.png)  

The more formal way to describe this is with big O notation, which we can think of as “on the order of”. For example, if our algorithm is linear search, it will take approximately O(*n*) steps, “on the order of *n*”. In fact, even an algorithm that looks at two items at a time and takes *n*/2 steps has O(*n*). This is because, as n gets bigger and bigger, only the largest term, *n*, matters.  

There are some common running times (how many seconds does it take, how many steps does it take, etc.):  

* O(*n*<sup>2</sup>)
* O(*n* log *n*)
* O(*n*) (linear search)
* O(log *n*) (binary search)
* O(1)  

Computer scientists might also use big Ω, big Omega notation, which is the lower bound of number of steps for our algorithm. (Big *O* is the upper bound of number of steps, or the worst case, and typically what we care about more.) With linear search, for example, the worst case is *n* steps, but the best case is 1 step since our item might happen to be the first item we check. The best case for binary search, too, is 1 since our item might be in the middle of the array.  

And we have a similar set of the most common big Ω running times:

* Ω(n2)
* Ω(n log n)
* Ω(n) (counting the number of items)
* Ω(log n)
* Ω(1) (linear search, binary search)  

## Linear Search  

Now let's create a program to better visualize a lienar search:  

``` c
#include <cs50.h>
#include <stdio.h>

int main(void)
{
	int numbers[6] = { 4, 8, 15, 16, 23, 42};

	for (int i = 0; i < 6; i++)
	{
		if (numbers[i] == 50)
		{
			printf("Found\n");
			return 0;
		}
	}
	printf("Not found\n");
	return 1;
}
```
Here we initialize an array with some values, and we check the items in the array one at a time, in order.  

And in each case, depending on whether the value was found or not, we can return an exit code of either 0 (for success) or 1 (for failure).  

We can do the same for names:  

``` c
#include <cs50.h>
#include <stdio.h>
#include <string.h>

int main(void)
{
    string names[4] = {"EMMA", "RODRIGO", "BRIAN", "DAVID"}; 

    for (int i = 0; i < 4; i++)
    {
        if (strcmp(names[i], "EMMA") == 0) // emma is the name we're looking for. note the use of strcmp
        {
            printf("Found\n");
            return 0;
        }
    }
    printf("Not found\n");
    return 1;
}
```

We can’t compare strings directly, since they’re not a simple data type but rather an array of many characters, and we need to compare them differently. Luckily, the `string` library has a `strcmp` function which compares strings for us and returns `0` if they’re the same, so we can use that.  

Now lets implement a phone book with the same ideas:  

``` c
#include <stdio.h>
#include <string.h>

int main(void)
{
    string names[4] = {"EMMA", "RODRIGO", "BRIAN", "DAVID"};
    string numbers[4] = {"617–555–0100", "617–555–0101", "617–555–0102", "617–555–0103"};

    for (int i = 0; i < 4; i++)
    {
        if (strcmp(names[i], "EMMA") == 0) // emma's phone number is what we're looking for
        {
            printf("Found %s\n", numbers[i]);
            return 0;
        }
    }
    printf("Not found\n");
    return 1;
}
```  
Now, if the name at a certain index in the `names` array matches who we’re looking for, we’ll return the phone number in the `numbers` array, at the same index. But that means we need to particularly careful to make sure that each number corresponds to the name at each index, especially if we add or remove names and numbers.

Let's improve the above code using our own custom data type!  

## Structs  

We can make our own custom data types called **structs**: 

``` c
#include <cs50.h>
#include <stdio.h>
#include <string.h>

typedef struct
{
    string name;
    string number;
}
person; // we are encapsulating both the strings name and number inside our struct "person"

int main(void)
{
    person people[4];

    people[0].name = "EMMA";
    people[0].number = "617–555–0100";

    people[1].name = "RODRIGO";
    people[1].number = "617–555–0101";

    people[2].name = "BRIAN";
    people[2].number = "617–555–0102";

    people[3].name = "DAVID";
    people[3].number = "617–555–0103";

    // Search for EMMA
    for (int i = 0; i < 4; i++)
    {
        if (strcmp(people[i].name, "EMMA") == 0)
        {
            printf("Found %s\n", people[i].number);
            return 0;
        }
    }
    printf("Not found\n");
    return 1;
}
``` 
We can think of structs as containers, inside of which are multiple other data types.  

Here, we create our own type with a struct called `person`, which will have a `string` called `name` and a `string` called `number`. Then, we can create an array of these struct types and initialize the values inside each of them, using a new syntax, `.`, to access the properties of each `person`.  

In our loop, we can now be more certain that the `number` corresponds to the `name` since they are from the same `person` element.  

## Sorting  

