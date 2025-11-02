# Flexbox — flex-basis, flex-grow, flex-shrink, and flex shorthand (Concepts with Code and Explanations)

Short, practical lecture-style notes linking flexbox theory to concise HTML/CSS examples. Emphasize theory and code.

---

## Table of contents
- flex-basis
- flex-grow
- flex-shrink
- flex (shorthand)
- Conclusion

---

## flex-basis

Theory
- Defines the initial size of the flex item along the main axis.
- If not set, the item's content size (or width) is used (depends on flex shorthand/defaults).

Example
```html
<div class="flex-container">
  <div class="flex-item item1">50px</div>
  <div class="flex-item item2">100px</div>
  <div class="flex-item item3">50px</div>
  <div class="flex-item item4">70px</div>
</div>
```

```css
.flex-container {
  border: 1px solid black;
  display: flex;
  width: 400px;
}

.flex-item {
  border: 1px solid black;
  text-align: center;
  margin: 5px;
}

.item1 { flex-basis: 50px; }
.item2 { flex-basis: 100px; }
.item3 { flex-basis: 50px; }
.item4 { flex-basis: 70px; }
```

Explanation
- Four items get initial widths from flex-basis.
- The sum of these sizes (plus margins) may leave free space or overflow the container depending on totals.

---

## flex-grow

Theory
- Defines how to distribute remaining free space among items.
- Remaining space is shared in proportion to each item's flex-grow value.
- Default flex-grow is 0 (no growth).

Examples

1) Items with same flex-basis, no flex-grow:
```css
.flex-item { flex-basis: 50px; } /* no flex-grow */
```

2) Add equal growth to all items:
```css
.flex-item {
  flex-basis: 50px;
  flex-grow: 1;
}
```

3) Make one item take more free space:
```css
.flex-item { flex-basis: 50px; flex-grow: 1; }
.item2 { flex-grow: 2; }
```

Explanation
- With flex-grow:1 on all items they equally share available free space.
- With item2 having flex-grow:2, free space is divided by sum (1+2+1+1 = 5); item2 receives two parts, others one part each.

---

## flex-shrink

Theory
- Defines how items shrink when total item sizes exceed the container.
- Items reduce in proportion to flex-shrink and their base size (final width considered with margins).
- Default flex-shrink is 1 (will shrink if necessary).

Example (overflow case)
```html
<div class="flex-container">
  <div class="flex-item item1">100px</div>
  <div class="flex-item item2">200px</div>
  <div class="flex-item item3">100px</div>
  <div class="flex-item item4">150px</div>
</div>
```

```css
.flex-container {
  border: 1px solid black;
  display: flex;
  width: 400px;
}

.flex-item {
  border: 1px solid black;
  text-align: center;
  margin: 5px;
}

.item1 { flex-basis: 100px; }
.item2 { flex-basis: 200px; }
.item3 { flex-basis: 100px; }
.item4 { flex-basis: 150px; }
```

When items overflow, add different flex-shrink values:
```css
.item1 { flex-shrink: 1; flex-basis: 100px; }
.item2 { flex-shrink: 2; flex-basis: 200px; }
.item3 { flex-shrink: 3; flex-basis: 100px; }
.item4 { flex-shrink: 4; flex-basis: 150px; }
```

Calculation (as in the example)
- Space deficiency = sum(final widths with margins) − container width  
  = (100+5+5) + (200+5+5) + (100+5+5) + (150+5+5) − 400 = 190
- Sum for proportion = Σ(flex-shrink_i × finalWidth_i) = 1500
- Reduction for each item = space_deficiency × flex-shrink_i × finalWidth_i / sum
  - item1: 190 × 1 × 110 / 1500 = 13.9 → 100 − 13.9 = 86.1
  - item2: 190 × 2 × 210 / 1500 = 53.2 → 200 − 53.2 = 146.8
  - item3: 190 × 3 × 110 / 1500 = 41.8 → 100 − 41.8 = 58.2
  - item4: 190 × 4 × 160 / 1500 = 81   → 150 − 81   = 69

Explanation
- Items shrink proportionally according to flex-shrink and their sizes.
- Browser rendering may show slight deviations due to rounding.

---

## flex (shorthand)

Theory
- Shorthand combines flex-grow, flex-shrink, and flex-basis: flex: <grow> <shrink> <basis>.
- Defaults when not set: flex-grow: 0; flex-shrink: 1; flex-basis: auto.
- Keyword mappings:
  - flex: initial; → flex: 0 1 auto;
  - flex: auto;    → flex: 1 1 auto;
  - flex: none;    → flex: 0 0 auto;

Explanation
- Use flex shorthand to set growth, shrink behavior, and base size in one declaration.
- Example: flex: 1 0 100px → grow to take space, do not shrink, base 100px.

---

## Conclusion

- flex-basis determines the initial item size along the main axis.
- flex-grow distributes remaining free space proportionally (sum of grow factors).
- flex-shrink reduces item sizes proportionally when items overflow (uses a weighted formula with final widths).
- Use flex shorthand to set grow, shrink, and basis together.
- The key idea: distribution (growth or shrinkage) is proportional to the respective factors.
