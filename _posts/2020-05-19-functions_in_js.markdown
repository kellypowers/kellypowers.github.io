---
layout: post
title:      "Functions in JS"
date:       2020-05-19 16:43:42 +0000
permalink:  functions_in_js
---


There are many ways to write functions in JavaScript, and I have decided to explain some of the ones I have learned here as a reference!


##Function Declaration
Function declaration explicity defines a function using the function keyword and the function name.  Parameters are in parentheses , the code to be executed is wrapped in curly braces, and the return keyword needs to explicitly say what to return, or else the return will be undefined.
```function myFunction(word) {
      console.log(word);
			return word
		}
		```
		
##Anonymous Function
Anonymous functions have no name in front of the function.  They are ususally used when they are saved as a variable as a function expression (shown below).
```function() {
  console.log("Yet more razzling")
}```
		
##Function expression
Function expressions saves a function as a variable.  It stores the work of the function in the variable.  It is called using the variable name with the parameter of the function in parentheses.
```
const square = function(number) { return number * number }
square(4) ```  // returns 16

##Nested functons
Javascript allows for functions to be nested.  Inner functions have access to variables of the outer functions, but the outer function does not have access to variables of inner functions (lexical scope).  The Flatiron lesson gave the following function as an example:
```function outer(greeting, msg="It's a fine day to learn") {
  let innerFunction =  function(name, lang="Python") { 
    return `${greeting}, ${name}! ${msg} ${lang}` 
  }
  return innerFunction
}
 ```
 The function above can be called using the name of the outer function, the parameters of the outer function in parentheses, followed by the parameters of the inner function in their own set of parentheses like this:
 ```
outer("Hello")("student", "JavaScript") 
```
 
 
##Immediately Invoked Functional Expression 
IIFE are functions that are called immediately upon reading it.  To make a IIFE, wrap the function in parentheses.

```(function () {
  var counter = 0;
  return function () {counter += 1; return counter}
})```

IIFE are used in 
From the w3schools Javascript docs:  "A closure is a function having access to the parent scope, even after the parent function has closed."
```var add = (function () {
  var counter = 0;
  return function () {counter += 1; return counter}
})();```


Function functions vs. arrow functions: Arrow functions do not have their own ```this``` value, whereas function functions do have their own value for ```this```.  This difference makes arrow functions easier to use in Object Oriented programming when using callback functions.  

##Arrow Functions 
with no parameters:
```() => {statements}```
with one parameter the parentheses are optional:
```parameter => {statements}```
With more than one parameter, parentheses are required:
```let funct = (parameter1, parameter2) => {code to be executed};```
Arrow functions are the newer way to function writing anonymous functions in shorthand.  An arrow ```=>``` points to the block of code to be performed.  If the code is one line the curly braces do not need to enclose the block of code and the function will return that expression without the return keyword.   If curly braces are around the block of code because the code is multiple lines, it is necessary to explicitly state the return value.  

Examples: 
```
[1, 2, 3].reduce(function(total, element) {
return element*2 + total} , 0) ```
Here, the reduce function uses IIFE to double each element of the array and add it to the total.  If it had a ```const funName = ``` before the array, in front of the line, it would be a functional expression.  This function written as an arrow function could look like: 
```
[1, 2, 3].reduce((total, element) => element*2 + total)```



