# Data Structures  

## Pointers  

In the [memory](c-memory.md) notes, we learned about pointers, `malloc`, and other useful tools for working with memory.  

Let's review the following snipped of code:  

```c
int main(void)
{
    int *x;
    int *y;

    x = malloc(sizeof(int));

    *x = 42;
    *y = 13;
}
```  
Here, the first two lines of code in our `main` function are declaring two pointers, `x` and `y`.  Then, we allocate enough memory for an `int` with `malloc`, and stores the address returned by `malloc` into `x`.  

With `*x = 42;`, we got to the address pointed to by `x`, and stores the value of `42` into that location.  

The final line, though, is buggy since we don't know what the value of `y` is, since we never set a value for it.  Instead , we can write:  

```c
y = x;
*y = 13;
```  

For a more fun way to understand the above, take a look at the short clip, [Pointer Fun with Blinky](https://www.youtube.com/watch?v=3uLKjb973HU).  

## Resizing arrays  

In the [arrays](c-arrays.md) notes, we learned about arrays, where we could store the same kind of value in a list side-by-side.  But we need to declare the size of arrays when we create them, and when we want to increase the size of the array, the memory surrounding it might be taken up by some other data.  

One solution might be to allocate more memory in a larger area that's free, and move our array there, where it has more space.  This sounds like it could work, but we'll need to copy our array, which becomes an operation with running time of *O(n)*, since we need to copy each of *n* elements in an array.  

We might write a program like the following, to do this in code:  

??? example "copy array code"
    ```c linenums="1"
	#include <stdio.h>
	#include <stdlib.h>

	int main(void)
	{
	    // Here, we allocate enough memory to fit three integers, and our variable
	    // list will point to the first integer.
	    int *list = malloc(3 * sizeof(int));
	    // We should check that we allocated memory correctly, since malloc might
	    // fail to get us enough free memory.
	    if (list == NULL)
	    {
	        return 1;
	    }

	    // With this syntax, the compiler will do pointer arithmetic for us, and
	    // calculate the byte in memory that list[0], list[1], and list[2] maps to,
	    // since integers are 4 bytes large.
	    list[0] = 1;
	    list[1] = 2;
	    list[2] = 3;

	    // Now, if we want to resize our array to fit 4 integers, we'll try to allocate
	    // enough memory for them, and temporarily use tmp to point to the first:
	    int *tmp = malloc(4 * sizeof(int));
	    if (tmp == NULL)
	    {
	        return 1;
	    }

	    // Now, we copy integers from the old array into the new array ...
	    for (int i = 0; i < 3; i++)
	    {
	        tmp[i] = list[i];
	    }

	    // ... and add the fourth integer:
	    tmp[3] = 4;

	    // We should free the original memory for list, which is why we need a
	    // temporary variable to point to the new array ...
	    free(list);

	    // ... and now we can set our list variable to point to the new array that
	    // tmp points to:
	    list = tmp;

	    // Now, we can print the new array:
	    for (int i = 0; i < 4; i++)
	    {
	        printf("%i\n", list[i]);
	    }

	    // And finally, free the memory for the new array.
	    free(list);
	}
    ```  
It turns out that there’s actually a helpful function, `realloc`, which will reallocate some memory: 

??? example "`realloc` example"
    ```c linenums="1"
	#include <stdio.h>
	#include <stdlib.h>

	int main(void)
	{
	    int *list = malloc(3 * sizeof(int));
	    if (list == NULL)
	    {
	        return 1;
	    }

	    list[0] = 1;
	    list[1] = 2;
	    list[2] = 3;

	    // Here, we give realloc our original array that list points to, and it will
	    // return a new address for a new array, with the old data copied over:
	    int *tmp = realloc(list, 4 * sizeof(int));
	    if (tmp == NULL)
	    {
	        return 1;
	    }
	    // Now, all we need to do is remember the location of the new array:
	    list = tmp;

	    list[3] = 4;

	    for (int i = 0; i < 4; i++)
	    {
	        printf("%i\n", list[i]);
	    }

	    free(list);
	}
    ```  
## Data Structures  

**Data structures** are programming constructs that allow us to store information in different layouts in our computer’s memory.  

To build a data structure, we’ll need some tools we’ve seen:  

* `struct` to create custom data types

* `.` to access properties in structure

* `*` to go to an address in memory pointed to by a pointer

## Linked Lists  

With a **linked list**, we can store a list of values that can easily be grown by storing values in different parts of memory:  

![linked-list](https://nicklyss.com/wp-content/uploads/2020/06/linked_list.png)  

* This is different than an array since our values are no longer next to one another in memory.  

![linked-list-with-addresses](https://nicklyss.com/wp-content/uploads/2020/06/linked_list_with_addresses.png)  

* This uses two chunks of memory, where the second chunk is used to point at the next chunk of memory. By the way, `NUL` refers to `\0`, a character that ends a string, and `NULL` refers to an address of all zeros, or a null pointer that we can think of as pointing nowhere.  These chunks are linked by the pointers in the second chunk of memory.  

Unlike with arrays, we no longer randomly access elements in a linked list. For example, we can no longer access the 5th element of the list by calculating where it is, in constant time. (Since we know arrays store elements back-to-back, we can add 1, or 4, or the size of our element, to calculate addresses.) Instead, we have to follow each element’s pointer, one at a time. And we need to allocate twice as much memory as we needed before for each element.  

In code, we might create our own struct called `node` (like a node from a graph in mathematics), and we need to store both an `int` and a pointer to the next `node` called `next`.  

```c
typedef struct node
{
    int number;
    struct node *next;
}
node; // this is the nickname for struct node
```  

* We start this struct with `typedef struct node` so that we can refer to a `node` inside our struct.  

We can build a linked list in code starting with our struct.  First, we'll want to remember an empty list, so we can use the null pointer: `node *list = NULL;`.  

To add an element, first we'll need to allocate some memory for a node, and set its values:  

```c
node *n = malloc(sizeof(node));
// We want to make sure malloc succeeded in getting memory for us:
if (n != NULL)
{
    // This (->) is equivalent to (*n).number, where we first go to the node pointed
    // to by n, and then set the number property. In C, we can also use this
    // arrow notation:
    n->number = 2;
    // Then we need to store a pointer to the next node in our list, but the
    // new node won't point to anything (for now):
    n->next = NULL;
}
```  
Now our list can point to this node: `list = n;`:  

![list-with-one-node](https://nicklyss.com/wp-content/uploads/2020/06/list_with_one_node.png)  

To add to our lsit, we'll create a new node the same way, perhaps with the value 4.  But now we need to update the pointer in our first node to point to it.  

since our `list` pointer points only to the first node (and we can't be sure that the list only has one node), we need to "follow the breadcrumbs" and follow each node's next pointer:  

```c
// Create temporary pointer to what list is pointing to
node *tmp = list;
// As long as the node has a next pointer ...
while (tmp->next != NULL)
{
    // ... set the temporary to the next node
    tmp = tmp->next;
}
// Now, tmp points to the last node in our list, and we can update its next
// pointer to point to our new node.
```  

If we want to insert a node to the front of our linked list, we would need to carefully update our node to point to the one following it, before updating the list.  Otherwise, we'll lose the rest of our list:  
```c
// Here, we're inserting a node into the front of the list, so we want its
// next pointer to point to the original list, before pointing the list to
// n:
n->next = list;
list = n;
``` 

And to insert a node in the middle of our list, we can go through the list, following each element one at a time, comparing its values, and changing the `next` pointers carefully as well.  

We can combine all of our snippets of code into a complete program:  

??? example "node example"
    ```c linenums="1"
	#include <stdio.h>
	#include <stdlib.h>

	// Represents a node
	typedef struct node
	{
	    int number;
	    struct node *next;
	}
	node;

	int main(void)
	{
	    // List of size 0, initially not pointing to anything
	    node *list = NULL;

	    // Add number to list
	    node *n = malloc(sizeof(node));
	    if (n == NULL)
	    {
	        return 1;
	    }
	    n->number = 1;
	    n->next = NULL;
	    // We create our first node, store the value 1 in it, and leave the next
	    // pointer to point to nothing. Then, our list variable can point to it.
	    list = n;

	    // Add number to list
	    n = malloc(sizeof(node));
	    if (n == NULL)
	    {
	        return 1;
	    }
	    n->number = 2;
	    n->next = NULL;
	    // Now, we go our first node that list points to, and sets the next pointer
	    // on it to point to our new node, adding it to the end of the list:
	    list->next = n;

	    // Add number to list
	    n = malloc(sizeof(node));
	    if (n == NULL)
	    {
	        return 1;
	    }
	    n->number = 3;
	    n->next = NULL;
	    // We can follow multiple nodes with this syntax, using the next pointer
	    // over and over, to add our third new node to the end of the list:
	    list->next->next = n;
	    // Normally, though, we would want a loop and a temporary variable to add
	    // a new node to our list.

	    // Print list
	    // Here we can iterate over all the nodes in our list with a temporary
	    // variable. First, we have a temporary pointer, tmp, that points to the
	    // list. Then, our condition for continuing is that tmp is not NULL, and
	    // finally, we update tmp to the next pointer of itself.
	    for (node *tmp = list; tmp != NULL; tmp = tmp->next)
	    {
	        // Within the node, we'll just print the number stored:
	        printf("%i\n", tmp->number);
	    }

	    // Free list
	    // Since we're freeing each node as we go along, we'll use a while loop
	    // and follow each node's next pointer before freeing it, but we'll see
	    // this in more detail in Problem Set 5.
	    while (list != NULL)
	    {
	        node *tmp = list->next;
	        free(list);
	        list = tmp;
	    }
	}
    ``` 

## More data structures  

A **tree** is another data structure where each node points to two other nodes, one to the left (with a smaller value) and one to the right (with a larger value):  

![binary-search-tree](https://nicklyss.com/wp-content/uploads/2020/06/binary_search_tree.png)  