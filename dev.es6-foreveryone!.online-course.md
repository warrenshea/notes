# Warren's Notes for ES6 for Everyone! (Online Course)
v.20171007
https://courses.wesbos.com/

---
## Legend
@FYI = For reference
@TODO = Need to revisit / clarify
@FILTER = Reference for useful filters

## Table of Contents
Modules 1 - 11: New things with ES6
Modules 12 - : Working with linters, nodeJS,

---

## Module 12: Code Quality with ESLint

###  Module 12.39: Getting Started with ESLint
* ESLint is one of the best linters and has support for all of the new ES6 features
```bash
  npm install npm@latest -g #install latest npm, -g for global
  npm install eslint -g     #install eslint, -g for global
  eslint file.js            #to eslint a file through command line (file.js) 
```
* different eslint settings for project
* `.eslintrc` is your settings
  * written in `json`
  * must use double quotes
```json
  {
    "env": {
      "es6": true,
      "browser": true
    },
    //"extends": "eslint:recommended", 
    "extends": "airbnb", //need to install module first (see Module 12.40)
    //https://eslint.org/docs/rules/
    "rules": {
      "no-console": 0, 
      "no-unused-vars": 1
    },
    "plugins": ["html", "markdown"]
  }
```
* rules can be Off ("off"/0), Warning ("warn"/1), or Error ("error"/2)
* can have 0/1/2,{} where the ,{} is for options

###  Module 12.40: Airbnb ESLint Settings
* [Airbnb ESLint JavaScript Styleguide](https://github.com/airbnb/javascript)
* [Airbnb ESLint ESLint Config](https://github.com/airbnb/javascript/tree/master/packages/eslint-config-airbnb)
* [Airbnb ESLint npm](https://www.npmjs.com/package/eslint-config-airbnb)
* To install, use something like this (up to date one on github)
```bash
  npm install -g eslint-config-airbnb eslint-plugin-jsx-a11y eslint-plugin-import eslint-plugin-react
```
* to automagically fix spacing and other minor items
```bash
esline file.js --fix
```
* your global .eslint file is in your home directory (e.g. ~ or the foldername with your user, e.g. c:\users\username)
* should have trailing comma for the last key in objects

###  Module 12.41: Line and File Specific Settings
* set globals in file so your eslint won't fire on them (e.g. `ga.track()` or `twttr.trackConversion()`)
* At the top of the file, write this to ignore
```javascript
  /* globals twttr ga */
```
* To turn off the linting for something in the file
```javascript
  /* eslint-disable no-extend-native */
```
OR
* Turn off the linting just for the line
```javascript
  /* eslint-disable no-extend-native */
  //offending line
  /* eslint-enable no-extend-native */
```
OR
* Turn off the linting for a chunk of code
```javascript
  /* eslint-disable */
  //offending chunk of code
  /* eslint-enable  */
```

###  Module 12.42: ESLint Plugins
* [dustinspecker](https://github.com/dustinspecker/awesome-eslint)
* Install html and markdown
```json
  {
    "plugins" : [
      "html",
      "markdown"
    ]
  }
```
* `--fix` only works for pure JS files, not HTML or Markdown

###  Module 12.43: ESLint inside Ataom and Sublime Text
* SublimeLinter 3 is a Sublime plugin/framework
* Use Sublime Package Manager to `SublimeLinter`
* Use Sublime Package Manager to `SublimeLinter-contrib-eslint`
* Have to have `eslint` globally installed (see [12.39]())



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
  //use let because they will change
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
      str += string + values[i];
      // returns "My dog's name is Loki and he is 3 years oldundefined", because strings is always 1 longer than values

      str += string + (values[i] || '');
      // returns "My dog's name is Loki and he is 3 years old", this is better than above

      str += `${string} <strong>${values[i] || ''}</strong>`;
      // returns "My dog's name is <strong>Loki</strong> and he is <strong>3</strong> years old"
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
  //string.startsWith();
  string.startsWith('subStringCheck'); //returns true/false, not case sensitive
  string.startsWith('subStringCheck',3); //returns true/false, starts after 3 characters

  //string.endsWith();
  string.endsWith('subStringCheck');
  string.endsWith('subStringCheck',3); //starts the first 3 charcters and checks if it wents with subStringCheck

  //string.includes() //used to be string.contains()

  //string.repeat() 
  function leftPad(string, length = 20) {
    return `${' '.repeat(length - str.length)}${str}`;
  }
```
* @FYI Batman joke :D

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
```javascript
  const details = ['Wes Bos', 123, 'wesbos.com'];

//OLD WAY
  const name = details[0];
  const id = details[1];
  const url = details[2];

//ES6 Way
  const [name, id, website] = details;

//{ } is destructuring for objects
//[] is destructuring for arrays

  const data = 'Basketball,Sports,90210,23,wes,bos,cool';
  const [itemName, category, sku, inventory] = data.split(',');
  //returns array and then deconstruct array
  //if there's extra values in data, it will not be destructured because there are no variables to kepe them

  const team = ['Wes', 'Harry', 'Sarah', 'Keegan', 'Riker'];
  const [captain, assistant, ...players] = team;
  //captain = "Wes"
  //assistant = "Harry"
  //players = ["Sarah,"Keegan","Riker"]
  //...variable is "the rest" operator. We have the captain, assistant and the rest
```

###  Module 5.20: Swapping Variables with Destructuring
* Switching variables (see [2.8](#module-28-arrow-functions-and-this))

###  Module 5.21: Destructuring Functions - Multiple returns and named defaults
```javascript
  function convertCurrency(amount) {
    const converted = {
      USD: amount * 0.76,
      GPB: amount * 0.53,
      AUD: amount * 1.01,
      MEX: amount * 13.30
    };
    return converted;
  }

  const hundo = convertCurrency(100);
  //OLD WAY
  console.log(hundo.AUD);
  console.log(hundo.MEX);
  //ES6
  const {USD, GPB, AUD, MEX} = convertCurrency(100);
  console.log(USD); //returns 76
  //can pick and choose the items you want

//function tipCalc( total = 100, tip = 0.15, tax = 0.13 ) {
  //^ the variables in specific order
  function tipCalc({ total = 100, tip = 0.15, tax = 0.13 } = {}) {
    //^ the variables are destructured, so that the order doesn't matter

    return total + (tip * total) + (tax * total);
  }
  
  const bill = tipCalc({ tip: 0.20, total: 200 });
  //the order can be placed in any way we want
  console.log(bill);
```

## Module 6: Iterables & Looping

###  Module 6.22: The for of loop
* The for of loop loops over iterables (anything that can be looped over like a DOM collection, arguments, array, string, map, set)
```javascript
const cuts ['chuck','brisket','shank','short rib'];

for (let i = 0;i < cuts.length; i++) { //ugly and confusing
  console.log(cuts[i]);
}
  
cuts.forEach((cut) => { //can't use break; or continue;
  console.log(cuts[i]);
});

for (const index in cuts) { //'for in', iterates of item + anything added (which is bad)
  console.log(cuts[index]); 
}

//for of - the best of all 3 worlds and can use it for everything except object
for (const cut of cuts) {
  console.log(cut);
  //can you break/continue
}
```

### Module 6.23: The for of Loop in Action
```javascript
const cuts ['chuck','brisket','shank','short rib'];

//cuts.entries(); // Array Iterator
const meat = cuts.entries();
meat.next(); //provides index and value

for (const cut of cuts.entries()) {
  console.log(cut); //cut is an array 
}

for (const [i,cut] of cuts.entries()) { //destructure
  console.log(`${cut} is the ${i} item`);
  //Chuck is the 1 item
  //Brisket is the 2 item
  //etc.
  //etc.
}

//trying to iterate over
function addUpNumbers() {
  console.log(arguments); //returns [10,23,52,43,34,87,64] list with length

  let total = 0;
  for (num of arguments) {
    total += num;
  }
  return total; //returns total
}
addUpNumbers(10,23,52,43,34,87,64)

const name = 'Warren Shea';
for (char of name) {
  console.log(char); //returns W, then a, then r, etc. etc.
}
```

### Module 6.24: Using for of with Objects
* object.entries() will be available later (in ES2017 and can be polyfilled)
* Alternatives to `for of` with Objects:
```javascript
const cuts ['chuck','brisket','shank','short rib'];

for const cut of Object.keys(cuts)) {
  const value = cuts[cut];
  console.log(value, cut);
}

for (const index in cuts) {
  console.log(cuts[index]); 
}
```

## Module 7: An Array of Array Improvements

###  Module 7.25: Array.from() and Array.of()
* New array method
* Array.from() -> turns something Array-ish (e.g. NodeList) and turn it into an Array
```javascript
  const peopleArray = Array.from(arrayIsh);

  const peopleArray = Array.from(arrayIsh, domNode => {
    return domNode.textContent;
  });

  function sumAll() {
    //arguments is array-ish
    return arguments.reduce((prev,next) => prev + next, 0); //fails
  }
  sumAll(3,3,56353,34343,3,32,34,323,3)

  function sumAll() {
    const nums = Array.from(arguments);
    return nums.reduce((prev,next) => prev + next, 0); //success
  }
  sumAll(3,3,56353,34343,3,32,34,323,3)
```
* Array.of(arguments) -> pass it as many arguments that you want, creates array for every argument that you pass it

###  Module 7.25: Array.find() and Array.findIndex()
* nice utility - might not need to add lodash because of this
* Array.find()
```javascript
  const apiObjectItem = apiObject.find(apiObjectItem => {
    if(apiObjectItem === 'some value') {
      return true;
    }
    return false;
  });
//OR
  const value = 'someValue';
  const apiObjectItem = apiObject.find(apiObjectItem => apiObjectItem.key === value);
```
* Array.findIndex()
```javascript
  const value = 'someValue';
  const apiObjectItemIndex = apiObject.findIndex((apiObjectItem) => {
    if (apiObjectItem.key === value) {
      return true;
    }
    return false;
  });
//OR
  const apiObjectItemIndex = apiObject.findIndex(apiObjectItem => apiObjectItem.key === value);
```

###  Module 7.26: Array.some() and Array.every()
* Array.some(): check items in array to see if some of the items meet the criteria you're looking for
```javascript
  const ages = [32,15,19,12]

  //are there any adults?
  const adultPresent = ages.some(ages => age >= 18);
  //returns true as soon as it succeed (it will return at 32)

```
* Array.every(): check items in array to see if all of the items meet the criteria you're looking for
```javascript
  const ages = [32,15,19,12]

  //is everyone old enough to drink?
  const allOldEnough = ages.every(ages => age >= 19);
  //returns false
```

## Module 8: Say Hello to ...Spread and ...Rest

###  Module 8.28: Spread Operator Introduction

* ...The Spread Operator: Takes every single item from an iterable (anything that can be looped over like a DOM collection, arguments, array, string, map, set) and apply it to the containing Array
```javascript
  ['warren'] //an array with the string "warren"
  //what if I want each character to be an iterable?
  [...'warren'] //=> ["w","a","r","r","e","n"]
/**************************************************************************/
  const featured = ['Deep Dish', 'Pepperoni', 'Hawaiian'];
  const specialty = ['Meatzza', 'Spicy Mama', 'Margherita'];
  
  //ES6 way of making an array of featured, 'veg', specialty
  const pizzas = [...featured, 'veg', ...specialty];
/**************************************************************************/
  //if we wanted to make a duplicate of pizzas,
  const fridayPizzas = pizzas;
  //if you changed fridayPizzas, pizzas would also be changed too! Uh oh!
  //const fridayPizzas = pizzas; is not a COPY, but a reference
  
  //OLD way to duplicate and array
  cost fridayPizzas = [].concat(pizzas);
  //ES6 way
  const fridayPizzas = [...pizzas];
```

###  Module 8.29: Spread Exercise
* Exercise to make each character in a string do something on hover

###  Module 8.30: More Spread Examples
* Spread is an alternative to `Array.from(arrayIsh);`
*
```javascript
  const people = document.querySelectorAll('p'); //return nodeList

  //if you want it to be an array
  const people = Array.from(document.querySelectorAll('p')); //return Array
//OR
  const people = [...document.querySelectorAll('p')]; //return Array
```
* If you wanted to remove an item from an array, but all you have is one reference...then you can do a findIndex and get everything until the index and add it to everything after the index
```javascript
  const comments = [
    { id: 209384, text: 'I love your dog!' },
    { id: 523423, text: 'Cuuute! 🐐' },
    { id: 632429, text: 'You are so dumb' },
    { id: 192834, text: 'Nice work on this wes!' },
  ];
  const id = 632429;
  const commentIndex = comments.findIndex(comment => comment.id === id);
  const newComments = [...comments.slice(0,commentIndex), ...comments.slice(commentIndex + 1)];
```

###  Module 8.31: Spreading into a function
* Combining arrays
```javascript
  const inventors = ['Einstein', 'Newton', 'Galileo'];
  const newInventors = ['Musk', 'Jobs'];

  //if you wanted to merge arrays

  //this will not work
  investors.push(newInvestors); //returns ['Einstein', 'Newton', 'Galileo', ['Musk', 'Jobs']] which is not what you want

  //Old way - weird/hard to understand
  inventors.push.apply(investors, newInvestors);

  //ES6 way
  inventors.push(...newInventors);
/**************************************************************************/
  const name = ['Wes', 'Bos'];

  function sayHi(first, last) {
    alert(`Hey there ${first} ${last}`);
  }

  sayHi(...name);
```

###  Module 8.32: The ...Rest param in Functions and destructuring
* ... for a Spread takes one array and unpacks it into items
* ... for a Rest takes multiple things and packs it into a single array
```javascript
  function convertCurrency(rate, tax, tip, ...amounts) {
    return amounts.map(amount => amount * rate);
  }
  const amounts = convertCurrency(1.54, 10, 23, 52, 1, 56);
/**************************************************************************/
  const runner = ['Wes Bos', 123, 5.5, 5, 3, 6, 35];
  const [name, id, ...runs] = runner; //runs is [5,3,6,35]
```

## Module 9: Object Literal Upgrades

###  Module 9.33: Object Literal Upgrades
```javascript
  //OLD WAY
  const dog = {
    first: first,
    last: last,
    age: age,
    breed: breed,
  }
//EQUALS
  const dog = {
    first,
    last,
    age,
    breed,
  };
/**************************************************************************/
  const modal = {
    create: function() {},
    open: function() {},
    close: function() {},
  }
//EQUALS
  //Note: Don't use => function because of `this` issues
  const modal = {
    create() {},
    open() {},
    close() {},
  }
/**************************************************************************/
  function invertColor(color) {
      return '#' + ("000000" + (0xFFFFFF ^ parseInt(color.substring(1),16)).toString(16)).slice(-6);
  }

  const key = 'pocketColor';
  const value = '#ffc600';

  const tShirt = {
    [key]: value,
    [`${key}Opposite`]: invertColor(value) //create pocketColorOpposite
  };
/**************************************************************************/
  const keys = ['size', 'color', 'weight'];
  const values = ['medium', 'red', 100];

  //Old Way
  const shirt = {
    [keys[0]] = [values[0]];
    [keys[1]] = [values[1]];
    [keys[2]] = [values[2]];
  }
  //ES6 Way
  const shirt = {
    [keys.shift()]: values.shift(),
    [keys.shift()]: values.shift(),
    [keys.shift()]: values.shift(),
  }
```

## Module 10: Promises

###  Module 10.34: Promises
* Promises are often used when you're fetching a JSON or have an API
* Promises is something that will happen in the future but probably not immediately
```javascript
//equal $.getJSON or $.ajax
const posts = fetch(url);
//^queues up the search immediately but doesn't store it in variable, stoes a promise 

posts
  .then(data => data.json())
  .then(data => { console.log(data.)})
  .catch((err) = > { console.error(err)})
//^ chaining format
```

###  Module 10.35: Building your own Promises
```
  const p = new Promise((resolve,reject) => {
    //call resolve() when you finish the promise
    resolve("data"); //don't stop JavaScript from running - start it and when it comes back, deal with it

    //call reject() when there's an error
    reject(Error("Error")); //throw Error object, not just string
  });

  p
    .then(data => {
      console.log(data);
    })
    .catch(err => {
      console.error(err);
    })
```

###  Module 10.36: Chaining Promises + Flow Control
* Simulate a posts and authors database and chain them together
```javascript
  const posts = [
    { title: 'I love JavaScript', author: 'Wes Bos', id: 1 },
    { title: 'CSS!', author: 'Chris Coyier', id: 2 },
    { title: 'Dev tools tricks', author: 'Addy Osmani', id: 3 },
  ];

  const authors = [
    { name: 'Wes Bos', twitter: '@wesbos', bio: 'Canadian Developer' },
    { name: 'Chris Coyier', twitter: '@chriscoyier', bio: 'CSS Tricks and CodePen' },
    { name: 'Addy Osmani', twitter: '@addyosmani', bio: 'Googler' },
  ];

  function getPostById(id) {
    // create a new promise
    return new Promise((resolve, reject) => {
      // using a settimeout to mimick a databse
      setTimeout(() => {
        // find the post we want
        const post = posts.find(post => post.id === id);
        if(post) {
          resolve(post); // send the post back
        } else {
          reject(Error('No Post Was Found!'));
        }
      }, 200);
    });
  }

  function hydrateAuthor(post) {
    // create a new promise
    return new Promise((resolve, reject) => {
      // find the author
      const authorDetails = authors.find(person => person.name === post.author);
      if(authorDetails) {
        // "hydrate" the post object with the author object
        post.author = authorDetails;
        resolve(post);
      } else {
        reject(Error('Can not find the author'));
      }
    });
  }

  getPostById(3)
    .then(post => { //first promise from getPostById
      return hydrateAuthor(post); //second promise from hydrateAuthor
    })
    .then(post => { //when both promises are complete, output post
      console.log(post);
    })
    .catch(err => {
      console.error(err);
    });
```

###  Module 10.37: Working with Multiple Promises
```javascript
   const weather = new Promise((resolve) => {
     setTimeout(() => {
       resolve({ temp: 29, conditions: 'Sunny with Clouds'});
     }, 2000);
   });

   const tweets = new Promise((resolve) => {
     setTimeout(() => {
       resolve(['I like cake', 'BBQ is good too!']);
     }, 500);
   });

   Promise
     .all([weather, tweets]) //waiting for all promises to be resolved before running then
     .then(responses => {
       const [weatherInfo, tweetInfo] = responses;
       console.log(weatherInfo, tweetInfo)
     });
/**************************************************************************/
  //^ Same as above but with real APIs
  //fetch API needs a server
  const postsPromise = fetch('http://wesbos.com/wp-json/wp/v2/posts');
  const streetCarsPromise = fetch('http://data.ratp.fr/api/datasets/1.0/search/?q=paris');

  Promise
    .all([postsPromise, streetCarsPromise])
    .then(responses => {
      return Promise.all(responses.map(res => res.json())) //data could be an arrayBuffer, blobl, json, text, formData. so .json() tells it to return json
    })
    .then(responses => {
      console.log(responses);
    });
```

## Module 11: Symbols

###  Module 11.38: All About Symbols
* 7th Primitive type added to JavaScript
* 6 primitive types: number, string, object, boolean, null, undefined
* Symbol is a unique identifier to avoid naming collision
```javascript
  const wes = Symbol('Wes'); //where 'Wes' is the discriptor
  const person = Symbol('Wes'); 
  wes === person //false
  wes == person //false
```
* Symbols are innumerable so sometimes you store private data in a symbol
```javascript
  const wes = Symbol('Wes');
  const person = Symbol('Wes');

  const classRoom = {
    [Symbol('Mark')] : { grade: 50, gender: 'male' },
    [Symbol('olivia')]: { grade: 80, gender: 'female' },
    [Symbol('olivia')]: { grade: 80, gender: 'female' },
  };

  for (const person in classRoom) {
    console.log(person);
  }

  const syms = Object.getOwnPropertySymbols(classRoom);
  const data = syms.map(sym => classRoom[sym]);
  console.log(data);
```
* @TODO I didn't really understand this but I don't think it matters/I don't think it's that important
