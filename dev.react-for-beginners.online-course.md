# Warren's Notes for React for Beginners (Online Course)
v.20180122\
https://courses.wesbos.com/

---
## Table of Contents
* [Module 01: Introduction, Tooling and Editor Setup]()
* [Module 02: Thinking and Understanding React Components]()
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
```
class StorePicker extends React.Component {
  render() {
    return <p>Hello</p>
  }
}

render(<StorePicker/>,document.querySelector('#main'));
```
* Best Practice is each component is its own file
* Each file in the `components` folder
* ./index.js
```
import React from 'react';
import { render } from 'react-dom';

import StorePicker from './components/StorePicker';

render(<StorePicker/>,document.querySelector('#main'));
```

* ./components/StorePicker.js
```
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
```
  return (
    All the HTML code you need
  )
```
* cannot use `class` because it is a reserved word/name in JavaScript - use `className`
* Can only return 1 parent element. This is okay:
```
  return (
    <form>
    </form>
  )
```
This is not:
```
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
```
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
```
(in App.js)
<Header tagline="Fresh Seafood Market"/>

(in Header.js)
<h3 className="tagline">{this.props.tagline}</h3>
```
* Passing a number, variable, for bollean, you need to wrap value in `{ }`
* If you need to debug a component, go to the component in React Dev Tools, then go to `Console` and press `$r`
* (Not React Related) If you need to debug some html, go to the component in Dev Tools, then go to `Console` and press `$0`

## Module 08: Stateless Functional Components
* Used for "simple" components that don't really do anything else/have no other methods expect render stuff
* Instead of
```
class Header extends React.Component {
  render () {
    return (
      {/* code */}
    );
  }
}
```
You can use (best practice):
```
const Header = (props) = > {
    return (
      {/* code */}
    );
}
```
or
```
function Header(props) {
    return (
      {/* code */}
    );
}
```
or
```
const Header = function(props) {
    return (
      {/* code */}
    );
}
```

## Module 09: Routing with React Router
* React Router is not part of React
* React Router 4 is being used - to show/hide components depending on URL
* index.js
```
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
## Module 11: Working with React Events
## Module 12: All About React Router
## Module 13: Understanding State
## Module 14: Loading data into state onClick
## Module 15: Displaying State with JSX
## Module 16: Updating Order State
## Module 17: Displaying Order State with JSX
## Module 18: Persisting our State with Firebase
## Module 19: Persisting Order State with localstorage
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