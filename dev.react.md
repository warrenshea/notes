# Warren Shea's Notes for React (and NextJS)
v20221114

## Notable JavaScript Experts
* [React, NextJS by Wes Bos](https://wesbos.com/courses){:target="_blank"}

## React
* Ternary `{ num === 7 ? <img> : null }`
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

