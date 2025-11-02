# HTML Forms — Concepts with Code and Explanations

Short, practical lecture-style notes linking HTML form theory to concise examples. Each section shows a core concept, a minimal HTML snippet, and a short explanation of what the code does and how it illustrates the theory.

---

## Table of contents
- Overview
- Creating forms
- Form attributes: action, method
- Input elements
  - Text fields
  - Password field
  - Radio buttons
  - Checkboxes
  - Buttons (submit)
- Label element
- Conclusion

---

## Overview

Theory
- Forms collect user data on a web page and send it to a server for processing.
- Typical uses: login, registration, purchases, sending messages.
- Form elements (inputs, labels, buttons) are placed inside the `<form>` tag.

---

## Creating forms

Theory
- Use the paired `<form>` tag. Input elements go inside it.
- Important attributes:
  - `action` — URL of the program/document that processes the form data.
  - `method` — HTTP method used to submit the form (`get` or `post`).

Example
```html
<!DOCTYPE html>
<html>
  <head><title>HTML Forms</title></head>
  <body>
    <form action="[value]" method="post">
       <!-- Input elements -->
    </form>
  </body>
</html>
```

Explanation
- The `<form>` wraps inputs and controls how and where data is sent. If `method` is omitted, `get` is used by default.

---

## Form attributes: action, method

Theory
- `action` specifies the server address that receives the form data.
- `method` controls how data is sent:
  - `get` — appends data to the URL (suitable for search forms).
  - `post` — sends data in the request body (suitable for large data, file uploads, database updates).

Explanation
- Choose `get` for requests that retrieve/search data and `post` when sending larger or sensitive payloads to the server.

---

## Input elements

Theory
- Input fields are created with the `<input>` tag (self-closing).
- The `name` attribute identifies the form field and is used when sending data to the server.
- Common input types: `text`, `password`, `radio`, `checkbox`, and buttons.

---

### Text fields

Example
```html
<form action="[value]" method="[value]">
  <p>First Name:</p>
  <input type="text" name="firstName">
  <p>Last Name:</p>
  <input type="text" name="lastName">
</form>
```

Explanation
- `type="text"` creates a single-line text input.
- The `name` attribute is required to identify the field in submitted data.
- Default width is 20 characters.

---

### Password field

Example
```html
<form action="[value]" method="[value]">
  <p>Password:</p>
  <input type="password" name="password">
</form>
```

Explanation
- `type="password"` masks entered characters (dots) to hide sensitive input from onlookers.

---

### Radio buttons

Example
```html
<form action="[value]" method="[value]">
  <input type="radio" name="language" value="english"> English
  <input type="radio" name="language" value="spanish"> Spanish
</form>
```

Explanation
- Radio buttons (same `name`) allow selecting exactly one option from a set.
- The `value` attribute supplies the value sent to the server when that option is chosen.

---

### Checkboxes

Example
```html
<form action="[value]" method="[value]">
  <input type="checkbox" name="technique" value="computer"> I have a computer
  <br>
  <input type="checkbox" name="technique" value="phone"> I have a phone
</form>
```

Explanation
- Checkboxes allow selecting any number of options.
- Use `<br>` (or CSS) to place checkboxes on separate lines if needed.
- Each checked checkbox sends its `name` and `value` to the server.

---

### Buttons (submit)

Example
```html
<form action="[value]" method="[value]">
  <button type="submit">Submit</button>
</form>
```

Explanation
- `<button type="submit">` sends the form data to the URL specified in `action` using the chosen `method`.
- Buttons are the primary way to trigger form submission.

---

## Label element

Theory
- `<label>` links descriptive text with a form control so clicking the text activates the control.
- Improves usability and accessibility.

Examples — implicit association
```html
<form action="[value]" method="[value]">
  <label><input type="radio" name="language" value="english"> English</label>
  <label><input type="radio" name="language" value="spanish"> Spanish</label>
</form>
```

Examples — explicit association using `for` and `id`
```html
<form action="[value]" method="[value]">
  <input id="english" type="radio" name="language" value="english">
  <label for="english">English</label>

  <input id="spanish" type="radio" name="language" value="spanish">
  <label for="spanish">Spanish</label>
</form>
```

Explanation
- Implicit `<label>` wraps the input and text; clicking either activates the input.
- Explicit `<label for="id">` links a label to an input elsewhere in the DOM via matching `id`.

---

## Conclusion

- Forms collect and transmit user input to a server; `<form>` with `action` and `method` controls submission.
- Use appropriate input `type` and `name` attributes to structure data sent to the server.
- `get` appends data to the URL (good for search), `post` sends data in the request body (good for larger or sensitive data).
- Use `<label>` to improve usability by linking text to form controls.
- Use `<button type="submit">` to trigger form submission.
