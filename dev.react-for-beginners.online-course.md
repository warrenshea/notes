# Warren Shea's Notes for React for Beginners - 2015v1 & 2018v2 (Online Course)
https://courses.wesbos.com/ | https://reactforbeginners.com/
**Version**: 20220729 | **Status**:  Completed

---
## Table of Contents
* [Module 01: Introduction, Tooling and Editor Setup](#module-01-introduction-tooling-and-editor-setup)
* [Module 02: Thinking and Understanding React Components](#module-02-thinking-and-understanding-react-components)
* [Module 03: Creating our First Components](#module-03-creating-our-first-components)
* [Module 04: Writing HTML with JSX](#module-04-writing-html-with-jsx)
* [Module 05: Loading CSS into our React Application](#module-05-loading-css-into-our-react-application)
* [Module 06: Creating our application layout with components](#module-06-creating-our-application-layout-with-components)
* [Module 07: Passing Dynamic data with props](#module-07-passing-dynamic-data-with-props)
* [Module 08: Stateless Functional Components](#module-08-stateless-functional-components)
* [Module 09: Routing with React Router](#module-09-routing-with-react-router)
* [Module 10: Helper and Utility Functions](#module-10-helper-and-utility-functions)
* [Module 11: Working with React Events](#module-11-working-with-react-events)
* [Module 12: Handling Event](#module-12-handling-event)
* [Module 13: Understanding State](#module-13-understanding-state)
* [Module 14: Loading data into state onClick](#module-14-loading-data-into-state-onclick)
* [Module 15: Displaying State with JSX](#module-15-displaying-state-with-jsx)
* [Module 16: Updating Order State](#module-16-updating-order-state)
* [Module 17: Displaying Order State with JSX](#module-17-displaying-order-state-with-jsx)
* [Module 18: Persisting our State with Firebase](#module-18-persisting-our-state-with-firebase)
* [Module 19: Persisting Order State with localstorage](#module-19-persisting-order-state-with-localstorage)
* [Module 20: Bi-directional Data Flow and Live State Editing](#module-20-bi-directional-data-flow-and-live-state-editing)
* [Module 21: Removing Items from State](#module-21-removing-items-from-state)
* [Module 22: Animating React Components](#module-22-animating-react-components)
* [Module 23: Component Validation with PropTypes](#module-23-component-validation-with-proptypes)
* [Module 24: Authentication](#module-24-authentication)
* [Module 25: Building React for Production](#module-25-building-react-for-production)
* [Module 26: Deploying to Now](#module-26-deploying-to-now)
* [Module 27: Deploying to Netlify](#module-27-deploying-to-netlify)
* [Module 28: Deploying to an Apache Server](#module-28-deploying-to-an-apache-server)
* [Module 29: Ejecting from create-react-app](#module-29-ejecting-from-create-react-app)

---

## Module 01: Introduction, Tooling and Editor Setup
* **Requirements:** NodeJS, React Dev Tools (Extension), Babel extension, Terminal (cmder)
* Shortcut: `cd` (and then drag folder into terminal) to navigation to folder quickly
* Dependency: react-scripts, concurrently (does Webpack for us as it's very complicated)
* npm start to run create-react-app

## Module 02: Thinking and Understanding React Components
* Everything in React is a component - a reusable piece of the website
* React - you can use your own tag
* Using React Dev Tools shows how a site is build/what custom components are used

## Module 03: Creating our First Components
* `<div id="main">` is the mounting point for React App
* `import { render } from 'react-dom';` to render the code as DOM/HTML
* An example of a simple component, rendered to a div (`<div id="#main">`)
* `./components/StorePicker.js`


```jsx
class StorePicker extends React.Component {
  render() {
    return <p>Hello</p>
  }
}

render(<StorePicker/>,document.querySelector('#main'));
```
* Best Practice is each component is its own file
* Each file in the `components` folder
* The following two notes is to import the component (index.js) and export the compoonent (export default StorePicker)
* `./index.js`


```jsx
import React from 'react';
import { render } from 'react-dom';

import StorePicker from './components/StorePicker';

render(<StorePicker/>,document.querySelector('#main'));
```

* `./components/StorePicker.js`


```jsx
import React from 'react';

class StorePicker extends React.Component {
  render() {
    return <p>Hello</p>
  }
}

export default StorePicker
```

## Module 04: Writing HTML with JSX
* JSX - write HTML inside JavaScript
* Better way

```jsx
return (
  All the HTML code you need
)
```
* cannot use `class` because it is a reserved word/name in JavaScript - use `className`
* Can only return 1 parent element. This is okay:

```jsx
return (
  <form>
  </form>
)
```
This is not:

```jsx
return (
  <form>
  </form>
  <p>
  </p>
)
```
* Now you can use Fragment, e.g.

```jsx
return (
  <React.Fragment>
    <form>
    </form>
    <p>
    </p>
  </React.Fragment>
)
```
or

```jsx
  return (
    <>
      <form>
      </form>
      <p>
      </p>
    </>
  )
```
* Self-closing tags need to be self-closed (similar to XHTML, not like HTML5) e.g. `img` `input` `hr` `br`
* Comments - `{/* comment */}` when in JSX, curly brackets means "I'm doing JavaScript"
* Comments - don't put them at the same level as your returned code, the render function can only return 1 parent element

## Module 05: Loading CSS into our React Application
* Ways to load CSS: Inline styles, separate files, or loading CSS/SASS into HTML file
* In this example, we're loading a file into the HTML file via `import './css/style.css';`

## Module 06: Creating our application layout with components
* Modified App component + Created 3 new components

```jsx
import React from 'react';
import Header from './Header';
import Order from './Order';
import Inventory from './Inventory';

class App extends React.Component {
  render() {
    /* comment */
    return (
      <div className="catch-of-the-day">
        <div className="menu">
          <Header />
        </div>
        <Order />
        <Inventory />
      </div>
    );
  }
}

export default App;
```

## Module 07: Passing Dynamic data with props
* Pass data to component via `props`, with is like an attribute for a component

```jsx
in `App.js`
<Header tagline="Fresh Seafood Market"/>

in `Header.js`
<h3 className="tagline-class">{this.props.tagline}</h3>
```
* `this` refers to the component
* Passing a number, variable, or boolean, you need to wrap value in `{ }`
* If you need to debug a component, go to the component in React Dev Tools, then go to `Console` and press `$r`
* (Not React Related) If you need to debug some html, go to the component in Dev Tools, then go to `Console` and press `$0`

## Module 08: Stateless Functional Components
* Used for "simple" components that don't really do anything else/have no other methods expect render stuff
* Instead of this React/Smart Component

```jsx
class Header extends React.Component {
  render () {
    return (
      {/* code */}
    );
  }
}
```
You can use Stateless/Dumb/Pure/Simple Component:

```jsx
const Header = props = > {
    return (
      {/* code....note, no this, so {props.tagline} */}
    );
}

const Header = props = > ( /* implicit return method */
    {/* code....note, no this, so {props.tagline} */}
)

const Header = ({tagline,age}) = > ( /* implicit return with destructuring */
    {/* code....note, no this, so {tagline} */}
)

```

## Module 09: Routing with React Router
* React Router is not part of React
* `index.js`

```jsx
import React from 'react';
import { render } from 'react-dom';
import { BrowserRouter, Route, Switch } from 'react-router';

import StorePicker from './components/StorePicker';
import App from './components/App';
import NotFound from './components/NotFound';

const Router = () => {
  return (
    <BrowserRouter>
      <Switch>
        {/* For the root */}
        <Route exact pattern='/' component={StorePicker} />
        {/* For anything '/store' */}
        <Route path='/store/:storeId' component={App} />
        {/* For anything '/store' */}
        <Route component={NotFound} />
      </Switch>
    </BrowserRouter>
  )
}

render(<Router/>,document.querySelector('#main'));
```

## Module 10: Helper and Utility Functions
* Helpers file to stick functions not tied to specific page/functionality - not big enough to be modules
* In the `helpers.js` file
```javascript
export function getFunName() {
}
```
And in the place to call the helper function,
```javascript
import { getFunName } from '../helpers';
```

## Module 11: Working with React Events
* Add events inline into code
* `render` is bound to the component, so refering `this` references the component
* In other functions, `this` does not reference the component
* handleClick on button code:

```jsx
import React from 'react';
import { getFunName} from "../helpers";

class StorePicker extends React.Component {
  handleClick() {
    console.log("clicked");
  }
  render() {
    return (
      <form>
        <button onclick={this.handleClick}>Click</button> {/* don't use this.handleClick() or it will run on mount */}
        <input
          type="text"
          placeholder="Store Name"
          defaultValue={getFunName()}
        />
        <button type="submit"></button
      </form>
    )
  }
}

export default StorePicker
```
* submit form code and get text from input with `ref` to access an item, you don't wanna touch DOM. here are two deprecated ways:

```jsx
<input
  type="text"
  placeholder="Store Name"
  defaultValue={getFunName()}
  ref={myInput} {/*this is deprecated, don't use that - FYI only*/
/>
```

```jsx
<input
  type="text"
  placeholder="Store Name"
  defaultValue={getFunName()}
  ref={(myInput) => this.myInput = myInput} {/*this is deprecated, don't use that - FYI only*/
/>
```
* This is an old way, for reference only and bad if there are a lot of methods

```jsx
import React from 'react';
import { getFunName} from "../helpers";

class StorePicker extends React.Component {
  constructor() {
    super();
    this.goToStore = this.goToStore.bind(this);
  }
  myInput = React.createRef();

  goToStore(event) {
    event.preventDefault(); /*stopped form from submitting*/
    console.log(this.myInput.value); /*grab text from box, this is the component only if goToStore is arrow function*/
  }
  render() {
    return (
      <form onSubmit={this.goToStore}>
        <input
          type="text"
          placeholder="Store Name"
          defaultValue={getFunName()}
          ref={this.myInput}
        />
        <button type="submit"></button
      </form>
    )
  }
}

export default StorePicker
```
* This is the proper way

```jsx
import React from 'react';
import { getFunName} from "../helpers";

class StorePicker extends React.Component {
  myInput = React.createRef();

  goToStore = event => {
    event.preventDefault(); /*stopped form from submitting*/
    console.log(this.myInput.value.value); /*grab text from box, this is the component only if goToStore is arrow function*/
    /*this.myInput.value is React, this.myInput.value.value is JavaScript */
  }
  render() {
    return (
      <form onSubmit={this.goToStore}>
        <input
          type="text"
          placeholder="Store Name"
          defaultValue={getFunName()}
          ref={this.myInput}
        />
        <button type="submit"></button
      </form>
    )
  }
}

export default StorePicker
```

## Module 12: Handling Event
* Change URL of page without window.location

```jsx
...
  goToStore = event => {
    event.preventDefault(); /*stopped form from submitting*/
    const storeName = this.myInput.value.value; /*grab text from box, this is the component only if goToStore is arrow function*/
    /*this.myInput.value is React, this.myInput.value.value is JavaScript */
    this.props.history.push(`/store/${storeName}`); /*this.props is taking props from parent component, which is React Router */
  }
...
```

## Module 13: Understanding State
* State is one object that holds all the data related to all/a piece of the application
* You store all data in a massive object called State - if you change anything on the page, you change State
* If you want to change anything on the page, you change the state / let React handle it for you
* State is tied to App Component - functions that change state are in App.js (in this example)
* State is always tied to a specific Component
* Each Component can have its own state
* Sometimes state needs to be shared among components (e.g. App w/ Order, Inventory) - so then we put State on App Component and pass it down
* Don't forget that if you need to access the function that changes state (e.g. AddFish), you have to attach it to components and reference them as props in the component
`App.js`

```jsx
class App extends React.Component {
  state = { //set initial state
    fishes: {},
    order: {}
  }

  addFish = fish => {
    const fishes = {...this.state.fishes}; /* 1. Take a copy of existing State, you don't want to reach into State and modify it directy */
    fishes[`fish${Date.now()}`] = fish; /* 2. Add new fishes to state */
    this.setState({ fishes }); /* 3. Update state with new fish */
  };
  render () {
    return (
      <div>
        <Inventory addFish={this.addFish} /> {/* addFish is passed down */}
      </div>
    );
  }
}
export default App;
```

`Inventory.js`

```jsx
        <AddFishForm addFish={this.props.addFish} />
```

`AddFishForm.js`

```jsx
class addFishForm extends React.Component {
  nameRef = React.createRef();
  priceRef = React.createRef();

  createFish = (event) => {
    event.preventDefault();
    const fish = {
      name: this.nameRef.value.value,
      price: parseFloat(this.nameRef.value.value), //float to store everything in cents
    };
    this.props.addFish(fish);
    event.currentTarget.reset(); //reset form
  }
  render () {
    return (
      <form className='fish-edit' onSubmit={this.createFish}>
        <input name="name" ref={this.nameRef} type="text" placeholder="Name" />
        <input name="price" ref={this.priceRef} type="text" placeholder="Price" />
        <button type='submit'>+ Add Fish</button>
      </form>
    );
  }
}
export default addFishForm;
```

## Module 14: Loading data into state onClick
* On click of a button in `Inventory.js`

```jsx
<button onClick={this.props.loadSampleFishes}>Load Sample Fishes</button>
```

We load in a fishes object from `sample-fishes.js`
In `App.js`

```jsx
import sampleFishes from '../sample-fishes'; //just an object with a lot of fishes

class App extends React.Component {
  state = { //set initial state
    fishes: {},
    order: {}
  }
  addFish = fish => {
    const fishes = {...this.state.fishes}; /* 1. Take a copy of existing State, you don't want to reach into State and modify it directy */
    fishes[`fish${Date.now()}`] = fish; /* 2. Add new fishes to state */
    this.setState({ fishes }); /* 3. Update state with new fish */
  };
  loadSamples = () => {
    this.setState({ fishes: sampleFishes });
  };
  render () {
    return (
      <div className='catch-of-the-day'>
        <Inventory addFish={this.addFish} loadSampleFishes={this.loadSampleFishes} /> {/* addFish is passed down */}
      </div>
    );
  }
}
```

## Module 15: Displaying State with JSX
* No loops or if or conditional in JSX - if you want it, you use regular JavaScript
* `Object.keys(object)` will map over object
* loop over object (`this.state.fishes`)

```jsx
import sampleFishes from '../sample-fishes'; //just an object with a lot of fishes

class App extends React.Component {
  state = { //set initial state
    fishes: {},
    order: {}
  }
  addFish = fish => {
    const fishes = {...this.state.fishes}; /* 1. Take a copy of existing State, you don't want to reach into State and modify it directy */
    fishes[`fish${Date.now()}`] = fish; /* 2. Add new fishes to state */
    this.setState({ fishes }); /* 3. Update state with new fish */
  };
  loadSamples = () => {
    this.setState({ fishes: sampleFishes });
  };
  render () {
    return (
      <div className='catch-of-the-day'>
        <Header />
        <ul className="fishes">
          {
            Object
              .keys(this.state.fishes) //turn object into array
              .map(key => <Fish key={key} details={this.state.fishes[key]}/>)
          }
        </ul>
        <Order />
        <Inventory addFish={this.addFish} loadSampleFishes={this.loadSampleFishes} /> {/* addFish is passed down */}
      </div>
    );
  }
}
```
`Fish.js` as Simple/Pure/Dumb/Stateless Component

```jsx
import React from 'react';

const Fish = ({ key, details }) => {
  const { image, name, price, desc, status } = details;
  return (
    <li className="menu-fish">
      <img src={image} alt={name} />
      <h3>{name}</h3>
      <span className="price">{formatPrice(price)}</span>
      <span className="description">{desc}</span>
    </li>
  );
}
export default Fish;
```

## Module 16: Updating Order State
* if you need to pass a key, use `index`. `key` is for the component, `index` is for you.

`App.js`

```jsx
import sampleFishes from '../sample-fishes'; //just an object with a lot of fishes

class App extends React.Component {
  state = { //set initial state
    fishes: {},
    order: {}
  }
  // addFish function
  // loadSamples function
  addToOrder = key = {
    const order = {...this.state.order}; //copy order
    order[key] = order[key] + 1 || 1; //Add to order or, if it doesn't exist, add 1
    this.setState({ order }); //update State
  }
  render () {
    return (
      <div className='catch-of-the-day'>
        <Header />
        <ul className="fishes">
          {
            Object
              .keys(this.state.fishes) //turn object into array
              .map(key => <Fish key={key} index={index} details={this.state.fishes[key]} addToOrder={this.addToOrder}/>)
          }
        </ul>
        <Order />
        <Inventory addFish={this.addFish} loadSampleFishes={this.loadSampleFishes} /> {/* addFish is passed down */}
      </div>
    );
  }
}

```

```jsx
import React from 'react';

const Fish = ({ details, addToOrder, index }) => {
  handleClick = () => {
    addToOrder(index);
  }
  const { image, name, price, desc, status } = details;
  const isAvailable = status === 'availabe';
  return (
    <li className="menu-fish">
      <img src={image} alt={name} />
      <h3>{name}</h3>
      <span className="price">{formatPrice(price)}</span>
      <span className="description">{desc}</span>
      <button disabled={!isAvailable} onClick={this.handeClick}>{ (isAvailable) ? "Add to Order" : "Sold Out!" }</button>
      {/* OR do it as a one liner */}
      <button disabled={!isAvailable} onClick={() => addToOrder(index)}>{ (isAvailable) ? "Add to Order" : "Sold Out!" }</button>
    </li>
  );
}
export default Fish;
```

## Module 17: Displaying Order State with JSX
* Not good practice to push state down, better to just pass down what you need e.g

```jsx
  <Order {...this.state}>
```
Reduce takes in data and takes in a tally

## Module 18: Persisting our State with Firebase
* Firebase is product from Google
* Uses HTML5 websockets - you can sync data from app and firebase and vice versa
* Firebase saves information as one big object which is good because state is one big object
* created base.js and filled it with Firebase code allowing export of `base` so it can be imported elsewhere
* `componentWillMount` - when component is mounted, you can do ajax request/connect to rebase/sync component state with firebase state
* Use firebase and these functions to maintain state across Firebase
* In the App.js

```jsx
componentDidMount () {
  const { params } = this.props.match
  this.ref = base.syncState(`${params.storeId}/fishes`, {
    context: this,
    state: 'fishes'
  });
}
componentWillUnmount () {
  base.removeBinding(this.ref);
}
```

## Module 19: Persisting Order State with localstorage
* Better to store this information as local storage VS cookies or Firebase
* Hook into `componentDidUpdate` - invoked before props or state changes
* information stored in Local Storage
``` jsx
componentDidUpdate () {
  localStorage.setItem(this.props.match.params.stordId,JSON.stringify(this.state.order);
}
```
* `JSON.stringify` to convert `object` to `string`
* information to load from Local Storage

```jsx
componentDidMount () {
  const { params } = this.props.match;
  /* new */
  const localStorageRef = localStorage.getItem(params.storeId);
  if (localStorageRef) {
    this.setState({ order: JSON.parse(localStorageRef) });
  } /* new end */
  this.ref = base.syncState(`${params.storeId}/fishes`, {
    context: this,
    state: 'fishes'
  });
}
```
* `JSON.parse` to convert `string` to `object`

## Module 20: Bi-directional Data Flow and Live State Editing
* console.log(event.currentTarget.name) in handleChange function can indicate which input got updated
* Changing input values, must update State (put function in App.js and pass function down as Props)

## Module 21: Removing Items from State

## Module 22: Animating React Components
* Using library for animation

```jsx
import { TransitionGroup, CSSTransition } from "react-transition-group";

<TransitionGroup component="ul"> replacing <ul>
<CSSTransition classNames="order" key="{key}" timeout={{ enter: 250, exit: 250 }}> WRAPS <li>

```

## Module 23: Component Validation with PropTypes
* React Prop Validation via PropTypes (or TypeScript)
* React Component

```jsx
import PropTypes from "prop-types";

class Fish extends React.Component {
  static propTypes = {
    tagline: PropTypes.string.isRequired,
    functionA : PropTypes.func,
    details: PropTypes.shape({
      image: PropTypes.string,
      price: PropTypes.number
    })
  }
  ...
```
* Simple Component

```jsx
import PropTypes from "prop-types";

const Header = props => (
  ...
);

Header.propTypes = {
  tagline: PropTypes.string.isRequired,
  functionA : PropTypes.func,
  details: PropTypes.shape({
    image: PropTypes.string,
    price: PropTypes.number
  })
}
```
## Module 24: Authentication
* Firebase authentication

## Module 25: Building React for Production
```bash
npm run build
```

## Module 26: Deploying to Now
```bash
npm i -g now
now -v
npm i -g serve
```
Replace `start` with `dev`, create new `start` url
```json
package.json

"start": "serve --single ./build"
```
```bash
now
```
will deploy to server

Use alias to deploy to same url

## Module 27: Deploying to Netlify
* You can upload zip file
* Hook to Git Repo
```bash
npm i -g netlify
netlify -v
netlify deploy
Q: Yes
A: Build
```
* Need _redirects file
```txt
/* /index.html 200`
```

## Module 28: Deploying to an Apache Server
* Important to put everything in clean subdomain name
* May need to add Firebase and "Authorize" site
* .htaccess file
```htaccess
RewriteBase /
RewriteRule ^index\.html$ - [L]
RewriteCond %{REQUEST_FILENAME} !-f
RewriteCond %{REQUEST_FILENAME} !-d
RewriteRule . /index.html [L]
```

## Module 29: Ejecting from create-react-app
* Do on a branch, you can't undo eject
* npm run eject
* It will have tons more packages in package.json
* Go through Webpack to see how it works
* Try stuff with Jest or Babel or something