# Warren Shea's Notes for CSS (and SASS)
v20221213

## Box Model
* in terms of width, padding and border is part of box model (`box-sizing: border-box`), margin is not

## Hex w/ Alpha Transparency
* `#XXXXXX30` = color #XXXXXX w/ 30% alpha transparency

## Performance
* Browsers read selectors right-to-left so the longer the selector is, the slower it is
* background is twice as fast than background-color
* "As you go down a stylesheet you should only ever be adding styles, not taking away. If you find you are having to undo styling as you go down your document the chances are you jumped the gun and started adding too much too soon." - https://csswizardry.com/2012/11/code-smells-in-css/
* `will-change` over `translate3d(0,0,0)` for elements likely to change

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
Inline styles - Example: `<h1 style="color: pink;">` \
IDs - Example: #navbar \
Classes, pseudo-classes, attribute selectors - Example: `.test`, `:hover`, `[href]` \
Elements and pseudo-elements - Example: `h1`, `:before`

### How to Calculate Specificity?
Start at 0, add 100 for each ID value, add 10 for each class value (or pseudo-class or attribute selector), add 1 for each element selector or pseudo-element. \
There is one exception to this rule: if you use the !important rule, it will even override inline styles!

___

## Flexbox (CSS Flexible Box Layout Module)
* `flex:1;` will evenly distribute everything - at what proportion should the item scale myself up or down
* `flex` (short form) is `flex-grow`, `flex-shrink`, `flex-basis`
* `flex-flow` (short form) is `flex-direction`, `flex-wrap`
* `flex-grow`: what do we do with the extra space
* `flex-shrink`: what do we do with not enough space - how much do i give up
* `order:0;` is default
* `align-items:baseline` is more useful than expected, by aligning the bottom of words/copy.
* `align-content` determines the spacing between lines. When there is only one line, align-content has no effect
* `align-items` determines how the items as a whole are aligned within the container
* `align-self` determines how the item is aligned within the container. It has the same properties as align-items.

### Resources
* [CSS Tricks - https://css-tricks.com/snippets/css/a-guide-to-flexbox/](https://css-tricks.com/snippets/css/a-guide-to-flexbox/){:target="_blank"}
* [Wes Bos - https://flexbox.io/](https://flexbox.io/){:target="_blank"}
* [https://flexboxfroggy.com/](https://flexboxfroggy.com/){:target="_blank"}
* [https://www.joshwcomeau.com/css/interactive-guide-to-flexbox/](https://www.joshwcomeau.com/css/interactive-guide-to-flexbox/){:target="_blank"}

___

## CSS Grid

### Resources

* [CSS Tricks - https://css-tricks.com/snippets/css/complete-guide-grid/](https://css-tricks.com/snippets/css/complete-guide-grid/){:target="_blank"}
* [Wes Bos - https://cssgrid.io/](https://cssgrid.io/){:target="_blank"}
* [https://cssgridgarden.com/](https://cssgridgarden.com/){:target="_blank"}

___

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

OR adding via the `console`:
```javascript
let module_ui = document.createElement("style");
module_ui.type = 'text/css';
module_ui.setAttribute("data-id","glitch-id-element");

let module_ui_content = `
* { background-color: rgba(255,0,0,.2); }
* * { background-color: rgba(0,255,0,.2); }
* * * { background-color: rgba(0,0,255,.2); }
* * * * { background-color: rgba(255,0,255,.2); }
* * * * * { background-color: rgba(0,255,255,.2); }
* * * * * * { background-color: rgba(255,255,0,.2); }
* * * * * * * { background-color: rgba(255,0,0,.2); }
* * * * * * * * { background-color: rgba(0,255,0,.2); }
* * * * * * * * * { background-color: rgba(0,0,255,.2); }`;
module_ui.appendChild(document.createTextNode(module_ui_content));
document.getElementsByTagName("head")[0].appendChild(module_ui);
```
