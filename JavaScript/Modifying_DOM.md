# DOM Modification — Concepts with Code and Explanations

Short, practical lecture-style notes linking DOM modification theory to concise JavaScript examples. Each section shows a core concept, a minimal code snippet, and a short explanation of what the code does and how it illustrates the theory.

---

## Table of contents
- innerHTML and textContent
- createElement() and createTextNode()
- appendChild()
- remove()
- Conclusion

---

## innerHTML and textContent

- Theory:
  - innerHTML: returns/sets HTML content of an element (string containing HTML markup).
  - textContent: represents the text content; safely inserts text (tags shown as plain text).
- Example (innerHTML):
```javascript
let container = document.querySelector(".container");
container.innerHTML = "<p>DOM is cool!</p>";

console.log(container); // <div class="container"><p>DOM is cool!</p></div>
```
- Example (clear innerHTML):
```javascript
container.innerHTML = "";

console.log(container); // <div class="container"></div>
```
- Example (textContent):
```javascript
container.textContent = "Hello, World!";

console.log(container); // <div class="container">Hello, World!</div>
```
- Notes:
  - textContent displays any tags as plain text (e.g., "<b>bold</b>" not bold).
  - Use innerHTML for inserting HTML markup; use textContent for plain text.

---

## createElement() and createTextNode()

- Theory:
  - createElement(tagName): creates a new HTML element specified by tag name. Must use a valid tag name.
  - createTextNode(text): creates a new text node with the provided text.
- Examples:
```javascript
let myElement = document.createElement("div");
let errorElement = document.createElement("Hello!"); // invalid
console.log(myElement); // <div></div>
// console.log(errorElement); // DOMException: The tag name provided ('Hello!') is not a valid name.
```
```javascript
let myText = document.createTextNode("I am learning DOM methods!");
let justTextNode = document.createTextNode("div");

console.log(myText); // I am learning DOM methods!
console.log(justTextNode); // div
```
- Notes:
  - createElement throws if tag name is invalid.
  - createTextNode produces plain text nodes to insert into the DOM.

---

## appendChild()

- Theory:
  - appendChild(node): inserts node as the last child of the specified parent; returns the appended element.
- Example:
```javascript
document.body.innerHTML = "<ul id='list'><li>An item</li></ul>";

let list = document.getElementById("list");
let newItem = document.createElement("li");
newItem.textContent = "A new item";
list.appendChild(newItem);

console.log(list); // <ul id='list'><li>An item</li><li>A new item</li></ul>
```
- Notes:
  - Use to add nodes to the end of a parent element's children.

---

## remove()

- Theory:
  - remove(): deletes an element from the DOM.
- Example:
```javascript
document.body.innerHTML = "<div id='container'><h1 id='heading'>I like JS!</h1></div>";

let container = document.getElementById("container");
let heading = document.getElementById("heading");
heading.remove();

console.log(container); // <div id="container"></div>
```
- Notes:
  - Removes the element node from its parent.

---

## Conclusion

- innerHTML and textContent: set HTML vs plain text content.
- createElement() and createTextNode(): create element and text nodes.
- appendChild(): insert node as last child.
- remove(): delete element from the DOM.
- These methods allow inserting, updating, and deleting document elements programmatically.
