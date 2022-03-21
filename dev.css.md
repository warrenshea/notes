# Warren Shea's Notes for CSS
v20210614

## Hex w/ Alpha Transparency
#XXXXXX30 = color #XXXXXX w/ 30% alpha transparency


## Performance
* Browsers read selectors right-to-left so the longe the selector is, the slower it is
* background is twice as fast than background-color
* "As you go down a stylesheet you should only ever be adding styles, not taking away. If you find you are having to undo styling as you go down your document the chances are you jumped the gun and started adding too much too soon." - https://csswizardry.com/2012/11/code-smells-in-css/

## will-change over translate3d(0,0,0) for elements likely to change

## Qualified Selectors (selectors prepended by an element)
Avoid these. They are slower, increase specificity and can't be used for different elements
```css
ul.list {}
```
Sometimes qualified selectors make a classname more semantic, but a better alternative is quasi-qualified selectors
```css
/*ul*/.list {}
```

## Specificity
Inline styles - Example: <h1 style="color: pink;">
IDs - Example: #navbar
Classes, pseudo-classes, attribute selectors - Example: .test, :hover, [href]
Elements and pseudo-elements - Example: h1, :before

### How to Calculate Specificity?
Start at 0, add 100 for each ID value, add 10 for each class value (or pseudo-class or attribute selector), add 1 for each element selector or pseudo-element.
There is one exception to this rule: if you use the !important rule, it will even override inline styles!

## Useful Chrome Extensions

* [Web Developer](https://chrome.google.com/webstore/detail/web-developer/bfbameneiokkgbdmiekhjnmfkcnldhhm)
* Pesticide
* Stylus

## Stylus

### Style configuration for noticing inconsistencies
```css
* { background-color: rgba(255,0,0,.2); }
* * { background-color: rgba(0,255,0,.2); }
* * * { background-color: rgba(0,0,255,.2); }
* * * * { background-color: rgba(255,0,255,.2); }
* * * * * { background-color: rgba(0,255,255,.2); }
* * * * * * { background-color: rgba(255,255,0,.2); }
* * * * * * * { background-color: rgba(255,0,0,.2); }
* * * * * * * * { background-color: rgba(0,255,0,.2); }
* * * * * * * * * { background-color: rgba(0,0,255,.2); }
```