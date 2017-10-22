# React.JS Essential Training
v.20171021

* ES6 - ECMAScript 6
* Read: React Documentation

React-detector

```javascript
const title = React.creatElement(
  '<element>',
  {properties},
  '<value>'
)

ReactDOM.render(
  title,
  document.getElementById('react-container')
)
```

* Install npm httpster - with this, run a server from any location on your computer
* `httpster -d ./dist -p 3000` = start a server on the dist folder on port 3000
* The problem is that JSX is not read by the browser - you need to Transpile it using Babel
* You can use ES6, ES2016, ES2017 right away.
* Babel 5.8 under Facebook React - great for dev, but for production code, you need to transpile earlier
* `npm init` to generate project - select a version
* `npm install --save-dev babel-cli` or `npm install -g babel-cli` (for global) will save to dev dependencies
* 
```json
.babelrc = presets, everything you want to transpile
  {
    'presets' : ['latest','react','stage-0']
  }
```
* `npm install --save-dev babel-preset-latest babel-preset-react`
`babel-preset-stage-0`
`babel ./src/index.js --out-file ./dist/bundle.js`
* WEBPACK
  - module bundler that creates static files
  - webpack config can enable hot reload on the dev server