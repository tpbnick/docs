# If Statements

Python often involves examining a set of conditions and deciding which action to take based on those conditions.  Python's `if` statement allows you to examine the current state of a program and respond appropriately to that state.  

## A Simple Example
The following short example shows how `if` tests let you respond to special situations correctly.  Imagine you have a list of cars and you want to print out the name of each car.  Car names are proper names, so the names of most cars should be printed in title case.  However, the value `'bmw'` should be printed in all uppercase.  The following code loops through a list of car names and looks for the value `'bmw'`.  Whenever the value is `'bmw'`, it's printed in uppercase instead of title case.  

```py linenums="1"
cars = ['audi', 'bmw', 'subaru', 'toyota']

for car in cars:
	if car == 'bmw':
		print(car.upper())
	else:
		print(car.title())
```
The loop in this example first checks to see if the current value of `car` is `'bmw'`.  If it is, the value is printed in all uppercase.  If the value of `car` is anything other than `'bmw'`, it's printed in title case:  

```
Audi
BMW
Subaru
Toyota
```

## Conditional Tests
