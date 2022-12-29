# Warren Shea's Notes for Advanced React (Online Course)
[https://courses.wesbos.com/](https://courses.wesbos.com/){:target="_blank"} | [https://advancedreact.com/](https://advancedreact.com/){:target="_blank"} \
**Version**: 20220729 | **Status**: Paused at Module 7 - will continue as needed

---
## Table of Contents
### Module 01: Introduction and Setup
* [Module 01.01 Tooling and Starter Files Setup]()
* [Module 01.02 The Tech Stack Explained]()

### Module 02: Learning Next.js
* [Module 02.01 An intro to Next]()
* [Module 02.02 Creating a Page Layout Component]()
* [Module 02.03 Creating our Header and Nav Components]()

### Module 03: CSS and Styled Components
* [Module 03.01 An Intro to Styled Components and CSS]()
* [Module 03.02 Global Styles, Typography and Layout Styles]()
* [Module 03.03 Visualizing Route Changes]()
* [Module 03.04 Fixing Styled Components Flicker on Server Render]()

### Module 04: Server Side GraphQL Development
* [Module 04.01 Setting up MongoDB]()
* [Module 04.02 An Intro to GraphQL]()
* [Module 04.03 Setting up Keystone and Typescript]()
* [Module 04.04 Creating our first User data type]()
* [Module 04.05 Adding Auth to our Application]()
* [Module 04.06 Creating our Products Data Type]()
* [Module 04.07 Uploading Product Images]()
* [Module 04.08 Creating two way data relationships in Keystone]()
* [Module 04.09 Inserting Seed Data]()

### Module 05: Client Side React + GraphQL Development
* [Module 05.01 Setting up Apollo Client]()
* [Module 05.02 Fetching Data with hooks and Displaying it in our Front End]()
* [Module 05.03 Fixing and Styling the Nav]()
* [Module 05.04 A real good lesson in React Forms and Custom Hooks]()
* [Module 05.05 Hooking up our File input and Form Styles]()
* [Module 05.06 Creating Products via our Mutations]()
* [Module 05.07 Refetching Queries after a Successful Mutation]()
* [Module 05.08 Programmatically Changing the Page after product creation]()
* [Module 05.09 Displaying Single Items, Routing and SEO]()

### Module 06: Working with Mutations
* [Module 06.01 Updating Items]()
* [Module 06.02 Using useEffect to deal with a tricky loading state issue]()
* [Module 06.03 Deleting Products]()
* [Module 06.04 Evicting Items from the Apollo Cache]()

### Module 07: Pagination
* [Module 07.01 Pagination Links]()
* [Module 07.02 Pagination Dynamic Routing]()
* [Module 07.03 Adjusting our Query for Pagination Values]()
* [Module 07.04 Custom Type Policies and Control over the Apollo Cache]()

### Module 08: User Registration + Authentication
* [Module 08.01 Querying The Current User]()
* [Module 08.02 Creating a Sign In Component]()
* [Module 08.03 Creating a Sign Out Component]()
* [Module 08.04 Creating our Sign Up Flow]()
* [Module 08.05 Password Reset - Requesting a Reset]()
* [Module 08.06 Password Reset - Setting a new Password]()
* [Module 08.07 Password Reset - sending the email]()

### Module 09: Shopping Cart Development
* [Module 09.01 Cart - Creating the Data Type and Two Way Relationships]()
* [Module 09.02 Cart - Displaying Items in a Custom Component]()
* [Module 09.03 Cart - Using React Context for our Cart State]()
* [Module 09.04 Cart - Adding Items to Cart]()
* [Module 09.05 Cart - Adding Items To Cart in React]()
* [Module 09.06 Cart - Animating the Cart Cart Value]()
* [Module 09.07 Cart - Remove From Cart Button]()
* [Module 09.08 Cart - Evicting Cart Items from the Cache]()

### Module 10: Search
* [Module 10.01 Search]()

### Module 11: Order Creation and Checkout
* [Module 11.01 Setting Up our Stripe Checkout]()
* [Module 11.02 Writing our Client Side Checkout Handler Logic]()
* [Module 11.03 Creating our Order and OrderItem Data Types]()
* [Module 11.04 Custom Checkout Mutation with Stripe]()
* [Module 11.05 Linking up our Frontend to the custom backend checkout mutation]()
* [Module 11.06 Creating our Order and OrderItems in our Mutation]()
* [Module 11.07 Finishing up the Checkout UI and Flow]()

### Module 12: Frontend Order Displaying
* [Module 12.01 Displaying a Single Order]()
* [Module 12.02 Displaying All Orders]()

### Module 13: Roles, Permissions and Restricting Access
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

### Module 14: Testing
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
* get variable from .env, put in `keystone.ts`
```typescript
  ...more stuff...
  const databaseURL = process.env.DATABASE_URL || 'mongodb://localhost/keystone-sick-fits-tutorial';
  const sessionConfig = {
    maxAge:  60 * 60 * 24 * 360, //how long they should be signed in
    secret: process.env.COOKIE_SECRET
  }

  export default config({
    server: {
      cors: {
        origin: [process.env.FRONTEND_URL],
        credentials: true,
      }
    },
    db: {
      adapter: 'mongoose',
      url: databaseURL,
      //TODO: Add data seeding here
    }
    lists: createScema({
      //scheme items go in here
    }),
    ui: {
      //change this for roles
      isAccessAllowed: () => true,
    },
    //TODO: Add Session values here
  });

```
* `npm run dev` to run keystone

## Module 04.04 Creating our first User data type
* Every time there's a datatype, we build a schema
* Set up Users section on Keystone

## Module 04.05 Adding Auth to our Application
* Adding Auth to Keystone
* Adding Session to Keystone

## Module 04.06 Creating our Products Data Type
* Creating Product list

## Module 04.07 Uploading Product Images
* Cloudinary - a service with a very generous free tier
* Can use NextJS image tag to display images
* Anytime you need environment variable, need `import 'dotenv/config';`

## Module 04.08 Creating two way data relationships in Keystone
* in the schema, you can do `ProductImage.ts`
`product: relationship({ ref: 'Product.photo' })` for a two way data relationship in Keystone. This is the Product datatype and the photo field
and in `Product.ts`
`photo: relationship({ ref: 'ProductImage.product' })`
*

## Module 04.09 Inserting Seed Data
* In `keystone.ts`, you can add Seed data but we only want to do it if there's an argument
```typescript
db: {
  adapter: 'mongoose',
  url: databaseURL,
  async onConnect(keystone) {
    if(process.argv.includes('--seed-data')) {
      await insertSeedData(keystone);
    }
  },
},
```
* you can run `npm run seed-data` via `package.json`
```json
"scripts": {
  "seed-data": "keystone-next --seed-data",
}
```

## Module 05.01 Setting up Apollo Client
* Used for making queries to GraphQL, cache data, handle mutations, give us data back from server (talk to GraphQL and manage data for us)
* Wrap `<Page>` app with ApolloClient

## Module 05.02 Fetching Data with hooks and Displaying it in our Front End
* If you want part of the same page on two pages, or a route to be the exact same as something else
```jsx
import ProductsPage from './products';
export default ProductsPage;

OR

export { default } from './products';
```
* How to query items from backend
```graphql
query ALL_PRODUCTS_QUERY {
  allProducts {
    id
    name
    price
    description
    photo {
      id
      image {
        publicUrlTransformed
      }
    }
  }
}
```
```jsx
import { useQuery } from '@apollo/client';
import gql from "graphql-tag";

const ALL_PRODUCTS_QUERY = gql`
  query ALL_PRODUCTS_QUERY {
    allProducts {
      id
      name
      price
      description
      photo {
        id
        image {
          publicUrlTransformed
        }
      }
    }
  }
`;

export default function Products() {
  const { data, error, loading } = useQuery(ALL_PRODUCTS_QUERY);
  if (loading) return <p>Loading...</p>;
  if (error) return <p>Error: {error.message}</p>;
  return (
    <div>
      { data.allProducts.map(product => (
       <p key={products.id}>{product.name}</p>
      ))}
    </div>
  )
}
```
* `product?.photo?.image?.something` Optional chaining, new in JavaScript
* formatMoney
```jsx
export default function formatMoney(amount = 0) {
  const options = {
    style: 'currency',
    currency: 'USD',
    minimumFractionDigits: 2,
  };

  if (amount % 100 === 0) {
    options.minimumFractionDigits = 0;
  }

  const formatter = Intl.NumberFormat('en-US',options);

  return formatter.format(amount/100);
}
```

## Module 05.03 Fixing and Styling the Nav

## Module 05.04 A real good lesson in React Forms and Custom Hooks
* React is VERY strict about source of truth for State, need onChange
```jsx
import {useState} from 'react';

export default function CreateProduct() {
  const [name, setName] = useState('Wes');
  return (
    <input
      value={name}
      onChange={(e) => {
        setName(e.target.value);
      }}
    >
  )
}
```
* useForm.js
```jsx
import { useEffect, useState } from 'react';

export default function useForm(initial = {}) {
  // create a state object for our inputs
  const [inputs, setInputs] = useState(initial);
  const initialValues = Object.values(initial).join(''); //* this can't be initial or it causes infinite loop

  useEffect(() => {
    // This function runs when the things we are watching change
    setInputs(initial);
  }, [initialValues]); //* this can't be initial or it causes infinite loop

  // {
  //   name: 'wes',
  //   description: 'nice shoes',
  //   price: 1000
  // }

  function handleChange(e) {
    let { value, name, type } = e.target;
    if (type === 'number') {
      value = parseInt(value);
    }
    if (type === 'file') {
      [value] = e.target.files; // value = e.target.files.value?
    }
    setInputs({
      // copy the existing state
      ...inputs,
      [name]: value,
    });
  }

  function resetForm() {
    setInputs(initial);
  }

  //blankState is turns object to array, changes values, then converts back to object
  function clearForm() {
    const blankState = Object.fromEntries( //turn to object
      Object.entries(inputs).map(([key, value]) => [key, '']) //turn to array and change values
    );
    setInputs(blankState);
  }

  // return the things we want to surface from this custom hook
  return {
    inputs,
    handleChange,
    resetForm,
    clearForm,
  };
}
```
```jsx
import { useForm } from '../lib/useForm';

export default function CreateProduct() {
  const { inputs, handleChange } = useForm({
    name: 'blah', //for testing purposes
    price: 234234
  });
  return (
    <input
      name="name"
      value={inputs.name}
      onChange={handleChange}
    >
    <input
      name="price"
      value={inputs.price}
      onChange={handleChange}
    >
  )
}
```

## Module 05.05 Hooking up our File input and Form Styles
* Accessible aria-busy which tells the user something is happening

## Module 05.06 Creating Products via our Mutations
* GraphQL for submitting form to
```graphql
mutation {
  createProduct(data:{
    name: "Test",
    description: "Test",
    price: 100,
    status: "Available",
  }) {
    id
    price
    description
  }
}
```
^ this works for manual running
* for submitting form stuff
```jsx
  const CREATE_PRODUCT_MUTATION = gql`
    mutation CREATE_PRODUCT_MUTATION(
      # which variables are getting passed in? what types are they
      $name: String!
      $description: String!
      $price: Int!
      $image: Upload
    ) {
      createProduct(
        data:{
          name: $name,
          description: $description
          price: $price
          status: "Available"
          photo: {
            create: {
              image: $image,
              altText: $name
            }
          }
        }
      ) {
        id
        price
        description
        name
      }
    }
`;

...

const [ createProduct, { loading, error, data }] = useMutation(CREATE_PRODUCT_MUTATION, {
  variables: inputs
});

...

<form onSubmit={ async (e) => { e.preventDefault(); const res = await createProduct(); }}></form>

...

<DisplayError error={error} /> // done by Wes Bos
<fieldset disabled={loading} aria-busy={loading}> //for loading

```

## Module 05.07 Refetching Queries after a Successful Mutation
* Go to a page, add product, go back - it's cached!
* Two options: modify cache directly in Apollo or tell Apollo behind the scenes to refetch
* Refect Query: Export Query (e.g. ALL_PRODUCTS_QUERY) and import it in new file,
```jsx
const [ createProduct, { loading, error, data }] = useMutation(CREATE_PRODUCT_MUTATION, {
  variables: inputs,
  refetchQueries: [{query: ALL_PRODUCTS_QUERY }] // refetchQueries: [{query: ALL_PRODUCTS_QUERY, variables }]
});
```

## Module 05.08 Programmatically Changing the Page after product creation
* Programmatically change page. Import Router and then...
```jsx
<form onSubmit={
  async (e) => {
    e.preventDefault();
    const res = await createProduct();
    clearForm();
    Router.push({
      pathname: `/product/${res.data.createProduct.id}`,
    });
  }
}></form>
```

## Module 05.09 Displaying Single Items, Routing and SEO
* Can have files like [id].js which Next will recognize
* You can only query single items (Product) based on unique fields (id)
```jsx
query {
  Product(where: {
    id: $id
  })
}
```
* Find by name
```jsx
query {
  allProduct(where: {
    name_contains_i: "yeti"
  }) {
    name
    price
  }
}
```
* wrap console.log in { } and it turns things to object, e.g. `console.log({data,loading,error});`
* GraphQL statement
```jsx
const SINGLIE_ITEM_QUERY = gql`
  query SINGLE_ITEM_QUERY($id: ID!)` {
    Product(where: {
      id: $id
    }) {
      name
      price
      description
    }
  }
`;
```
* Updating <head> stuff, you can just put anything in (similar to react-helmet)
```jsx
return (
  <div>
    <Head>
      <title>Sick Fits | {Product.name}</title>
    </Head>
    <stuff>
  </div>
)
```

## Module 06.01 Updating Items
* Two queries/mutations inside single function - rename as destructuring

## Module 06.02 Using useEffect to deal with a tricky loading state issue
* useEffect will allow monitor state/variables and when they change, run some code
```jsx
  useEffect(() => {
    // This function (setInputs(initial)) runs when the things we are watching ([initialValues]) change
    setInputs(initial);
  }, [initialValues]);
```

## Module 06.03 Deleting Products
* Soft Delete - not actually deleting it

## Module 06.04 Evicting Items from the Apollo Cache
* Apollo has cool argument
* function to run after delete
```jsx
function update(cache,payload) {
  cache.evict(cache.identify(payload.data.deleteProduct)
}
```

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
