# Arrays

## What are Arrays?  

Arrays are a fundamental data structure, and they are extremely useful!  

We use arrays to hold values of the same type at contiguous memory locations (A way to group together data types (integers, characters, floats) in memory really close together without giving each one their own name).  

A good analogy to use for arrays is a post office:  

| **Arrays**                                                                                         | Post Office Boxes                                                                                           |
|----------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------|
| An **array** is a block of contiguous space in memory...                                           | A **mail bank** is a large space o the wall of the post office...                                           |
| ...which has been partitioned into small, identically-sized blocks of space called **elements**... | ...which has been partitioned into small, identically-sized blocks of space called **post office boxes**... |
| ...each of which can store a certain amount of **data**...                                         | ...each of which can hold a certain amount of **mail**...                                                   |
| ...all of the same data type such as **`int`** or **`char`**...                                    | ...all of a familiar type such as **letters** or **small packages**...                                      |
| ...and which can be accessed directly by an **index**.                                             | ...and which can be accessed directly by a **mailbox number**.                                              |  

In C, the elements of an array are indexed starting from 0.  

If an array consists of *n* elements, the first element is located at index 0.  The last element is located at (*n*-1).  For example, if an array has 50 elements, the first is located at index 0 and the last is located at index 49).  

C is very lenient with arrays when compiled, which can lead to unforseen errors when the program is run. "Segmentation Faults" are common if you ask the program to access memory outside the bounds of what you asked the program to give you.  

## Array Declarations  

&emsp;&emsp;`#!c type` `#!c name` `#!c [size];`

The `#!c type` is what kind of variable (data type) each element of the array will be.  
The `#!c name` is what you want to call your array.  
The `#!c size` is how many elements you would like your array to contain.  

Examples:  

&emsp;&emsp;`#!c int data[100];` -> This array, named data, will store 100 integers.  
&emsp;&emsp;`#!c float numbers[5];` -> This array, named numbers, will store 5 floating-point values.  

When declaring and initializing an array simultaneously, there is a special syntax that may be used to fill up the array with its starting values.  

&emsp;&emsp;**Instantiation syntax**  
&emsp;&emsp;`#!c bool truthtable[3] = { false, true, true};` -> if the `[ ]` is left blank, C will automatically create an array for the number of items in the `{ }`. 
  
&emsp;&emsp;**Individual element syntax**  
&emsp;&emsp;`#!c bool truthtable[3];`  
&emsp;&emsp;`#!c truthtable[0] = false;`  
&emsp;&emsp;`#!c truthtable[1] = true;`  
&emsp;&emsp;`#!c truthtable[2] = true;`  

Both of these arrays will have the same output.  

Arrays are not restricted to a single dimension. You can have as many size specifiers as you wish.  For example:  

&emsp;&emsp;`#!c bool battleship[10][10];`  

You can choose to think of this as either a 10x10 grid of cells, but it's really just a 100-element one-dimensional array.  Multi-dimensional arrays are great abstractions to help visualize game boards (such as Battleship above) or other complex representations.  


**Important Note**  
While we can treat individual elements of arrays as variables, we cannot treat entire arrays themselves as variables.  We cannot, for instance assign one array to another using the assignment operator.  Instead, we must use a loop to copy over the elements one at a time.  

For example, the following code would not work:  
```c
int foo[5] = { 1, 2, 3, 4, 5 };
int bar[5];

bar = foo;
```  
In the above code we are attempting to copy `foo` into `bar`, but this would not work correctly.  We must use a loop to copy the elements of `foo` into `bar` as follows:  
```c
int foo[5] = { 1, 2, 3, 4, 5 };
int bar[5];
  
for(int j = 0; j < 5; j++)
{
bar[j] = foo[j];
}
```

The simple `bar = foo;` does not work in C, but a simple `element = element` does work in many more modern programming languages.  

## Basic Array Program  

Lets make our first program using an array.  Let's say we want to create a program that prints out the average scores for a quiz.  We could have the following code that works perfectly:  

```c
#include <stdio.h> 
#include <cs50.h> 

int main(void)
{
	int score1 = 73; 
	int score2 = 77;
	int score3 = 36;
  
	printf("The average score was %i\n", (score1 + score2 + score3) / 3); 
}
```
Now lets convert the above code to use an array:

```c
#include <stdio.h>
#include <cs50.h>

int main(void) 
{
	int scores[3];
	scores[0] = 73;  //(note how we started counting at 0)  
	scores[1] = 77; 
	scores[2] = 36;
  
	printf("The average score was %i\n", (scores[0] + scores[1] + scores[2]) / 3);  
} 
```
Now lets make this program more intuitive and ask for user input.  Let's also make it so it is not constrained to just 3 scores.  

```c
#include <stdio.h>
#include <cs50.h>

float average(int length, int array[]);

int main(void) 
{
    int n = get_int("Number of scores: ");
  
    int scores[n];
  
    for (int i = 0; i < n; i++) 
    {
        scores[i] = get_int("Score %i: ", i + 1); //this will ask the user for input of Score 1, Score 2, Score 3, etc.
    }

        printf("The average score was %.2f\n", average(n, scores));
    }

float average(int length, int array[])
{
    int sum = 0;
    for (int i = 0; i < length; i++)
        {
            sum = sum + array[i];
        } 
        return (float) sum / (float) length;
}

```  
  
This should now allow a user to input the number of scores they want to be averaged and the program will prompt the user for each score.  After the scores have been inserted, the average will be displayed (with a decimal point because we chose to use `#!c float` for the average).  




## Other Array Tips  

Unlike most variables in C, arrays are not passed by value.  Arrays are passed by reference.  Instead of making an actual copy, arrays trust that functions will not break anything.  


## Reading Levels Program  

According to Scholastic, E.B. White’s “Charlotte’s Web” is between a second and fourth grade reading level, and Lois Lowry’s “The Giver” is between an eighth grade reading level and a twelfth grade reading level. What does it mean, though, for a book to be at a “fourth grade reading level”?  

Well, in many cases, a human expert might read a book and make a decision on the grade for which they think the book is most appropriate. But you could also imagine an algorithm attempting to figure out what the reading level of a text is.  

So what sorts of traits are characteristic of higher reading levels? Well, longer words probably correlate with higher reading levels. Likewise, longer sentences probably correlate with higher reading levels, too. A number of “readability tests” have been developed over the years, to give a formulaic process for computing the reading level of a text.  

One such readability test is the Coleman-Liau index. The Coleman-Liau index of a text is designed to output what (U.S.) grade level is needed to understand the text. The formula is:  

```c
    index = 0.0588 * L - 0.296 * S - 15.8
```  

Here, `#!c L` is the average number of letters per 100 words in the text, and `S` is the average number of sentences per 100 words in the text.  

Let’s write a program called `#!c readability` that takes a text and determines its reading level. For example, if user types in a line from Dr. Seuss:  

```
$ ./readability
Text: Congratulations! Today is your day. You're off to Great Places! You're off and away!
Grade 3
```  

The text the user inputted has 65 letters, 4 sentences, and 14 words. 65 letters per 14 words is an average of about 464.29 letters per 100 words. And 4 sentences per 14 words is an average of about 28.57 sentences per 100 words. Plugged into the Coleman-Liau formula, and rounded to the nearest whole number, we get an answer of 3: so this passage is at a third grade reading level.  

```
$ ./readability
Text: Harry Potter was a highly unusual boy in many ways. For one thing, he hated the summer holidays more than any other time of year. For another, he really wanted to do his homework, but was forced to do it in secret, in the dead of the night. And he also happened to be a wizard.
Grade 5
```  

This text has 214 letters, 4 sentences, and 56 words. That comes out to about 382.14 letters per 100 words, and 7.14 sentences per 100 words. Plugged into the Coleman-Liau formula, we get a fifth grade reading level.  

As the average number of letters and words per sentence increases, the Coleman-Liau index gives the text a higher reading level. If you were to take this paragraph, for instance, which has longer words and sentences than either of the prior two examples, the formula would give the text an eleventh grade reading level.  

```
$ ./readability
Text: As the average number of letters and words per sentence increases, the Coleman-Liau index gives the text a higher reading level. If you were to take this paragraph, for instance, which has longer words and sentences than either of the prior two examples, the formula would give the text an eleventh grade reading level.
Grade 11
```  

For this program we need to start with counting the letters, words, and sentences there are in the submitted text.  Next, we will plug those results into the Coleman-Liau index, mentioned above, `#!c index = 0.0588 * L - 0.296 * S - 15.8`.  Finally, we will take the result from the Coleman-Liau index and display the correct (U.S.) grade level.  

**Walkthrough**  

First, we will look at the letters in the submitted text.  We will need to count the number of both uppercase and lowercase letters in the text.  We will also need to ignore the spaces and punctuation.  We will need to look at each letter in the submitted text as it's own space as follows:  

| 1 | 2 | 3 | 4 | 5 | - | - | 6 | 7 | 8 | 9 | 10 | - |
|---|---|---|---|---|---|---|---|---|---|---|----|---|
| H | e | l | l | o | , |   | w | o | l | r | d  | ! |  

We will utilize the library `#include <ctype.h>` to help differentiate characters from each other.  

We will then need to calculate the number of words in a sentence.  We will do this by thinking that any sequence of characters separated by one or more spaces is a word.  This would look as follows:  

| 1 |   |   |   |   |   |   | 2 |   |   |   |   |   |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| H | e | l | l | o | , |   | w | o | l | r | d | ! |  

Finally, we will look at sentences.  For this problem, any period, exclamation point, or question mark will indicate a sentence.  This may no be true in some instances (Mr. or Mrs.), but should work in most cases.  

After these steps, we should have an accurate count of `#!c letters`, `#!c words`, and `#!c sentences`.  We should then run these numbers through the Coleman-Liau index.  

The formula should give out a real number, but we should round to the nearest whole number (`#!c int`).  Output should be "Grade #", where # is the grade level.  If the output is less than 1, we will output "Before Grade 1" and if it is above 16, we will output "Grade 16+".  

Let's begin programming!  

``` c
#include <stdio.h>
#include <cs50.h>
#include <math.h>
#include <ctype.h>
#include <string.h>

int main(void)
{
    string s = get_string("Text: ");
    int words, sentences, letters;
    words = sentences = letters = 0; // setting word, sentences, and letter count to 0
    for (int i = 0, len = strlen(s); i < len; i++)
    {
        if (isalpha(s[i]))  // checks to see if i is an alphanumeric character
            letters++; // if it is an alphanumeric character, letters increases by 1
        if((i == 0 && s[i] != ' ') || (i != len - 1 && s[i] == ' ' && s[i + 1] != ' ')) // checks to see if there are any spaces between groups of letters
            words++;    // if there are spaces between groups of letters, words increases by 1
        if (s[i] == '.' || s[i] == '!' || s[i] == '?') // checks to see if there is a ., !, or ?
            sentences++;  // if there is a ., !, or ?, it increases by 1
    }

    float L = ((float) letters / (float) words) * 100; // converts the number of letters and words to float, then divides them by each other and multiplies the result by 100
    float S = ((float) sentences / (float) words) * 100; // converts the number of sentences and words to float, then divides them by each other and multiplies the result by 100
    int index = round(0.0588 * L - 0.296 * S - 15.8); // the float L and S are then ran through the Coleman-Liau index.

    if(index < 1) // if the index (Coleman-Liau index) is less than 1
        printf("Before Grade 1\n");
    else if (index < 16) // if the index is less than 16
        printf("Grade %i\n", index);
    else // if it is >= 16
        printf("Grade 16+\n");
}
```

## Caesar's Cipher 

We will now create a program that will take text and run it through Caesar's encryption method.  Supposedly, Caesar (yes, that Caesar) used to “encrypt” (i.e., conceal in a reversible way) confidential messages by shifting each letter therein by some number of places. For instance, he might write A as B, B as C, C as D, …, and, wrapping around alphabetically, Z as A. And so, to say HELLO to someone, Caesar might write IFMMP. Upon receiving such messages from Caesar, recipients would have to “decrypt” them by shifting letters in the opposite direction by the same number of places.  

The secrecy of this “cryptosystem” relied on only Caesar and the recipients knowing a secret, the number of places by which Caesar had shifted his letters (e.g., 1). Not particularly secure by modern standards, but, hey, if you’re perhaps the first in the world to do it, pretty secure!  

!!! note 
    Unencrypted text is generally called *plaintext*. Encrypted text is generally called *ciphertext*. And the secret used is called a *key*.  

To be clear, then, here’s how encrypting `HELLO` with a key of 1 yields `IFMMP`:  

| plaintext    | H | E | L | L | O |
|--------------|---|---|---|---|---|
| + key        | 1 | 1 | 1 | 1 | 1 |
| = ciphertext | I | F | M | M | P |  

More formally, Caesar’s algorithm (i.e., cipher) encrypts messages by “rotating” each letter by *k* positions. More formally, if *p* is some plaintext (i.e., an unencrypted message), p<sub>i</sub> is the i<sup>th</sup> character in *p*, and *k* is a secret key (i.e., a non-negative integer), then each letter, c<sub>i</sub>, in the ciphertext, *c*, is computed as:
<p style="font-size:20px">c<sub>i</sub> = (p<sub>i</sub> + k) % 26</p>  

wherein `% 26` here means “remainder when dividing by 26.” This formula perhaps makes the cipher seem more complicated than it is, but it’s really just a concise way of expressing the algorithm precisely. Indeed, for the sake of discussion, think of A (or a) as 0, B (or b) as 1, …, H (or h) as 7, I (or i) as 8, …, and Z (or z) as 25. Suppose that Caesar just wants to say Hi to someone confidentially using, this time, a key, *k*, of 3. And so his plaintext, *p*, is Hi, in which case his plaintext’s first character, p<sub>0</sub>, is H (aka 7), and his plaintext’s second character, p<sub>1</sub>, is i (aka 8). His ciphertext’s first character, c<sub>0</sub>, is thus K, and his ciphertext’s second character, c<sub>1</sub>, is thus L. Can you see why?  

Here are a few examples of how the program might work. For example, if the user inputs a key of `1` and a plaintext of `HELLO`:  

```
$ ./caesar 1
plaintext:  HELLO
ciphertext: IFMMP
```  

Here’s how the program might work if the user provides a key of `13` and a plaintext of `hello, world`:  

```
$ ./caesar 13
plaintext:  hello, world
ciphertext: uryyb, jbeyq
```  

**Now let's get coding!**  

We need our program to do the following:  

* Get Key (the amount to shift the text by)  
* Get plaintext  
* Encipher  
* Print ciphertext  

!!! note 
    We will preserve case for letters (Keep capital letters capital, and lowercase lowercase).  We will also wrap the alphabet (If we go beyond the boundaries of the alphabet, it will just start over).  

Let's walkthrough each piece of the program.  

**Get the Key**  

We will be taking the key as a [command line argument](c-cl-arguments.md):  

```
$ ./caesar 3
```  

Remember that in C our main function can take arguments using the following:  

``` c
int main(int argc, string argv[])
{
    // code here
}
```  

**Getting the Key**  

* Ensure single command-line argument (print error message if command-line argument is out of bounds)  
* Make sure argument contains only digit characters  
* Convert argument to an integer  

We will also need to convert the `string` from the command line argument into a number using the `atoi` function, declared in `<stdlib.h>`.  

**Getting the Plaintext**  

We will simply use the `get_string` function to get user input for the plaintext.  

**Encipher the Plaintext**  

If it's alphabetic, shift the plaintext character by key, preserving the case.  

If it's not alphabetic, leave the character as-is.  

We can use the following functions to help us identify character type: `isalpha`, `isupper`, and `islower`.  These functions will return a boolean value (`true` or `false`).  

Here is the correct program:  

``` c
#include <stdio.h>
#include <cs50.h>
#include <stdlib.h>
#include <string.h>
#include <ctype.h>

bool check_key(string s);

int main(int argc, string argv[]) //argc takes in the number of arguments and argv creates an array for the arguments themselves.
{
    if (argc != 2 || !check_key(argv[1])) // checking if the number of arguments is not 2 and if the key is valid
    {
        printf("Usage: ./caesar key"); // if the input is not valid, it will print an error message with the correct way to enter
        return 1;
    }
    int key = atoi(argv[1]); // converts from ASCII to integer

    string plaintext = get_string("plaintext: ");
    printf("ciphertext: ");
    for (int i = 0, len = strlen(plaintext); i < len; i++)
    {
        char c = plaintext[i];
        if (isalpha(c))
        {
            char m = 'A';
            if (islower(c))
                m = 'a';
            printf("%c", (c - m + key) % 26 + m); // inputs the plaintext into Caesar's cipher
        }
        else
            printf("%c", c); // if the character is not alphabetic, it will print it as is
    }
    printf("\n");
}

bool check_key(string s) // this string checks to see if the key is valid
{
    for (int i = 0, len = strlen(s); i < len; i++)
        if (!isdigit(s[i])) // if its not a digit, return false
            return false;
    return true;
}
```  