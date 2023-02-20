# Warren Shea's Notes for NodeJS
v20230108

## MEXN: Node & Express & MongoDB & Your front-end framework

## Express
* Used with Node as a Framework
* Can be used for routing: \
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

* Middleware: A simple way to write and execute middleware before routes
* Templating: Express works with Pug, EJS, Mustache
* Static File serving
* HTTP Helpers

## MongoDB
* You can use Mongoose to connect Node to MongoDB, but you can use the native MongoDB driver for Node as well

