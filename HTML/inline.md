# Inline Elements — Concepts with Code and Explanations

Short, lecture‑style notes that emphasize theory and concise HTML examples. Follow the same format as your class sources: present the theory first, then minimal code snippets with a short "Explain code" commentary that links the code to the theory.

---

## Table of contents
- Overview
- Key characteristics of inline elements
- Common inline elements (examples + explanations)
  - a (anchor)
  - span
  - button
  - b (bold)
  - sub (subscript)
  - sup (superscript)
- Inline vs block — quick comparison
- Rules and restrictions
- Accessibility & semantics notes
- Small examples and patterns
- Conclusion

---

## Overview

Theory
- Inline elements participate in the flow of text: they occupy only as much width as their content and do not start a new line.
- They are used to mark up parts of a line (phrasing content), apply styling, or provide behavior (links, buttons).
- Inline elements may be nested inside block elements and other inline elements, but they must not contain block-level elements.

---

## Key characteristics of inline elements

Theory
- Stay in the same text line; the browser does not insert line breaks before or after by default.
- Width and height are determined by content and surrounding layout (CSS width/height often ignored or behaves differently).
- Can contain text and other inline (phrasing) elements, but not block-level elements.
- Useful for semantic markup and small UI controls within text.

Practical note
- CSS can change display behavior (e.g., `display: inline-block`, `display: block`) but keep semantics clear: don't use inline elements only to force layout when a block or semantic element makes more sense.

---

## Common inline elements

a — anchor (link)

```html
<a href="https://jetbrains.com">Click here to access the JetBrains website!</a>
```
Explain code
- `<a>` creates a hyperlink; `href` specifies the destination. The annotated text becomes clickable and normally styled (underline, color). It remains inline with surrounding text.

span — generic inline container

```html
<p>For the first time <span class="highlight">on our site</span>?</p>
<span class="cta">Sign up now!</span>
```
Explain code
- `<span>` has no semantic meaning and is used to wrap text for styling or scripting. Use classes/IDs + CSS to style or select the span.

button — clickable control

```html
<button type="button">Click</button>
```
Explain code
- `<button>` renders an inline control that reacts to clicks. By default it is inline (but can behave like inline-block depending on browser/CSS). Use `type` to control behavior (`button`, `submit`, `reset`).

b — presentational bold

```html
<p>I'm <b>John Doe</b>, and what's your name?</p>
```
Explain code
- `<b>` is an inline element that renders text in bold. Prefer semantic alternatives (e.g., `<strong>`) when the bolding implies importance, but use `<b>` for purely stylistic bolding.

sub — subscript

```html
<p>The formula of water is H<sub>2</sub>O.</p>
```
Explain code
- `<sub>` renders its content as subscript (smaller and lowered). Useful for chemical formulas, footnote markers, etc.

sup — superscript

```html
<p>x<sup>2</sup> = 4</p>
```
Explain code
- `<sup>` renders its content as superscript (raised and smaller). Useful for exponents, ordinal indicators (1<sup>st</sup>), and footnote markers.

---

## Inline vs block — quick comparison

Theory
- Inline: flows inside lines, content-sized, cannot contain block-level elements.
- Block-level: starts on a new line, expands to container width by default, can contain inline and block elements.

Example (visual difference):
```html
<div>Block element (new line)</div>
<span>Inline element</span><span> — continues on same line</span>
```
Explain code
- The `<div>` forces a line break. The two `<span>` elements sit on the same line unless the line wraps.

---

## Rules and restrictions

Theory & rules
- Inline elements must not contain block-level elements (e.g., avoid `<span><div>…</div></span>`).
- CSS can alter display modes (e.g., `display:inline-block` gives inline layout with box dimensions) but does not change the element's semantic role.
- Top/bottom margins and heights behave differently on inline elements; prefer `inline-block` or block elements if you need consistent box-model behavior.

Practical tip
- If you need to size or vertically align a piece of inline UI (e.g., icon buttons), `display: inline-block` is often the right compromise.

---

## Accessibility & semantics notes

Theory
- Choose semantic elements when possible: `<a>` for links, `<button>` for actions, `<strong>/<em>` for emphasis — these convey meaning to assistive tech.
- Use `aria-*` attributes when necessary to clarify roles or states for custom inline widgets (e.g., `role="button"` + keyboard handlers if using non-button elements).
- Avoid repurposing `<span>` for interactive controls without adding proper accessibility (keyboard, focus, role, state).

Example — accessible custom control (bad -> good):
```html
<!-- Bad: clickable span with no role/keyboard support -->
<span class="play">Play</span>

<!-- Better: real button -->
<button class="play">Play</button>
```
Explain code
- Use native interactive elements (`<button>`, `<a>`) so the browser and assistive technologies get built-in behavior (keyboard, focus, semantics).

---

## Small examples and patterns

Inline styling with CSS class:
```html
<style>
  .highlight { background: yellow; }
  .inline-box { display: inline-block; padding: 0.2em 0.4em; border-radius: 3px; }
</style>

<p>Please read the <span class="highlight">important</span> note.</p>
<span class="inline-box">Badge</span>
```
Explain code
- `highlight` uses a `<span>` to style part of a sentence.
- `inline-box` uses `inline-block` to allow padding/width while staying in the text flow.

Semantic emphasis:
```html
<p>This is <strong>important</strong> and this is <em>emphasized</em>.</p>
```
Explain code
- Use `<strong>` and `<em>` for semantic emphasis rather than purely visual tags like `<b>` or `<i>` when the meaning matters for accessibility and SEO.

Using anchors for navigation:
```html
<a href="#section2">Jump to section 2</a>
...
<section id="section2">...</section>
```
Explain code
- Anchors can link to in-page IDs for quick navigation. They remain inline and are part of the text flow.

---

## Conclusion

- Inline elements are ideal for marking and styling fragments of text and for small interactive controls placed inside text.
- Prefer semantic elements (`<a>`, `<button>`, `<strong>`, `<em>`) to convey meaning and help accessibility.
- When layout or sizing is required, switch to `display:inline-block` or a block-level element, but keep semantics consistent.
- Use devtools to inspect box model behavior and ensure your inline choices match both presentation and accessibility goals.

---

If you want, I can:
- convert this into a one‑page printable cheat‑sheet,
- add short exercises with solutions (e.g., fix malformed nesting, replace non-semantic controls with accessible elements),
- or produce slide‑friendly bullets for teaching.

Which would you like next?
