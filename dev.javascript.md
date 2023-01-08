# Warren Shea's Notes for JavaScript (and TypeScript)
v20230104

## Notable JavaScript Experts
* [TypeScript, ES6 by Wes Bos](https://wesbos.com/courses){:target="_blank"}
* [Just JavaScript by Dan Abramov](https://justjavascript.com/){:target="_blank"}
* [Design Patterns by Addy Osmani](https://www.patterns.dev/posts/classic-design-patterns/){:target="_blank"}

## Quick Reference

### Terms
* `nullish` is `null` or `undefined`
* `method`: a function inside an object
* `smooth brackets` or `parenthesis`: `()`
* `curly brackets`: `{}`
* `square brackets`: `[]`
* `truthy`: a value accepted as true in a condition statement
* `falsy`: a value accepted as false in a condition statement
* `bang`: `!`
* `bang bang`: `!!`, which converts a truthy to true or falsy to false

### Conversions

#### NodeList to Array
* `[...NodeList]` or `Array.from(NodeList)`

## Various Notes (no particular order)

### Truthy/Falsy
In a conditional statement, these values are not true or false (boolean) but are accepted as conditions:
* Truthys: `Object`, `Array`, non empty string, number other than 0, Date
* Falsys: `""`, `0`, `null`, `undefined`, `NaN`
`!!` ("bang bang") converts Truthy/Falsy to boolean "true" or "false"

### Better console.log
* Original `console.log(error,loading,success,data);`
* Variant 1: `console.log(`Error:${error},Loading:${loading},Success:${success},Data:${data}`);`
* Variant 2: `console.log({error,loading,success,data});`
* Grouping logs: `console.groupCollapsed` / `console.groupEnd`

### events
* `event.target` <-- the thing that actually got clicked
* `event.currentTarget` <-- the thing that fired the event listener, this is what you should use in most cases

#### Pointer events
* `isTrusted` is a parameter for determining if the event is clicked by the mouse or programmatically clicked

#### prevent from running
* `event.preventDefault();`
* `event.preventStopPropagation();`

#### Propagation (bubbling up) + Capture (trickle down)
* *Note: I still don't quite understand this, specifically the capture phase and reversing the order*
* Capture phase, Target phase, Bubbling phase
* Capture Phase: `Document` -> `<html>` -> `<body>` -> `<main>`
* Target Phase: `<button>`
* Bubbling Phase: `<main>` -> `<body>` -> `<html>` -> `Document`
*  `addEventListener(type, listener, useCapture)`, e.g. `addEventListener('click', functionCallback(), { capture: true})` to reverse (so this is the Capture down, instead of the Bubbling up)

### Functional Programming via Filter Map Sort Reduce
* **filter** - loop over array and for each item, decide to keep or not. return `true` means keep it
* **map** - loop over array and returns new array of same length,
* **sort** - loop over array and returns new array of same length, return "1" if condition is true, and -1 if not
* **reduce** - loop over array and count

```javascript
const totalValue = arrayName.reduce((total,arrayItem) => {
  return total + arrayItem.doSomething;
},0);
```

### Imperative Programming
 * uses a sequence of statements to determine how to reach a certain goal
 * these statements are to change the state of the program as each one is executed in turn

### JAMstack - Javascript, APIs, Markup
* Javascript: Vue, React, Angular, Ember
* APIs: Contetnful, GraphQL, IMGIX
* Markup: Gatsby, Markdown, YAML, HTML

### Adding to the DOM via JavaScript
* `document.getQuerySelector().insertAdjacentElement(position,element);`

```html
<!-- beforebegin -->
<p>
  <!-- afterbegin -->
  foo
  <!-- beforeend -->
</p>
<!-- afterend -->
```
* Doing this allows use of DOM code manipulation on html_code_string (e.g. adding an Event Listener), which you wouldn't be able to do with an html_code_string
`document.createRange().createcontextualFragment(html_code_string)`

### Scope

#### Global Scope
* Global Scope is attached to Window
* `var` variables and functions are attached to the window object and globally scoped
* `let` and `const` are globally scoped by not attached to the window object

#### Block Scope
* `let` and `const` and block scoped
* `{` and `}` are like gates

#### Function Scope
* `var` is function scoped
* Scope Lookup - it checks current scope and if not found, goes up a level
* Variable is Shadowed when a variable with the same name is created in a function. Not illegal but not a good idea.

#### Lexical Scoping
* arrow functions do not beind their own `this`, instead they inherit the one from the parent scope
* `this` is referrring to where it's defined, not where it's run

### `this`
* in regular functions, `this` keyword represented the object that called the function, which could be the window, the document, a button or whatever
* Dan Abramov: in arrow functions, `this` keyword always represents the object that defined the arrow function. don't use arrow functions if you need `this`, for event listeners
 says: "it’s like a hidden argument to your function. calls with dot, like obj.fn(), pass the part before the dot (obj) as this. calls without a dot, like fn(), don’t pass any this. if you didn’t pass any this, it’s set to a default (undefined in strict mode, window in loose mode)"

### Hoisting
* before executing your code in the order you wrote it, javascript “pulls up” two types of declarations, so you can call them before they're defined.

```javascript
function functionName() {} //function declaration
var variableName; //variable declaration
```
to the top of the containing function (or file if you’re at top level). this lets you call a function declared this way even if it’s defined below.

However, function expressions are not hoisted up, nor are variables defined with `let`
```javascript
const functionName = function() {} //function expression
let variableName; //let variable declaration
```

### Closures
* Ability to access a parent scope data after it's run and (it should be garbage collected)
* Dan Abramov: function variables are still accessible after function is run
 says: "functions can read or write variables “outside” of them. this works not only with top level variables, but with local variables too (from nested functions). that’s called closures."

### Adding Event Listeners to multiple items
* One way (what I usually do):

```javascript
buyButtons.forEach(button => {
  button.addEventListeners('click', callbackFunction);
});
```
* Another way + the ability to unbind

```javascript
function handleClick(button) {
  button.addEventListeners('click', callbackFunction);
}
buyButtons.forEach(handleClick);
```

### Headless
* Wordpress, Drupal, Shopify are now also Headless (previously not Headless)
* Head is the what is seen (website, mobile, shop, social media, wearable)
* Body is the data, the backend

### The Main Thread
* Parses HTML, Builds the DOM, Parses CSS, Executes JavaScript, Responds to User Events
* try to leave main thread for UI updates + User Interaction

### Web Workers
* Make it possible to run a script operation in a background thread separate from the main execution thread of a web app
* Cannot make changes to the DOM directly
* Service worker is specialized version of web worker

### Arrow functions
* are anonymous functions (you don't use the term function)
* implicit return - one line, no return, no curly brackets
* if you wanted to implicitly return an object, wrap in parenthesis/smooth bracket ();

### IIFE - Immediate-invoked Function Expressions
To execute functions immediately, as soon as they are created
Don't pollute the global object, simple way to isolate variables declarations

```javascript
(function() {
  /* */
})();

(function doSomething() {
  /* */
})();

(() => {
  /* */
})();
```

### Async Await
* A concept of asynchronous programming, a specific way to write asynchronous promise based code.
* Example:

```javascript
async function functionName() {
  const res = await fetch("url");
  console.log(res.json());
}
```
The console.log doesn't run until after the `await` is completed

### Promises

#### What is the extent of your experience with Promises and/or their polyfills? What are the pros and cons of using Promises instead of callbacks?
* Async Await is cleaner to write and easier to deal with when there are lots of callbacks (and you get into nested callback hell)

### JavaScript Functions are First Class Citizens
* functions are values, they can be stored as variables

### `.apply` and `.call`
* apply lets you invoke the function with arguments as an array;
* [MDN - apply](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/apply){:target="_blank"}
* call requires the parameters be listed explicitly.
* [MDN - call](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/call){:target="_blank"}
* Example:

```javascript
function theFunction(name, profession) {
    console.log("My name is " + name + " and I am a " + profession +".");
}
theFunction("John", "fireman");
theFunction.apply(undefined, ["Susan", "school teacher"]);
theFunction.call(undefined, "Claude", "mathematician");
theFunction.call(undefined, ...["Matthew", "physicist"]); // used with the spread operator
```

### function.prototype.bind
* Dan Abramov: a method that, when called, has its `this` keyword set to the provided value
* `this` is a hidden argument to your function. "bind" wraps a function with the `this` you provide so that you don’t need to remember to pass the correct `this` every time
* [MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_objects/Function/bind){:target="_blank"}

### When would you use document.write()?
* sometimes working with third parties like Google Analytics, which have no control over the users brower's dependencies (e.g. jQuery)
* Note: `document.write()` fires after a page is finished loading and may not even fire at all

### What's the difference between feature detection, feature inference, and using the UA string?
* Feature Detection: Checking if the feature exists, e.g. `if (navigator.geolocation) { /* do something */ }`
* Feature Inference: Assuming the feature exists and using it
* UA String: navigator.userAgent outputs a string of data. this method can be easily spoofed

### Explain how JSONP works and why it's not really AJAX
* JSONP is sending JSON data without cross domain issues, e.g. requesting an external script from another domain:

Instead of
```javascript
//alpha.com code
fetch('https://beta.com/file.json')
```
which would return a cross domain issue (CORS), you could do
```html
<!--alpha.com code-->
<script src="https://beta.com/file.json"></script>
```

```javascript
//https://beta.com/file.json
myFunction({
  //object
})
```
where `myFunction` is defined on alpha.com code.

### Difference between document load event and document ready event?
* **document load event**: When the DOM has loaded, without waiting for the resouces to load, e.g. `document.addEventListener("DOMContentLoaded", () => { })`;
* **document ready event**: When the DOM and resources are loaded, ready to execute JavaScript code, e.g. `window.addEventListener('load', () => { }, false)`;

#### Why would you use something like the load event? Does this event have disadvantages? Do you know any alternatives, and why would you use those?
* load event fires at the end of the document loading process (DOM + resources) have finished loading.
* DOMContentLoaded event will fire after the DOM for the page has been constructed, but do not wait for other resources to finish loading. This is preferred in certain cases when you do not need the full page to be loaded before initializing.

### Explain the same-origin policy with regards to Javascript
* security mechanism that restricts a resource that is loaded/accessed in one particular origin from another origin
* two origins are considered the same if their hostname, port, and protocol are the same

### Why is it called a Ternary expression, what does the word "Ternary" indicate?
* Ternary operand accepts three parameters:

```javascript
//conditional
if(conditional) { // one
  truthy_block // two
} else {
  falsy_block // three
}

//ternary expression
(conditional) ? truthy_block : falsy_block
```

### what is `"use strict";`? what are the advantages and disadvantages to using it?
* `"use strict";` instructs the browser to use the Strict mode, which is a reduced and safer feature set of JavaScript
* Advantages:
  * eliminates some JavaScript silent errors by changing them to throw errors
  * fixes mistakes that make it difficult for JavaScript engines to perform optimizations: strict mode code can sometimes be made to run faster than identical code that’s not strict mode
  * prohibits some syntax likely to be defined in future versions of ECMAScript
  * prevents, or throws errors, when relatively “unsafe” actions are taken (such as gaining access to the global object)
  * disables features that are confusing or poorly thought out
  * makes it easier to write “secure” JavaScript

### Explain what a single page app is and how to make one SEO-friendly.
* A page/app/website that doesn’t require any more page loads after the first page view load (e.g. React, Angular, and Vue)
* To improve SEO, ensure there's an XML sitemap, Views as URLs (via a router), Static Site Generation

### What are some of the advantages/disadvantages of writing Javascript code in a language that compiles to Javascript?
Advantages:
* Types (via TypeScript) can improve stability and reduces errors in JavaScript
Disadvantages:
* Need something to transpile the code to JavaScript

### What is the purpose of a code style linting tool?
* Lint, or a linter, is a static code analysis tool (e.g. eslint) used to flag programming errors, bugs, stylistic errors and suspicious constructs

### What is an event loop?
* JavaScript's runtime model, responsible for executing the code, collecting and processing events, and executing queued sub-tasks
* Dan Abramov: event loop is a set of rules for how the runtime (browser / Node) decides what code to run when it has finished running the current code. for example “okay we’ve exited all functions, so now, let’s run expired timeouts”. that includes code after “await” if the thing has resolved
* [MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/EventLoop){:target="_blank"}

___

## To Revisit

I've posted some questions I've seen online that I tried to look into but I still have trouble understanding. Sometimes with experience, things like this clear themselves up over time.

### What are generators
* allow you to define an iterative algorithm by writing a single function whose execution is not continuous
* Generator functions are written using the function* syntax
* Dan Abramov: generators let your function return multiple values. not necessarily immediately — the caller decides when to ask for the next one. useful to describe operations where you can “ask for more”, like processing a long list or deciding each next step based on user input
* [MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Iterators_and_Generators#generator_functions){:target="_blank"}

### What is currying
* an advanced technique of working with functions
* a transformation of functions that translates a function from callable as `function(a, b, c)` into callable as `functions(a)(b)(c)`
* Dan Abramov: imagine functions only take one argument. how would we pass many? one way is to pass an object: `({ a, b, c }) => …` but we could also turn our function into a matryoshka of many functions where each takes one arg: `(a) => (b) => (c) => …` that’s currying. not very useful in js.
* Example:

```javascript
function curry(f) { // curry(f) does the currying transform
  return function(a) {
    return function(b) {
      return f(a, b);
    };
  };
}

// usage
function sum(a, b) {
  return a + b;
}

let curriedSum = curry(sum);

console.log( curriedSum(1)(2) ); // 3
```

### What are monads?
* highly composable unit (a kind of building blocks of programming) in functional programming
* Dan Abramov: it’s an abstraction but a very generic one so hard to describe. i’d describe it as “wrapper for a value which lets you apply operations on that value, producing more such wrappers”. promise then(), if we skip minor pedantic distinctions, are an example of that.

### When to use classes instead of factory functions
* factory function returns an object
* Dan Abramov: if you want people to extend your classes (to fill in some functionality) then it seems like it’s easier to do this with actual classes.

### Use cases for WeakMap/WeakSet
* Dan Abramov: associate some information with an object i don’t own. like a memoization cache. weakmap is good for this because it doesn’t hold onto it, so i’m not causing a memory leak. the tradeoff is i can’t iterate over the list of objects for which i hold information.

___

## TypeScript

`if (typeof padding === "number") {`
* Type Narrowing: the _process_ of refining types to more specific types
* Type Guards: this code is a special form of code called _type guard_
--
* Implicit Types do not need to be declared. Examples can be private or local variables
* Explicit Types should be declared: function inputs, outputs, anything exported or public
--
* TC39 - Types //as Comments ECMAScript Proposal for TypeScript inside JavaScript

___

## The State of JS

I always find the State of JS survey as one of the best ways to learn something new/cutting edge.
Here, I'll list some items and a brief description / info on what it is - mostly for my own learning:

### Language

#### Numeric Separators
* To improve readability, this feature enables underscores as separators in numeric literals.
* For example: \
`1000000000000` -> `1_000_000_000_000` \
`1019436871.42` -> `1_019_436_871.42`
* [MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Lexical_grammar){:target="_blank"}

#### String.prototype.replaceAll()
* The `replaceAll()` method returns a new string with all matches of a `pattern` replaced by a `replacement`
* Example:

```javascript
const p = 'The quick brown fox jumps over the lazy dog. If the dog reacted, was it really lazy?';
//
console.log(p.replaceAll('dog', 'monkey'));
// expected output: "The quick brown fox jumps over the lazy monkey. If the monkey reacted, was it really lazy?"
//
// global flag required when calling replaceAll with regex
const regex = /Dog/ig;
console.log(p.replaceAll(regex, 'ferret'));
// expected output: "The quick brown fox jumps over the lazy ferret. If the ferret reacted, was it really lazy?"
```
* [MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/replaceAll){:target="_blank"}

#### String.prototype.matchAll()
* The `matchAll()` method returns an iterator of all results matching a string against a regular expression, including capturing groups.
* Example:

```javascript
const regexp = /t(e)(st(\d?))/g;
const str = 'test1test2';
//
const array = [...str.matchAll(regexp)];
//
console.log(array[0]);
// expected output: Array ["test1", "e", "st1", "1"]
//
console.log(array[1]);
// expected output: Array ["test2", "e", "st2", "2"]
```
* [MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/matchAll){:target="_blank"}

#### Regexp Match Indices / String.prototype.match()
* The match() method retrieves the result of matching a string against a regular expression.
* Example:

```javascript
const paragraph = 'The quick brown fox jumps over the lazy dog. It barked.';
const regex = /[A-Z]/g;
const found = paragraph.match(regex);
//
console.log(found);
// expected output: Array ["T", "I"]
```
* [MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/match){:target="_blank"}

#### Array.prototype.at()
* The at() method takes an integer value and returns the item at that index, allowing for positive and negative integers. Negative integers count back from the last item in the array.
* Example:

```javascript
const array1 = [5, 12, 8, 130, 44];
let index = 2;
//
console.log(`Using an index of ${index} the item returned is ${array1.at(index)}`);
// expected output: "Using an index of 2 the item returned is 8"
//
index = -2;
//
console.log(`Using an index of ${index} item returned is ${array1.at(index)}`);
// expected output: "Using an index of -2 item returned is 130"
```

#### Array.findLast()
* The `findLast()` method iterates the array in reverse order and returns the value of the first element that satisfies the provided testing function. If no elements satisfy the testing function, undefined is returned.
* Example:

```javascript
const array1 = [5, 12, 50, 130, 44];

const found = array1.findLast((element) => element > 45);

console.log(found);
// expected output: 130
```
* [MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/findLast){:target="_blank"}

#### Object.hasOwn()
* The `Object.hasOwn()` static method returns `true` if the specified object has the indicated property as its own property. If the property is inherited, or does not exist, the method returns `false`.
* Example:

```javascript
const object1 = {
  prop: 'exists'
};
console.log(Object.hasOwn(object1, 'prop'));                    // expected output: true
console.log(Object.hasOwn(object1, 'toString'));                // expected output: false
console.log(Object.hasOwn(object1, 'undeclaredPropertyValue')); // expected output: false
```
* [MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/hasOwn){:target="_blank"}

#### Promise.allSettled()
* Takes an array of promises and returns a single Promise. The returned promise fulfills when all the input promises are settled and returns with an array that describes each outcome of each input promise (e.g. "fulfilled" "rejected")
* [MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise/allSettled){:target="_blank"}

#### Promise.any()
* The Promise.any() method takes an iterable of promises as input and returns a single Promise. This returned promise fulfills when any of the input's promises fulfills, with this first fulfillment value. It rejects when all of the input's promises reject (including when an empty iterable is passed), with an AggregateError containing an array of rejection reasons.
* Example:

```javascript
const promise1 = Promise.reject(0);
const promise2 = new Promise((resolve) => setTimeout(resolve, 100, 'quick'));
const promise3 = new Promise((resolve) => setTimeout(resolve, 500, 'slow'));
//
const promises = [promise1, promise2, promise3];
//
Promise.any(promises).then((value) => console.log(value));
//
// expected output: "quick"
```
* [MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise/any){:target="_blank"}

#### Top Level await()
* Top-level await enables developers to use the await keyword outside of async functions. It acts like a big async function causing other modules who import them to wait before they start evaluating their body.
* Old way:

```javascript
(async function() {
  await Promise.resolve(console.log('🎉'));
  // → 🎉
}());
```

* New way:

```javascript
await Promise.resolve(console.log('🎉'));
// → 🎉
```
* [v8.dev](https://v8.dev/features/top-level-await){:target="_blank"}

#### Dynamic Import
* A module path must be a string, not a function `import ... from getModuleName();` will fail
* You can't import conditionally `if (...) { import ...; }`
* The `import(module)` expression loads the module and retursn a promise that resolves into a module object.

* [JavaScript.info](https://javascript.info/modules-dynamic-imports){:target="_blank"}

```javascript
// say.js
export function hi() {
  alert(`Hello`);
}

export function bye() {
  alert(`Bye`);
}

// another file.js
let {hi, bye} = await import('./say.js');

hi();
bye();
```

#### Temporal
* Temporal, a global Object that acts as a top-level namespace (like Math), that brings a modern date/time API to the ECMAScript language.
* [https://tc39.es/proposal-temporal/docs/](https://tc39.es/proposal-temporal/docs/)

#### Logical OR `||` e.g. `expr1 || expr2`
* If `expr1` can be converted to `true`, returns `expr1`; else, returns `expr2`.
* `false` is `null`, `NaN`, `0`, empty string `""`, `''`, or undefined
* [MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Logical_OR){:target="_blank"}

#### Logical AND `&&` e.g. `expr1 && expr2`
* If value can be converted to true, value is truthy. If value can be converted to false, value is falsy.
* Items that can be converted to `false` is `null`, `NaN`, `0`, empty string `""`, `''`, or undefined
* In React, `(true && 'Hello World')` evaluates to `Hello World` and  `(false && 'Hello World')` evaluates to false
* [MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Logical_AND){:target="_blank"}

#### Nullish Coalescing
**Operator** `??`
* The *nullish coalescing* `??` operator is a logical operator that returns its right-hand side operand when its left-hand side operand is `null` or `undefined`, and otherwise returns its left-hand side operand.
* For example:

```javascript
const foo = null ?? 'default string';
console.log(foo);
// expected output: "default string"

const baz = 0 ?? 42;
console.log(baz);
// expected output: 0
```
* [MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Nullish_coalescing){:target="_blank"}

**Assignment** `??=`
* The *nullish coalescing assignment* `x ??= y` operator only assigns if x is `nullish` (`null` or `undefined`).
* For example:

```javascript
const a = { duration: 50 };

a.duration ??= 10;
console.log(a.duration);
// expected output: 50

a.speed ??= 25;
console.log(a.speed);
// expected output: 25
```
* [MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Nullish_coalescing_assignment){:target="_blank"}

#### Logical Assignment
* The *logical OR assignment* `(x ||= y)` operator only assigns if x is `falsy`
* Example:

```javascript
const a = { duration: 50, title: '' };
//
a.duration ||= 10;
console.log(a.duration);
// expected output: 50
//
a.title ||= 'title is empty.';
console.log(a.title);
// expected output: "title is empty"
```
* [MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Logical_OR_assignment){:target="_blank"}

#### Proxies
* Create a proxy for another object that can intercept, redefine fundamental operations for that object. Generally used to log property access, validate, format, or sanitize inputs, etc.
* [MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Proxy){:target="_blank"}

#### Private Fields
* ES2022 allows private fields for a class - you can prefix the field name with #, e.g.

```javascript
class ClassWithPrivate {
  #privateField;
  #privateFieldWithInitializer = 42;

  #privateMethod() {
    // …
  }

  static #privateStaticField;
  static #privateStaticFieldWithInitializer = 42;

  static #privateStaticMethod() {
    // …
  }
}
```
* [MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Classes/Private_class_fields){:target="_blank"}

#### Error.prototype.cause
* The cause data property of an Error instance indicates the specific original cause of the error. It is used when catching and re-throwing an error with a more-specific or useful error message in order to still have access to the original error.
* Example:

```javascript
try {
  connectToDatabase();
} catch (err) {
  throw new Error('Connecting to database failed.', { cause: err });
}
```
* [MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Error/cause){:target="_blank"}

### Browser APIs

#### Service Workers
* Service worker is specialized version of web worker.
* Service workers act as proxy servers that sit between web applications, the browser, and the network (when available).
* Service workers are intended to enable the creation of effective offline experiences, intercept network requests and take appropriate action based on whether the network is available, and update assets residing on the server.
* Service workers will also allow access to push notifications and background sync APIs.
* [MDN](https://developer.mozilla.org/en-US/docs/Web/API/Service_Worker_API){:target="_blank"}

#### Intl
* A Global Object namespace for the ECMAScript Internationalization API, which provides language sensitive string comparison, number formatting, and date and time formatting
* [MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Intl){:target="_blank"}

#### WebGL
* Web Graphics Library (WebGL) is a JavaScript API for rendering interactive 2D and 3D graphics within any compatible web browser without the use of plug-ins.
* [MDN](https://developer.mozilla.org/en-US/docs/Web/API/WebGL_API){:target="_blank"}

#### Web Animations
* Using .animate as an alternative to CSS animations
* [MDN](https://developer.mozilla.org/en-US/docs/Web/API/Web_Animations_API){:target="_blank"}

#### WebRTC
* Enables websites to optinally capture and stream video and audio
* [MDN](https://developer.mozilla.org/en-US/docs/Web/API/WebRTC_API){:target="_blank"}

#### Web Speech API
* For speech recognition or Speech synthesis (aka text-to-speech, or tts)
* [MDN](https://developer.mozilla.org/en-US/docs/Web/API/Web_Speech_API/Using_the_Web_Speech_API){:target="_blank"}

#### WebSocket
* open a two-way interactive communication session between the user's browser and a server (send messages to a server and receive event-driven responses)
* [MDN](https://developer.mozilla.org/en-US/docs/Web/API/WebSockets_API){:target="_blank"}

#### Custom Elements
* customElements (read-only property) of `window` interface that returns a reference to the `CustomElementRegistry` object, which can be used to register new custom elements and get information about previously registered custom elements.
* The basis for Web Components
* [MDN](https://developer.mozilla.org/en-US/docs/Web/API/Window/customElements){:target="_blank"}
* [GitHub - Web Component Examples](https://github.com/mdn/web-components-examples/){:target="_blank"}

#### Shadow DOM
* > "An important aspect of web components is encapsulation — being able to keep the markup structure, style, and behavior hidden and separate from other code on the page so that different parts do not clash, and the code can be kept nice and clean. The Shadow DOM API is a key part of this, providing a way to attach a hidden separated DOM to an element."
* [MDN](https://developer.mozilla.org/en-US/docs/Web/Web_Components/Using_shadow_DOM){:target="_blank"}

#### Page Visibility API
* provides events to know when a document becomes visible or hidden
* useful for saving resources and improving performance by letting a page avoid performing unnecessary tasks when the document isn't visible.
* `document.visibilityState`: A string indicating the document's current visibility state. Possible values are:
`visible`: The page content may be at least partially visible. In practice this means that the page is the foreground tab of a non-minimized window.
`hidden`: The page's content is not visible to the user, either due to the document's tab being in the background or part of a window that is minimized, or because the device's screen is off.
* Example of listener for visibility change:
```javascript
document.addEventListener("visibilitychange", () => {
  if (document.hidden) {
    audio.pause();
  } else {
    audio.play();
  }
});
```
* [MDN](https://developer.mozilla.org/en-US/docs/Web/API/Page_Visibility_API){:target="_blank"}

#### Broadcast Channel API
* allows basic communication between browsing contexts (that is, windows, tabs, frames, or iframes) and workers on the same origin
* [MDN](https://developer.mozilla.org/en-US/docs/Web/API/Broadcast_Channel_API){:target="_blank"}

#### Geolocation API
* allows the user to provide their location to web applications if they so desire
* [MDN](https://developer.mozilla.org/en-US/docs/Web/API/Geolocation_API){:target="_blank"}

#### File System Access API
* allows interaction with files on a user's local device, or on a user-accessible network file system. Core functionality of this API includes reading files, writing or saving files, and access to directory structure.
* [MDN](https://developer.mozilla.org/en-US/docs/Web/API/File_System_Access_API){:target="_blank"}

#### Web Share API
* provides a mechanism for sharing text, links, files, and other content to an arbitrary share target selected by the user
* [MDN](https://developer.mozilla.org/en-US/docs/Web/API/Web_Share_API){:target="_blank"}

#### WebXR Device API
* Find compatible VR or AR output devices, Render a 3D scene to the device at an appropriate frame rate, (Optionally) mirror the output to a 2D display, Create vectors representing the movements of input controls
* [MDN](https://developer.mozilla.org/en-US/docs/Web/API/WebXR_Device_API){:target="_blank"}

### Other Features

#### Progressive Web Apps
* Progressive Web Apps (PWAs) are web apps that use service workers, manifests, and other web-platform features in combination with progressive enhancement to give users an experience on par with native apps.
* [MDN](https://developer.mozilla.org/en-US/docs/Web/Progressive_web_apps){:target="_blank"}

#### WebAssembly (WASM)
* WebAssembly is a new type of code that can be run in modern web browsers — it is a low-level assembly-like language with a compact binary format that runs with near-native performance and provides languages such as C/C++, C# and Rust with a compilation target so that they can run on the web. It is also designed to run alongside JavaScript, allowing both to work together.
* [MDN](https://developer.mozilla.org/en-US/docs/WebAssembly){:target="_blank"}

### Front end Frameworks (2022 version)
* [React](https://reactjs.org/){:target="_blank"}
* [Vue](https://vuejs.org/){:target="_blank"}
* [Angular (currently at v15.0.4)](https://angular.io/){:target="_blank"}
* [Preact](https://preactjs.com/){:target="_blank"}
* [Ember](https://emberjs.com/){:target="_blank"}
* [Svelte](https://svelte.dev/){:target="_blank"}
* [Alpine](https://alpinejs.dev/){:target="_blank"}
* [Lit](https://lit.dev/){:target="_blank"}
* [Solid](https://www.solidjs.com/){:target="_blank"}
* [Qwik](https://qwik.builder.io/){:target="_blank"}
* [Stencil](https://stenciljs.com/){:target="_blank"}

### Rendering Frameworks
* [Next](https://nextjs.org/){:target="_blank"}
* [Nuxt](https://nuxtjs.org/){:target="_blank"}
* [Gatsby](https://www.gatsbyjs.com/){:target="_blank"}
* [Remix](https://remix.run/){:target="_blank"}
* [Astro](https://astro.build/){:target="_blank"}
* [Eleventy](https://www.11ty.dev/){:target="_blank"}
* [SvelteKit](https://kit.svelte.dev/){:target="_blank"}
* [Docusaurus](https://docusaurus.io/){:target="_blank"}

### Testing
* [Jest](https://jestjs.io/){:target="_blank"}
* [Mocha](https://mochajs.org/){:target="_blank"}
* [Storybook](https://storybook.js.org/docs/react/writing-tests/introduction){:target="_blank"}
* [Cypress](https://www.cypress.io/){:target="_blank"}
* [AVA](https://github.com/avajs/ava){:target="_blank"}
* [Jasmine](https://jasmine.github.io/){:target="_blank"}
* [Puppeteer](https://pptr.dev/){:target="_blank"}
* [Testing Library](https://testing-library.com/){:target="_blank"}
* [Playwright](https://playwright.dev/){:target="_blank"}
* [WebdriverIO](https://webdriver.io/){:target="_blank"}
* [Vitest](https://vitest.dev/){:target="_blank"}
* [Selenium](https://www.selenium.dev/){:target="_blank"}
* [TestCafe](https://testcafe.io/){:target="_blank"}

### Mobile & Desktop
* [Electron](https://www.electronjs.org/){:target="_blank"}
* [React Native](https://reactnative.dev/){:target="_blank"}
* [Native Apps](){:target="_blank"}
* [Cordova](https://cordova.apache.org/){:target="_blank"}
* [Ionic](https://ionicframework.com/){:target="_blank"}
* [Capacitor](https://capacitorjs.com/){:target="_blank"}
* [NW.JS](https://nwjs.io/){:target="_blank"}
* [Expo](https://expo.dev/){:target="_blank"}
* [Quasar](https://quasar.dev/){:target="_blank"}
* [Tauri](https://tauri.app/){:target="_blank"}
* [NativeScript](https://nativescript.org/){:target="_blank"}

### Build Tools
* [webpack](https://webpack.js.org/){:target="_blank"}
* [Parcel](https://parceljs.org/){:target="_blank"}
* [Gulp](https://gulpjs.com/){:target="_blank"}
* [Rollup](https://rollupjs.org/guide/en/){:target="_blank"}
* [Browserify](https://browserify.org/){:target="_blank"}
* [tsc CLI](https://www.typescriptlang.org/){:target="_blank"}
* [Rome](https://rome.tools/){:target="_blank"}
* [Snowpack](https://www.snowpack.dev/){:target="_blank"}
* [SWC](https://swc.rs/){:target="_blank"}
* [esbuild](https://esbuild.github.io/){:target="_blank"}
* [Vite](https://vitejs.dev/){:target="_blank"}
* [WMR](https://wmr.dev/){:target="_blank"}
* [Turbopack](https://turbo.build/pack){:target="_blank"}

### Monorepo Tools
* [Rush](https://rushjs.io/){:target="_blank"}
* [Turborepo](https://turbo.build/repo){:target="_blank"}
* [Yarn Workspaces](https://classic.yarnpkg.com/lang/en/docs/workspaces/){:target="_blank"}
* [Yalc](https://github.com/wclr/yalc){:target="_blank"}
* [Lerna](https://lerna.js.org/){:target="_blank"}
* [npm Workspaces](https://docs.npmjs.com/cli/v7/using-npm/workspaces){:target="_blank"}
* [pnpm](https://pnpm.io/){:target="_blank"}
* [Nx](https://nx.dev/){:target="_blank"}

### Other Tools
* [Immer](https://immerjs.github.io/immer/){:target="_blank"}
* [Lodash](https://lodash.com/){:target="_blank"}
* [Underscore.js](https://underscorejs.org/){:target="_blank"}
* [Ramda](https://ramdajs.com/){:target="_blank"}
* [jQuery](https://jquery.com/){:target="_blank"}
* [RxJS](https://rxjs.dev/){:target="_blank"}
* [stdlib](https://stdlib.io/){:target="_blank"}
* [Zod](https://zod.dev/){:target="_blank"}
* [Partytown](https://partytown.builder.io/){:target="_blank"}
* [Mitosis](https://mitosis.builder.io/){:target="_blank"}

### Date Management
* [Moment](https://momentjs.com/docs/){:target="_blank"}
* [Day.js](https://day.js.org/){:target="_blank"}
* [date-fns](https://date-fns.org/){:target="_blank"}
* [Luxon](https://moment.github.io/luxon/){:target="_blank"}

### Data Visualization
* [D3](https://d3js.org/){:target="_blank"}
* [Mermaid](https://mermaid.js.org/){:target="_blank"}
* [Nivo](https://nivo.rocks/){:target="_blank"}
* [Recharts](https://recharts.org/){:target="_blank"}
* [Visx](https://airbnb.io/visx/){:target="_blank"}
* [Victory](https://formidable.com/open-source/victory/){:target="_blank"}
* [ECharts](https://echarts.apache.org/en/index.html){:target="_blank"}
* [Chart.js](https://www.chartjs.org/){:target="_blank"}
* [Highcharts](https://www.highcharts.com/){:target="_blank"}
* [Plotly](https://plotly.com/){:target="_blank"}

### Graphics & Animations
* [Three.js](https://threejs.org/){:target="_blank"}
* [Theatre.js](https://www.theatrejs.com/){:target="_blank"}
* [Anime.js](https://animejs.com/){:target="_blank"}
* [React-Spring](https://www.react-spring.dev/){:target="_blank"}
* [Lottie](https://lottiefiles.com/){:target="_blank"}
* [GreenSock](https://greensock.com/){:target="_blank"}
* [Popmotion](https://popmotion.io/){:target="_blank"}
* [Framer Motion](https://www.framer.com/motion/){:target="_blank"}
* [motion_one](https://motion.dev/){:target="_blank"}

### Data Fetching
* [tRPC](https://trpc.io/){:target="_blank"}
* [Apollo Client](https://www.apollographql.com/docs/react/){:target="_blank"}
* [Axios](https://axios-http.com/){:target="_blank"}
* [TanStack Query (React Query)](https://tanstack.com/query/v4){:target="_blank"}
* [swr](https://swr.vercel.app/){:target="_blank"}
* [Relay](https://relay.dev/){:target="_blank"}

### Back-end Frameworks
* [Express](https://expressjs.com/){:target="_blank"}
* [Nest](https://nestjs.com/){:target="_blank"}
* [Strapi](https://strapi.io/){:target="_blank"}
* [Fastify](https://www.fastify.io/){:target="_blank"}
* [Meteor](https://www.meteor.com/){:target="_blank"}
* [Hapi](https://hapi.dev/){:target="_blank"}
* [Koa](https://koajs.com/){:target="_blank"}
* [Adonis](https://adonisjs.com/){:target="_blank"}
* [Keystone](https://keystonejs.com/){:target="_blank"}
* [Redwood](https://redwoodjs.com/){:target="_blank"}

### Utilities
* [Babel](https://babeljs.io/){:target="_blank"}
* [nvm](https://github.com/nvm-sh/nvm){:target="_blank"}
* [n](https://github.com/tj/n){:target="_blank"}
* [zx](https://github.com/google/zx){:target="_blank"}
* [Volta](https://volta.sh/){:target="_blank"}
* [Verdaccio](https://verdaccio.org/){:target="_blank"}

### JavaScript Runtimes
* Browser
* [Node.js](https://nodejs.org/){:target="_blank"}
* [Deno](https://deno.land/){:target="_blank"}
* [ChakraCore](https://github.com/chakra-core/ChakraCore){:target="_blank"}
* [Hermes](https://hermesengine.dev/){:target="_blank"}
* Service Workers
* [Bun](https://bun.sh/){:target="_blank"}

### JavaScript Edge/Serverless Runtimes
* [AWS Lambda](https://aws.amazon.com/lambda/){:target="_blank"}
* [Cloudflare Workers](https://workers.cloudflare.com/){:target="_blank"}
* [Netlify Edge Functions](https://www.netlify.com/products/edge/){:target="_blank"}
* [Fastly Edge Compute](https://www.fastly.com/products/edge-compute){:target="_blank"}
* [Google Cloud Functions](https://cloud.google.com/functions){:target="_blank"}
* [Akamai EdgeWorkers](https://www.akamai.com/solutions/edge){:target="_blank"}
* [Next.js Edge Runtime](https://nextjs.org/docs/api-reference/edge-runtime){:target="_blank"}
* [Fly.io](https://fly.io/){:target="_blank"}
* [Digital Ocean Functions](https://docs.digitalocean.com/products/functions/){:target="_blank"}

### JavaScript Flavors
* [TypeScript](https://www.typescriptlang.org/){:target="_blank"}
* [Reason](https://reasonml.github.io/){:target="_blank"}
* [Flow](https://flow.org/){:target="_blank"}
* [Elm](https://elm-lang.org/){:target="_blank"}
* [ClojureScript](https://clojurescript.org/reference/javascript-api){:target="_blank"}
* [PureScript](https://www.purescript.org/){:target="_blank"}
* [CoffeeScript](https://coffeescript.org/){:target="_blank"}
* [ReScript](https://rescript-lang.org/){:target="_blank"}
* [Imba](https://imba.io/){:target="_blank"}

### Non-JavaScript Languages
* [PHP](https://www.php.net/){:target="_blank"}
* [Ruby](https://www.ruby-lang.org/en/){:target="_blank"}
* [Python](https://www.python.org/){:target="_blank"}
* [Go](https://go.dev/){:target="_blank"}
* [Rust](https://www.rust-lang.org/){:target="_blank"}
* [Java](https://www.java.com/){:target="_blank"}
* [C/C++](https://isocpp.org/){:target="_blank"}
* [Objective-C](https://developer.apple.com/library/archive/documentation/Cocoa/Conceptual/ProgrammingWithObjectiveC/Introduction/Introduction.html){:target="_blank"}
* [Scala](https://www.scala-lang.org/){:target="_blank"}
* [Swift](https://www.swift.com/){:target="_blank"}

### Which sites/courses/etc. do you consult?
* [Stack Overflow](https://stackoverflow.com/){:target="_blank"}
* [Udemy](https://www.udemy.com/){:target="_blank"}
* [W3Schools](https://www.w3schools.com/){:target="_blank"}
* [MDN](https://developer.mozilla.org/en-US/){:target="_blank"}
* [freeCodeCamp](https://www.freecodecamp.org/){:target="_blank"}
* [Codecademy](https://www.codecademy.com/){:target="_blank"}
* [Web.dev](https://web.dev/){:target="_blank"}
* [JavaScript.info](https://javascript.info/){:target="_blank"}
* [Scrimba](https://scrimba.com/){:target="_blank"}
* [Frontend Masters](https://frontendmasters.com/){:target="_blank"}

### Video Creators
* [Fireship](https://www.youtube.com/@Fireship/){:target="_blank"}
* [Kevin Powell](https://www.youtube.com/@KevinPowell){:target="_blank"}
* [Fun Fun Function](https://www.youtube.com/@funfunfunction){:target="_blank"}
* [Theo - ping․gg](https://www.youtube.com/@t3dotgg){:target="_blank"}
* [Tina Huang](https://www.youtube.com/@TinaHuang1){:target="_blank"}
* [Jason Goodison](https://www.youtube.com/@JasonGoodison){:target="_blank"}
* [Programming with Mosh](https://www.youtube.com/@programmingwithmosh){:target="_blank"}
* [Kent C. Dodds](https://www.youtube.com/@KentCDodds-vids){:target="_blank"}
* [Brad Traversy](https://www.youtube.com/@TraversyMedia){:target="_blank"}
* [Clever Programmer](https://www.youtube.com/@CleverProgrammer){:target="_blank"}

### Podcasts
* [Syntax](https://syntax.fm/){:target="_blank"}
* [JS Party](https://changelog.com/jsparty){:target="_blank"}
* [The Changelog](https://changelog.com/podcast){:target="_blank"}
* [HTTP 203](https://developers.google.com/web/shows/http203/podcast){:target="_blank"}
* [Shop Talk Show](https://shoptalkshow.com/){:target="_blank"}
* [Full Stack Radio](https://fullstackradio.com/){:target="_blank"}
* [JavaScript Jabber](https://topenddevs.com/podcasts/javascript-jabber){:target="_blank"}
* [Front End Happy Hour](https://www.frontendhappyhour.com/){:target="_blank"}
* [React Podcast](https://reactpodcast.simplecast.com/){:target="_blank"}
* [Ladybug Podcast](https://www.ladybug.dev/){:target="_blank"}

___

## OLD STUFF: Vanilla JS IE11 Friendly AJAX Request
```javascript
Vanilla JS IE11 Friendly AJAX Requestfunction jsonp(uri) {
  return new Promise(function(resolve, reject) {
    var id = '_' + Math.round(10000 * Math.random());
    var callbackName = 'jsonp_callback_' + id;
    window[callbackName] = function(data) {
      delete window[callbackName];
      var ele = document.getElementById(id);
      ele.parentNode.removeChild(ele);
      resolve(data);
    }

    var src = uri + '&callback=' + callbackName;
    var script = document.createElement('script');
    script.src = src;
    script.id = id;
    script.addEventListener('error', reject);
    (document.getElementsByTagName('head')[0] || document.body || document.documentElement).appendChild(script)
  });
}

if (navigator.userAgent.toLowerCase().indexOf('msie') > -1 && window.XDomainRequest) {
  // Use Microsoft XDR
  var xdr = new XDomainRequest();
  xdr.open("get", url);
  xdr.onload = function() {
    // XDomainRequest doesn't provide responseXml, so if you need it:
    var dom = new ActiveXObject("Microsoft.XMLDOM");
    dom.async = false;
    dom.loadXML(xdr.responseText["data"][0]);
  };
  xdr.send();
} else {
  jsonp(url).then(function(data){
    temp_get_symbol_payload = data["data"][0];

    /*if there are more than 1 result(s)*/
    if (temp_get_symbol_payload) {
      if (temp_get_symbol_payload.length > 0) {
        get_holding_payload.classList.remove("display:none");
        get_holding_payload.innerHTML = "";
        /*iterate through*/
        for(let i=0;i<temp_get_symbol_payload.length;i++) {
          get_holding_payload.insertAdjacentHTML('beforeend', self.render_autocomplete_result(query,i,input_id,autocomplete_id,temp_get_symbol_payload[i]));
          if (i === results_max_results) {
            break;
          }
        }
      }
    }
  });
}
```