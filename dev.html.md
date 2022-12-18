# Warren Shea's Notes for HTML
v20221213

## The difference between Attributes and Properties
* Attributes are defined by HTML (e.g. id, type, and aria-required are attributes in `<input id="input_id" type="text" aria-required="true">`)
* Properties are accessed from DOM (Document Object Model) nodes (e.g. id is a property in `<input id="input_id" type="text">` because you can do `document.getElementById("input_id).id` but aria-required is not a property because you can't do `document.getElementById("input_id).[something for aria-required]`.)
* A few HTML attributes have 1:1 mapping to properties; for example, `id`.
* Some HTML attributes don’t have corresponding properties; for example, `aria-\*`.
* Some DOM properties don’t have corresponding attributes; for example, textContent.

## Web Components
custom elements -> define components \
shadow dom -> encapsulate styles \
slots and templates
