# Fetch API — Concepts with Code and Explanations

Short, practical lecture-style notes linking Fetch API theory to concise JavaScript examples. Emphasize theory and minimal, runnable code snippets with short explanations.

---

## Table of contents
- Overview
- Basic fetch flow (.then/.catch and async/await)
- Query parameters (URL / URLSearchParams)
- Request headers
- Methods and request body (POST/PUT/PATCH)
- Processing response (parsing and response properties)
- Error handling (network vs HTTP status)
- Best practices & tips
- Conclusion

---

## Overview

Theory
- The Fetch API provides a modern Promise-based interface to perform HTTP requests from the browser.
- `fetch()` returns a Promise that resolves to a Response object. The response body is a ReadableStream and must be parsed (e.g., `.json()`).
- Requests are asynchronous — other JS executes while waiting for the network.

---

## Basic fetch flow (.then/.catch and async/await)

Theory
- Two equivalent styles: Promise chaining (`.then/.catch`) and `async/await`.
- Common pattern: call `fetch(url, options)`, parse body (e.g., `response.json()`), then use data.

Example — Promise chaining:
```javascript
fetch("https://jsonplaceholder.typicode.com/users")
  .then(response => response.json())    // parse response body as JSON (returns Promise)
  .then(json => console.log(json))      // use the parsed data
  .catch(error => console.error(error)); // network or parsing errors
```

Example — async/await:
```javascript
async function fetchUsers() {
  try {
    const response = await fetch("https://jsonplaceholder.typicode.com/users");
    const data = await response.json();
    console.log(data);
  } catch (error) {
    console.error(error);
  }
}
```

Explanation
- `.json()` returns a Promise because body parsing is asynchronous.
- Use either style depending on readability and control-flow needs.

---

## Query parameters (URL / URLSearchParams)

Theory
- Attach query parameters to URLs with `?name=value&...` or use the `URL` API for safer composition.

Example — inline:
```javascript
fetch("https://api.example.com/items?_limit=10&page=3");
```

Example — URL object:
```javascript
const url = new URL("https://api.example.com/items");
url.searchParams.set("_limit", "10");
url.searchParams.set("page", "3");
fetch(url);
```

Explanation
- `URL` / `URLSearchParams` handle encoding and are safer than manual string concatenation.

---

## Request headers

Theory
- Headers send metadata (e.g., Authorization, Content-Type).
- Use a plain object in `fetch` options or the `Headers` class.

Example — Headers object:
```javascript
const authHeaders = new Headers();
authHeaders.set("Authorization", "Bearer ea1359...");
authHeaders.set("Accept", "application/json");

fetch("https://api.example.com/profile", { headers: authHeaders });
```

Example — plain object:
```javascript
fetch("https://api.example.com/profile", {
  headers: {
    "Authorization": "Bearer ea1359...",
    "Accept": "application/json"
  }
});
```

Explanation
- When sending JSON in the body, set `Content-Type: application/json`.

---

## Methods and request body (POST/PUT/PATCH)

Theory
- Use the `method` option for non-GET requests and `body` to send payloads.
- Commonly send JSON: `JSON.stringify()` the payload and set `Content-Type`.

Example — POST JSON:
```javascript
const requestBody = { name: "John", age: 16 };

fetch("https://jsonplaceholder.typicode.com/users", {
  method: "POST",
  headers: { "Content-Type": "application/json" },
  body: JSON.stringify(requestBody)
})
  .then(res => res.json())
  .then(data => console.log(data));
```

Explanation
- `body` must be a string, FormData, Blob, etc. For JSON, serialize with `JSON.stringify()`.

---

## Processing response (parsing and response properties)

Theory
- The Response object provides useful properties and body-parsing methods.
  - `status` — HTTP status code (e.g., 200).
  - `ok` — boolean for 2xx responses.
  - `statusText` — status message.
  - `headers` — Headers object.
  - `url` — final URL.
  - `bodyUsed` — whether body has been read.
- Parse body using `.json()`, `.text()`, `.blob()`, `.arrayBuffer()`, or `.formData()`.

Example — response properties:
```javascript
fetch("/resource")
  .then(response => {
    console.log(response.status, response.ok, response.headers.get("content-type"));
    return response.json();
  })
  .then(json => console.log(json));
```

Explanation
- Body parsing consumes the stream; if you need the data multiple times, clone the response (`response.clone()`).

---

## Error handling (network vs HTTP status)

Theory
- `fetch()` rejects only on network failure or if something prevents the request (it does NOT reject for non-2xx HTTP statuses).
- To treat non-2xx as errors, check `response.ok` or `response.status` and throw manually.

Example — throw on bad status (Promise chain):
```javascript
fetch("/users")
  .then(response => {
    if (!response.ok) throw new Error("Incorrect server response: " + response.status);
    return response.json();
  })
  .then(json => console.log(json))
  .catch(err => console.error(err.message));
```

Example — async/await with status check:
```javascript
async function fetchData() {
  try {
    const response = await fetch("/users");
    if (!response.ok) throw new Error(`HTTP ${response.status}`);
    const data = await response.json();
    console.log(data);
  } catch (err) {
    console.error(err.message);
  }
}
```

Explanation
- Distinguish between network-level errors (fetch Promise rejection) and application-level errors (HTTP status). Always validate `response.ok` when you expect success statuses.

---

## Best practices & tips

- Always set `Content-Type: application/json` when sending JSON bodies.
- Validate `response.ok` or check `status` ranges (e.g., 200–299) before parsing.
- Wrap `await fetch(...)` and parsing in `try/catch` to handle network and parse errors.
- Use `URL` / `URLSearchParams` instead of manual query-string building.
- Use `response.clone()` if you need to read the body multiple times (e.g., logging + parsing).
- Be cautious with remote fonts/CSP/hosting restrictions when fetching cross-origin resources — handle CORS and credentials:
  - `fetch(url, { credentials: "include" })` for cookies.
- When calling APIs that return streams or large files, prefer `.blob()` or streaming constructs.
- Consider timeouts (fetch has no built-in timeout; use `AbortController` to cancel slow requests).

Example — AbortController timeout:
```javascript
const controller = new AbortController();
const id = setTimeout(() => controller.abort(), 5000); // abort after 5s

try {
  const res = await fetch("/slow-endpoint", { signal: controller.signal });
  clearTimeout(id);
  const data = await res.json();
} catch (err) {
  if (err.name === "AbortError") console.error("Request timed out");
  else console.error(err);
}
```

---

## Conclusion

- Fetch is the modern Promise-based API for HTTP requests in the browser.
- Core steps: `fetch(url, options)` → check `response.ok`/`status` → parse body (`.json()`, `.text()`, …) → handle errors.
- Use `async/await` or `.then/.catch` consistently, set headers and body correctly for non-GET requests, and validate HTTP responses explicitly to avoid silent failures.
