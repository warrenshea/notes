# Warren Shea's Notes for JavaScript (and TypeScript)
v20221114

## Notable JavaScript Experts
* [TypeScript, React, NextJS, ES6 by Wes Bos](https://wesbos.com/courses){:target="_blank"}
* [Design Patterns by Addy Osmani](https://www.patterns.dev/posts/classic-design-patterns/){:target="_blank"}

## Truthy/Falsy
In a conditional statement, these values are not true or false (boolean) but are accepted as conditions:

* Truthys: `Object`, `Array`, non empty string, number other than 0, Date
* Falsys: `""`, `0`, `null`, `undefined`, `NaN`

`!!` ("bang bang") converts Truthy/Falsy to boolean "true" or "false"

## Better console.log
* Original `console.log(error,loading,success,data);`
* Variant 1: `console.log(`Error:${error},Loading:${loading},Success:${success},Data:${data}`);`
* Variant 2: `console.log({error,loading,success,data});`

## event.prevent
* `event.preventDefault();`
* `event.preventStopPropagation();`

___

## TypeScript

`if (typeof padding === "number") {`
* Type Narrowing: the _process_ of refining types to more specific types
* Type Guards: this code is a special form of code called _type guard_

* Implicit Types do not need to be declared. Examples can be private or local variables
* Explicit Types should be declared: function inputs, outputs, anything exported or public

* TC39 - Types //as Comments ECMAScript Proposal for TypeScript inside JavaScript

___

## React
* Ternerary `{ num === 7 ? <img> : null }`
* Another way
```
{ num === 7 &&
    <img>
}
```
### Hooks
* useState: `const [piece of state, function of piece of state] = useState(initialValue)`
```jsx
[count,setCount] = useState(count)
onClick={() => setCount(count +1)};

[calculator,setCalculator] = useState({ count }) //if you wanted calculator.count to update
onClick={() => setCalculator({...calculator,count:calculator.count + 1})};
```
* useToggle: (from Udemy 248)
```jsx
import { useState } from "react";
function useToggle(initialVal = false) {
  const [state,setState] = useState(initialVal);
  const toggle = () => {
    setState(!state);
  };
  return [state, toggle];
}
export default useToggle;
```
* useEffect: runs after every render
```jsx
useEffect = () => {
  document.title = `You clicked ${count} times`;
}
```
* Don't update state in useEffect
* if you don't want useEffect to always run
```jsx
useEffect = () => {
  //do something only when number or year is changed
}, [number ,year];
```
___

## NextJS

___

## IIFE - Immediate-invoked Function Expressions
To execute functions immediately, as soon as they are created
Don't pollute the global object, simple way to isolate variables declarations

```javascript
(function() {
  /* */
})()

(function doSomething() {
  /* */
})()

(() => {
  /* */
})()
```

___

## Questions to look into at some point

## Difference between .call and .apply
## Explain function.prototype.bind
## When would you use document.write()?
## What's the difference between feature detection, feature inference, and using the UA string?
## Explain how JSONP works and why it's not really AJAX
## Explain event bubbling
## Explain the difference between and "attribute" and a "property"
## Difference between document load event and document ready event?
## Explain the same-origin policy with regards to Javascript.
## Why is it called a Ternary expression, what does the word "Ternary" indicate?
## what is "use strict";? what are the advantages and disadvantages to using it?
## Why would you use something like the load event? Does this event have disadvantages? Do you know any alternatives, and why would you use those?
## Explain what a single page app is and how to make one SEO-friendly.
## What is the extent of your experience with Promises and/or their polyfills? What are the pros and cons of using Promises instead of callbacks?
## What are some of the advantages/disadvantages of writing Javascript code in a language that compiles to Javascript?
## What is the purpose of a code style linting tool?

## Explain hoisting
before executing your code in the order you wrote it, javascript “pulls up” two types of declarations:

function bla() {}
var bla

to the top of the containing function (or file if you’re at top level). this lets yiu call a function declared this way even if it’s defined below.
- Dan Abramov

## What is "this"
it’s like a hidden argument to your function. calls with dot, like obj.fn(), pass the part before the dot (obj) as this. calls without a dot, like fn(), don’t pass any this. if you didn’t pass any this, it’s set to a default (undefined in strict mode, window in loose mode).
- Dan Abramov

## What are closures
functions can read or write variables “outside” of them. this works not only with top level variables, but with local variables too (from nested functions). that’s called closures.
- Dan Abramov

## What are generators
generators let your function return multiple values. not necessarily immediately — the caller decides when to ask for the next one. useful to describe operations where you can “ask for more”, like processing a long list or deciding each next step based on user input
- Dan Abramov

## What is currying
imagine functions only take one argument. how would we pass many? one way is to pass an object: ({ a, b, c }) => … but we could also turn our function into a matryoshka of many functions where each takes one arg: (a) => (b) => (c) => … that’s currying. not very useful in js.
- Dan Abramov

## What is bind()
"this" is a hidden argument to your function. "bind" wraps a function with the "this" you provide so that you don’t need to remember to pass the correct "this" every time
- Dan Abramov

## What are monads?
it’s an abstraction but a very generic one so hard to describe. i’d describe it as “wrapper for a value which lets you apply operations on that value, producing more such wrappers”. promise then(), if we skip minor pedantic distinctions, are an example of that.
- Dan Abramov

## What is an event loop?
event loop is a set of rules for how the runtime (browser / Node) decides what code to run when it has finished running the current code. for example “okay we’ve exited all functions, so now, let’s run expired timeouts”. that includes code after “await” if the thing has resolved
- Dan Abramov

## When to use classes instead of factory functions
if you want people to extend your classes (to fill in some functionality) then it seems like it’s easier to do this with actual classes.
- Dan Abramov

## Use cases for WeakMap/WeakSet
associate some information with an object i don’t own. like a memoization cache. weakmap is good for this because it doesn’t hold onto it, so i’m not causing a memory leak. the tradeoff is i can’t iterate over the list of objects for which i hold information.
- Dan Abramov

https://justjavascript.com/

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

