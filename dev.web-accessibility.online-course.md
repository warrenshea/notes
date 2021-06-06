# Warren's Notes for CN-2582-WEB-ACCESSIBILITY-FOR-DEVELOPERS (Sep2018) (Online Course)
v.20181015

* Alt text should be limited to 125 characters, thus would not provide sufficient space to present a complex description. The others would allow any number of characters to present the description.

* POUR: Perceivable, Operable, Understandable, Robust

* WAI-ARIA: “Web Accessibility Initiative,” the W3C subgroup that developed the specification, and “Accessible Rich Internet Applications”

* WAI-ARIA 1.0 released March of 2014. WAI-ARIA 1.1 (Stable version) was released in December 2017

* jQuery UI Accessibility Enhancements https://hanshillen.github.io/jqtest/

* Good reads
      * https://www.w3.org/TR/wai-aria-practices/
      * https://www.w3.org/TR/WCAG20-TECHS/aria
      * https://www.w3.org/TR/aria-in-html/

*  Most HTML has built-in semantics, and does not generally need WAI-ARIA. However, when HTML is being used in a non-standard way, like making a button out of a div, then WAI-ARIA can be added to that div to make it appear as a button to a screen reader.

    e.g `<div role=”button” aria-pressed=”false” tabindex=”0”>Press Me</div>`

    In the case of an actual `<button>` element, these properties are already defined so there is no need to use WAI-ARIA.

* "WAI-ARIA provides a framework for adding attributes to identify features for user interaction, how they relate to each other, and their current state" - W3C

* WAI-ARIA provides web authors with the following:
      * Roles to describe the type of widget presented, such as “menu”, “treeitem”, “slider”, and “progressmeter”
      * Roles to describe the structure of the web page, such as headings, regions, and tables (grids)
      * Properties to describe the state widgets are in, such as “checked” for a check box, or “haspopup” for a menu.
      * Properties to define live regions of a page that are likely to get updates (such as stock quotes), as well as an interruption policy for those updates – for example, critical updates may be presented in an alert dialog box and incidental updates occur within the page
      * Properties for drag-and-drop that describe drag sources and drop targets
      * A way to provide keyboard navigation for the web objects and events, such as those mentioned above

* "Curb Cuts" - accommodations provided to improve web accessibility for people with disabilities

* BP - For some of the newer HTML5 elements, like `<nav>` and `<main>` for instance, it does not hurt to include the WAI-ARIA equivalent `role=”navigation”` and `role=”main”` in these elements for the time being, to accommodate some of the inconsistent support for these elements across browsers and ATs.

* Be careful when using WAI-ARIA with HTML elements that already have semantics, e.g. `<h3 role=”button”>Chapter 2</h3>`. `<div role=”button”><h3>Chapter 2</h3></div>` would be better.

* Roles, States, and Properties

* Roles
      * Main indicator of type. This semantic association allows tools to present and support interaction with the object in a manner that is consistent with user expectations about other objects of that type.”
      * Must not change over time
      * 6 groupings:
            * Abstract role (not to be used by authors in content, the base for the WAI-ARIA ontology)
            * Widget roles (e.g. button, link, menuitem)
            * Document structure roles (e.g. article, feed, list, table)
            * Landmark roles (e.g. banner, navigation, main, complementary)
            * Live region roles (e.g. alert, log, timer)
            * Window roles (e.g. alertdialog, dialog)
      * Full list of roles: https://www.w3.org/TR/2017/REC-wai-aria-1.1-20171214/#role_definitions

* States & Properties
      * States:
            * “A state is a dynamic property expressing characteristics of an object that may change in response to user action or automated processes. States do not affect the essential nature of the object, but represent data associated with the object or user interaction possibilities. See clarification of states versus properties.”
            * define its functional status and change while an app/widget is used (e.g. aria-checked)
            * All prefixed with "aria-" (e.g. aria-busy, aria-checked, aria-expanded, aria-disabled, aria-hidden)
      * Properties
            * “Attributes that are essential to the nature of a given object, or that represent a data value associated with the object. A change of a property may significantly impact the meaning or presentation of an object. Certain properties (for example, aria-multiline) are less likely to change than states, but note that the frequency of change difference is not a rule. A few properties, such as aria-activedescendant, aria-valuenow, and aria-valuetext are expected to change often. See clarification of states versus properties.”
            * tend to remain the same (this is not a rule)
            * e.g. aria-describedby, aria-atomic, aria-autocomplete, aria-colcount, aria-colspan, aria-controls
      * Full list of States and Properties https://www.w3.org/TR/2017/REC-wai-aria-1.1-20171214/#states_and_properties

* Static WAI-ARIA properties:
      * aria-describedby: Identifies the element (or elements) that describes the object.
      * aria-labelledby: Identifies the element (or elements) that labels the current element.
      * aria-label: Defines a string value that labels the current element.
      * aria-controls: Identifies the element (or elements) whose contents or presence are controlled by the current element.
      * aria-owns: Identifies an element (or elements) in order to define a visual, functional, or contextual parent/child relationship between DOM elements where the DOM hierarchy cannot be used to represent the relationship.
      * aria-details: Identifies the element that provides a detailed, extended description for the object.
      * aria-haspopup: Indicates the availability and type of interactive popup element, such as menu or dialog, that can be triggered by an element.
      * aria-modal: Indicates whether an element is modal when displayed
      * aria-readonly: Indicates that the element is not editable but is otherwise operable.
      * aria-required: Indicates that user input is required on the element before a form may be submitted.
      * aria-live: Indicates that an element will be updated and describes the types of updates the user agents, assistive technologies, and user can expect from the live region.
      * aria-atomic: Indicates whether assistive technologies will present all, or only parts of, the changed region based on the change notifications defined by the aria-relevant attribute.
      * aria-relevant: Indicates what notifications the user agent will trigger when the accessibility tree within a live region is modified.

* Graceful Degradation vs Progressive Enhancement
      * General progressive enhancement is preferred over graceful degradation
      * “Progressive enhancement – Starting with a baseline of usable functionality, then increasing the richness of the user experience step by step by testing for support for enhancements before applying them
      * “Graceful degradation – Providing an alternative version of your functionality or making the user aware of shortcomings of a product as a safety measure to ensure that the product is usable.”
      * For newer HTML elements it is okay to include redundant WAI-ARIA roles to ensure broader support. These are two examples of where redundant roles are helpful. e.g. `<nav role=”navigation”></nav>` `<main role=”main”></main>`

* Validating WAI-ARIA
      * W3C HTML Validator (validates WAI-ARIA as part of HTML5): https://validator.w3.org/
      * Lighthouse (extends Chrome Developer Tools with an Audit tab): https://developers.google.com/web/tools/lighthouse/
      * ARIA Validator: https://chrome.google.com/webstore/detail/aria-validator/oigghlanfjgnkcndchmnlnmaojahnjoc
      * Deque's aXe (for Chrome): https://chrome.google.com/webstore/detail/axe/lhdoppojpmngadmnindnejefpokejbdd
      * Aria Cheat Sheet https://www.cheatography.com/jreiche/cheat-sheets/wai-aria-1-1/

* WAI-ARIA Landmarksl
      * WAI-ARIA landmarks are used to define regions on a web page, providing a means for assistive technology users to effectively navigate among the various areas of the page. They should be used with other means of within-page navigation, such as bypass links and page headings. These two latter means have been around for much longer and many will continue to use these elements as their primary method of moving around within a web page.
      * 8 landmark roles
            * banner
            * complementary
            * contentinfo
            * form
            * main
            * navigation
            * region (accompanied by `aria-label` / `aria-labelledby`)
            * search
      * Best Practice: All information presented on a page is within a region
      * For duplicate landmarks, use `aria-label` / `aria-labelledby` to distinguish

* Static WAI-ARIA often used
      * aria-describedby - https://www3.org/TR/wai-aria-1.1/#aria-describedby
      * aria-labelledby - https://www3.org/TR/wai-aria-1.1/#aria-labelledby
      * aria-label - https://www3.org/TR/wai-aria-1.1/#aria-label
      * aria-required - https://www3.org/TR/wai-aria-1.1/#aria-required
      * aria-controls - https://www3.org/TR/wai-aria-1.1/#aria-controls
      * aria-details - https://www3.org/TR/wai-aria-1.1/#aria-details
      * aria-haspopup - https://www3.org/TR/wai-aria-1.1/#aria-haspopup
      * aria-live - https://www3.org/TR/wai-aria-1.1/#aria-live
      * aria-owns - https://www3.org/TR/wai-aria-1.1/#aria-owns
      * aria-relevant - https://www3.org/TR/wai-aria-1.1/#aria-relevant
      * aria-roledescription - https://www3.org/TR/wai-aria-1.1/#aria-roledescription

* WAI-ARIA Alert and Message Dialogs
      * When the content of the container element with `role=”alert”` changes, the content that appears is automatically read aloud by screen readers
      * A WAI-ARIA alert has an implicit `aria-live=”assertive”` and `aria-atomic=”true”`
      * `role=alert`
            * for Errors, Warning, Completion Feedback
            * when no user input is needed
      * `role=alertdialog`
            * for Confirmatiom Feedback
            * when user input is expected, with focus sent to the dialog
            * At least one element in the dialog must be focusable when using role=”alertdialog”
      * Model Dialogs
            * Interrupt users and require an action
            * defined using `role=”alertdialog”` and `aria-modal=”true”`
            * when a modal dialog is displayed, focus must be sent to the dialog and must remain in the dialog until whatever interaction (e.g. click the confirmation button) is complete and the dialog has been closed
            * when the dialog closes, focus must be returned to the location from where the dialog was opened

* Tabindex
      * `tabindex=”0”` was added to make it possible for developers to add keyboard accessibility to an element that would not normally have keyboard functionality
      * `tabindex=”0”` can be used in static way when context is needed, to describe how to use a menu for instance
```html
<div tabindex=”0” aria-label=”Use tab key to enter menu, up and down arrow keys to navigate, left and right to open or collapse submenus, space or enter to select.”>
  // Menu code goes here
</div>
```
      * `tabindex=”-1”` was added to remove keyboard accessibility from an element.

* Keyboard interaction
```html
<p>Click on the DIV below, or use Tab key to move focus to it and press Enter.</p>
<div id="button" tabindex="0" role="button">Click Me</div>
<div id="message" aria-live="assertive" aria-atomic="false"></div>
```
```javascript
var btn, msg;
btn = document.getElementById('button');
msg = document.getElementById('message');
btn.addEventListener('click', handleEvents, false);
btn.addEventListener('keydown', handleEvents, false);
function handleEvents(evt) {
  if (evt.type === 'click' || ( evt.type === 'keydown' && evt.keyCode === 13 ) ) {
    msg.innerHTML += 'action triggered by ' + ( evt.type === 'click' ? 'mouse' : 'keyboard') + '<br>';
  }
}
```
      * Predictability, Consistency, Convention - rules for keyboard interaction
      * Combo box (aka Select box) example
      * Conventional keyboard interaction for a combo box
            * Tab to navigate into the combo box
            * While in focus, tab to navigate beyond the combo box
            * While in focus, Shift+Tab to navigate before the combo box
            * While in focus, Down Arrow to show next option
            * While in focus, Up Arrow to show previous option
            * While in focus, Alt+Down Arrow to display options list
            * While options list is open, Alt+Up Arrow to close the options list
            * While options list is open, Esc to close the options list and return to default state
            * While an option is in focus, Enter to select that option
      * Other Design patterns
            * Combobox - https://www.w3.org/TR/wai-aria-practices/#combobox
            * Grid - https://www.w3.org/TR/wai-aria-practices/#grid
            * Listbox - https://www.w3.org/TR/wai-aria-practices/#listbox
            * Menu or menu bar - https://www.w3.org/TR/wai-aria-practices/#menu
            * Radiogroup - https://www.w3.org/TR/wai-aria-practices/#radiobutton
            * Tabs - https://www.w3.org/TR/wai-aria-practices/#tabpanel
            * Toolbar - https://www.w3.org/TR/wai-aria-practices/#toolbar
            * Tree View - https://www.w3.org/TR/wai-aria-practices/#TreeView

* Application Role
      * The application role is used when there is not a corresponding widget interaction pattern available to provide semantics for a custom widget.
      * Disables default keyboard functionality

* Presentation Role
      * `role="none"` removes default semantics from children of the element it applies to
      * Disables default keyboard functionality
      * So, for instance, if you have a list with role=”presentation”, it should not announce as a list, and its list items should not announce as list items. However, nested lists within those suppressed list items will announce as usual.
      * If you are trying to hide elements completely from screen readers, you might consider using either `aria-hidden` or CSS `display:none`.
      * Three common uses for role=”presentation” include:
            * Hiding a decorative image; it is equivalent to giving the image null alt text.
            * Suppressing table semantics for tables used for layout in circumstances where the table semantics do not convey meaningful relationships.
            * Eliminating semantics of intervening orphan elements in the structure of a composite widget, such as a tablist, menu, or tree as demonstrated in the example above.

* Live Regions
      * Live regions are used to present changes in web content that occur after a web page has loaded. e.g. news feeds, feedback/error messages, live chat output
      * `aria-live: polite` indictes the priority of the content updated - will wait for a break in audio before announcng
      * `aria-live: assertive` inpterrupts screen reader and reads changed content before continuing. To be avoided except in cases of critical information (e.g. error mesage or critical feedback)
      * `aria-live` would not be used for feedback/error messages, `role=alert` would be used
      * `role=log`, `role=marquee`, `role=timer`, `role=status` are other common live regions
      * Be careful with Live Regions with Carousel bannerws and timers.

