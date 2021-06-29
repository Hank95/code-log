---
title: "Iffy on IIFE's"
categories:
  - JavaScript
tags:
  - JS
  - IIFE
  - Closures
---

An IIFE, Immediatly Invoked Function Expression, or “self-executing anonymous function” is exactly that, a function in Javascript that is invoked as soon as it it defined. Here is how and why ...

Lets make sure everyone is on the same page and start with some regular old functions.

```javascript
function frendlyGreeting(name) {
  console.log(`Howdy ${name}`);
}
frendlyGreeting("Gerorge"); // Console logs "Howdy George"
```

This is a standard operating proceedure, this is a function decleration. We can declare a function then call it where we like in our code.

Here is a function expression:

```javascript
const frendlyGreeting = function (name) {
  console.log(`Howdy ${name}`);
};
frendlyGreeting("Gerorge"); // Console logs "Howdy George"
```

In this example we get the same out come but this time we assigned a function to a variable and then refered to it at a late date. One of the major diffreneces between funtion declaration and expression is that declerations can be called anywhere in the code, even before they are defined. Function expressions can only be called after they have been defined. Only function expressions can be IIFEs hence why they are called Immediatly Invoked "Expressions". With a little adjusting we can turn a decleration into an expression so we dont throw any errors. Also, anonymous funtions or just unnamed function expressions will work as well.

Finally, lets take a look at these IIFE's and then we can talk through them.

```javascript
// 1
const expressive = (function () {
  console.log("Expression");
})(); // "Expression"

// 2
function declarative() {
  console.log("declaration");
}(); // ERROR: Expression expected

// 3
(function declarative() {
  console.log("Declaration");
})(); // "Declaration"

// 4
(function () {
  console.log("Anonymous");
})(); // Anonymous
```

Notice how we are invoking the function as soon as it is defined. No hesitation, to waiting around to call it later, just BAM execute it. Our first example in the snippet above it an example of named IIFE, all looks good with it, the parentheses aroud the funtion and the empty parns to invoke it. If there we any arguments to call they would go in those empty parens.  
The second example is a declarative function that is trying to sneek by and will throw an error everytime. The third example is proper proceedure. See how the function is wraped up nicly in some parentheses. This removes the function from the global scope and that really is the meat of the matter that well will go in to more depth on in a second.  
The forth example is the anonymous funtion example and is usful if you need to execute a funtion and never need it again.

There are two way to create these IIFE's, they will both execute in the same manor and the difference really just comes down to personal preffrence.

```javascript
// Option 1
(function(){Your code here}())
// Option 2
(function(){Your code here})()
```

## What's the Point?

I'll tell you, it removes things from the global scope. If you dont watch out things can get very messy very quickly, declairing variables left and right, declairing functions as you go. And then if you start colaberating on code with other developers, adding other .js files, libraries, and so on, things can start to mess with code that is gloably delcaired. Aka, don't air your dirty laundry. The global scope by definition can be accessed by all the other JavaScript in your app. Immediatly invoked functions are a great way to compartmentalize and privatize your code. It can keep variables hidden from the rest of the code and allow you code to grow with less of a chance that you will need to go back and refactor everthing or spend days looking for that one piece of code messing with that one variable.
