# JavaScript Basics

## Quick Links  

* [You Don't Know JS Yet: Get Started (Online Book)](https://github.com/getify/You-Dont-Know-JS/blob/2nd-ed/get-started/README.md)  

* [Eloquent JavaScript (Online Book)](https://eloquentjavascript.net/)  

* [JavaScript: Notes for Professionals (PDF)](https://books.goalkicker.com/JavaScriptBook/JavaScriptNotesForProfessionals.pdf)  

* [Interactive JS CheatSheet](https://htmlcheatsheet.com/js/)  

* [JavaScript and JQuery - Interactive Front-End Web Development (PDF)](https://cdn.nickplatt.dev/files/Docs/JavaScript-and-JQuery-Interactive-Front-End-Web-Development.pdf)

## Introduction  

JavaScript, often abbreviated as JS, is a scripting or programming language that allows you to implement complex features on web pages - every time a web page does mroe than just sit there and display static information for you to look at - displaying timely content updates, interactive maps, animated 2D/3D graphics, etc. - you can bet that JavaScript is probably involved.  Most modern webpages are a mix of HTML, CSS, and JavaScript.  

## Setup and Hello World!
Whenever we are writing JS, we can either write the code directly inside the HTML file or we can create a separate JS file that we link into the HTML.  To start, we are going to be writing the JS directly inside the HTML file.  We are going to use a basic HTML file titled `index.html`.  We will work directly inside a `#!html <script>` tag and open the .html file inside a browser.  Saving the file and refreshing the browser should show any updates that have been made.  Below is the `index.html` file we will be working with:
```html linenums="1"
<html>
<head>
	<meta charset="UTF-8">
	<title>JavaScript Testing</title>
</head>
<body>
	<!-- JavaScript Code goes here inside a <script> tag -->
</body>
</html>
```
Now that we have the basic HTML file ready to go, let's insert the following JS:
```html linenums="1"
<script type="text/javascript">
	// This 
	alert("Hello World!");
	// This writes text to the screen
	document.write("Hello World!");
</script>
```
The above `#!js document.write("")` command is the most basic way to write something to the screen.  The `#!js alert("")` command will display text in a dialog box that pops up on the screen.  

Linking a seperate JS file into HTML can be helpful for organization and is a simple process.  Create another file in the same directory as the `index.html` file and name it something like `script.js`.  You can name it whatever you want, it just needs to end with the file type `.js`.  To link the `.js` file into the HTML file, we will add the following code into the `#!html <head>` tag:
```html linenums="1"
<html>
<head>
	<meta charset="UTF-8">
	<title>JavaScript Testing</title>
	<script src="script.js"></script>
</head>
<body>

</body>
</html>
```
Functionally, including the JS as a file or directly inside the HTML file are functionally the same.

## Writing HTML in JavaScript
Let's start with a blank HTML file, like the one from above, that links to an outside JS file.  In that JS file, let's add the following:
```js linenums="1"
document.write("<h2 style='color:blue;'>JavaScript Rules!</h2>");
document.write("<hr/>");
```
The `#!js document` command refers to the HTML document that the entire file is linked to.  The `#!js write()` command let's us write whatever we want to the HTML document.  We can write plain text or actual HTML tags (like the example above).  Moving the `#!html <script>` tag within the HTML file will determine where that JS will write the HTML.