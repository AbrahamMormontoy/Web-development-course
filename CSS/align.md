# Flexbox — Align (Concepts with Code and Explanations)

Short, practical lecture-style notes linking flexbox alignment theory to concise CSS/HTML examples. Each section shows core concept, minimal code, and a short explanation.

---

## Table of contents
- Overview
- justify-content
- align-items
- align-self
- align-content
- Summary

---

## Overview
- Theory:
  - Flexbox organizes layout along two axes:
    - Main axis — direction set by flex-direction (row / column).
    - Cross axis — perpendicular to the main axis.
  - Use justify-content to distribute free space along the main axis.
  - Use align-items / align-self to control alignment on the cross axis.
  - Use align-content to distribute free space between lines when the flex container has multiple lines (wrap).

---

## justify-content
- Theory:
  - Distributes free space along the main axis without resizing items.
  - Useful when items don't grow/shrink and you want gaps or positioning.
- Common values:
  - flex-start — items at main-start (default).
  - flex-end — items at main-end.
  - center — items centered.
  - space-between — first at start, last at end, equal gaps between items.
  - space-around — equal space around items (end gaps half-size of inter-item gaps).
- Example:
```html
<div class="row">
  <div>1</div><div>2</div><div>3</div>
</div>
```
```css
.row {
  display: flex;
  justify-content: space-between; /* try flex-start / center / space-around */
}
```
- Explanation:
  - With space-between the three items fill the row with equal spacing between them; with center they cluster at center.

---

## align-items
- Theory:
  - Aligns all flex items along the cross axis.
  - Affects every item in the container (unless overridden by align-self).
- Common values:
  - flex-start — cross-start (top in row layout).
  - flex-end — cross-end (bottom in row layout).
  - center — centered on cross axis.
  - baseline — aligned by text baseline.
  - stretch — items stretch to fill cross size (default when no fixed height).
- Example:
```css
.container {
  display: flex;
  height: 8em;
  align-items: center; /* try flex-start / flex-end / stretch / baseline */
}
.container > div { width: 4em; border: 1px solid #333; }
```
- Explanation:
  - align-items:center vertically centers items inside a flex row with fixed container height; stretch makes items fill the cross size.

---

## align-self
- Theory:
  - Overrides align-items for a single flex item.
  - Values: auto (inherit), flex-start, flex-end, center, baseline, stretch.
- Key point:
  - align-self takes precedence over container's align-items for that item.
- Example:
```html
<div class="flex-container">
  <div class="item">item1</div>
  <div class="item item2">item2</div>
  <div class="item">item3</div>
</div>
```
```css
.flex-container {
  display: flex;
  align-items: flex-start;
  height: 6em;
}
.item { border: 1px solid brown; padding: .5em; }
.item2 { align-self: flex-end; } /* this item aligns to bottom despite container's align-items */
```
- Explanation:
  - Container aligns items to the top (flex-start); item2 overrides and is aligned to the bottom (flex-end).

---

## align-content
- Theory:
  - Distributes free space between multiple flex lines along the cross axis (applies only when flex-wrap creates multiple lines and there's extra cross-axis space).
  - Similar values to justify-content (flex-start, center, space-between, space-around, etc.).
  - If there's only one line, align-content has no effect.
- Example:
```css
.grid {
  display: flex;
  flex-wrap: wrap;
  height: 20em;              /* give extra cross-axis space */
  align-content: space-between; /* try center / flex-start / space-around */
}
.grid > div { width: 8em; height: 4em; border: 1px solid #444; margin: 4px; }
```
- Explanation:
  - When items wrap into multiple rows, align-content: space-between spreads the rows vertically so the first row sits at the top and the last at the bottom with equal spacing between rows.

---

## Summary
- justify-content → distributes free space along the main axis (horizontal in row).
- align-items → aligns all items along the cross axis (vertical in row).
- align-self → per-item override of align-items.
- align-content → distributes free space between lines when there are multiple flex lines.
- Use combinations (and flex-wrap / heights) to control layout precisely without changing item sizes.

--- 

End of notes. If you want, I can:
- Produce compact bullet-only cheat-sheet version.
- Add visual ASCII diagrams for each value.
- Create short practice exercises with solutions.
