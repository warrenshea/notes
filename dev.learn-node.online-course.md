# Warren Shea's Notes for Learn Node (Online Course)
[https://courses.wesbos.com/](https://courses.wesbos.com/){:target="_blank"} | [https://learnnode.com/](https://learnnode.com/){:target="_blank"} | [https://github.com/wesbos/Learn-Node](https://github.com/wesbos/Learn-Node){:target="_blank"} \
**Version**: 20230101| **Status**: Completed

---
## Table of Contents
### Module 01: Introduction and Setup
* [Module 01.01 Getting Setup]()
* [Module 01.02 Setting up Mongo DB]()
* [Module 01.03 Starter Files and Environmental Variables]()

### Module 02: Core Concepts
* [Module 02.04 Core Concept - Routing]()
* [Module 02.05 Core Concept - Templating]()
* [Module 02.06 Core Concept - Template Helpers]()
* [Module 02.07 Core Concept - Controllers and the MVC Pattern]()
* [Module 02.08 Core Concept - Middleware and Error Handling]()

### Module 03: Database Storage
* [Module 03.09 Creating our Store Model]()
* [Module 03.10 Saving Stores and using Mixins]()

### Module 04: Control Flow
* [Module 04.11 Using Async Await]()
* [Module 04.12 Flash Messages]()
* [Module 04.13 Querying our Database for Stores]()
* [Module 04.14 Creating an Editing Flow for Stores]()

### Module 05: Geolocation
* [Module 05.15 Saving Lat and Lng for each store]()
* [Module 05.16 Geocoding Data with Google Maps]()
* [Module 05.17 Quick Data Visualization Tip]()

### Module 06: File Handing and Image Resizing
* [Module 06.18 Uploading and Resizing Images with Middleware]()
* [Module 06.19 Routing and Templating Single Stores]()

### Module 07: Custom Queries and Hooks
* [Module 07.20 Using Pre-Save hooks to make Unique Slugs]()
* [Module 07.21 Custom MongoDB Aggregations]()
* [Module 07.22 Multiple Query Promises with Async:Await]()

### Module 08: User Accounts and Authentication
* [Module 08.23 Creating User Accounts]()
* [Module 08.24 Saving Registered Users to the Database]()
* [Module 08.25 Virtual Fields, Login:Logout middleware and Protecting Routes]()
* [Module 08.26 Creating a User Account Edit Screen]()
* [Module 08.27 Password Reset Flow]()

### Module 09: Advanced - Email and Permissions
* [Module 09.28 Sending email with Nodejs]()
* [Module 09.29 Locking down our application with User Permissions]()

### Module 10: Ajax REST API 1
* [Module 10.30 Loading Sample Data]()
* [Module 10.31 JSON endpoints and creating MongoDB Indexes]()
* [Module 10.32 Creating an Ajax Search Interface]()

### Module 11: Ajax REST API 2
* [Module 11.33 Creating a Geospatial Ajax Endpoint]()
* [Module 11.34 Plotting Stores on a Custom Google Map]()

### Module 12: Ajax REST API 3
* [Module 12.35 Pushing User Data to our API]()
* [Module 12.36 Displaying our Hearted Stores]()

### Module 13: Advanced Relationships + Aggregations
* [Module 13.37 Adding a Reviews Data Model]()
* [Module 13.38 Advanced Relationship Population - Displaying Our Reviews]()
* [Module 13.39 Advanced Aggregation]()

### Module 14: Pagination
* [Module 14.40 Implementing Pagination]()

### Module 15: Deployment
* [Module 15.41 Deployment Setup]()
* [Module 15.42 Deploying to Now]()
* [Module 15.43 Deploying to Heroku]()
* [Module 15.44 Deploying to Digital Ocean Linux]()

---

## Module 01.01 Getting Setup
* .pug files require jade
* Need Javascript (Babel) for syntax highlighting

## Module 01.02 Setting up Mongo DB
* Cloud via DBaaS (Database As A Service). Can use MongoDB Compass via GUI or mongoose via code
* Locally (Mac): `mongo --version` to see version. `sudo mongod` to run MongoDB
* Locally (Windows): [not documented]

## Module 01.03 Starter Files and Environmental Variables
* Build on nodeJS Application on Express
* `.env`, environmental variables, should never go to github
* Tells us how to use ES6 Promises (ASYNC/AWAIT).
* Details on package.json and webpack files

## Module 02.04 Core Concept - Routing
* Example:
```javascript
//routes/index.js
const router = express.Router();
router.get('/', (req, res) => {
  res.send('it works');
  //res.json(something);
  res.send(req.query.name); //for url /?name=warren&age=100
});

router.get('/reverse/:name', (req, res) => {
  res.send(req.params.name); //e.g. /reverse/warren
});
```

## Module 02.05 Core Concept - Templating
* pug is a templating language popular with node (used to be called Jade)
* Example code:
```javascript
//app.js
app.set('views', path.join(__dirname, 'views'));
app.set('view engine', 'pug'); //pug, mustache, ejs work great

//routes/index.js
const router = express.Router();
router.get('/', (req, res) => {
  res.render('hello'); //to render out hello.pug
  //OR
  res.render('hello', {
    "dog": "Loki",
    "name": req.param.name
  }); //to render out hello.pug
});

//in .pug file, you can pass
//#{dog} or #{name} to reference
```
* can "extend" the layout and overwrite it

## Module 02.06 Core Concept - Template Helpers
* creates helpers.js file which contains helper information
* Example:
```javascript
// pass variables to our templates + all requests
app.use((req, res, next) => {
  res.locals.h = helpers;
  res.locals.flashes = req.flash();
  res.locals.user = req.user || null;
  res.locals.currentPath = req.path;
  next();
});
```
* and can reference with `#{h.moment().endOf('day').fromNow()}`

## Module 02.07 Core Concept - Controllers and the MVC Pattern
* Controller - make various controllers for each functional part of the application
* Example:
```javascript
//controllers/storeController
exports.homePage = (req, res) => {
  res.render('index');
}

//index.js
const express = require('express');
const router = express.Router();
const storeController = require('../controllers/storeController');

routers.get('/', storeController.homePage);
```

## Module 02.08 Core Concept - Middleware and Error Handling
* Middleware - fundamental to express - between the request and the response, e.g. in a Login, normalize/stanitize inputs, authorize user, etc. before Displaying Profile (success) or Login page (failed)
*
```javascript
//controllers/storeController
exports.myMiddleware = (req, res, next) => {
  next();
}

exports.homePage = (req, res, next) => {
  res.render('index');
}

//index.js
const express = require('express');
const router = express.Router();
const storeController = require('../controllers/storeController');

routers.get('/', storeConroller.myMiddleware, storeController.homePage);

//app.js
app.use(doSomething());
//any app.use is a middleware
```

## Module 03.09 Creating our Store Model
* Model - where our data is stored
* Example:
```javascript
//models/Store.js
const mongoose = require('mongoose');
mongoose.Promise = global.Promise;
const slug = require('slugs');

const storeSchema = new mongoose.Schema({
  name: {
    type: String,
    trim: true,
    required: 'Please enter a store name!'
  },
  slug: String,
  description: {
    type: String,
    trim: true
  },
  tags: [String]
});

storeSchema.pre('save', function(next) {
  if (!this.isModified('name')) {
    next(); // skip it
    return; // stop this function from running
    //or return next();
  }
  this.slug = slug(this.name);
  next();
  // TODO make more resiliant so slugs are unique
});

module.exports = mongoose.model('Store', storeSchema);

//start.js
//...
//import all of our models
require('./models/Store');
//...
```

## Module 03.10 Saving Stores and using Mixins
* [To summarize video] Adding a store. Create a .pug mixin for creating a store (using GET/POST)
* Mixin - pass in some data and it returns something to you
* Mongoose is a package used to interface with the MongoDB Database

## Module 04.11 Using Async Await
* You can't just "save the store and redirect" because JavaScript is Asynchronous. It won't wait - so you have to use await (in the past, used Callbacks).
* Wrap your async/await on a try/catch OR a middleware called catchErrors
* Example:
```javascript
//controllers/storeController.js
exports.createStore = async (req, res) => {
  const store = new Store(req.body);
  store
    .save()
    .then(store => {
      return Store.find()
    })
    .then(store => {
      return doSomething
    })
    .catch(error => {
      throw Error(err)
    })
};

//OR

//ES8
exports.createStore = async (req, res) => {
  const store = new Store(req.body);
  await store.save(); //need to do this line, before moving to the next
  res.redirect(`/`);
  //OR do this, which combines the who lines into a response, so you can call ${store.slug} later
  const store = await (new Store(req.body)).save();
  req.flash('success', `Successfully Created ${store.name}. Care to leave a review?`); //type of flash (e.g. success, warning, error, info)
  res.redirect(`/store/${store.slug}`);
};

//routes/index.js
router.post('/add', catchErrors(storeController.createStore));
```

## Module 04.12 Flash Messages
* (https://www.npmjs.com/package/connect-flash)[https://www.npmjs.com/package/connect-flash]
* "The flash is a special area of the session used for storing messages. Messages are written to the flash and cleared after being displayed to the user. The flash is typically used in combination with redirects, ensuring that the message is available to the next page that is to be rendered."

## Module 04.13 Querying our Database for Stores
*  Example:
```javascript
//controllers/storeController.js
exports.getStores = async (req, res) => {
  // 1. Query the database for a list of all stores
  const stores = await Store.find();
  res.render('stores', { title: 'Stores', stores });
};
```

## Module 04.14 Creating an Editing Flow for Stores
* Example:
```javascript
//controllers/storeController.js
exports.editStore = async (req, res) => {
  // 1. Find the store given the ID
  const store = await Store.findOne({ _id: req.params.id });
  // 2. confirm they are the owner of the store
  // TODO
  // 3. Render out the edit form so the user can update their store
  res.render('editStore', { title: `Edit ${store.name}`, store });
};

exports.updateStore = async (req, res) => {
  // find and update the store
  const store = await Store.findOneAndUpdate({ _id: req.params.id }, req.body, {
    new: true, // return the new store instead of the old one
    runValidators: true
  }).exec();
  req.flash('success', `Successfully updated <strong>${store.name}</strong>. <a href="/stores/${store.slug}">View Store →</a>`);
  res.redirect(`/stores/${store._id}/edit`);
  // Redirect them the store and tell them it worked
};
```

## Module 05.15 Saving Lat and Lng for each store
* Adding a Lat, Long for the database

## Module 05.16 Geocoding Data with Google Maps
* Use Google Maps API for Geolocation

## Module 05.17 Quick Data Visualization Tip
* Seeing the point in MongoDB

## Module 06.18 Uploading and Resizing Images with Middleware
* change form action to `enctype="multipart/form-data"`
* use package called `multer` for file upload middleware/upload request

## Module 06.19 Routing and Templating Single Stores
* rendering the store/page

## Module 07.20 Using Pre-Save hooks to make Unique Slugs
* deals with duplicate slugs

## Module 07.21 Custom MongoDB Aggregations
* Handle tags for store

## Module 07.22 Multiple Query Promises with Async:Await
* `await Promise.all([array_of_promises]);`

## Module 08.23 Creating User Accounts
## Module 08.24 Saving Registered Users to the Database
## Module 08.25 Virtual Fields, Login:Logout middleware and Protecting Routes
## Module 08.26 Creating a User Account Edit Screen
## Module 08.27 Password Reset Flow
## Module 09.28 Sending email with Nodejs
## Module 09.29 Locking down our application with User Permissions
## Module 10.30 Loading Sample Data

## Module 10.31 JSON endpoints and creating MongoDB Indexes
* Indexes make queries ahead of time and make queries faster
* Indexing will occur in Schema
* Create routes for API
* Example code with score and sorted:
```javascript
exports.searchStores = async (req, res) => {
  const stores = await Store
  // first find stores that match
  .find({
    $text: {
      $search: req.query.q
    }
  }, {
    score: { $meta: 'textScore' }
  })
  // the sort them
  .sort({
    score: { $meta: 'textScore' }
  })
  // limit to only 5 results
  .limit(5);
  res.json(stores);
};
```

## Module 10.32 Creating an Ajax Search Interface
* HTML/CSS for the dropdown
* sanitize input via `dompurify`. `dompurify.sanitize()` stuff

## Module 11.33 Creating a Geospatial Ajax Endpoint
* Creating an API based on range/distance from a point
* Example:
```javascript
exports.mapStores = async (req, res) => {
  const coordinates = [req.query.lng, req.query.lat].map(parseFloat);
  const q = {
    location: {
      $near: {
        $geometry: {
          type: 'Point',
          coordinates
        },
        $maxDistance: 10000 // 10km
      }
    }
  };

  const stores = await Store.find(q).select('slug name description location photo').limit(10);
  res.json(stores);
};
```

## Module 11.34 Plotting Stores on a Custom Google Map
* Example for making a map

## Module 12.35 Pushing User Data to our API
* Adding "hearts" per store, per user

## Module 12.36 Displaying our Hearted Stores
* Display hearted stores: Query User and it's hearts, or Stores where id is in user's hearts

## Module 13.37 Adding a Reviews Data Model
* Adding "Reviews" section

## Module 13.38 Advanced Relationship Population - Displaying Our Reviews
* Display reviews
* `storeSchema.virtual` - kinda like a SQL join
* virtual fields don't go in JSON unless it's explicit

## Module 13.39 Advanced Aggregation
* Get Top 10 stores
* .aggregate is a function like .find
* Example:
```javascript
//models/Store.js
storeSchema.statics.getTopStores = function() {
  return this.aggregate([
    // Lookup Stores and populate their reviews
    { $lookup: { from: 'reviews', localField: '_id', foreignField: 'store', as: 'reviews' }},
    // filter for only items that have 2 or more reviews
    { $match: { 'reviews.1': { $exists: true } } },
    // Add the average reviews field
    { $project: {
      photo: '$$ROOT.photo',
      name: '$$ROOT.name',
      reviews: '$$ROOT.reviews',
      slug: '$$ROOT.slug',
      averageRating: { $avg: '$reviews.rating' }
    } },
    // sort it by our new field, highest reviews first
    { $sort: { averageRating: -1 }},
    // limit to at most 10
    { $limit: 10 }
  ]);
}
```

## Module 14.40 Implementing Pagination

## Module 15.41 Deployment Setup
* Postmark for emails

## Module 15.42 Deploying to Now
* add "now" to packages.json

## Module 15.43 Deploying to Heroku
* environment variables go into dashboard

## Module 15.44 Deploying to Digital Ocean Linux
* `forever` package if something drops
* `forever start start.js`
* `forever restart 0`