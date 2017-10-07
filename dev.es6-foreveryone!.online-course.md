# ES6 for Everyone!
last updated - Oct 7, 2017
https://courses.wesbos.com/

## Module 5: Destructuring

###  Module 5.18: Destructuring Objects

* Destructuring: A JavaScript expression that allows us to extra data from arrays, objects, and @TODO(something sets)
* Old way VS ES6 Way
```javascript
  const person = {
    first: 'Clark',
    last: 'Kent'
  };

//OLD WAY
  const first = person.first;
  const last = person.last;
  
//ES6 Way
  const { first , last } = person;
  //{ } is destructing syntax
  //make a variable called first and take it from person
```

```javascript
  const superhero = {
    first: 'James',
    last: 'Howlett',
    links: {
      social: {
        twitter: 'https://twitter.com/wolverine',
        facebook: 'https://facebook.com/wolverine',
      }
    }
  };

//OLD WAY
  const twitter = superhero.links.social.twitter;
  const facebook = superhero.links.social.facebook;

//ES6 Way
  const { twitter , facebook } = wes.links.social;
  //Renaming variables
  const { twitter: tweet, facebook: fb } = wes.links.social;

//Set Defaults
  const settings = { width: 300, color: 'black' }  // height, fontSize
  const { width = 100, height = 100, color = 'blue', fontSize = 25} = settings;
  //^ is: sets defaults = overrides
  //settings = { width: 300, color: 'black'};
  //width = 300
  //height = 100
  //color = 'black'
  //fontSize = 25
```

###  Module 5.19: Destructing Arrays


## Module 1: New Variables - Creation, Updating and Scoping

###  Module 1.1: var Scoping refresh

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

* Arrow Functions are not named functions (it is an anonymous function) but you can put it in a variable
```javascript
  const sayMyName = (name) => {console.log(name)};
  sayMyName('warren'); //returns 'warren'
  //Not good for stack traces but good if you're not concerned
```

###  Module 2.7: More Arrow Function Examples
```javascript
  const race = '100m Dash';
  const winners = ['Wally West','Barry Allen','Bart Allen'];
  const win = winners.map((winner,i) => ({name: winner, race: race, place: i + 1}))
  //extra ( ) around {} means it's an object literal
  //@FYI: console.table(win) gives you sweet looking table !

  //another way to write it:
  const win2 = winners.map((winner,i) => ({name: winner, race, place: i + 1}))
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
```javascript
  //what if tax and tip are undefined?
  function calculateBill(total, tax, tip)
    if (tax === undefined) { tax = 0.13; } //or tax = tax || 0.13;
    if (tip === undefined) { tax = 0.15; } //or tip = tip || 0.15;
    return total + (total * tax) + (total * tip);
  }
  calculateBill(100);
//OR
  function calculateBill(total, tax = 0.13, tip = 0.15){
    return total + (total * tax) + (total * tip);
  }
  calculateBill(100);
//OR
  function calculateBill(total, tax = 0.13, tip = 0.15){
    return total + (total * tax) + (total * tip);
  }
  calculateBill(100,undefined,0.25);
  //assume tax=0.13, but the tip is 0.25
```

### Module 2.10: When NOT to use the Arrow Function
```javascript
  // When you really need `this`
  const button = document.querySelector('#pushy');
//button.addEventListener('click', () =>  { // because `this` will be the window
  button.addEventListener('click', function() { //good
    console.log(this);
    this.classList.toggle('on');
  });

  // When you need a method to bind to an object
  const person = {
    points: 23,
  //score() => { //bad because `this` will be the window
  //score(): function { //good
    score() { //even better!
      console.log(this);
      this.points++;
    }
  }

  // When you need to add a prototype method
  class Car {
    constructor(make, colour) {
      this.make = make;
      this.colour = colour;
    }
  }
  const beemer = new Car('bmw', 'blue');
  const subie = new Car('Subaru', 'white');

//Car.prototype.summarize = () => { //bad, because `this` is window
  Car.prototype.summarize = function() { //good
     return `This car is a ${this.make} in the colour ${this.colour}`;
  };

  // When you need arguments object
  //const orderChildren = () => { //bad, arguments will not be passed in properly
  const orderChildren = function() { //good
    const children = Array.from(arguments); 
    return children.map((child, i) => {
      return `${child} was child #${i + 1}`;
    })
    console.log(arguments);
  }
  orderChilden('alan','hal','guy','john','kyle');
```

### Module 2.11: Arrow Functions Exercises
```javascript
  //@FYI Convert Node List to Array
  Array.from(nodeList); //converts nodeList to Array

  //@FYI @FILTER Check if an array item includes a string
  items.filter(item => item.textContent.includes(str));

  //@FYI @FILTER map down things
  items.map(item => item.dataset.time); //gives you data-time attribute

  //@FYI @TODO @FILTER reduce
  items.reduce((value1,value2) => value1+value2,0); //I don't know how this works
```

## Module 3: Template Strings

###  Module 3.12: Template String Introduction
* Dropping variables in a string via Template Strings or Template Literals
```javascript
  let sentance = `backtick ${variable} backtick`;
```

###  Module 3.13: Creating HTML fragments with Template Literals
```javascript
  //@FYI Multiline HTML string with backticks
  let markup = `
    <div class="person">
      <h1>test</h1>
    </div>
  `;

  //@FYI Nest Template Strings
  const dogs = [
    {name: 'Loki', age: 3},
    {name: 'Thor', age: 4}
  ];
  let markup = `
    <ul class="dogs">
      ${dogs.map(dog => `
      <li>${dog.name}</li>
      `).join('')}
    </ul>
  `;
  //.map will return an array, so you need .join('') to make it one string

  //@FYI Conditional (ternary) Operator
  const dogs = [
    {name: 'Loki', age: 3}
  ];
  let markup = `
    ${dogs.name ? `${dogs.name}` : ''}
  `;
  console.log(markup); //Loki

  const cats = [
    {age: 3}
  ];
  let markup = `${cats.name ? `${cats.name}` : ''}`;
  console.log(markup); //(blank)

  //if song.featuring exists, show the value of the variable, otherwise show nothing

  //@FYI Render function
  function renderFunction(keywords) {
    return `
    <ul class="beerKeywords">
      ${beerKeywords.map(keyword => `
      <li>${beer.keywords}</li>
      `).join('')}
    </ul>
    `;
  }
  ${renderFunction(beer.keywords)}
  //if song.featuring exists, show the value of the variable, otherwise show nothing
```

###  Module 3.14: Tagged Template Literals/Strings
*
```javascript
  //BASE EXAMPLE/UNDERSTANDING
  function highlight(strings, ...values) { //...values takes the rest of the arguments
    //strings Array = ["My dog's name is ", " and he is ", "years old"]
    //values Array = ["Loki",3]
    //strings Array always 1 longer than values
  }
  const name = 'Loki';
  const age = 3;
  const sentence = highlight`My dog's name is ${name} and he is ${age} years old`;
  //PRACTICAL USE
  function highlight(strings, ...values) { //...values takes the rest of the arguments
    let str = '';
    strings.forEach((string,i) => {
      str += string + values[i]; // returns "My dog's name is Loki and he is 3 years oldundefined", because strings is always 1 longer than values

      str += string + (values[i] || ''); // returns "My dog's name is Loki and he is 3 years old", this is better than above

      str += `${string} <strong>${values[i] || ''}</strong>`; // returns "My dog's name is <strong>Loki</strong> and he is <strong>3</strong> years old"
      //this is if you want to add formatting to the string
    });
    return str; 
//OR
    let str = '';
    strings.map((string,i) => {
      str += `${string} <strong>${values[i] || ''}</strong>`;
    })
    return str; 
  }
  const name = 'Loki';
  const age = 3;
  const sentence = highlight`My dog's name is ${name} and he is ${age} years old`;
```

###  Module 3.15: Tagged Templates Exercise
*A good use of Template strings is a dictionary/abbreviations example
```javascript
  const dict = {
    HTML: 'Hyper Text Markup Language',
    CSS: 'Cascading Style Sheets',
    JS: 'JavaScript'
  };

  function addAbbreviations(strings, ...values) {
    const abbreviated = values.map(value => {
      if(dict[value]) {
        return `<abbr title="${dict[value]}">${value}</abbr>`
      }
      return value;
    });

    return strings.reduce((sentence, string, i) => {
      return sentence + string + (abbreviated[i] || '');
    }, '');
  }

  const first = 'Wes';
  const last = 'Bos';
  const sentence = addAbbreviations`Hi my name is ${first} ${last} and I love to code ${'JS'}, ${'HTML'} and ${'CSS'} all day and all night long!`

  const bio = document.querySelector('.bio');
  const p = document.createElement('p');
  p.innerHTML = sentence;
  bio.appendChild(p);
```

###  Module 3.16: Sanitizing User Data with Tagged Templates
* Any time you display data from a user, you need to sanitize it
* When you let someone else put malicious code/JavaScript in your site, that's XSS Scripting
* Loaded library called dompurify [dompurify](https://cdnjs.cloudlfare.com/ajax/libs/dompurify/0.8.2/purify.min.js")
```javascript
  function sanitize (strings, ...values) {
    const dirty = strings.reduce((prev,next,i => `${prev}${next}$values[i] || ''}`, ''));
    return DOMpurify.sanitize(dirty)
  }
```

## Module 4: Additional String Improvements

###  Module 4.17: New String Methods
* 4 new methods that help reduce the need for Regex
```
  //string.startsWith('subStringCheck'); //returns true/false, not case sensitive
  //string.startsWith('subStringCheck',3); //returns true/false, starts after 3 characters

  //string.endsWith('subStringCheck');
  //string.endsWith('subStringCheck',3); //starts the first 3 charcters and checks if it wents with subStringCheck

  //string.includes() //used to be string.contains()

  //string.repeat() 
  function leftPad(string, length = 20) {
    return `${' '.repeat(length - str.length)}${str}`;
  }
```
* @FYI Batman joke :D
