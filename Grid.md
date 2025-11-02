# Gap — Grid gap properties (Concepts with Code and Explanations)

Short, practical lecture-style notes linking gap theory to concise CSS/HTML examples. Emphasize theory and code.

---

## Table of contents
- Overview
- row-gap
- column-gap
- gap (shorthand)
- Example (HTML + CSS)
- Conclusion

---

## Overview

Theory
- Gap-related properties control spacing between grid tracks (rows and columns).
- Properties covered:
  - row-gap (formerly grid-row-gap)
  - column-gap (formerly grid-column-gap)
  - gap (shorthand; formerly grid-gap)
- Note: the grid- prefix is deprecated; browsers treat grid-row-gap as row-gap, grid-column-gap as column-gap, grid-gap as gap.
- gap works with grid layouts and can also be used with flexbox and multi-column layouts (this topic focuses on grid).

---

## row-gap

Theory
- row-gap sets the size of the gap between grid rows only.

Example
```css
.container {
  display: grid;
  grid-template-columns: auto auto auto;
  background-color: #9771D5;
  padding: 10px;

  /* Applying the row-gap property */
  row-gap: 20px;
}

.container > div {
  background-color: #FDFDFD;
  text-align: center;
  padding: 20px 0;
  font-size: 30px;
  border-radius: 5pt;
}
```

Explanation
- Only vertical spacing between rows is 20px; no column gap is applied.
- The property applies to every row in the grid.

---

## column-gap

Theory
- column-gap sets the size of the gap between grid columns (also works with flexbox and multi-column).

Example
```css
.container {
  display: grid;
  grid-template-columns: auto auto auto;
  background-color: #9771D5;
  padding: 10px;

  /* Applying the column-gap property */
  column-gap: 20px;
}

.container > div {
  background-color: #FDFDFD;
  text-align: center;
  padding: 20px 0;
  font-size: 30px;
  border-radius: 5pt;
}
```

Explanation
- Only horizontal spacing between columns is 20px; rows remain adjacent.

---

## gap (shorthand)

Theory
- gap is a shorthand for row-gap and column-gap.
- Syntax:
  - gap: <row-gap> <column-gap>;
  - If two values are provided, the first is row-gap, the second is column-gap.
- Default value is 0 (no gap).
- Accepts any CSS length units (px, %, em, etc.).

Examples
- Equivalent separate properties:
```css
.container {
  column-gap: 20px;
  row-gap: 30px;
}
```
- Shorthand form (same result):
```css
.container {
  gap: 30px 20px; /* row-gap: 30px; column-gap: 20px; */
}
```

Explanation
- Use gap when you want to set row and column gaps in a single declaration.
- The first value corresponds to the vertical gap (rows), the second to the horizontal gap (columns).

---

## Example (HTML + CSS)

HTML:
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>Example</title>
  <link rel="stylesheet" href="style.css">
</head>
<body>
  <div class="container">
    <div class="item-one">Item 1</div>
    <div class="item-two">Item 2</div>
    <div class="item-three">Item 3</div>
    <div class="item-four">Item 4</div>
    <div class="item-five">Item 5</div>
    <div class="item-six">Item 6</div>
  </div>
</body>
</html>
```

CSS (using gap):
```css
.container {
  display: grid;
  grid-template-columns: auto auto auto;
  background-color: #9771D5;
  padding: 10px;

  /* Applying the gap property */
  gap: 20px;
}

.container > div {
  background-color: #FDFDFD;
  text-align: center;
  padding: 20px 0;
  font-size: 30px;
  border-radius: 5pt;
}
```

Explanation
- The .container grid with three columns shows 20px between both rows and columns.
- Removing the gap property eliminates the spacing between items.

---

## Conclusion

- Use row-gap to control vertical spacing and column-gap for horizontal spacing.
- Use gap as a convenient shorthand: gap: <row-gap> <column-gap>.
- The grid- prefixed properties are deprecated; use row-gap/column-gap/gap.
- gap accepts standard CSS length units and defaults to 0 (no spacing).
- gap is supported for grid and (in modern CSS) also usable with flexbox and multi-column layouts.
