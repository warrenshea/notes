# ES6 for Everyone!
last updated - Sept 28, 2017
https://courses.wesbos.com/

## New Variables - Creation, Updating and Scoping

###  Module 1: var Scoping refresh

* ${*var*}
```javascript
var dogYears = age * 7;
console.log(“You are “ + dogYears + “ dog years old!”);
/*is the same as */ console.log(`You are ${dogYears} dog years old!`);
```
* var variables are function scoped, but if there’s no function, it will be block scoped (between { and }) 
* let variables are block scoped
```javascript
let x = 1;
if (x === 1) {
  let x = 2;
  console.log(x); //2...because the "x" variables are different, the "x" variables are scoped differently
}
```
* let variables are made to be updated
* const variables are never to be updated
* Object.freeze (not ES6): used to freeze the variable from being changed
```javascript
const person = {
  name: 'warren',
  age: 35
}
const warren = Object.freeze(person);
warren.age = 30;
console.log(warren.age); //35
```
