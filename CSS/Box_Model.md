# Box Model — Concepts with Code and Explanations

Short, practical lecture-style notes emphasizing theory and minimal HTML/CSS examples. Focus on content, padding, border, margin, and how width/height are computed.

---

## Table of contents
- What is the Box Model?
- Content
- Padding
- Border
- Margin
- Height and width
- Conclusion

---

## What is the Box Model?
- Theory:
  - Every HTML element generates a rectangular box.
  - Boxes combine content, padding, border, and margin to form the whole element.
  - Properties: margin, padding, height, width, border.
- Diagram:
  - Content in the middle → padding → border → margin (margin is transparent).

---

## Content
- Theory:
  - The content area holds text, images, etc.
  - width and height properties control content dimensions.
- Example (HTML + CSS):
```html
<p>I am learning about the Box Model.</p>
<p>The Box Model is amazing.</p>
```
```css
body { background-color: lightcoral; }
p { border: 1px solid blue; }
```
- Explanation:
  - Two p tags with blue border and default margins (p has default margin-top/bottom ≈ 16px).
  - No padding applied; borders sit directly around content.

---

## Padding
- Theory:
  - Space between content and border.
  - Can be set per side: padding-top, padding-right, padding-bottom, padding-left.
- Examples:
```css
p {
  border: 1px solid blue;
  padding: 10px;
}
```
```css
p {
  border: 1px solid blue;
  padding: 10px 30px 2px 40px; /* top - right - bottom - left */
}
```
```css
p {
  border: 1px solid blue;
  padding: 10px 5px 30px; /* top - right & left - bottom */
}
```
- Explanation:
  - Padding increases space inside the border.
  - For block elements (like p), element width fills available horizontal space inside its border.

---

## Border
- Theory:
  - Region between padding and margin.
  - Controlled by border-width, border-style, border-color (or shorthand border).
- Example:
```css
p {
  border: 10px solid blue;
  padding: 10px;
}
```
- Explanation:
  - Border surrounds padding and content and contributes to the element's overall size.

---

## Margin
- Theory:
  - Outermost transparent layer outside the border.
  - Controlled by margin-top, margin-right, margin-bottom, margin-left (or shorthand margin).
- Examples:
```css
p {
  border: 1px solid blue;
  padding: 10px;
  margin: 20px;
}
```
```css
p {
  border: 1px solid blue;
  padding: 10px;
  margin: 10px 30px 10px 5px; /* top - right - bottom - left */
}
```
```css
p {
  border: 1px solid blue;
  padding: 10px;
  margin: 10px 15px; /* top & bottom - right & left */
}
```
- Explanation:
  - Margin increases space outside the border; background of parent shows through because margin is transparent.

---

## Height and width
- Theory:
  - height and width affect the content area size.
  - Padding and border add to the element's full size (unless box-sizing changes this).
- Calculation (when using content-box):
  - Height = height + padding-top + border-top + padding-bottom + border-bottom
  - Width  = width  + padding-left + border-left + padding-right + border-right
- Note:
  - CSS3 box-sizing (content-box / border-box) changes how calculations are applied (covered in a later topic).

---

## Conclusion
- All HTML elements form boxes composed of content, padding, border, and margin.
- Use height, width, padding, border, and margin to control placement and sizing.
- Understanding the Box Model is essential for layout and sizing in CSS.
