---
layout: post
title:      "Hoisting and Block Scope: var vs. const & let"
date:       2020-05-28 22:41:39 +0000
permalink:  hoisting_and_block_scope_var_vs_const_and_let
---


During my assessment of the Javascript section, it became clear to both myself and my reviewer 1) I confused hoisting with closure and 2) because I was taught to not use var anymore since the introduction of let and const in ES6, I just disregarded it.  However, although ES6 introduced let and const and it is recommended to use these to declare / assign variables, var still exists in code and I need to understand it and how it differs from the new syntax.

So, hoisting:

JS runs code from top to bottom, but it runs twice.  The first run is the compilation phase where it compiles and stores function and variable declaration to the top of the current scope. This is hoisting.  Variable declarations that use the keyword ‘var’ are hoisted, but not their assignment.

Declaring a variable happens by using a variable declaration keyword (let, const, var) and stating the variable name:
let pet;

The assignment happens when the variable name is actually assigned a value:
pet =”Rugby”;

It is only the declaration that is hoisted during the compilation phase, and not the assignment. 

As an example, the following code would recognize that the variable exists, but would not know it’s assignment because only the declaration was hoisted:

console.log(pet);
var pet = “Rugby”;

During the execution run, the console.log statement runs first; and because the pet variable was defined with the keyword var JS knows it exists because of hoisting, but it does not know the assignment, so it would return undefined.  The assignment of the string “Rugby” to the variable pet comes after the log statement, and only the declaration is hoisted.  

On the other hand, let and const are not hoisted. If the same code was run but instead of var we used let or const, the log statement would return a reference error that pet is not defined.  Let and const are not hoisted during the compilation phase, and therefore have to be declared before use to get an undefined return, and all variables have to be assigned before they are used to allow access to the value of the variable.

Var is also different from let and const because var has function scope while let and const have block scope. 

So, Scope:

Scope in Javascript defines the area in which variables are visible in your code.  Global scope variables are accessible within the entire code, and variables in the global scope are defined outside of functions.  Function scope refers to variables defined within the function, these variables are not accessible outside of the function.  Nested functions have outer and an inner function(s).  Inner functions have access to the variables defined in their outer parent function, but variables defined in the inner function cannot be accessed from the outer functions.  An outer function’s scope includes the children function nested within, but the children’s scope is the area of just the inner function and any functions that may be nested under it.  This is called lexical scope.  Inner functions are a closure of their outer function.

Block scope is the area within the block.  The block of a function is defined by curly braces {}, the curly braces and the code inside is the area of block scope.  Both block scope and function scope are categorized as local scope.  Functions have blocks of code, but function scope and block scope are different because ES6 introduced let and const instead of var for declaring / assigning variables and var has functional scope while let and const have block scope.

This difference can be shown in a case of an if statement:
``` let i = 4; if (i % 2 === 0) {var evenNum = `${i} is an even number!`; console.log(var);}```

This is not a function, but there is a block of code.  Because var has function scope and this is not a function, it can be accessed globally outside of the block.
calling :
evenNum; 
will return the string “4 is an even number!”

If let was used to assign the variable in the block, when the block runs the console.log will log the string assigned to the variable (same as var) because the log statement is inside the block.   However, if you called evenNum outside of the block, you would get an error that the variable is not defined.  This is the difference between function and block scope, and why it is important.  If statements, switch statements, and for and while loops have blocks that are not necessarily within a function, which makes variables declared or assigned with let inaccessible outside of the curly braces, while variables with var are placed into the global scope. 


My dive into hoisting and scope has definitely helped my understanding of var, let and const; thank you Juan for showing me that this is something I did not understand completely and for encouraging me to learn it!




