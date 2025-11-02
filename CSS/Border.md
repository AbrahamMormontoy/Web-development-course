# Border — Concepts with Code and Explanations

Short, practical lecture-style notes emphasizing theory and minimal CSS examples. Each section shows core concepts, code snippets, and brief explanations.

---

## Table of contents
- Border style
- Border color
- Border width
- Border shorthand (border)
- Border for one side of the element
- Conclusion

---

## Border style

Theory
- Use `border-style` to display an element's border and set its visual style.
- Common keyword values: dotted, dashed, solid, double, groove, ridge, inset, outset.

Example
```css
h1 {
  border-style: double;
}
```

Explanation
- Sets the `<h1>` element's border style to double.

---

## Border color

Theory
- `border-color` sets the border's color.
- If not specified, the border color defaults to the element's text color.

Example
```css
p {
  border-style: solid; /* enables a border */
  border-color: brown; /* sets border color */
}
```

Explanation
- Applies a solid brown border to the `<p>` element.

---

## Border width

Theory
- `border-width` controls the border thickness; accepts CSS length units (e.g., `px`).

Example
```css
h4 {
  border-style: dotted; /* enables a border */
  border-width: 4px;    /* sets border thickness */
}
```

Explanation
- Gives the `<h4>` a dotted border 4 pixels wide.

---

## Border shorthand (border)

Theory
- The `border` shorthand lets you set border width, style, and color in one declaration.
- Values can be written in any order.

Example
```css
p {
  border: 2px solid gray;
}
```

Explanation
- Sets a 2px solid gray border on the `<p>` element using the shorthand.

---

## Border for one side of the element

Theory
- You can apply borders to individual sides using:
  - `border-top`, `border-right`, `border-bottom`, `border-left`.
- Each accepts the same width/style/color combinations as `border`.

Example 1
```html
<p>In<span>troduction to C</span>SS</p>
```
```css
span {
  border-bottom: 2px solid green;
}
```

Explanation
- Adds a 2px solid green border only under the `<span>` text.

Example 2
```html
<p>News</p>
```
```css
p {
  border-bottom: 2px solid red;
  border-left: 2px solid red;
}
```

Explanation
- Adds red borders to the bottom and left sides of the `<p>` element.

---

## Conclusion

- Borders are configurable via `border-style`, `border-color`, and `border-width`.
- The `border` shorthand combines width, style, and color in one declaration.
- Use side-specific properties (`border-top`, `border-right`, `border-bottom`, `border-left`) to style individual edges.
- Borders are useful for decoration and highlighting interactive or important elements.
