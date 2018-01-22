# Warren's Notes for ES6 for Everyone! (Online Course)
v.20171219\
https://courses.wesbos.com/

---
## Legend
&#35;REFERENCE = For reference\
&#35;TODO = Need to revisit / clarify\
&#35;FILTER = Reference for useful filters\
&#35;BESTPRACTICE = Best Practice

## Table of Contents

* [Module 01: New Variables - Creation, Updating and Scoping](#module-01-new-variables---creation-updating-and-scoping)
* [Module 02: Function Improvements: Arrows and Default Arguments](#module-02-function-improvements-arrows-and-default-arguments)
* [Module 03: Template Strings](#module-03-template-strings)
* [Module 04: Additional String Improvements](#module-04-additional-string-improvements)
* [Module 05: Destructuring](#module-05-destructuring)
* [Module 06: Iterables & Looping](#module-06-iterables--looping)
* [Module 07: An Array of Array Improvements](#module-07-an-array-of-array-improvements)
* [Module 08: Say Hello to ...Spread and ...Rest](#module-08-say-hello-to-spread-and-rest)
* [Module 09: Object Literal Upgrades](#module-09-object-literal-upgrades)
* [Module 10: Promises](#module-10-promises)
* [Module 11: Symbols](#module-11-symbols)
* [Module 12: Code Quality with ESLint](#module-12-code-quality-with-eslint)
* [Module 13: JavaScript Modules and Using npm](#module-13-javascript-modules-and-using-npm)
* [Module 14: ES6 Tooling](#module-14-es6-tooling)
* [Module 15: Classes](#module-15-classes)
* [Module 16: Generators](#module-16-generators)
* [Module 17: Proxies](#module-17-proxies)
* [Module 18: Sets and WeakSets](#module-18-sets-and-weaksets)
* [Module 19: Map and Weak Map](#module-19-map-and-weak-map)
* [Module 20: Async + Await Flow Control](#module-20-async--await-flow-control)
* [Module 21: ES7, ES8 + Beyond](#module-21-es7-es8--beyond)
---


## Module 01: New Variables - Creation, Updating and Scoping

###  Module 01.01: var Scoping refresh

* `var` variables are function scoped, but if there’s no function, it will be block scoped (between { and } )

###  Module 01.02: `let` VS `const`

* `let` variables are block scoped
    ```javascript
    let x = 1;
    if (x === 1) {
      let x = 2;
    }
    console.log(x); //1...because the "x" variables are different, the "x" variables are scoped differently
    ```

* `let` variables are made to be updated
  `const` variables are never to be updated

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

###  Module 01.03: `let` and `const` in Real World

* Immediately-invoked function expression - [iife](https://en.wikipedia.org/wiki/Immediately-invoked_function_expression)
    ```javascript
    (function () { /* ... */ })();
    (function () { /* ... */ }());
    (() => { /* ... */ })(); // With ES6 arrow functions (though parentheses only allowed on outside)
    ```
    What it does: a function that runs itself immediately and creates a scope where nothing is going to leak into the parent scope (e.g. global scope of the window)

* with `let` and `const`, you don't need to do this because they're block scoped
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
    ```

    ```javascript
    for (let i = 0; i < 10; i++) {
      console.log(i); //returns 0, then 1, then 2, ... to 10 each loop
      setTimeOut(function() {
        console.log("The number is " + i); //returns "The number is 1", "The number is 2", etc. **
      },1000);
    }
    //** this i variable is now scoped to the loop
    ```

###  Module 01.04: Temporal Dead Zone

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

###  Module 01.05: Is `var` Dead? What should I use?

* Using `let` / `const` / `var` : the [Mathias Bynens](https://mathiasbynens.be/notes/es6-const) & Wes Bos approach &#35;BESTPRACTICE
  * use `const` by default
  * only use `let` if rebinding is needed
  * (`var` shouldn’t be used in ES6)

* Using `let` / `const` / `var` : the [Kyle Simpson](https://github.com/getify/You-Dont-Know-JS/tree/master/es6%20%26%20beyond) approach
  * use `var` for top-level variables that are shared across many (especially larger) scopes
  * use `let` for localized variables in smaller scopes
  * refactor `let` to `const` only after some code has been written and you're reasonably sure you've got a case where there shouldn't be variable reassignment

## Module 02: Function Improvements: Arrows and Default Arguments

###  Module 02.06: Arrow Functions Introduction

* 3 benefits:
  * More concise
  * Implicit returns (nifty one-liners)
  * Doesn't rebind value of `this` when you use arrow function inside another function

* Example
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

* If you had no parameter to return, you can take out the `name` parameter
    ```javascript
    const name = ['warren', 'will', 'wally'];
    const fullNames5 = names.map(() => `two shea`);
    console.log(fullNames); //returns ["two shea", "two shea", "two shea"]
    ```

* Named Function (REFERENCE only)
    ```javascript
    function thisIsANamedFunction(x) {
      console.log(x);
    }
    //Useful for debugging, to see the function that might cause an error
    ```

* Arrow Functions are not named functions (it is an anonymous function) but you can put it in a variable
    ```javascript
    //ES6
    const sayMyName = (name) => {console.log(name)};
    //EQUALS this for ES2015
    var sayMyName = function sayMyName(name) {
      console.log(name);
    };

    sayMyName('warren'); //returns 'warren'
    ```

###  Module 02.07: More Arrow Function Examples

*
    ```javascript
    const race = '100m Dash';
    const winners = ['Wally West','Barry Allen','Bart Allen'];
    const win = winners.map((winner,i) => ({name: winner, race: race, place: i + 1}))
    ```

    ```javascript
    const win2 = winners.map((winner,i) => ({name: winner, race, place: i + 1}))
    //just say "race", and it will automatically mean "race: race"
    ```

    ```javascript
    const ages = [3,34,62,31,25,15,46,76]
    //const old = ages.filter(age => (age >= 60)); //returns [62,76]
    const old = ages.filter(age => age >= 60); //returns [62,76] #BESTPRACTICE #FILTER
    ```

###  Module 02.08: Arrow Functions and `this`

*
    ```javascript
      var box = document.querySelector('.box'); //equals $('.box');
      box.addEventListener('click', () => {
        console.log(this) // this is the window!
      }); //this is bad!

      box.addEventListener('click', function() {
        this.classList.toggle('add-class');
        setTimeout(() => {
          this.classList.toggle('add-second-class');
          //where this is inherited from above (where add-class is logged), as opposed to doing self = this;
        }, 500);
      });
    ```

    ```javascript
      //#REFERENCE #BESTPRACTICE
      //Switch values in ES6
      let first = "first";
      let second = "second";
      [first,second] = [second,first];
      //use let because they will change
    ```

###  Module 02.09: Default Function Arguments

*
    ```javascript
    //what if tax and tip are undefined?
    function calculateBill(total, tax, tip) {
      if (tax === undefined) { tax = 0.13; } //or tax = tax || 0.13;
      if (tip === undefined) { tax = 0.15; } //or tip = tip || 0.15;
      return total + (total * tax) + (total * tip);
    }
    calculateBill(100);
    ```

    ```javascript
    //OR this, where tax and tip have defaults
    function calculateBill(total, tax = 0.13, tip = 0.15){
      return total + (total * tax) + (total * tip);
    }
    calculateBill(100);
    ```

    ```javascript
    //OR this, where tax and tip have defaults, but can be overridden by the function
    function calculateBill(total, tax = 0.13, tip = 0.15){
      return total + (total * tax) + (total * tip);
    }
    calculateBill(100,undefined,0.25);
    //assume tax=0.13, but the tip is 0.25
    ```

### Module 02.10: When NOT to use the Arrow Function

*
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
    orderChildren('alan','hal','guy','john','kyle');
    ```

### Module 02.11: Arrow Functions Exercises

*
    ```javascript
    //#REFERENCE Convert Node List to Array
    Array.from(nodeList); //converts nodeList to Array
    ```

    ```javascript
    //#REFERENCE #FILTER Check if an array item includes a string
    items.filter(item => item.textContent.includes(str));
    ```

    ```javascript
    //#REFERENCE #FILTER map down things
    items.map(item => item.dataset.time); //gives you data-time attribute
    ```

    ```javascript
    //#REFERENCE #TODO #FILTER reduce
    items.reduce((value1,value2) => value1+value2,0); //I don't know how this works
    ```

## Module 03: Template Strings

###  Module 03.12: Template String Introduction
* Dropping variables in a string via Template Strings or Template Literals
    ```javascript
    let sentence = `backtick ${variable} backtick`;
    ```

###  Module 03.13: Creating HTML fragments with Template Literals
*
    ```javascript
    //#REFERENCE Multiline HTML string with backticks
    let markup = `
      <div class="person">
        <h1>test</h1>
      </div>
    `;
    ```

    ```javascript
    //#REFERENCE Nest Template Strings
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
    ```

    ```javascript
    //#REFERENCE Conditional (ternary) Operator
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
    ```

    ```javascript
    //#REFERENCE Render function
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
    ```

###  Module 03.14: Tagged Template Literals/Strings
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

      //OPTION A
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

      //OPTION B
      let str = '';
      strings.map((string,i) => {
        str += `${string} <strong>${values[i] || ''}</strong>`;
      })
      return str;

    }
    ```

###  Module 03.15: Tagged Templates Exercise
* A good use of Template strings is a dictionary/abbreviations example
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

###  Module 03.16: Sanitizing User Data with Tagged Templates
* Any time you display data from a user, you need to sanitize it
* When you let someone else put malicious code/JavaScript in your site, that's XSS Scripting
* Loaded library called dompurify [dompurify](https://cdnjs.cloudlfare.com/ajax/libs/dompurify/0.8.2/purify.min.js")
    ```javascript
    function sanitize (strings, ...values) {
      const dirty = strings.reduce((prev,next,i => `${prev}${next}$values[i] || ''}`, ''));
      return DOMpurify.sanitize(dirty)
    }
    ```

## Module 04: Additional String Improvements

###  Module 04.17: New String Methods
* 4 new methods that help reduce the need for Regex
    ```javascript
    //string.startsWith();
    string.startsWith('subStringCheck'); //returns true/false, not case sensitive
    string.startsWith('subStringCheck',3); //returns true/false, starts after 3 characters
    ```

    ```javascript
    //string.endsWith();
    string.endsWith('subStringCheck');
    string.endsWith('subStringCheck',3); //starts the first 3 charcters and checks if it wents with subStringCheck
    ```

    ```javascript
    //string.includes() //used to be string.contains()
    ```

    ```javascript
    //string.repeat()
    function leftPad(string, length = 20) {
      return `${' '.repeat(length - str.length)}${str}`;
    }
    ```
* &#35;REFERENCE Batman joke :D

## Module 05: Destructuring

###  Module 05.18: Destructuring Objects
* Destructuring: A JavaScript expression that allows us to extra data from arrays, objects, and #TODO(something sets)
* Old way VS ES6 Way
    ```javascript
    const person = {
      first: 'Clark',
      last: 'Kent'
    };

    //OLD WAY
    const first = person.first;
    const last = person.last;

    //ES6 Way #BESTPRACTICE
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

    //ES6 Way ##BESTPRACTICE
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

###  Module 05.19: Destructing Arrays
*
    ```javascript
    const details = ['Wes Bos', 123, 'wesbos.com'];

    //OLD WAY
    const name = details[0];
    const id = details[1];
    const url = details[2];

    //ES6 Way #BESTPRACTICE
    const [name, id, website] = details;

    //#REFERENCE
    //{ } is destructuring for objects
    //[] is destructuring for arrays

    const data = 'Basketball,Sports,90210,23,wes,bos,cool';
    const [itemName, category, sku, inventory] = data.split(',');
    //returns array and then deconstruct array
    //if there's extra values in data, it will not be destructured because there are no variables to keep them

    const team = ['Wes', 'Harry', 'Sarah', 'Keegan', 'Riker'];
    const [captain, assistant, ...players] = team;
    //captain = "Wes"
    //assistant = "Harry"
    //players = ["Sarah,"Keegan","Riker"]
    //...variable is "the rest" operator. We have the captain, assistant and the rest
    ```

###  Module 05.20: Swapping Variables with Destructuring
* Switching variables (see [2.8](#module-28-arrow-functions-and-this))

###  Module 05.21: Destructuring Functions - Multiple returns and named defaults
*
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
    ```

    ```javascript
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

## Module 06: Iterables & Looping

###  Module 06.22: The for of loop
* The for of loop loops over iterables (anything that can be looped over like a DOM collection, arguments, array, string, map, set)
    ```javascript
    const cuts = ['chuck','brisket','shank','short rib'];
    ```

    ```javascript
    //ugly and confusing
    for (let i = 0;i < cuts.length; i++) {
      console.log(cuts[i]);
    }
    ```

    ```javascript
    //can't use break; or continue;
    cuts.forEach((cut,i) => {
      console.log(cuts[i]);
    });
    ```

    ```javascript
    //'for in', iterates of item + anything added (which is bad)
    for (const index in cuts) {
      console.log(cuts[index]);
    }
    ```

    ```javascript
    //for of - the best of all 3 worlds and can use it for everything except object #BESTPRACTICE
    for (const cut of cuts) {
      console.log(cut);
      //can you break/continue
    }
    ```

### Module 06.23: The for of Loop in Action
*
    ```javascript
    const cuts = ['chuck','brisket','shank','short rib'];

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
    ```

    ```javascript
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
    ```

    ```javascript
    const name = 'Warren Shea';
    for (char of name) {
      console.log(char); //returns W, then a, then r, etc. etc.
    }
    ```

### Module 06.24: Using for of with Objects
* object.entries() will be available later (in ES2017 and can be polyfilled)
* Alternatives to `for of` with Objects:
    ```javascript
    const cuts = ['chuck','brisket','shank','short rib'];

    for const cut of Object.keys(cuts)) {
      const value = cuts[cut];
      console.log(value, cut);
    }

    for (const index in cuts) {
      console.log(cuts[index]);
    }
    ```

## Module 07: An Array of Array Improvements

###  Module 07.25: Array.from() and Array.of()
* New array method
* Array.from() -> turns something Array-ish (e.g. NodeList) and turn it into an Array
    ```javascript
    const peopleArray = Array.from(arrayIsh);

    const peopleArray = Array.from(arrayIsh, domNode => {
      return domNode.textContent;
    });
    ```

    ```javascript
    function sumAll() {
      //arguments is array-ish
      return arguments.reduce((prev,next) => prev + next, 0); //fails
    }
    sumAll(3,3,56353,34343,3,32,34,323,3)
    ```

    ```javascript
    function sumAll() {
      const nums = Array.from(arguments);
      return nums.reduce((prev,next) => prev + next, 0); //success
    }
    sumAll(3,3,56353,34343,3,32,34,323,3)
    ```
* Array.of(arguments) -> pass it as many arguments that you want, creates array for every argument that you pass it

###  Module 07.25: Array.find() and Array.findIndex()
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

###  Module 07.26: Array.some() and Array.every()
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

## Module 08: Say Hello to ...Spread and ...Rest

###  Module 08.28: Spread Operator Introduction

* ...The Spread Operator: Takes every single item from an iterable (anything that can be looped over like a DOM collection, arguments, array, string, map, set) and apply it to the containing Array
    ```javascript
    ['warren'] //an array with the string "warren"
    //what if I want each character to be an iterable?
    [...'warren'] //=> ["w","a","r","r","e","n"]

    ```

    ```javascript
    const featured = ['Deep Dish', 'Pepperoni', 'Hawaiian'];
    const specialty = ['Meatzza', 'Spicy Mama', 'Margherita'];

    //ES6 way of making an array of featured, 'veg', specialty
    const pizzas = [...featured, 'veg', ...specialty];
    ```

    ```javascript
    //if we wanted to make a duplicate of pizzas,
    const fridayPizzas = pizzas;
    //if you changed fridayPizzas, pizzas would also be changed too! Uh oh!
    //const fridayPizzas = pizzas; is not a COPY, but a reference

    //OLD way to duplicate and array
    cost fridayPizzas = [].concat(pizzas);
    //ES6 way
    const fridayPizzas = [...pizzas];
    ```

###  Module 08.29: Spread Exercise
* Exercise to make each character in a string do something on hover

###  Module 08.30: More Spread Examples
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

###  Module 08.31: Spreading into a function
* Combining arrays
    ```javascript
    const inventors = ['Einstein', 'Newton', 'Galileo'];
    const newInventors = ['Musk', 'Jobs'];

    //if you wanted to merge arrays

    //this will not work
    investors.push(newInvestors); //returns ['Einstein', 'Newton', 'Galileo', ['Musk', 'Jobs']] which is not what you want

    //Old way - weird/hard to understand
    inventors.push.apply(investors, newInvestors);

    //ES6 way #BESTPRACTICE
    inventors.push(...newInventors);
    ```

    ```javascript
    const name = ['Wes', 'Bos'];

    function sayHi(first, last) {
      alert(`Hey there ${first} ${last}`);
    }

    sayHi(...name);
    ```

###  Module 08.32: The ...Rest param in Functions and destructuring
* ... for a Spread takes one array and unpacks it into items
* ... for a Rest takes multiple things and packs it into a single array
    ```javascript
    function convertCurrency(rate, tax, tip, ...amounts) {
      return amounts.map(amount => amount * rate);
    }
    const amounts = convertCurrency(1.54, 10, 23, 52, 1, 56);
    ```

    ```javascript
    const runner = ['Wes Bos', 123, 5.5, 5, 3, 6, 35];
    const [name, id, ...runs] = runner; //runs is [5,3,6,35]
    ```

## Module 09: Object Literal Upgrades

###  Module 09.33: Object Literal Upgrades
*
    ```javascript
    //OLD WAY
    const dog = {
      first: first,
      last: last,
      age: age,
      breed: breed,
    };
    //EQUALS (#BESTPRACTICE)
    const dog = {
      first,
      last,
      age,
      breed,
    };
    ```


    ```javascript
    const modal = {
      create: function() {},
      open: function() {},
      close: function() {},
    };
    //EQUALS
    //Note: Don't use => function because of `this` issues
    const modal = {
      create() {},
      open() {},
      close() {},
    };
    ```

    ```javascript
    function invertColor(color) {
      return '#' + ("000000" + (0xFFFFFF ^ parseInt(color.substring(1),16)).toString(16)).slice(-6);
    }

    const key = 'pocketColor';
    const value = '#ffc600';

    const tShirt = {
      [key]: value,
      [`${key}Opposite`]: invertColor(value) //create pocketColorOpposite
    };
    ```

    ```javascript
    const keys = ['size', 'color', 'weight'];
    const values = ['medium', 'red', 100];

    //Old Way
    const shirt = {
      [keys[0]] = [values[0]];
      [keys[1]] = [values[1]];
      [keys[2]] = [values[2]];
    };
    //ES6 Way
    const shirt = {
      [keys.shift()]: values.shift(),
      [keys.shift()]: values.shift(),
      [keys.shift()]: values.shift(),
    };
    ```

## Module 10: Promises

###  Module 10.34: Promises
* Promises are often used when you're fetching a JSON or have an API
* Promises is something that will happen in the future but probably not immediately
    ```javascript
    //equal $.getJSON or $.ajax
    const posts = fetch(url);
    //^queues up the search immediately but doesn't store it in variable, stores a promise

    posts
      .then(data => data.json())
      .then(data => { console.log(data.)})
      .catch((err) = > { console.error(err)})
    //^ chaining format #REFERENCE #BESTPRACTICE
    ```

###  Module 10.35: Building your own Promises
*
    ```javascript
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
          // using a setTimeout to mimick a database
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
*
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
    ```

    ```javascript
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
    //(wes === person) returns false
    //(wes == person) returns false
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
* &#35;TODO I didn't really understand this but I don't think it matters/I don't think it's that important

## Module 12: Code Quality with ESLint

###  Module 12.39: Getting Started with ESLint
* ESLint is one of the best linters and has support for all of the new ES6 features
    ```shell
    npm install npm@latest -g #install latest npm, -g for global
    npm install eslint -g     #install eslint, -g for global
    eslint file.js            #to eslint a file through command line (file.js)
    ```
* different eslint settings for project
* `.eslintrc` is your settings
  * written in `json`
  * must use double quotes
* Example:
    ```javascript
    {
      "env": {
        "es6": true,
        "browser": true
      },
      /*"extends": "eslint:recommended", */
      "extends": "airbnb", /*need to install module first (see Module 12.40)*/
      /*https://eslint.org/docs/rules/*/
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
    ```shell
    npm install -g eslint-config-airbnb eslint-plugin-jsx-a11y eslint-plugin-import eslint-plugin-react
    ```
* to automagically fix spacing and other minor items
    ```shell
    eslint file.js --fix
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

###  Module 12.43: ESLint inside Atom and Sublime Text
* SublimeLinter 3 is a Sublime plugin/framework
* Use Sublime Package Manager to `SublimeLinter`
* Use Sublime Package Manager to `SublimeLinter-contrib-eslint`
* Have to have `eslint` globally installed (see [12.39](#module-1239-getting-started-with-eslint))
* In Command Palette for Sublime, `SublimeLinter: Choose Lint Mode`, and choose Background, Load/Save, Save only, Manual
* Red dots on the sidebar to indicate errors
* Atom Instructions (skipped)

###  Module 12.44: Only Allow ESLint Passing Code into your git repos
* there's a folder in `.git` called hooks which is things that run before someone commits
* Delete hooks/commit.msg and copy everything from [wesbos/commit-msg](https://gist.github.com/wesbos/8aec9d2ff7f7cf9dd65ca2c20d5dfc23)
* The commit will be denied if the ESLint fails

## Module 13: JavaScript Modules and Using npm

###  Module 13.45: JavaScript Modules and WebPack 2 Tooling Setup
* JavaScript Module - a file with one or many functions inside of it, you can make the functions available to other files
* `import slug from 'slug';` as an example
* `package.json` to install external dependencies from npm
* use webpack to bundle up all JavaScript
* when you install npm packages, your package.json will be updated
* if you delete `node_modules`, you can use `npm install` and it will re-install your dependencies
* look into: `insane`, `jsonp`, `lodash`, `slug` ?
* `babel` will take your ES6 code and convert it to ES5 and make it work in all browsers
* `webpack.config.js` in root folder (with `package.json`) - see `\es6.io\13 - JavaScript Modules and Using npm\es6modules-FINISHED` on local computer
* `npm run build` where, in `package.json`
    ```json
    "scripts": {
      "build": "webpack --progress --watch"
    }
    ```

###  Module 13.46: Creating your own Modules
* how to get config.js' variable? in app.js
    ```javascript
    //app.js
    import apiKey from './src/config';
    ```
but this only imports, we need to export
* in `config.js`
    ```javascript
    //config.js
    const apiKey = 'abc123';
    export default apiKey; //don't use this, use what's below
    ```
* don't use the above, this (below) is better
* any file can only have 1 default export, but you can have multiple named exports
    ```javascript
    //app.js
    //Named export - must import it the way it's exported
    export const apiKey = 'abc123';
    //OR
    const age = 3
    const dog = 'Loki';
    export { age, dog };
    ```
* if you want to import Named export,
    ```javascript
    //config.js
    import { apiKey, age, dog } from './src/config';
    ```
* Can also export functions:
    ```javascript
    //app.js
    export function sayHi(name) {
      console.log("Hello there ${name}");
    }
    ```

    ```javascript
    //config.js
    import { apiKey, age, dog, sayHi } from './src/config';
    ```
* Further Reading: [Mozilla export](https://developer.mozilla.org/en-US/docs/web/javascript/reference/statements/export)
* Renaming variables
    ```javascript
    //config.js
    import { apiKey as key, age, dog, sayHi } from './src/config';
    ```

    ```javascript
    //app.js
    const age = 3
    const dog = 'Loki';
    export { age as old, dog };
    ```
* Readability
    ```javascript
    //config.js
    import {
      apiKey as key,
      age,
      dog,
      sayHi
    } from './src/config';
    ```

###  Module 13.47: More ES6 Module Practice
* Example: gravatar
* Create nice and tidy modules, put functions in their own files

## Module 14: ES6 Tooling

###  Module 14.48: Tool-Free Modules with SystemJS (+bonus BrowserSync setup)
* Webpack, SystemJS are bundlers
* jspm works on top of npm
* jspm can run in the browser
* install BrowserSync
    ```shell
    npm install --save-dev browser-sync
    ```

    ```javascript
  //package.json
  "scripts": {
    "server": "browser-sync start --director --server --files '*.js, *.html, *.css'"
  }
    ```

###  Module 14.49: All About Babel + npm scripts
* Babel is a JavaScript compiler/transpiler, converts to ES5 to ensure ES6 code can be interpreted by older browsers
* `npm install --save-dev babel-cli@next` if it's version 7+, you don't need @next
    ```javascript
    //package.json
    "scripts": {
      "babel": "babel app.jst--watch --out-file app-compiled.js"
    }
    ```
* `npm install --save-dev babel-preset-env@next` works like auto-prefixer in CSS. Tell it what browsers you want to support
* You can have a `.babelrc` file but Wes Bos likes the config in package.json...AND SO DO I NOW!
    ```javascript
    "dependencies": {
    },
    "babel": {
      /*takes all options the .babelrc file has*/
      "presets": [
        ["env", {
          "targets": {
            "browsers": [
              "last 2 versions",
              "safari >= 7"
            ]
          }
        }]
      ],
      "plugins": [
        "pluginExample"
      ]
    }
    ```

###  Module 14.50: Polyfilling ES6 for Older Browsers
* Babel won't confirm Array.from() so you do a Polyfill
* Polyfill: If the browser does not have it, we must recreate it with regular JavaScript
* Babel has a polyfill
    ```javascript
    import 'babel-polyfill';
    ```
* Polyfill.io - dynamically generates JavaScript file based on browser
    ```html
    <script src="https://cdn.polyfill.io/v2/polyfill.min.js"></script>
    ```
* Polyfill.io - you can tailor your own polyfill

## Module 15: Classes

###  Module 15.51: Prototypal Inheritance Review
*
    ```javascript
    function Dog(name,breed) { //capital D means Constructor function
      this.name = name;
      this.breed = breed;
    }
    const loki = new Dog('Loki',"Pomeranian");
    ```
* Prototypal Inheritance is when you put a method on the original constructor, it will be inherited by the rest
    ```javascript
    function Dog(name,breed) { //capital D means Constructor function
      this.name = name;
      this.breed = breed;
    }
    Dog.prototype.bark = function() {
      console.log(`Bark! My name is ${this.name}`);
    }
    const loki = new Dog('Loki',"Pomeranian");
    loki.bark(); //`Bark! My name is Loki`
    ```

###  Module 15.52: Say Hello to Classes
* Class Delcaration
    ```javascript
    class Dog {
    }
    ```
* Class Expression (Wes Bos preferred!)
    ```javascript
    cost Dog = class {
    }
    ```
* Expanding on the Class Declaration
    ```javascript
    class Dog {
      constructor(name,freed) { //when someone creates a new version
        this.name = name;
        this.breed = breed;
      } //NOTE: NO COMMA!
      bark() {}
      cuddle() {}
      static info() {} //static method - can only call it on Dog directly - useful as factor methods, conversion methods, and general class helper methods
      get description() { //not a method, a property
        return `${name} is a ${breed}`;
      }
      set nickname(value) {
        this.nick = value.trim();
      }
      get nicknames() {
        return this.nick;
      }
    }
    ```

###  Module 15.53: Extending Classes and using super()
*
    ```javascript
    class Animal {
      constructor(name) {
        this.name = name;
        this.thirst = 100;
        this.belly = [];
      }
      drink() {
        this.thirst -= 10;
        return this.thirst;
      }
      eat(food) {
        this.belly.push(food);
        return this.belly;
      }
    }

    class Dog extends Animal {
      constructor(name, breed) {
        super(name); //Call the thing you're extending first

        this.breed = breed;
      }
      bark() {
        console.log('Bark bark I\'m a dog');
      }
    }

    const rhino = new Animal('Rhiney');
    const snickers = new Dog('Snickers', 'King Charles');
    ```

###  Module 15.54: Extending Arrays with Classes for Custom Collections
*
    ```javascript
    class MovieCollection extends Array {
      constructor(name, ...items) { //name of MovieCollect, then items
        super(...items); //extending Array constructor with a "the rest"
        this.name = name;
      }
      add(movie) {
        this.push(movie);
      }
      topRated(limit = 10) {
        return this.sort((a, b) => (a.stars > b.stars ? -1 : 1)).slice(0, limit);
      }
    }

    const movies = new MovieCollection('Wes\'s Fav Movies',
      { name: 'Bee Movie', stars: 10 },
      { name: 'Star Wars Trek', stars: 1 },
      { name: 'Virgin Suicides', stars: 7 },
      { name: 'King of the Road', stars: 8 }
    );

    movies.add({ name: 'Titanic', stars: 5 });
    ```
* for in will iterate over everything (it will iterate name, then the movies)
* for of will only iterate over the iterables (it will only iterate over the movies)

## Module 16: Generators

###  Module 16.55: Introducing Generators
* functions run top to bottom
* generator functions (generators) is a function you can start/stop/pause/pass additional information at a later time
* `function*` to make a generator function, `yield` is a return - it will return the item until the function is called again
* function will need to be
    ```javascript
    function* listPeople() {
      yield 'Wes';
      yield 'Kait';
      yield 'Snickers';
    }

    const people = listPeople();

    console.log(people); //tells us nothing
    people.next(); //returns value: "Wes", done: false
    people.next(); //returns value: "Kai", done: false
    ```

    ```javascript
    const inventors = [
      { first: 'Albert', last: 'Einstein', year: 1879 },
      { first: 'Isaac', last: 'Newton', year: 1643 },
      { first: 'Galileo', last: 'Galilei', year: 1564 },
      { first: 'Marie', last: 'Curie', year: 1867 },
      { first: 'Johannes', last: 'Kepler', year: 1571 },
      { first: 'Nicolaus', last: 'Copernicus', year: 1473 },
      { first: 'Max', last: 'Planck', year: 1858 },
    ];

    function* loop(arr) {
      console.log(inventors);
      for (const item of arr) {
        yield item;
      }
    }

    const inventorGen = loop(inventors);
    //investorGen won't return anything
    investorGen.next().value; //returns { first: 'Albert', last: 'Einstein', year: 1879 }

    ```

###  Module 16.56: Using Generators for Ajax Flow Control
* use case for Generators is waterfall-like AJAX request (e.g. /search/wes -> /user/1223 -> /photo/456)
    ```javascript
    function ajax(url) {
      fetch(url).then(data => data.json()).then(data => dataGen.next(data))
    }

    function* steps() {
      console.log('fetching beers');
      const beers = yield ajax('http://api.react.beer/v2/search?q=hops&type=beer');
      console.log(beers);

      console.log('fetching wes');
      const wes = yield ajax('https://api.github.com/users/');
      console.log(wes);

      console.log('fetching fat joe');
      const fatJoe = yield ajax('https://api.discogs.com/artists/51988');
      console.log(fatJoe);
    }

    const dataGen = steps(); //on page load, create dataGen
    dataGen.next(); // kick it off
    //after that, the ajax function continues the .next() and continues the steps() function
    ```

###  Module 16.57: Looping Generators with for of
*
    ```javascript
    function* lyrics() {
      yield `But don't tell my heart`;
      yield `My achy breaky heart`;
      yield `I just don't think he'd understand`;
      yield `And if you tell my heart`;
      yield `My achy breaky heart`;
      yield `He might blow up and kill this man`;
    }

    const achy = lyrics();
    for (const line of achy) {
      console.log(line);
    }
    ```

## Module 17: Proxies

###  Module 17.58: What are Proxies?
* Proxies allow you to overwrite default behavior for object's default behavior
    ```javascript
    const person = { name: 'Wes', age: 100 };
    const personProxy = new Proxy(person, {} //proxy takes 2 arguments (target, which object you want to proxy - and then handler, which operations you wish to rewrite)
      get(target, name) { //"a trap" - rewrites the operation
        // console.log('someone is asking for ', target, name);
        return target[name].toUpperCase();
      },
      set(target, name, value) { //"a trap" - rewrites the operation
        if(typeof value === 'string') {
          target[name] = value.trim().toUpperCase() + '✂️';
        }
      }
    });

    personProxy.name = 'Wesley';
    ```

###  Module 17.59: Another Proxy Example
*
    ```javascript
    const phoneHandler = {
      set(target, name, value) {
        target[name] = value.match(/[0-9]/g).join(''); //combines all digits (as string)
      },
      get(target, name) {
        return target[name].replace(/(\d{3})(\d{3})(\d{4})/, '($1)-$2-$3'); //when you get the #, it will be (123)-123-1234 format
      }
    }

    const phoneNumbers = new Proxy({}, phoneHandler);
    ```

###  Module 17.60: Using Proxies to combat silly errors
* example to fix issues with incorrect variable names (e.g. normalize them all the lowercase)

## Module 18: Sets and WeakSets

###  Module 18.61: Sets
* Set is a unique array (can only add the same item once) with a nice API for managing the items inside
* Different from array because you can't access items individually and not index-based. It's a list of items you can add to/remove from.
    ```javascript
    const people = new Set();
    people.add('Wes');
    people.add('Snickers');
    people.add('Kait');
    console.log(people.size); //returns 3
    console.log(people); //returns Set {"Wes","Snickers","Kait"}
    console.log(people.delete('Wes')); //deletes 'Wes'
    console.log(people.size); //returns 2
    console.log(people.clear()); //gives us empty set
    console.log(people.values()); //SetIterator {"Wes, "Snickers", "Kait"} (a Generator)
    const it = people.values()
    it.next() //returns Object {values: "Snickers", done:false}
    it.next() //returns Object {values: "Kait", done:false}
    it.next() //returns Object {values: undefined, done:true}
    //can put it in a for of loop
    for (const person of people) {
      console.log(person);
    }
    people.keys(); // = people.values()
    people.entries(); //returns {["Snickers","Snickers"],["Kait","Kait"],}

    const students = new Set(['Wes', 'Kara', 'Tony']);
    students.has('Tony'); //returns true
    students.has('Wess'); //returns false

    const dogs = ['Snickers', 'Sunny'];
    const dogSet = new Set(dogs);
    ```

###  Module 18.62: Understanding Sets with Brunch
*
    ```javascript
    const brunch = new Set();
    // as people start coming in
    brunch.add('wes');
    brunch.add('Sarah');
    brunch.add('Simone');
    // ready to open!
    const line = brunch.values(); //SetIterator {"Wes, "Sarah", "Simone"} (a Generator)
    console.log(line.next().value); //Wes
    console.log(line.next().value); //Sarah
    //.next will remove it from the iterator
    brunch.add('Heather');
    brunch.add('Snickers');
    console.log(line.next().value); //Simone
    console.log(line.next().value); //Heather
    console.log(line.next().value); //Snicker
    ```

###  Module 18.63: WeakSets
* Like a set but there are some limitations
* WeakSet can only contain objects
* Cannot innumerate/loop over it - no iterator
* There's no .clear() method because WeakSets clean themselves up (which is great for garbage collection and memory)
* Great if you're storing a DOM node

## Module 19: Map and Weak Map

###  Module 19.64: Maps
* If Sets are to Arrays, Maps are to Objects
* Maps are like sets but it has a key and value
    ```javascript
    const dogs = new Map();

    dogs.set('Snickers', 3);
    dogs.set('Sunny', 2);
    dogs.set('Hugo', 10);
    console.log(dogs.has("Snickers")); //returns true
    console.log(dogs.get("Snickers")); //returns 3
    console.log(dogs.delete("Hugo")); //returns true
    console.log(dogs); //Map {"Snickers" => 3, "Sunny" => 2}

    dogs.forEach((val, key) => console.log(val, key)); //to loop over a map, use forEach
    //OR
    for (const [key, val] of dogs) { //to loop over a map, use for of
      console.log(key, val);
    }
    ```

###  Module 19.65: Map Metadata with DOM Node Keys
* Store Meta Data about an object

###  Module 19.66: WeakMap and Garbage Collection
* WeakMap like WeakSet - can't tell size, not innumerable (can't loop over it), and items will get garbage collector
* Better for garbage collection where you don't have to monitor it

## Module 20: Async + Await Flow Control

###  Module 20.67: Async Await - Native Promises Review
* A lot of APIs nowadays use Promises, not callbacks.
    ```html
    <video controls class="handsome"></video>
    ```

    ```javascript
    fetch('API URL').then(response => {
      return response.json(); //this returns a promise, hence the next line
    }).then(response => {
      console.log(response);
    }).catch(err => {
      console.error(err);
    })
    ```

    ```javascript
    //Asks for access to the webcam, displays it in the video tag
    const video = document.querySelector('.handsome');

    navigator.mediaDevices.getUserMedia({ video: true }).then(mediaStream => {
      video.srcObject = mediaStream;
      video.load();
      video.play();
    }).catch(err => {
      console.error(err);
    })
    ```

###  Module 20.68: Async Await - Custom Promises Review
* Any function that returns a Promise has a Promise-based API
    ```javascript
    function breathe(amount) { //amount we should breath
      return new Promise((resolve, reject) => {
        if (amount < 500) {
          reject('That is too small of a value');
        }
        setTimeout(() => resolve(`Done for ${amount} ms`), amount);
      });
    }
    breathe(1000).then(res => {
      console.log(res);
      return breathe(500);
    }).then(res => {
      console.log(res);
      return breathe(300);
    }).then(res => {
      console.log(res);
      return breathe(600);
    }).catch(err => {
      console.error(err);
      console.error('YOU SCREWED UP');
    })
    ```

###  Module 20.69: All About Async + Await
* Synchronous - wait for task to be done before you continue on
* Asynchronous - start the task, move on to the next value
* `alert`, `prompt`, `confirm` are some of the few synchronous things
* Make an Async and then Await values
* Async + Await is built on top of Promises, it doesn't replace it
    ```javascript
    function breathe(amount) {
      return new Promise((resolve, reject) => {
        if (amount < 500) {
          reject('That is too small of a value');
        }
        setTimeout(() => resolve(`Done for ${amount} ms`), amount);
      });
    }

    //await needs to be in an async function
    async function go(name, last) {
      console.log(`Starting for ${name} ${last}!`);
    //const res = breathe(1000); //breath would return promise
      const res = await breathe(1000); //with "await", breath will return promise but await will say "everyone, hold on until this function resolves or rejects!"
      console.log(res);
      const res2 = await breathe(300);
      console.log(res2);
      const res3 = await breathe(750);
      console.log(res3);
      const res4 = await breathe(900);
      console.log(res4);
      console.log('end');
    }
   //OR
    //another way of writing it
    /*const go = async () => {
    }*/
    ```

###  Module 20.70: Async + Await Error Handling
* There's no "then"
    ```javascript
    function breathe(amount) {
      return new Promise((resolve, reject) => {
        if (amount < 500) {
          reject('That is too small of a value');
        }
        setTimeout(() => resolve(`Done for ${amount} ms`), amount);
      });
    }
    ```

    ```javascript
    async function go(name, last) {
      try {
        console.log(`Starting for ${name} ${last}!`);
        const res = await breathe(1000);
        console.log(res);
        const res2 = await breathe(300);
        console.log(res2);
        const res3 = await breathe(750);
        console.log(res3);
        const res4 = await breathe(900);
        console.log(res4);
        console.log('end');
      } catch (err) {
        console.error(err);
      }
    }
  //OR
    //HIGH ORDER FUNCTION WAY
    async function go() {
      console.log(`Starting for ${name} ${last}!`);
      const res = await breathe(1000);
      console.log(res);
      const res2 = await breathe(300);
      console.log(res2);
      const res3 = await breathe(750);
      console.log(res3);
      const res4 = await breathe(900);
      console.log(res4);
      console.log('end');
    }

    //high order function
    function catchErrors(fn) { //fn = function
      return function () {
        return fn(...args).catch((err) => {
          console.error('Ohhhh nooo!!!!!');
          console.error(err);
        });
      }
    }
    const wrappedFunction = catchErrors(go);
    wrappedFunction();
  //OR
    //HIGH ORDER FUNCTION WAY, with parameters
    async function go(name, last) {
      console.log(`Starting for ${name} ${last}!`);
      const res = await breathe(1000);
      console.log(res);
      const res2 = await breathe(300);
      console.log(res2);
      const res3 = await breathe(750);
      console.log(res3);
      const res4 = await breathe(900);
      console.log(res4);
      console.log('end');
    }

    //high order function
    function catchErrors(fn) { //fn = function
      return function (...args) {
        return fn(...args).catch((err) => {
          console.error('Ohhhh nooo!!!!!');
          console.error(err);
        });
      }
    }
    const wrappedFunction = catchErrors(go);
    wrappedFunction("FirstName","LastName");
    ```

###  Module 20.71: Waiting on Multiple Promises
* fire multiple things at the same time, but wait for them to all come back
    ```javascript
    async function go() {
      const p1 = fetch('https://api.github.com/users/wesbos');
      const p2 = fetch('https://api.github.com/users/stolinski');
      // Wait for both of them to come back
      const res = await Promise.all([p1, p2]);
      const dataPromises = res.map(r => r.json());
      const [wes, scott] = await Promise.all(dataPromises);
      console.log(wes, scott);
    }
    go();
    ```
* in this case, get various jsons from github array, just by passing userid
    ```javascript
    async function getData(names) {
      const promises = names.map(name => fetch(`https://api.github.com/users/${name}`).then(r => r.json()));
      const people = await Promise.all(promises);
      console.log(people);
    }

    getData(['wesbos', 'stolinski', 'darcyclarke']);
    ```

###  Module 20.72: Promisifying Callback Based Functions
* Promises are great but still lots of existing JS/APIs/libraries that are still callback based
* Promisifying without a library example
    ```javascript
    function getCurrentPosition(...args) {
      return new Promise((resolve, reject) => {
        navigator.geolocation.getCurrentPosition(...args, resolve, reject);
      });
    }

    async function go() {
      console.log('starting');
      const pos = await getCurrentPosition();
      console.log(pos);
      console.log('finished');
    }
    ```

## Module 21: ES7, ES8, + Beyond

###  Module 21.73: Class Properties

* Not yet out
* Adding a properties to the class, for example, a bark property for class Dog, rather than creating this.barks into the constructor

###  Module 21.74: padStart and padEnd
*
    ```javascript
    'string'.padStart(3) //returns "   string"
    'string'.padEnd(3) //returns "string   "
    '1'.padStart(3,"0") //returns "001"
    '1'.padEnd(3,"0") //returns "100"

    const strings = ['short', 'medium size', 'this is really really long', 'this is really really really really really really long'];
    const longestString = strings.sort(str => str.length).map(str => str.length)[0];

    strings.forEach(str => console.log(str.padStart(longestString)));
    ```

###  Module 21.75: ES7 Exponential Operator
*
    ```javascript
    //OLD WAY
    Math.pow(3,3)
    //ES7 Way
    3 ** 3; //returns 27;

    //OLD WAY
    Math.pow(Math.pow(2,2),2)
    //ES7 WAY #BESTPRACTICE
    2 ** 2 ** 2; //returns 16;
    ```

###  Module 21.76: Function Arguments Trailing Comma

* Comma dangle is okay! Use extra comma for next person adding something
    ```javascript
    function family(mom,dad,) {
    }
    ```

###  Module 21.77: Object.entries() and Object.values()
*
    ```javascript
    const inventory = {
      backpacks: 10,
      jeans: 23,
      hoodies: 4,
      shoes: 11
    };

    // Make a nav for the inventory
    const nav = Object.keys(inventory).map(item => `<li>${item}</li>`).join('');
    console.log(nav);

    // tell us how many values we have
    const totalInventory = Object.values(inventory).reduce((a, b) => a + b);
    console.log(totalInventory);

    // Print an inventory list with numbers
    Object.entries(inventory).forEach(([key, val]) => {
      console.log(key, val);
    });

    for (const [key, val] of Object.entries(inventory)) {
      console.log(key);
      if (key === 'jeans') break;
    }
    ```
