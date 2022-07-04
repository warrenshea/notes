  # Warren Shea's Notes for Advanced React (Online Course)
https://courses.wesbos.com/ | https://advancedreact.com/
**Version**: 20210702 | **Status**:  In Progress

---
## Table of Contents
### Module 01 Introduction and Setup
* [Module 01.01 Tooling and Starter Files Setup]()
* [Module 01.02 The Tech Stack Explained]()
### Module 02 Learning Next.js
* [Module 02.01 An intro to Next]()
* [Module 02.02 Creating a Page Layout Component]()
* [Module 02.03 Creating our Header and Nav Components]()
### Module 03 CSS and Styled Components
* [Module 03.01 An Intro to Styled Components and CSS]()
* [Module 03.02 Global Styles, Typography and Layout Styles]()
* [Module 03.03 Visualizing Route Changes]()
* [Module 03.04 Fixing Styled Components Flicker on Server Render]()
### Module 04 Server Side GraphQL Development
* [Module 04.01 Setting up MongoDB]()
* [Module 04.02 An Intro to GraphQL]()
* [Module 04.03 Setting up Keystone and Typescript]()
* [Module 04.04 Creating our first User data type]()
* [Module 04.05 Adding Auth to our Application]()
* [Module 04.06 Creating our Products Data Type]()
* [Module 04.07 Uploading Product Images]()
* [Module 04.08 Creating two way data relationships in Keystone]()
* [Module 04.09 Inserting Seed Data]()
### Module 05 Client Side React + GraphQL Development
* [Module 05.01 Setting up Apollo Client]()
* [Module 05.02 Fetching Data with hooks and Displaying it in our Front End]()
* [Module 05.03 Fixing and Styling the Nav]()
* [Module 05.04 A real good lesson in React Forms and Custom Hooks]()
* [Module 05.05 Hooking up our File input and Form Styles]()
* [Module 05.06 Creating Products via our Mutations]()
* [Module 05.07 Refetching Queries after a Successful Mutation]()
* [Module 05.08 Programmatically Changing the Page after product creation]()
* [Module 05.09 Displaying Single Items, Routing and SEO]()
### Module 06 Working with Mutations
* [Module 06.01 Updating Items]()
* [Module 06.02 Using useEffect to deal with a tricky loading state issue]()
* [Module 06.03 Deleting Products]()
* [Module 06.04 Evicting Items from the Apollo Cache]()
### Module 07 Pagination
* [Module 07.01 Pagination Links]()
* [Module 07.02 Pagination Dynamic Routing]()
* [Module 07.03 Adjusting our Query for Pagination Values]()
* [Module 07.04 Custom Type Policies and Control over the Apollo Cache]()
### Module 08 User Registration + Authentication
* [Module 08.01 Querying The Current User]()
* [Module 08.02 Creating a Sign In Component]()
* [Module 08.03 Creating a Sign Out Component]()
* [Module 08.04 Creating our Sign Up Flow]()
* [Module 08.05 Password Reset - Requesting a Reset]()
* [Module 08.06 Password Reset - Setting a new Password]()
* [Module 08.07 Password Reset - sending the email]()
### Module 09 Shopping Cart Development
* [Module 09.01 Cart - Creating the Data Type and Two Way Relationships]()
* [Module 09.02 Cart - Displaying Items in a Custom Component]()
* [Module 09.03 Cart - Using React Context for our Cart State]()
* [Module 09.04 Cart - Adding Items to Cart]()
* [Module 09.05 Cart - Adding Items To Cart in React]()
* [Module 09.06 Cart - Animating the Cart Cart Value]()
* [Module 09.07 Cart - Remove From Cart Button]()
* [Module 09.08 Cart - Evicting Cart Items from the Cache]()
### Module 10 Search
* [Module 10.01 Search]()
### Module 11 Order Creation and Checkout
* [Module 11.01 Setting Up our Stripe Checkout]()
* [Module 11.02 Writing our Client Side Checkout Handler Logic]()
* [Module 11.03 Creating our Order and OrderItem Data Types]()
* [Module 11.04 Custom Checkout Mutation with Stripe]()
* [Module 11.05 Linking up our Frontend to the custom backend checkout mutation]()
* [Module 11.06 Creating our Order and OrderItems in our Mutation]()
* [Module 11.07 Finishing up the Checkout UI and Flow]()
### Module 12 Frontend Order Displaying
* [Module 12.01 Displaying a Single Order]()
* [Module 12.02 Displaying All Orders]()
### Module 13 Roles, Permissions and Restricting Access
* [Module 13.01 Roles and Permissions - A Primer]()
* [Module 13.02 Creating the Roles and Permissions Schema + UI]()
* [Module 13.03 Basic Access Control via Sessions]()
* [Module 13.04 Permissions Access Functions]()
* [Module 13.05 More Flexible Rule Based Functions]()
* [Module 13.06 Getting Meta - Roles based Roles and Hiding UI]()
* [Module 13.07 Cart and Order based Rules]()
* [Module 13.08 User and Field Based Permissions]()
* [Module 13.09 Product Image Permissions]()
* [Module 13.10 Creating a Gated Sign In Component]()
### Module 14 Testing
* [Module 14.01 Test Setup, Tooling and Methodology]()
* [Module 14.02 Testing Basics]()
* [Module 14.03 Testing our formatMoney function]()
* [Module 14.04 React Testing Library]()
* [Module 14.05 Snapshot Testing]()
* [Module 14.06 More on Testing Library Queries]()
* [Module 14.07 Mocking GraphQL Data Requests]()
* [Module 14.08 Updating Props and re-rendering]()
* [Module 14.09 Testing Signed in and Signed out Nav States]()
* [Module 14.10 Pagination Testing]()
* [Module 14.11 Testing User Events and Mutations]()
* [Module 14.12 Testing Password Reset Component]()
* [Module 14.13 Mocking 3rd Party Libraries]()

---

## Module 01.01 Tooling and Starter Files Setup
* Node, React Dev Tools, Apollo Client Developer Tools, MongoDB Compass, VSCode, Terminal

## Module 01.02 The Tech Stack Explained
* Frontend: React, NextJS, Apollo Client, Styled Components
* Backend: Keystone.js, Node, MongoDB

## Module 02.01 An intro to Next
* React is Library, takes data and puts it into templates, and renders it into a page
* NextJS is a Framework - routing, linking, lazy loading, images, ssr (server side rendering), static/pre-rendering
* /pages/index.js is our index.html
```jsx
export default function Homepage() {
  return <div></div>
}
```
* `npm run dev`
* React Router is config based routing, NextJS is file system based routing
* Can do server rendering or static rendering

## Module 02.02 Creating a Page Layout Component
* a file in pages/ folder is just in the body tag
* components/Page.js
* can Auto Import component with VSCode
```jsx
import PropTypes from 'prop-types';
export default function Page({children,cool}) {
  return (
    <div>
      {cool}
      {children}
    </div>
  )
}

Page.propTypes = {
  children: PropTypes.any,
  cool: PropTypes.string,
}

import Page from '../components/Page';

export default function IndexPage() {
  return (
    <Page cool="test">
      <p>1</p>
      <p>2</p>
    </Page>
  )
}
```

```html

<div>
  test
  <p>1</p>
  <p>2</p>
</div>

```

* Anything to control higher than the page is in your pages\_app.js file
* pages\_document.js
```jsx
import Document, { Html, Head, NextScript, Main} from 'next/document';

export default class MyDocument extends Document {
  render() {
    return (
      <Html lang="en-CA">
        <Head></Head>
        <body>
          <Main />
          <NextScript />
        </body>
      </Html>
    )
  }
}
```

## Module 02.03 Creating our Header and Nav Components
* Creating a header/nav component
* NextJS uses HTML push.state instead of anchor, you so can use <Link>, `import Link from 'next/link'`

## Module 03.01 An Intro to Styled Components and CSS
* `import styled from 'styled-components'`
* Example of styled components

```jsx
const Logo = styled.h1`
  background: red;
  a { color: white; }
`;
```
* replace '<h1>' with '<Logo>'

## Module 03.02 Global Styles, Typography and Layout Styles
* `import { createGlobalStyle } from 'styled-components'`
* Example:
```jsx
const GlobalStyles = createGlobalStyle`
  html {
    box-sizing: border-box;
    /*stuff*/
  }
  *,*::before,*::after {
    box-sizing:inherit;
  }
`;

export default function Page({children,cool}) {
  return (
    <div>
      <GlobalStyles />
      <Header />
      <InnerStyles>
        {children}
      </InnerStyles>
    </div>
  )
}
```

## Module 03.03 Visualizing Route Changes
* Line across the top for progress (nprogress)
* Example for main `<Page>`
```jsx
import 'Nprogress' from nprogress;
import 'nprogress/nprogress.css'; //Can use your own CSS instead
import Router from 'next/router';

Router.events.on('routeChangeStart', () > NProgress.start());
Router.events.on('routeChangeComplete', () > NProgress.done());
Router.events.on('routeChangeError', () > NProgress.done());
```
## Module 03.04 Fixing Styled Components Flicker on Server Render
* pages\_document.js
```jsx
import Document, { Html, Head, NextScript, Main} from 'next/document';
import { ServerStyleSheet } from 'styled-components';

export default class MyDocument extends Document {
  static getInitialProps({ renderPage }) {
    const sheet = new ServerStyleSheet();
    const page = renderPage(App => props => sheet.collectStyles(<App {...props} />));
    const styleTags = sheet.getStyleElement();
    return { ...page, styleTags };
  }
  render() {
    return (
      <Html lang="en-CA">
        <Head></Head>
        <body>
          <Main />
          <NextScript />
        </body>
      </Html>
    )
  }
}
```

## Module 04.01 Setting up MongoDB
* Keystone runs ontop of MongoDB/Postgres
* Mongo Atlas for cloud version
* Rename sample.env to .env

## Module 04.02 An Intro to GraphQL
* GraphQL - specification for requesting/pushing data to server
* Keystone, Apollo build a layer ontop of GraphQL
* In Keystone, can see API Explorer
*
```graphql
query {
  allProducts {
    name
    description
    price
  }
}
```

## Module 04.03 Setting up Keystone and Typescript
*
*


## Module 04.04 Creating our first User data type

## Module 04.05 Adding Auth to our Application

## Module 04.06 Creating our Products Data Type

## Module 04.07 Uploading Product Images

## Module 04.08 Creating two way data relationships in Keystone

## Module 04.09 Inserting Seed Data

## Module 05.01 Setting up Apollo Client

## Module 05.02 Fetching Data with hooks and Displaying it in our Front End

## Module 05.03 Fixing and Styling the Nav

## Module 05.04 A real good lesson in React Forms and Custom Hooks

## Module 05.05 Hooking up our File input and Form Styles

## Module 05.06 Creating Products via our Mutations

## Module 05.07 Refetching Queries after a Successful Mutation

## Module 05.08 Programmatically Changing the Page after product creation

## Module 05.09 Displaying Single Items, Routing and SEO

## Module 06.01 Updating Items

## Module 06.02 Using useEffect to deal with a tricky loading state issue

## Module 06.03 Deleting Products

## Module 06.04 Evicting Items from the Apollo Cache

## Module 07.01 Pagination Links

## Module 07.02 Pagination Dynamic Routing

## Module 07.03 Adjusting our Query for Pagination Values

## Module 07.04 Custom Type Policies and Control over the Apollo Cache

## Module 08.01 Querying The Current User

## Module 08.02 Creating a Sign In Component

## Module 08.03 Creating a Sign Out Component

## Module 08.04 Creating our Sign Up Flow

## Module 08.05 Password Reset - Requesting a Reset

## Module 08.06 Password Reset - Setting a new Password

## Module 08.07 Password Reset - sending the email

## Module 09.01 Cart - Creating the Data Type and Two Way Relationships

## Module 09.02 Cart - Displaying Items in a Custom Component

## Module 09.03 Cart - Using React Context for our Cart State

## Module 09.04 Cart - Adding Items to Cart

## Module 09.05 Cart - Adding Items To Cart in React

## Module 09.06 Cart - Animating the Cart Cart Value

## Module 09.07 Cart - Remove From Cart Button

## Module 09.08 Cart - Evicting Cart Items from the Cache

## Module 10.01 Search

## Module 11.01 Setting Up our Stripe Checkout

## Module 11.02 Writing our Client Side Checkout Handler Logic

## Module 11.03 Creating our Order and OrderItem Data Types

## Module 11.04 Custom Checkout Mutation with Stripe

## Module 11.05 Linking up our Frontend to the custom backend checkout mutation

## Module 11.06 Creating our Order and OrderItems in our Mutation

## Module 11.07 Finishing up the Checkout UI and Flow

## Module 12.01 Displaying a Single Order

## Module 12.02 Displaying All Orders

## Module 13.01 Roles and Permissions - A Primer

## Module 13.02 Creating the Roles and Permissions Schema + UI

## Module 13.03 Basic Access Control via Sessions

## Module 13.04 Permissions Access Functions

## Module 13.05 More Flexible Rule Based Functions

## Module 13.06 Getting Meta - Roles based Roles and Hiding UI

## Module 13.07 Cart and Order based Rules

## Module 13.08 User and Field Based Permissions

## Module 13.09 Product Image Permissions

## Module 13.10 Creating a Gated Sign In Component

## Module 14.01 Test Setup, Tooling and Methodology

## Module 14.02 Testing Basics

## Module 14.03 Testing our formatMoney function

## Module 14.04 React Testing Library

## Module 14.05 Snapshot Testing

## Module 14.06 More on Testing Library Queries

## Module 14.07 Mocking GraphQL Data Requests

## Module 14.08 Updating Props and re-rendering

## Module 14.09 Testing Signed in and Signed out Nav States

## Module 14.10 Pagination Testing

## Module 14.11 Testing User Events and Mutations

## Module 14.12 Testing Password Reset Component

## Module 14.13 Mocking 3rd Party Libraries
