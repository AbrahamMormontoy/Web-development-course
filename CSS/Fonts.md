# Fonts — Concepts with Code and Explanations

Short, practical lecture-style notes linking font theory to concise HTML/CSS examples. Emphasize theory and minimal code.

---

## Table of contents
- Fonts (what is a font)
- External fonts (@import)
- @font-face (local font files)
- Multiple fonts (weights/styles)
- Fallback fonts
- Technical details
- Conclusion

---

## Fonts (what is a font)

Theory
- A font is more than letter appearance: it includes style, weight, and size.
- Examples of font components:
  - font-weight — values: bold / bolder / lighter or 100, 200, ..., 900.
  - font-size — sets the size.
  - font-stretch — stretches the glyphs (not letter spacing).
  - font-family — picks a font (system or external).
- CSS can use fonts installed on the OS; prefer widely available fonts for compatibility.

Example
```css
.block {
  font-weight: 700;
  font-size: 16px;
  font-stretch: normal;
  font-family: Arial, sans-serif;
}
```

Explanation
- Combine weight, size and family to define the concrete font used for rendering.

---

## External fonts (@import)

Theory
- Use an external service (e.g., Google Fonts) and import the font into your CSS with @import.
- This is convenient but can cause performance overhead (font file weight and loading delay).

Example
```css
@import url('https://fonts.googleapis.com/css2?family=Montserrat&display=swap');
.block{
  font-family: 'Montserrat', sans-serif;
}
```

Explanation
- The example connects Montserrat from Google Fonts and uses it as the font-family for .block.
- Note: there may be a visible gap or fallback rendering until the external font loads.

---

## @font-face (local font files)

Theory
- Use @font-face to add a font from a file in your project (e.g., .OTF, .TTF).
- @font-face defines font-family, src (path to file), and optional font-stretch, font-weight, font-style.
- Put @font-face at the start of the CSS file. You cannot place @font-face inside a selector.

Syntax
```css
@font-face {
  font-family: <family-name>;
  src: <src>;
  font-stretch: <font-stretch>;
  font-weight: <font-weight>;
  font-style: <font-style>;
}
```

Example (local file)
```html
<div class="block">
  <p>This is Montserrat</p>
</div>
```
```css
@font-face {
  font-family: the-best-font;
  src: url('montserrat-400.OTF');
  font-stretch: normal;
  font-weight: 400;
  font-style: normal;
}

.block {
  font-family: the-best-font;
}
```

Explanation
- The @font-face rule creates a named font ("the-best-font") from the montserrat-400.OTF file and .block uses it.

---

## Multiple fonts (weights/styles)

Theory
- CSS needs separate font files for different weights or styles (bold, italic); add multiple @font-face rules using the same font-family name but different font-weight/font-style values.

Example
```css
@font-face {
  font-family: the-best-font;
  src: url('montserrat-400.OTF');
  font-stretch: normal;
  font-weight: 400;
  font-style: normal;
}

@font-face {
  font-family: the-best-font;
  src: url('montserrat-bold.OTF');
  font-stretch: normal;
  font-weight: bold;
  font-style: normal;
}

.block {
  font-family: the-best-font;
  font-weight: bold;
}
```

Explanation
- Two files are registered under the same family with different weights so font-weight: bold selects the bold file.

---

## Fallback fonts

Theory
- A user may not have a font or a font file may be missing; list multiple font names as fallbacks in font-family.
- End with a generic family (serif / sans-serif / monospace) to ensure a similar font is used.

Example
```css
.block {
  font-family: the-best-font-ever, Courier, Arial, sans-serif;
}
```

Explanation
- If the-best-font-ever is unavailable, the browser tries Courier, then Arial, then any sans-serif.

---

## Technical details

Theory & Notes
- @import: convenient for linking remote font services (e.g., Google Fonts).
- @font-face: best for local font files; put it at the beginning of your CSS for performance.
- Some hosting/publishing setups may block remote font resources when used via src in @font-face — prefer @import for remote links and @font-face for local files.
- Do not place @font-face inside a selector.

Incorrect example (do not use)
```css
.block {
  @font-face {
    font-family: the-best-font;
    src: url('montserrat-400.OTF');
    font-stretch: normal;
    font-weight: bold;
    font-style: normal;
  }
  font-family: the-best-font;
  font-weight: bold;
}
```

Explanation
- @font-face must be at top-level in CSS, not nested inside selectors.

---

## Conclusion

- Three common scenarios:
  - Use default system fonts.
  - Use Google Fonts (or other services) via @import.
  - Use local font files via @font-face.
- Place @import and @font-face at the start of CSS for better performance.
- Provide fallback font names in font-family to handle missing fonts.
