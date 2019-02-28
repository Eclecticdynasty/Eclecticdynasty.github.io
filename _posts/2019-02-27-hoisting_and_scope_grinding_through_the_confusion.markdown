---
layout: post
title:      "Hoisting and Scope: Grinding through the confusion"
date:       2019-02-27 21:40:36 -0500
permalink:  hoisting_and_scope_grinding_through_the_confusion
---




Two concepts I wanted to explore and gain a better understanding of is **Scope** and **Hoisting**. *Scope* determines the visibility of variables and other resources in your code. Also, scoping your code helps to improve efficiency and provide some level of security to your code. *Hoisting* is a little harder to explain and define. Generally, hoisting is how the creation and execution phase works in JS for variables and functions. Concept-wise, variable and function declarations are put into memory, but also stay where they are in your code.

Starting with Scope. There's **Global Scope** and **Local Scope**. A variable is in the global scope if it's defined outside of a function. Variables defined inside a function are in the local scope. 

```
const global = 'This is a global scoped variable'

function () {
    const global = 'This is locally scoped';
		}
```

Besides the difference in location, an important differentiation between local and global scope is that variables inside the global scope can be accessed and altered in any other scope;  variables in the local scope are bound to their respective functions and are not accessible in other functions.

Within the concept of scope; An interesting topic is the *this* keyword. The *this* keyword references the object that receives the method call. It allows us to reference the object receiving the method from inside a method call. The value of the 'this' keyword changes based on where it is. Outside of any function, this refers to the global object(*the browser window*). Inside an object method, this refers to the object that received the method call. Inside a standalone function, this will either default to the global object or be undefined.

```
function greet() {
    console.log(`my name is ${this.name}, hi!`);
}
 
greet(); // my name is , hi!
 
let person = {
    name: 'Bob',
    greet: greet
};
 
person.greet();

We have a function, greet, that logs a string. When the greet is invoked as a function, this is referring to the global object (the browser window). However, when greet in invoked as a method of an object, this changes to refer to the object the method is invoked in. Since person has a name property set, so this.name means the value of bob. 
```
	
**Arrow functions** help to simplify function scope and much using the 'this keyword' much more straightforward. 


Now on to a few key points within the concept of *hoisting*. All variable declarations using**var**  are hoisted to the top of their local/functional scope or to the top of their global scope regardless of where the actual declaration has been made. **Function declarations** are also hoisted. 
A function declaration defines a function; function expressions are quite different. 
**Function expressions** are not hoisted and will return a *TypeError* because you cannot use function expressions before defining them. 

Variable hoisting can be different based on the variable keyword used when a variable is declared. Keep in mind that while* variable declarations are hoisted, the actual value given to the variable is not*. The difference between **var**, **let** and **const** is that let and const will throw a *Reference Error* if you try to call one before it has been assigned a value. In regards to, block statements let and const keywords support the declaration of local scope inside block statements.

A **var** keyword variable declaration returns undefined. **Undefined** means that JS recognizes that the variable name exists. This is because when you see ```var a = 2;```, you probably think of that as one statement. But JavaScript actually thinks of it as two statements: ```var a; and a = 2;```. The first statement, the declaration, is processed during the compilation phase. The second statement, the assignment, is left in place for the execution phase.

These concepts are still confusing and in my research, it seems there are JS programmers with more experience who still struggle with it from time to time(which I find comforting) but with time and experience understanding hoisting and scope will get easier. 

