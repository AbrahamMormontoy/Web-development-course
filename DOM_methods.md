# DOM Element Selection — Concepts with Code and Explanations

Short, practical lecture-style notes linking DOM selection theory to concise JavaScript examples. Emphasize theory and code.

---

## Table of contents
- getElementById()
- getElementsByClassName()
- getElementsByTagName()
- querySelector()
- querySelectorAll()
- Conclusion

---

## getElementById()
- Theory:
  - Selects a single element by its unique id attribute.
  - Returns a reference to the element for manipulation.
- Example:
```html
<div id="header">Welcome to My Website</div>

<script>
  const headerElement = document.getElementById('header');
  headerElement.style.color = 'blue'; // Changes the text color to blue
</script>
```
- Explanation:
  - getElementById('header') selects the <div id="header"> element and sets its text color to blue.

---

## getElementsByClassName()
- Theory:
  - Selects all elements with a given class name.
  - Returns a live HTMLCollection (array-like) of matching elements.
- Example:
```html
<p class="note">Note 1</p>
<p class="note">Note 2</p>

<script>
  const notes = document.getElementsByClassName('note');
  for (let i = 0; i < notes.length; i++) {
    notes[i].style.fontWeight = 'bold'; // Makes the text bold
  }
</script>
```
- Explanation:
  - getElementsByClassName('note') returns all <p class="note"> elements; loop applies bold font to each.

---

## getElementsByTagName()
- Theory:
  - Selects all elements with the specified tag name.
  - Returns a live HTMLCollection of matching elements.
- Example:
```html
<ul>
  <li>Item 1</li>
  <li>Item 2</li>
</ul>

<script>
  const listItems = document.getElementsByTagName('li');
  for (let item of listItems) {
    item.style.listStyleType = 'square'; // Changes bullet points to squares
  }
</script>
```
- Explanation:
  - getElementsByTagName('li') selects all list items; each item’s bullet style is changed to square.

---

## querySelector()
- Theory:
  - Returns the first element that matches the specified CSS selector.
- Example:
```html
<div class="container">
  <p>First paragraph</p>
  <p>Second paragraph</p>
</div>

<script>
  const firstParagraph = document.querySelector('.container p');
  firstParagraph.style.color = 'green'; // Changes the text color to green
</script>
```
- Explanation:
  - querySelector('.container p') selects the first <p> inside .container and sets its color to green.

---

## querySelectorAll()
- Theory:
  - Returns a static NodeList of all elements matching the CSS selector.
  - NodeList supports forEach iteration.
- Example:
```html
<div class="container">
  <p>First paragraph</p>
  <p>Second paragraph</p>
</div>

<script>
  const paragraphs = document.querySelectorAll('.container p');
  paragraphs.forEach(paragraph => {
    paragraph.style.fontSize = '18px'; // Sets the font size to 18px
  });
</script>
```
- Explanation:
  - querySelectorAll('.container p') selects all <p> in .container; forEach sets each paragraph’s font size to 18px.

---

## Conclusion
- JavaScript provides multiple DOM methods to obtain elements in different ways:
  - getElementById(): single element by id.
  - getElementsByClassName(): live collection by class.
  - getElementsByTagName(): live collection by tag.
  - querySelector(): first match by CSS selector.
  - querySelectorAll(): static NodeList for all matches by CSS selector.
- Each method returns elements that can be manipulated to change structure, style, or content.
