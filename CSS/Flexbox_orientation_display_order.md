# Flexbox — Direction, Wrapping, Flow, and Order (Concepts with Code and Explanations)

Short, practical lecture-style notes emphasizing theory and concise HTML/CSS examples. Each section shows the core concept, a minimal code snippet, and a short explanation of how the code illustrates the theory.

---

## Table of contents
- Overview
- flex-direction
- flex-wrap
- flex-flow (shorthand)
- order
- Summary

---

## Overview

Theory
- Flexbox controls layout along two axes:
  - Main axis — direction of flex items (controlled by flex-direction).
  - Cross axis — perpendicular to the main axis.
- Use flex-container properties (flex-direction, flex-wrap, flex-flow) to control axes and wrapping.
- Use item-level property order to change visual ordering without changing HTML.

---

## flex-direction

Theory
- Determines the direction in which flex items are laid out along the main axis.
- Default: row (left → right).
- Values:
  - row — left to right (default).
  - row-reverse — right to left.
  - column — top to bottom (cross axis becomes main).
  - column-reverse — bottom to top.

Example
```html
<div class="flex-container">
  <div class="flex-item">item 1</div>
  <div class="flex-item">item 2</div>
  <div class="flex-item">item 3</div>
</div>
```
```css
.flex-container {
  flex-direction: column;
}
```

Explanation
- With `flex-direction: column`, items stack vertically from top to bottom along the main axis.

---

## flex-wrap

Theory
- Controls whether flex items stay on one line or wrap to multiple lines when they exceed container space.
- Default: nowrap (items stay on a single line and may shrink or overflow).
- Values:
  - nowrap — no wrapping (default).
  - wrap — items wrap onto multiple lines (new lines follow main axis direction).
  - wrap-reverse — items wrap but the cross-axis order is reversed (new lines placed in reverse).

Example (wrap)
```css
.flex-container {
  display: flex;
  flex-wrap: wrap;
}
```

Explanation
- `flex-wrap: wrap` causes overflow items to move to the next line (or next column when using `flex-direction: column`).
- `wrap-reverse` reverses the direction of the cross-axis when wrapping occurs.

---

## flex-flow (shorthand)

Theory
- Shorthand for `flex-direction` and `flex-wrap`.
- Syntax: `flex-flow: <flex-direction> <flex-wrap>;`
- Recommended to use shorthand for concise CSS.

Example (equivalent)
```css
.flex-container {
  flex-direction: row-reverse;
  flex-wrap: wrap;
}

/* same as */
.flex-container {
  flex-flow: row-reverse wrap;
}
```

Explanation
- `flex-flow: row-reverse wrap;` sets the main axis direction to right→left and enables wrapping on overflow.

---

## order

Theory
- Item-level property that controls visual order of flex items.
- Value is an integer (default 0). Lower values appear earlier.
- Items with same `order` preserve source (HTML) order.

Examples

1) Move last item before others
```html
<div class="flex-container">
  <div class="flex-item item1">item 1</div>
  <div class="flex-item item2">item 2</div>
  <div class="flex-item item3">item 3</div>
</div>
```
```css
.item3 { order: -1; }
```
Explanation
- `item3` appears before the other items because its `order` is lower than the default 0.

2) Custom ordering
```css
.item1 { order: 3; }
.item2 { order: 1; }
.item3 { order: 2; }
```
Explanation
- Items are displayed in increasing order values: item2 (1), item3 (2), item1 (3).

3) Same order values
```css
.item1 { order: 1; }
.item2 { order: 1; }
.item3 { order: 1; }
```
Explanation
- When multiple items share the same `order` value, they render in the same sequence as they appear in the HTML.

---

## Summary

- flex-direction sets the main axis direction: row, row-reverse, column, column-reverse.
- flex-wrap controls whether items wrap to new lines: nowrap, wrap, wrap-reverse.
- flex-flow is shorthand for combining flex-direction and flex-wrap.
- order reorders individual flex items visually via integer values; equal values preserve source order.
- These properties let you change layout direction, handle overflow, and rearrange visual order without modifying the HTML structure.
