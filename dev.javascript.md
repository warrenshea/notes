# Warren Shea's Notes for JavaScript
v20191221

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