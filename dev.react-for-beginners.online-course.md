# Warren's Notes for React for Beginners (Online Course)
v.20180122\
https://courses.wesbos.com/

---
## Table of Contents
* [Module 01: Introduction, Tooling and Editor Setup](#module-01-introduction-tooling-and-editor-setup)
* [Module 02: Thinking and Understanding React Components](#module-02-thinking-and-understanding-react-components)
* [Module 03: Creating our First Components]()
* [Module 04: Writing HTML with JSX]()
* [Module 05: Loading CSS into our React Application]()
* [Module 06: Creating our application layout with components]()
* [Module 07: Passing Dynamic data with props]()
* [Module 08: Stateless Functional Components]()
* [Module 09: Routing with React Router]()
* [Module 10: Helper and Utility Functions]()
* [Module 11: Working with React Events]()
* [Module 12: All About React Router]()
* [Module 13: Understanding State]()
* [Module 14: Loading data into state onClick]()
* [Module 15: Displaying State with JSX]()
* [Module 16: Updating Order State]()
* [Module 17: Displaying Order State with JSX]()
* [Module 18: Persisting our State with Firebase]()
* [Module 19: Persisting Order State with localstorage]()
* [Module 20: Bi-directional Data Flow and Live State Editing ]()
* [Module 21: Removing Items from State]()
* [Module 22: Animating React Components]()
* [Module 23: Component Validation with PropTypes]()
* [Module 24: Authentication]()
* [Module 25: Building React for Production]()
* [Module 26: Deploying to now.sh]()
* [Module 27: Deploying to GitHub Pages]()
* [Module 28: Deploying to an Apache Server]()
* [Module 29: Future React Today - Property Initializers and getting rid of .bind()]()
* [Module 30: Ejecting from create-react-app]()
---

## Module 01: Introduction, Tooling and Editor Setup
* **Requirements:** NodeJS, React Dev Tools (Extension), Babel extension, Terminal (cmder)
* Need Module bundler (e.g. Webpack) rather than link to react references all the time
* Shortcut: `cd` (and then drag folder into terminal) to navigation to folder quickly
* Need: Create React App (create-react-app) via `npm install -g create-react-app`

## Module 02: Thinking and Understanding React Components
* Everything is a component - a reusable peice of the website
* React - you can use your own tag
* Using React Dev Tools shows how a site is build/what custom components are used

## Module 03: Creating our First Components
* `<div id="main">` is the mounting point for React App
* `import { render } from 'react-dom';` to render the code as DOM/HTML (as opposed to for an Android App)
* `import ReactDom from 'react-dom';` will load the whole ReactDom package but we don't need entire package, just need `render` method
* An example of a simple component, rendered to a div (`<div id="#main">`)
```javascript
class StorePicker extends React.Component {
  render() {
    return <p>Hello</p>
  }
}

render(<StorePicker/>,document.querySelector('#main'));
```
* Best Practice is each component is its own file
* Each file in the `components` folder
* `./index.js`
```javascript
import React from 'react';
import { render } from 'react-dom';

import StorePicker from './components/StorePicker';

render(<StorePicker/>,document.querySelector('#main'));
```

* `./components/StorePicker.js`
```javascript
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
* `return React.createElement('p', {className: 'Testing'}, 'Test');` - a (bad) way to write HTML
* Better way
```javascript
  return (
    All the HTML code you need
  )
```
* cannot use `class` because it is a reserved word/name in JavaScript - use `className`
* Can only return 1 parent element. This is okay:
```javascript
  return (
    <form>
    </form>
  )
```
This is not:
```javascript
  return (
    <form>
    </form>
    <p>
    </p>
  )
```
* Self-closing tags need to be self-closed (similar to XHTML, not like HTML5) e.g. `img` `input` `hr` `br`
* Comments - `{/* comment */}` when in JSX
* Comments - don't put them at the same level as your returned code, the render function can only return 1 parent element

## Module 05: Loading CSS into our React Application
* Ways to load CSS: Inline styles, separate files, or loading CSS/SASS into HTML file
* In this example, we're loading a file into the HTML file via `import './css/style.css';`

## Module 06: Creating our application layout with components
* Modified App component + Created 3 new components
```javascript
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

export default App
```

## Module 07: Passing Dynamic data with props
* Pass data to component via `props`, with is like an attribute for a component
```javascript
in `App.js`
<Header tagline="Fresh Seafood Market"/>

in `Header.js`
<h3 className="tagline">{this.props.tagline}</h3>
```
* `this` refers to the component
* Passing a number, variable, for bollean, you need to wrap value in `{ }`
* If you need to debug a component, go to the component in React Dev Tools, then go to `Console` and press `$r`
* (Not React Related) If you need to debug some html, go to the component in Dev Tools, then go to `Console` and press `$0`

## Module 08: Stateless Functional Components
* Used for "simple" components that don't really do anything else/have no other methods expect render stuff
* Instead of
```javascript
class Header extends React.Component {
  render () {
    return (
      {/* code */}
    );
  }
}
```
You can use (best practice):
```javascript
const Header = (props) = > {
    return (
      {/* code */}
    );
}
```
or
```javascript
function Header(props) {
    return (
      {/* code */}
    );
}
```
or
```javascript
const Header = function(props) {
    return (
      {/* code */}
    );
}
```

## Module 09: Routing with React Router
* React Router is not part of React
* React Router 4 is being used - to show/hide components depending on URL
* `index.js`
```javascript
import React from 'react';
import { render } from 'react-dom';
import { BrowserRouter, Match, Miss } from 'react-router';

import App from './components/App';
import StorePicker from './components/StorePicker';
import NotFound from './components/NotFound';

const Root = () => {
  return (
    <BrowserRouter>
      <div>{/* Match cannot be a child of BrowserRouter....I guess? */}
        {/* For the root */}
        <Match exactly pattern='/' component={StorePicker} />
        {/* For anything '/store' */}
        <Match pattern='/store/:storeId' component={App} />
        {/* For anything '/store' */}
        <Miss component={NotFound} />
      </div>
    </BrowserRouter>
  )
}

render(<Root/>,document.querySelector('#main'));
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
* In React, you don't want to touch the DOM
* This will make it so that `StorePicker.storeInput` references the `input`
```javascript
<input type='text' required placeholder='Store Name' defaultValue={getFunName()}
  ref={(input) => { this.storeInput = input}} />
```
* Constructor - the code that runs when a component is created
* To bind `this` inside a function, you can do :
```javascript
  constructor() {
    super(); /*runs React.Component*/
    this.goToStore = this.goToStore.bind(this);
  }
  goToStore(event) {
    console.log(this); /*is now the correct 'this'*/
  }
```
And call the event through
```javascript
<form action='' className='store-selector' onSubmit={this.goToStore.bind(this)}>
```
OR
```javascript
<form action='' className='store-selector' onSubmit={(e) => this.goToStore(e)}>
```
* Altogether
```javascript
class StorePicker extends React.Component {
  goToStore(event) {
    /*stopped form from submitting*/
    event.preventDefault();
    //grab text from box
    console.log(this.storeInput.value);
    //transition from / to store/id
  }

  render () {
    return (
      <form action='' className='store-selector' onSubmit={(e) => this.goToStore(e)}>
        <input type='text' required placeholder='Store Name' defaultValue={getFunName()} ref={(input) => { this.storeInput = input}} />
      </form>
    );
  }
}
```

## Module 12: All About React Router
* React Router 4: 2 main ways to change the page: Declarative (use a component) and Imperative (use a function e.g. `.transitionTo`)
* BrowserRouter is the parent of the entire application, so you can access it at any time
* Use "Context" to surface the router - delcare something at a top level and it will be made available to children
* State holds data, Props passes data from parent to child
* At the bottom:
```javascript
/* Tells react that StorePicker wants router */
StorePicker.contextTypes = {
  router: React.PropTypes.object
}
```
* Using transitionTo:
```javascript
  goToStore(event) {
    /*
      code...
    */
    const storeId = this.storeInput.value;
    //transition from / to store/id
    this.context.router.transitionTo(`/store/${storeId}`);
  }
```
* This is all client side so transitionTo uses HTML5 pushState

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
```javascript
class App extends React.Component {
  constructor () {
    super();
    this.addFish = this.addFish.bind(this);
    this.state = {
      fishes: {}
    };
  }

  addFish (fish) {
    const fishes = {...this.state.fishes};
    /* change fishes */
    this.setState({ fishes });
  }
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
```javascript
        <AddFishForm addFish={this.props.addFish} />
```

`AddFishForm.js`
```javascript
class addFishForm extends React.Component {
  createFish (event) {
    event.preventDefault();
    const fish = {
      name: this.name.value,
      price: this.price.value,
      status: this.status.value,
      desc: this.desc.value,
      image: this.image.value
    };
    this.props.addFish(fish);
    this.fishForm.reset();
  }
  render () {
    return (
      <form ref={(input) => { this.fishForm = input; }} action='' className='fish-edit' onSubmit={(e) => this.createFish(e)}>
        <button type='submit'>Add Item</button>
      </form>
    );
  }
}
export default addFishForm;
```

## Module 14: Loading data into state onClick
* On click of a button in `Inventory.js`
```javascript
<button onClick={this.props.loadSamples}>Load Samples</button>
```

We load in a fishes object from `sample-fishes.js`
In `App.js`
```javascript
import sampleFishes from '../sample-fishes';

class App extends React.Component {
  constructor () {
    super();
    this.loadSamples = this.loadSamples.bind(this);
    // getInitialState
    this.state = {
      fishes: {}
    };
  }
  loadSamples () {
    this.setState({
      fishes: sampleFishes
    });
  }
  render () {
    return (
      <div className='catch-of-the-day'>
        <Inventory addFish={this.addFish} loadSamples={this.loadSamples} /> {/* addFish is passed down */}
      </div>
    );
  }
}
```

## Module 15: Displaying State with JSX
* No loops or login in JSX - if you want it, you use regular JavaScript
* `Object.keys(object)` will map over object
* loop over object (`this.state.fishes`)
```javascript
  {
    Object
      .keys(this.state.fishes)
      .map(key => <Fish key={key} details={this.state.fishes[key]}/>)
  }
```

## Module 16: Updating Order State
* if you need to pass a key, use `index`. `key` is for the component, `index` is for you.

## Module 17: Displaying Order State with JSX
* Not good practice to push state down

## Module 18: Persisting our State with Firebase
* Firebase is product from Google
* Uses HTML5 websockets - you can sync data from app and firebase and vice versa
* Firebase saves information as one big object which is good because state is one big object
* created base.js and filled it with Firebase code allowing export of `base` so it can be imported elsewhere
* `componentWillMount` - when component is mounted, you can do ajax request/connect to rebase/sync component state with firebase state
* Use firebase and these functions to maintain state across Firebase
```javascript
  componentWillMount () {
    this.ref = base.syncState(`${this.props.params.storeId}/fishes`, {
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
* Hook into `componentWillUpdate` - invoked before props or state changes
* information stored in Local Storage
``` javascript
  componentWillUpdate (nextProps, nextState) {
    localStorage.setItem('order-${this.props.params.storeId}',JSON.stringify(nextState.order);
  }
```
* `JSON.stringify` to convert `object` to `string`
* information to load from Local Storage
```javascript
  const localStorageRef = localStorage.getItem(`order-${this.props.params.storeId}`);
  if (localStorageRef) {
    this.setState({
      order: JSON.parse(localStorageRef)
    });
  }
```
* `JSON.parse` to convert `string` to `object`

## Module 20: Bi-directional Data Flow and Live State Editing
## Module 21: Removing Items from State
## Module 22: Animating React Components
## Module 23: Component Validation with PropTypes
## Module 24: Authentication
## Module 25: Building React for Production
## Module 26: Deploying to now.sh
## Module 27: Deploying to GitHub Pages
## Module 28: Deploying to an Apache Server
## Module 29: Future React Today - Property Initializers and getting rid of .bind()
## Module 30: Ejecting from create-react-app