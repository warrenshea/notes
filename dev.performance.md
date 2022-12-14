# Warren Shea's Notes for Performance
**Version**: 20221211

## Notable Performance Experts
* LCP - Harry Roberts
* Image Optimization - Addy Osmani

## Website Testers
* [PageSpeed Inights - https://pagespeed.web.dev/](https://pagespeed.web.dev/)
* Good LCP (Largest Contentful Paint) is 2.5 seconds

## JavaScript bundle testers
* [Lighthouse Treemap](https://googlechrome.github.io/lighthouse/treemap/)
* [Webpack Bundle Analyzer](https://www.npmjs.com/package/webpack-bundle-analyzer)

## Core Web Vitals

### LCP - Largest Contentful Paint
* quantify how fast the page feels visually
* measures how long it takes for the largest piece of content to appear on the screen

### FID - First Input Delay
* how long for the site to react to first interaction

### CLS - Cumulative Layout Shift
* measure visual stability of page (does stuff move around while loading)

## Preload Scanner
Invented in IE8, some resources are downloaded asynchronously/parallel. Resources in this scanner will always perform better than those that are not.<br>
`<img>` is an example of a resource in that scanner.

* `rel=preload` - this resource hint re-introduces item to preload scanner. But use it sparingly. This usually goes in the `<head>`
For images above the fold:
* `fetchpriority=high` - Priority Hints. This usually goes in the `<body>`. Useful for in-page resources.
* `decoding=sync` - Decoding images.

For images below the fold:

* `loading=lazy` and
* `decoding=async`

## Specific Code Performance and Benchmarking
[MeasureThat.net](https://www.measurethat.net/Benchmarks/Add): Compare performance of JavaScript code, e.g.

__HTML__:
```html
<div id="testElement"></div>
```

__JavaScript__:
```javascript
let el = document.querySelector('#testElement');
```
VS

```javascript
let el = document.getElementById('testElement');
```

document.querySelector x 5,467,960 ops/sec ±0.57% (66 runs sampled)<br>
document.getElementById x 39,677,211 ops/sec ±0.25% (69 runs sampled)

