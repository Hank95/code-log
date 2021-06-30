---
title: "Iffy on IIFE's"
categories:
  - JavaScript
tags:
  - JS
  - IIFE
  - Closures
---

## And Welcome to My Blog

An IIFE, Immediately Invoked Function Expression, or “self-executing anonymous function” is exactly that, a function in Javascript that is invoked as soon as it is defined. Here is how and why ...

I ask you to bare with me as I have had my head dowm fot the past few weeks trying to learn as much JavaScript as my brain can take in. This is one of those blogs that is here more for me than you. This is my attept to grasp an idea I have been struggling wiht and maybe pass along some knowlege in a some what legible manner. I'll do what I can for typos but please forgive any janky code, I am dipping in my toe and the ocean is deep and wide.

With that out of the way, let's learn.

To make sure everyone is on the same page and start with some regular old functions.

```javascript
function frendlyGreeting(name) {
  console.log(`Howdy ${name}`);
}
frendlyGreeting("Gerorge"); // Console logs "Howdy George"
```

This is a standard operating procedure, this is a function declaration. We can declare a function then call it where we like in our code.

Here is a function expression:

```javascript
const frendlyGreeting = function (name) {
  console.log(`Howdy ${name}`);
};
frendlyGreeting("Gerorge"); // Console logs "Howdy George"
```

In this example, we get the same outcome but this time we assigned a function to a variable and then referred to it at a later date. One of the major differences between function declaration and expression is that declarations can be called anywhere in the code, even before they are defined. Function expressions can only be called after they have been defined.
Only function expressions can be IIFEs hence why they are called Immediately Invoked "Expressions". With a little adjusting, we can turn a declaration into an expression so we don’t throw any errors. Also, anonymous functions or just unnamed function expressions will work as well.

Finally, let us take a look at these IIFE's and then we can talk through them.

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

Notice how we are invoking the function as soon as it is defined. No hesitation, to waiting around to call it later, just BAM execute it. Number one in the example above, with the varuiable expressive, id dtsmdsrd operating proceedure. The parentheses around the function and the empty parens to invoke it. If there we any arguments to call they would go in those empty parens.
The second example is a declarative function that is trying to be called as an IIFE and will throw an error every time. The third example is proper way to do it. See how the function is wrapped up nicely in some parentheses. This removes the function from the global scope and that is the meat of the matter that well will go into more depth in a second.
The fourth example is the anonymous function example and is useful if you need to execute a function and never need it again.

There is two way to create these IIFE's, they will both execute in the same manner and the difference just comes down to personal preference.

```javascript
// Option 1
(function(){Your code here}())
// Option 2
(function(){Your code here})()
```

## What's the Point?

It removes things from the global scope. If you don’t watch out things can get very messy very quickly, declaring variables left and right, declaring functions as you go. And then, I anticipate, if you start collaborating on code with other developers, adding other .js files, libraries, and so on, things can start to mess with code that is globally declared. Aka, don't air your dirty laundry. The global scope by definition can be accessed by all the other JavaScript in your app. Immediately invoked functions are a great way to compartmentalize and privatize your code. It can keep variables hidden from the rest of the code and allow your code to grow with less of a chance that you will need to go back and refactor everything or spend days looking for that one piece of code messing with that one variable.

So yes, there is th how and why of it. Let's move on to some 'closer to real world' applications. If we mix in some [closers](url) we will really start to make some cool thigs

```javascript
const piggyBank = (function () {
  let coins;
  const bankObj = {};
  bankObj.withdrawl = function (ammount) {
    if (coins - ammount < 0) {
      console.log("Innsuficient funds");
    } else {
      coins = -ammount;
      return coins;
    }
  };
  bankObj.deposit = function (ammount) {
    return (coins = +ammount);
  };
  bankObj.checkBalance = function () {
    return coins;
  };
  return bankObj;
})();

piggyBank.deposit(100); //100 coins
piggyBank.withdrawl(200); //"Innsuficient funds"
piggyBank.withdrawl(25); //75 coins
piggyBank.withdrawl(60); //15 coins
```

It's a little much, but if you take the time to go through this function you can see that coins in defined in the function and even after the function piggyBank has been called the interior fucntion still have acess to the coins. But if you we to to copy down this code you would find that it would impossible to access or change the value without calling one of our inner functions. In that way it kind of does act like a irl pigg bank. We coudl have called withdrawl, deposit, and checkBalance right in the global scope and acheived the same results, but if we did that, anyone coudl come along and just declair coins to be what ever they want!

This is a great example of combining closures and IIFEs in the a practical and usful example.

## Bibliography/Further Reading

- IIFE - [developer.mozilla.org](https://developer.mozilla.org/en-US/docs/Glossary/IIFE)

- Flatiron School - [flatironschool.com](https://flatironschool.com)

- Immediately-Invoked Function Expression (IIFE) - [Ben Alman](https://web.archive.org/web/20171201033208/http://benalman.com/news/2010/11/immediately-invoked-function-expression/#iife)

- Essential JavaScript: Mastering Immediately-invoked Function Expressions - [Chandra Gundamaraju](https://vvkchandra.medium.com/essential-javascript-mastering-immediately-invoked-function-expressions-67791338ddc6)

* Learning JavaScript Closures through the Laws of Karma - [Chandra Gundamaraju](https://vvkchandra.medium.com/learn-javascript-closures-through-the-laws-of-karma-49d32d35b3f7)
