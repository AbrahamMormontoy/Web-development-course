# Width & Height — Concepts with Code and Explanations

Short, practical lecture-style notes emphasizing theory and concise CSS examples. Focus on setting element sizes and using min/max constraints.

---

## Table of contents
- Width
- Min-width and Max-width
- Height
- Min-height and Max-height
- Conclusion

---

## Width

Theory
- `width` sets the content width of an element.
- Applies to block elements and some replaced/inline elements (e.g., `<img>`).
- Accepts any CSS length unit (px, %, em, vh, etc.).

Example
```css
p {
  width: 100px;
}
```

Explanation
- The `<p>` element's content box width becomes 100px.
- If changes aren't visible, add a background to confirm layout differences.

---

## Min-width and Max-width

Theory
- `min-width` prevents an element from becoming narrower than the specified size.
- `max-width` prevents an element from becoming wider than the specified size.
- These are constraints, not strict sizes — used for responsive layouts.

Examples
```css
p {
  min-width: 10vh;
}

p {
  max-width: 80vh;
}
```

Explanation
- `min-width: 10vh` ensures the element stays at least 10% of viewport height in width.
- `max-width: 80vh` caps the element's width to 80% of viewport height.
- Use these to keep layouts reasonable across different screen sizes.

---

## Height

Theory
- `height` sets the content height of an element.
- Accepts any CSS length unit.
- Negative values are not allowed.

Example
```css
div {
  height: 50px;
}
```

Explanation
- The `<div>` content box height becomes 50px.

---

## Min-height and Max-height

Theory
- `min-height` ensures an element is at least a given height.
- `max-height` caps the element's height.
- Useful for responsive vertical sizing and preventing overflow.

Examples
```css
div {
  min-height: 50px;
}

div {
  max-height: 50px;
}
```

Explanation
- `min-height: 50px` guarantees at least 50px height.
- `max-height: 50px` limits height to 50px.

---

## Conclusion

- Use `width` and `height` to set fixed sizes.
- Use `min-` / `max-` properties to add responsive constraints (they don't force a strict size).
- These properties are commonly used for sidebars, images, tables, and other blocks to control layout across devices.
