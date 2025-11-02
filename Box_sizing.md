# Box Sizing — Concepts with Code and Explanations

Short, practical lecture-style notes emphasizing theory and minimal CSS/HTML examples. Use box-sizing to control whether width/height include padding and border.

---

## Table of contents
- Box sizing (overview)
- content-box (default)
- border-box
- What to choose?
- Conclusion

---

## Box sizing (overview)
- Theory:
  - The box-sizing property controls how width and height values are applied to an element.
  - It specifies whether width/height include border and padding.
  - Values:
    - content-box (default)
    - border-box
  - Deprecated value (don't use): padding-box
- Example (demonstrates difference):
```html
<div class="content-box">Content Box</div>
<hr>
<div class="border-box">Border Box</div>
```
```css
div {
    border: 2px solid black;
    width: 150px;
    height: 150px;
    padding: 10px;
    background-color: aquamarine;
}
.content-box { box-sizing: content-box; }
.border-box  { box-sizing: border-box; }
```
- Result (concept):
  - The Content Box item is bigger than the Border Box item (due to how padding/border are counted).

---

## content-box
- Theory:
  - Default value.
  - width/height include only the content area.
  - padding and border are added outside the specified width/height.
- Example:
```css
div {
  box-sizing: content-box;
  width: 260px;
  height: 120px;
}
```
- Calculations:
  - Content width: 260px.
  - Content height: 120px.
  - Total width = 260px + padding-left + padding-right + border-left + border-right.
  - Total height = 120px + padding-top + padding-bottom + border-top + border-bottom.

---

## border-box
- Theory:
  - width/height include padding and border.
  - Total element size equals the specified width/height regardless of padding/border.
- Example:
```css
div {
  box-sizing: border-box;
  width: 260px;
  height: 120px;
}
```
- Calculations:
  - Total width of the element: 260px.
  - Total height of the element: 120px.
  - Content width = 260px - padding-left - padding-right - border-left - border-right.
  - Content height = 120px - padding-top - padding-bottom - border-top - border-bottom.

---

## What to choose?
- Recommendation:
  - Prefer box-sizing: border-box because it simplifies width and height calculations (specified size stays constant).
- Caveat:
  - Very old browsers may not support border-box (introduced in CSS3); most modern browsers do support it.
- Note:
  - Margin is outside the box and is not included in width/height calculations; account for margins when laying out multiple elements.

---

## Conclusion
- box-sizing determines whether padding and border are included in width/height calculations.
- content-box: width/height apply to content only; padding/border add to total size.
- border-box: width/height include padding and border; total size remains as specified.
- Understanding the CSS Box Model is essential for mastering layout and sizing.
