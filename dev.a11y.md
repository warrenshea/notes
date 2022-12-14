# Warren Shea's Notes for a11y (accessibility)
v20221212

## Useful standards
* [w3c Aria Practices](https://w3c.github.io/aria-practices/)
* [w3c Aria Practices Examples](https://w3c.github.io/aria-practices/examples/combobox/combobox-select-only.html)
* [w3 ARIA Authoring Practices Guide (APG)](https://www.w3.org/WAI/ARIA/apg/patterns/)

## Useful checkers
* [PageSpeed Inights - https://pagespeed.web.dev/](https://pagespeed.web.dev/)
* [Web Accessibility Initiative - https://www.w3.org/WAI/tutorials/](https://www.w3.org/WAI/tutorials/)

## Useful a11y examples
* [Ryerson Web a11y Course examples - https://warrenshea.github.io/learnaria/](https://warrenshea.github.io/learnaria/)
* [a11y Style Guide](https://a11y-style-guide.com/style-guide/section-navigation.html#kssref-navigation-accordion)

## Useful Chrome Extensions
* axe DevTools - Web Accessibility Testing [Chrome Extension](https://chrome.google.com/webstore/detail/axe-devtools-web-accessib/lhdoppojpmngadmnindnejefpokejbdd)
* ASLint [Bookmarklet](https://aslint.org/)
* Squizlabs HTML_Codesniffer [Bookmarklet](https://squizlabs.github.io/HTML_CodeSniffer/) or [Chrome Extension](https://chrome.google.com/webstore/detail/htmlcodesniffer-extension/lbdmdmikomieilpnlihfhianednecpcl)
* tota11y [Bookmarklet](https://khan.github.io/tota11y/) or [Chrome Extension](https://chrome.google.com/webstore/detail/tota11y-for-chrome/nkghaekndgmonifcpfgjmpfjlhnmflhp?hl=en)

## General Notes

### Page related
* add lang attribute to `<html>` tag
* add lang attribute if word/text is written in language different from page (e.g. a Français link)
* have a Skip Navigation link
* page content is in Landmarks (HTML, Banner, Complementary, Contentinfo, Form, Main, Navigation, Region, Search, Asst. Tech., Resources)
* `aria-hidden="true"` attribute/value is for skipping screen reader content (e.g. `<hr aria-hidden="true">`)
* $22<sup>22</sup> reads as "two thousand twenty two dollars" - so put a "footnote" screen reader copy, "twenty two dollars footnote twenty two"
* You can programmatically shift focus to something (like an `<h2>` or `<legend>` if you have a tabindex=-1 attribute on it, but that will not make it focusable via tabbing

### Anchors (and sometimes, Buttons)
* Better to use aria-label rather than show-for-sr class
* aria-label contains or begins with visual text of the link to keep ensure visual and screen reader experience is similar/consistent
* aria-label for phone number should be something like "Call us at 987 654 3210"
* some screen readers read "LEARN MORE" like "EL EE AY ARE EN ..." so next should not be uppercase (use CSS). A recent example is COVID-19 should be written as "covid nineteen" in the aria-label
* `<a><img>` (or `<button><img>` should have either an aria-label on the `<a>` (or `<button>`) or an alt on `<img>` - both are not required
* don't use word "link" in aria-label (e.g. "homepage link") because Screen Reader will read anchor tag as "Link", e.g. link homepage link
* Buttons should have a visible outline on focus
* If a button IS a button, BUT then redirects you to another page, use role="link"

### Text
* Add role="text" if a `<span>` or `<p>` has multiple elements (e.g. `<sup>` or `<sub>`) in it to have the screen reader read without pause

### List
* `<ul>` should have role="list" to improve screen reader experience
* `<li>` should ahve role="listitem" to improve screen reader experience

### Heading
* Any text that looks like a heading is implemented as a heading

### Abbreviation
* Use `<abbr>` with title attribute, do not use "show-for-sr" class for the same issue

### Tables
* Has visible or SR specific caption (title/heading of table). If there is a lot to add,, it should be provided in the `<table summary="">`.
* table has appropriate `<thead>`, `<tbody>`, `<th>` (table header) with appropriate scope="row" or "col"
* don't use display:flex for `<table>`
* use for tabular data, don't use for `<table>` for layout

### Video / iFrame
* Youtube embedded `<iframe>`s or `<iframe>s, in general, require a title attribute
* Video has proper controls, transcripts, captions

### Accordion
* Header button wrapped in a heading element, e.g. `<h3><button>` (instead of `<button><h3>`) and the `<button>` is the only element inside the heading element
* e.g. [https://w3c.github.io/aria-practices/examples/accordion/accordion.html](https://w3c.github.io/aria-practices/examples/accordion/accordion.html)

### Navigation
* `<nav>` should have unique aria-label attribute
* aria-current="page" should be on any link that references the page you're on

### Modal
* Has an `<h2>` element, even if the heading is invisible
* Upon opening a modal, the button should go to the first element, which should be the close button
* Focus should never leave the modal (focus trap)
* When a modal is closed, the focus goes back to what triggered the modal

### Forms
* Required input fields have "aria-required" (or "required") property
* Errors use aria-describedby (which can contain multiple IDs, separated by a space)
* If there's an error, the focus should focus on the first error and VO should automatically read the error message (via aria-lve="assertive" on the error message)
* Error messages provide descriptionve information for users to correct it

### Images
* Background images: alt, title, aria-label, role="img" attributes should not be added
* Background Images: cannot be focused upon by keyboard or VO
* [Decorative] Icons: should have focusable="false"
* [Non-decorative] Icons (e.g. Linkedin): `<a><svg>` should have a title on the anchor, `<a title="">` for a "tooltip"

### Carousel
* Tabbings focus goes to visible slides (first), left and right arrows if applicable (second), carousel indicator dots (third). Tabbing focus never goes to hidden slides
* By selecting a slide through indicator dots, focus shifts to slide or first interactable item on the slide
* Navigating to a new slide via the carousel indicator dots or left and right arrows, a hidden element should aanount "slide # / total #"
* If a carousel autoplays for more than 5 seconds, there's must be controls to pause/play. Recommend no autoplay though.

## Safari + VoiceOver cheat sheet
* Read Next/Previous Item (CTRL + OPT + Left/Right Arrow)
* Activate a link/button (CTRL + OPT + Space)
* Start Reading automatically (CTRL + OPT + A)
* Focus Next Item (OPT + Tab)
* Focus Previous Item (OPT + Shift + Tab)
