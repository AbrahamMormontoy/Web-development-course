# Block‑Level Elements — Concepts with Code and Explanations

Short, lecture‑style notes that emphasize theory and concise HTML examples. Each section shows a core concept, a minimal code snippet, and a short explanation linking theory → code.

---

## Table of contents
- Overview
- Core characteristics
- Block vs inline (short note)
- Common block-level elements (examples + explanations)
  - div
  - p
  - h1–h6
  - ul / ol / li
  - table
  - section / article / header / footer
  - hr
- Inspecting layout (devtools tip)
- Structured page example (full HTML)
- Best practices
- Conclusion

---

## Overview

Theory
- Browsers parse HTML into elements and render them as rectangular boxes.
- Elements are broadly grouped into two categories: block‑level and inline.
- Block‑level elements define structural blocks on the page and are the primary building blocks for layout and document structure.

---

## Core characteristics

Theory
- New line start: a block element begins on a new line (creates vertical separation).
- Full‑width by default: it stretches to fill the available width of its parent container (unless width is constrained).
- Can contain other elements: block elements may contain inline elements and other block elements (nesting).
- Semantic meaning: many modern block elements convey semantics (e.g., `<header>`, `<article>`) which helps accessibility and SEO.

Practical note
- The displayed behavior (new line / full width) is the default; it can be changed with CSS (e.g., `display: inline`, `display: inline-block`, etc.).

---

## Block vs inline (short note)

Theory
- Inline elements flow inside a line and only take the width their content needs (e.g., `<span>`, `<a>`, `<strong>`).
- Block elements form vertical blocks and typically control layout and sections.

Quick example
```html
<div>This is a block element (starts on a new line).</div>
<span>This is inline</span><span> — still inline</span>
```

Explanation
- The `<div>` forces a line break before/after; two `<span>` elements sit on the same line.

---

## Common block-level elements

div — generic container
```html
<div>
  <h1>Heading inside a div</h1>
  <p>Paragraph inside the same div.</p>
</div>
```
Explanation
- `<div>` is a neutral container used to group content or apply styles/layout. It has no semantic meaning by itself.

p — paragraph
```html
<p>It's a paragraph of text.</p>
<p>And this is another paragraph.</p>
```
Explanation
- `<p>` represents a paragraph. Each `<p>` starts on a new line and creates vertical spacing by default.

h1–h6 — headings
```html
<h1>Heading level 1</h1>
<h2>Heading level 2</h2>
<!-- ... up to h6 -->
```
Explanation
- Heading elements define document structure and decrease in semantic importance from `h1` → `h6`.

ul / ol / li — lists
```html
<ul>
  <li>First item</li>
  <li>Second item</li>
</ul>

<ol>
  <li>First</li>
  <li>Second</li>
</ol>
```
Explanation
- Lists create grouped, semantic list structures. `<li>` is the list item and behaves as a block inside the list.

table — tabular data
```html
<table>
  <tr><th>Name</th><th>Age</th></tr>
  <tr><td>Ada</td><td>30</td></tr>
</table>
```
Explanation
- `<table>` and its children (`<tr>`, `<th>`, `<td>`) structure tabular data. Tables are block-level and typically expand to fit content.

section / article / header / footer — semantic sections
```html
<section>
  <h2>Section title</h2>
  <p>Section content…</p>
</section>

<article>
  <h3>Article title</h3>
  <p>Self-contained content</p>
</article>

<header>
  <h1>Site header</h1>
</header>

<footer>
  <p>Footer information</p>
</footer>
```
Explanation
- These semantic elements describe the role of content: sections, standalone articles, page header, and footer. Use them to improve document structure and accessibility.

hr — thematic break
```html
<p>Above the line</p>
<hr>
<p>Below the line</p>
```
Explanation
- `<hr>` inserts a horizontal rule (a thematic break between content). It's rendered as a block-level element.

---

## Inspecting layout (devtools tip)

Theory + Quick tip
- Open browser DevTools (Ctrl+Shift+I / Cmd+Opt+I) and hover elements to see the highlighted box model (content, padding, border, margin).
- This helps visualize how block elements occupy space and interact with neighbors.

---

## Structured page example (complete HTML)

Theory
- Combine block-level elements to create clear page structure: header, nav, content, footer.

Example — full HTML
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="utf-8" />
  <title>Structured Web Page</title>
</head>
<body>
  <header>
    <h1>Welcome to My Website</h1>
  </header>

  <nav>
    <ul>
      <li><a href="#home">Home</a></li>
      <li><a href="#about">About</a></li>
      <li><a href="#contact">Contact</a></li>
    </ul>
  </nav>

  <main>
    <section>
      <h2>Introduction</h2>
      <p>This is an example of a structured web page using block-level elements.</p>
    </section>

    <article>
      <h2>Article title</h2>
      <p>Self-contained piece of content.</p>
    </article>
  </main>

  <footer>
    <p>Website by Khan designs</p>
  </footer>
</body>
</html>
```

Explanation
- Each major page region is represented by a block-level semantic element (`header`, `nav`, `main`, `section`, `article`, `footer`) improving readability and maintainability.

---

## Best practices

Theory & practical guidance
- Prefer semantic block elements (`header`, `main`, `nav`, `section`, `article`, `footer`) over generic `<div>` where the meaning is clear.
- Use `<div>` when you need a non-semantic container for styling/layout only.
- Keep markup structured and nested logically — this helps CSS layout, accessibility (screen readers), and SEO.
- Use CSS (`display`) to change visual behavior when needed (e.g., `display:inline-block`, `display:flex`, `display:grid`) but keep semantic HTML intact.
- Avoid excessive div-nesting ("div soup"); prefer meaningful containers.

---

## Conclusion

- Block-level elements form the structural backbone of HTML documents.
- They start on a new line, typically fill available width, and can contain both block and inline elements.
- Use semantic block elements to create readable, maintainable, and accessible pages; use DevTools to inspect how blocks occupy space.

---

If you'd like, I can:
- produce a one‑page printable cheat‑sheet version;
- convert this into slide‑friendly bullets;
- add short in‑class exercises (with answers) such as "identify which elements should be semantic vs `<div>`" or "fix this broken structure".

Which would you prefer next?
