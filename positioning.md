# Positioning — Concepts with Code and Explanations

Short, practical lecture-style notes emphasizing theory and minimal CSS examples. Each section shows the core concept, a minimal code snippet, and a short explanation of what the code does.

---

## Table of contents
- Property not applicable
- top
- bottom
- left
- right
- Conclusion

---

## Property not applicable

Theory
- Positioning properties (top, bottom, left, right) do not work unless the element's `position` is not `static`.
- The default `position` value is `static`.
- To move an element with these properties you must set `position` to a non-static value (e.g., `relative`, `absolute`, `fixed`, `sticky`).

Example
```css
/* Without a non-static position, top/left/etc. have no effect */
div {
  position: relative;
  top: 10px;
}
```

Explanation
- `position: relative;` enables the `top: 10px;` offset. Without a non-static `position`, the `top` would be ignored.

---

## top

Theory
- `top` sets how far an element moves from the top.
- Accepts positive and negative values, any CSS length unit or percentage.
- When `position` is non-static, a positive `top` moves the element down.

Example
```css
div {
  position: relative; 
  top: 10px;
}
```

Explanation
- The element's top edge is shifted down by 10 pixels relative to its normal position.

---

## bottom

Theory
- `bottom` sets how far the element's bottom edge is shifted.
- Positive values move the element upward (i.e., lift its bottom edge).

Example
```css
p {
  position: relative; 
  bottom: 5px;
}
```

Explanation
- The `<p>` element is moved up by 5 pixels from its normal position.

---

## left

Theory
- `left` controls horizontal offset from the left edge.
- Positive `left` moves the element to the right; negative `left` moves it to the left (outside its original block).

Example
```css
div {
  position: relative; 
  left: -25px;
}
```

Explanation
- The element is shifted 25 pixels to the left (negative value moves it outside the original block to the left).

---

## right

Theory
- `right` controls horizontal offset from the right edge.
- Positive `right` moves the element to the left; values may be percentages or lengths.

Example
```css
div {
  position: relative; 
  right: -2%;
}
```

Explanation
- The element's right edge is offset by -2% (moving it to the right by 2% in this example because the value is negative).

---

## Conclusion

- Position offsets (`top`, `bottom`, `left`, `right`) allow precise movement of elements, but only when `position` is set to a non-static value.
- Each property accepts positive/negative values and standard CSS units (including percentages).
- Use these offsets to finely control layout for interfaces like galleries, pop-ups, or decorative elements.
