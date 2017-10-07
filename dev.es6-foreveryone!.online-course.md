# ES6 for Everyone!
last updated - Sept 28, 2017
https://courses.wesbos.com/

## Module 2: Function Improvements: Arrows and Default Arguments

###  Module 2.6: Arrow Functions Introduction

* 3 benefits:
  * More concise
  * Implicit returns (nifty one-liners)
  * Doesn't rebind value of `this` when you use arrow function inside another function

```javascript
const name = ['warren', 'will', 'wally'];
const fullNames = names.map(function(name) {
// EQUALS   ... = names.map((name) => {
// EQUALS   ... = names.map(name => {
    return `${name} shea`;
});
console.log(fullNames); //returns ["warren shea", "will shea", "wally shea"]
```
EQUALS
```javascript
const name = ['warren', 'will', 'wally'];
const fullNames4 = names.map(name => `${name} shea`); //*
console.log(fullNames); //returns ["warren shea", "will shea", "wally shea"]
//* where { and } are removed to implicitly return
//and where `return` being used above is an explicit return
```

If you had no parameter to return, you can take out the `name` parameter
```javascript
const name = ['warren', 'will', 'wally'];
const fullNames5 = names.map(() => `two shea`); //*
console.log(fullNames); //returns ["two shea", "two shea", "two shea"]
```

* Named Function (FYI only)
```javascript
function thisIsANamedFunction(x) {
  console.log(x);
}
//Useful for debugging, to see the function that might cause an error
```

* Arrow Functions are not named functions (it is an anonymouse function) but you can put it in a variable
```javascript
const sayMyName = (name) => {console.log(name)};
sayMyName('warren'); //returns 'warren'
//Not good for stack traces but good if you're not concerned
```

###  Module 2.7: More Arrow Function Examples
```javascript
const race = '100m Dash';
const winners = ['Wally West','Barry Allen','Bart Allen'];
const win = winners.map((winner,i) => ({name: winner, race: race, place: i +}))
//extra ( ) around {} means it's an object literal
//@FYI: console.table(win) gives you sweet looking table !

//another way to write it:
const win2 = winners.map((winner,i) => ({name: winner, race, place: i +}))
//just say "race", and it will automatically mean "race: race"
```

```javascript
const ages = [3,34,62,31,25,15,46,76]
//const old = ages.filter(age => (age >= 60)); //returns [62,76]
const old = ages.filter(age => age >= 60); //returns [62,76]
```

###  Module 2.8: Arrow Functions and `this`

```javascript
var box = document.querySelector('.box'); //equals $('.box');
box.addEventListener('click', () => {
    console.log(this) // this is the window!
}); //this is bad!

box.addEventListener('click', function() => {
    this.classList.toggle('add-class');
    setTimeout(() => {
      this.classList.toggle('add-second-class');
      //where this is inherited from above (where add-class is logged), as opposed to doing self = this;
    }, 500);
});
```

```javascript
//@FYI Switch values in ES6
let first = "first";
let second = "second";
[first,second] = [second,first];
```

###  Module 2.9: Default Function Arguments



## Module 1: New Variables - Creation, Updating and Scoping

###  Module 1.1: var Scoping refresh

* `${var}`
```javascript
var dogYears = age * 7;
console.log(“You are “ + dogYears + “ dog years old!”);
/*is the same as */ console.log(`You are ${dogYears} dog years old!`);
```

* `var` variables are function scoped, but if there’s no function, it will be block scoped (between { and } )

###  Module 1.2: `let` VS `const`

* `let` variables are block scoped
```javascript
let x = 1;
if (x === 1) {
  let x = 2;
}
console.log(x); //1...because the "x" variables are different, the "x" variables are scoped differently
```

* `let` variables are made to be updated

* `const` variables are never to be updated

* `Object.freeze` (not ES6): used to freeze the variable from being changed
```javascript
const person = {
  name: 'warren',
  age: 35
}
const warren = Object.freeze(person);
warren.age = 30;
console.log(warren.age); //35
```

###  Module 1.3: `let` and `const` in Real World

* Immediately-invoked function expression - [iife](https://en.wikipedia.org/wiki/Immediately-invoked_function_expression)
```javascript
(function () { /* ... */ })();
(function () { /* ... */ }());
(() => { /* ... */ })(); // With ES6 arrow functions (though parentheses only allowed on outside)
```
What it does: a function that runs itself immediately and creates a scope where nothing is going to leak into the parent scope (e.g. global scope of the window)

* with `let` and `const`, you don't need to do this because they're block scoped.
```javascript
{
  const name = 'warren';
  console.log(name); //warren
}
```

* also with `let` and `const`, you have an issue with `for` loops
```javascript
for (var i = 0; i < 10; i++) {
  console.log(i); //returns 0, then 1, then 2, ... to 10 each loop
  setTimeOut(function() {
    console.log("The number is " + i); //returns 10x 10 at the very end *
  },1000);
}
//* this executes after 1 second, after the loop has finished
/**************************************************************************/
for (let i = 0; i < 10; i++) {
  console.log(i); //returns 0, then 1, then 2, ... to 10 each loop
  setTimeOut(function() {
    console.log("The number is " + i); //returns "The number is 1", "The nubmer is 2", etc. **
  },1000);
}
//** this i variable is now scoped to the loop
```

###  Module 1.4: Temporal Dead Zone

* Temporal Dead zone
```javascript
var pizza = "deep dish";
console.log(pizza); //returns undefined
```
The `var` variables can be access before it's defined
You can't access the value, but you can access the variable
```javascript
let/const pizza = "deep dish";
console.log(pizza); //returns "Uncaught ReferenceError: pizza is not defined"
```
You can't access the variable (`let` / `const`) before it's defined

###  Module 1.5: Is `var` Dead? What should I use?

* Using `let` / `const` / `var` : the [Mathias Bynens](https://mathiasbynens.be/notes/es6-const) & Web Bos approach
  * use `const` by default
  * only use `let` if rebinding is needed
  * (`var` shouldn’t be used in ES6)

* Using `let` / `const` / `var` : the [Kyle Simpson](https://github.com/getify/You-Dont-Know-JS/tree/master/es6%20%26%20beyond) approach
  * use `var` for top-level variables that are shared across many (especially larger) scopes
  * use `let` for localized variables in smaller scopes
  * refactor `let` to `const` only after some code has been written and you're reasonably sure you've got a case where there shouldn't be variable reassignment


