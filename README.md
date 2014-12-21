scribly
=======

Scribly is a javascript object made to allow for the dynamic creation of editable text elements within a webpage. It includes storing the values of the edited fields in the `sessionStorage` to send back to the server (yourself). Give the user control over their content without messing with the bulk of a CMS.

Features
========

The object comes with several methods:

* `edit(selector, parent, inputType)`
  * provide the CSS selector of the element(s) that you want editable
  * provide a DOM element as a parent element to search in for the selector
  * use `text` or `textarea` for the inputType, defaults to `text`
  * this function gives the selected element an attribute: `data-sid`. this is its scribly id and is used for its key in the `sessionStorage`. it tries to be as specific as possible by using an elements id, class, or tag, depending on which exists (tag being the fall-back), and the elements index in the element collection from the selector. formatted like: `p-0` meaning: `[id:class:tag]-[index]`. while being edited, the key in the `sessionStorage` would be prefixed by `edit` like: `edit-p-0`

* `save(parent)`
  * updates the elements text, saves the edited portions to the `sessionStorage`
  * provide a parent element (must be HTML element object) to search through or leave blank to save all within the document

* `cancel(parent)`
  * reverts the elements back to their original state, saves no edits
  * provide a parent element (must be HTML element object) to search through or leave blank to save all within the document

* `sessionStorage`
  * while an element is being edited, its current text is stored 

Use
===

Say you want every `p` element to become editable when a user presses a button, and then saves when the use presses a save button. You would do:
```HTML
<button onclick="scribly.edit('p')">Edit</button>
<button onclick="scribly.save()">Save</button>
```
This code will generate input boxes with a type of text to replace the `innerHTML` property of every element with a `p` tag. When the save button is pressed, scribly will store the newly edited text in the `sessionStorage` and update the `innerHTML` of the elements that were edited.

To provide the user with an option to opt-out of their current edits, you could provide a cancel button:
```HTML
<button onclick="scribly.cancel()">Cancel</button>
```
This will reset all editable elements and their `innerHTML` providing no changes. It will also not store any of the edits.

Scribly also provides functionality for editing, cancelling and saving certain elements while leaving others unaffected by passing a DOM element to the `parent` parameter.
```javascript
var div1 = document.getElementById('div1');
scribly.edit('p', div1); //to edit 
scribly.save(div1); //to save
scrible.cancel(div1); //to cancel
```
This would edit, save, and close elements that are only in `div1`, leaving any others open for editing.
