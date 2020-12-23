# Variables and Simple Data Types  

## Variables 

Variables are a JavaScript developer's bread and butter. They make it really easy to write complex programs with lots and lots of instructions, and keep everything organized and straight.  Often times when you're writing a program in JavaScript, there will be several pieces of data that you need to keep track of.  Think for example of Facebook. Facebook keeps track of tons of information and displays it on their websites and apps. Things like names, birthdays, status', etc. In order for us to write more complex programs like these, that do more than print text out onto the screen, we'll need to learn how to manage all of the information in our programs and use variables.  

Variables are essentially containers which allow a program to store different pieces of information inside of them. Once the information is stored inside the variable, that information can then be accessed throughout the program simply by referring to the variable's name.  Using variables is a great way to keep track of and organize your data.  When creating variables, make sure to use descriptive names!  For example, if we were creating a variable to hold someones age, using `#!js var age` is much better than `#!js var a`.  This can save time trying to figure out what each variable is defining!

Let's make some variables in JS:
```js
var phrase = "To be or not to be";

document.write(phrase);
```

`#!js var` is a special word in JS, which tells JS that a variable is being created.  Now we can call the variable within the `#!js document.write();` command instead of having to type out the string.  This can be very powerful and save programmers a ton of time!  We can also change the variable after defining it originally:
```js
var phrase = "To be or not to be";

document.write(phrase);
phrase = "Apple"
document.write(phrase);
```
Now it should print out `To be or not to be` and `apple`.

We are not limited to only storing strings of text within a variable.  We can also store numbers (whole numbers or decimals), boolean variables, undefined, and Null:
```js
var name = "Nick"
var age = 25;
var gpa = 3.8;
var isMale = true;
var flaws = null;
var description = undefined;

document.write(`${name} is ${age} years old.`);
if(isMale = true){
	document.write(`He has a ${gpa} GPA.`);
}
else{
	document.write(`She has a ${gpa} GPA.`);
}
```
The above code should have the following output:
```
Nick is 25 years old.He has a 3.8 GPA.
```
`#!js null` and `#!js undefined` are different because when you use `#!js null`, you are saying that there is no value, but `#!js undefined` says that there is no value *yet*.  You will probably not use `#!js null` or `#!js undefined` much as a developer, but they are still good to know/understand.

Remember to **use descriptive variable names**!  Think of a variable as a moving box.  When you fill up the box it is common to write on the outside of the box what it contains.  Use similar logic when it comes to naming variables.

## Strings
