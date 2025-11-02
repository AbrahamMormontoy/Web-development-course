# async / await — Concepts with Code and Explanations

Short, practical lecture‑style notes that emphasize theory and concise JavaScript examples. Each section shows the core concept, a minimal code snippet, and a short explanation linking theory → code. Follow the same format as your class sources: emphasize theory and show code with brief "Explain code" commentary.

---

## Table of contents
- Overview
- The async function
- The await operator
- Error handling with try / catch / finally
- Sequential vs parallel awaits
- Returning and consuming async functions
- Converting promise chains to async/await
- Common pitfalls and best practices
- Conclusion

---

## Overview

Theory
- `async` / `await` (ES2017) are syntactic sugar over Promises that make asynchronous code read like synchronous code.
- An `async` function always returns a Promise:
  - If the function returns a value, the returned Promise resolves with that value.
  - If the function throws, the returned Promise rejects with that error.
- `await` pauses execution of an `async` function until the awaited Promise settles (resolves or rejects). `await` can only be used inside `async` functions (or top-level in modern environments that support top-level await).

---

## The async function

Theory
- Mark a function with `async` to make it return a Promise implicitly.
- Useful for composing asynchronous operations and using `await` inside.

Example
```javascript
async function greet() {
  return "Hello, Async!";
}

console.log(greet()); // Promise { "Hello, Async!" }
```
Explain code
- `greet()` is an `async` function that returns a resolved Promise with value `"Hello, Async!"`. You can `.then()` it or `await` it.

Consuming the returned promise:
```javascript
greet().then(value => console.log(value)).catch(err => console.error(err));
// Hello, Async!
```
Explain code
- `.then()` receives the resolved value. Errors inside `greet` would be caught by `.catch()`.

---

## The await operator

Theory
- Use `await` before a Promise to pause execution until it resolves and return the resolved value (or throw if the Promise rejects).
- Makes asynchronous code look linear and easier to reason about.

Example (fetch JSON):
```javascript
async function fetchPosts() {
  const response = await fetch("https://jsonplaceholder.typicode.com/posts");
  const data = await response.json();
  return data;
}
```
Explain code
- `await fetch(...)` waits for the network request to complete; `await response.json()` waits for body parsing. `fetchPosts()` returns a Promise resolving with parsed JSON.

---

## Error handling with try / catch / finally

Theory
- Use `try { await ... } catch (err) { ... }` inside `async` functions for error handling — clearer than `.then/.catch` chains.
- `finally` runs whether the `try` succeeded or `catch` ran — useful for cleanup (stop spinner, close resources).

Example
```javascript
async function findUser(id) {
  try {
    const res = await fetch(`https://api.example.com/users/${id}`);
    if (!res.ok) throw new Error(`HTTP ${res.status}`);
    const user = await res.json();
    return user;
  } catch (err) {
    console.error("Failed to fetch user:", err.message);
    throw err; // rethrow if caller should handle it
  } finally {
    console.log("Request finished (success or failure)");
  }
}
```
Explain code
- Checks `res.ok` to treat non‑2xx status as error; `catch` handles network or thrown errors; `finally` always runs.

---

## Sequential vs parallel awaits

Theory
- Awaiting promises sequentially waits for each to finish before starting the next → slower if operations are independent.
- To run independent async tasks in parallel, start them without `await`, collect Promises, then `await` `Promise.all()`.

Sequential (slower):
```javascript
async function getAllSequential() {
  const a = await fetch("/a").then(r => r.json());
  const b = await fetch("/b").then(r => r.json());
  return [a, b];
}
```
Explain code
- `fetch("/b")` does not start until `/a` has completed and parsed — unnecessary serialization if requests are independent.

Parallel (faster):
```javascript
async function getAllParallel() {
  const pa = fetch("/a").then(r => r.json());
  const pb = fetch("/b").then(r => r.json());
  const [a, b] = await Promise.all([pa, pb]);
  return [a, b];
}
```
Explain code
- Both fetches start immediately. `Promise.all` waits until both resolve (or rejects fast if one fails).

Note: use `Promise.allSettled` if you want results even when some fail.

---

## Returning and consuming async functions

Theory
- An `async` function returns a Promise; callers may `await` it or use `.then/.catch`.
- You can `return` values normally inside `async` functions or `throw` to reject.

Example (caller):
```javascript
async function main() {
  try {
    const posts = await fetchPosts();
    console.log(posts.length);
  } catch (err) {
    console.error("Error in main:", err);
  }
}
main(); // run the async main
```
Explain code
- `main()` uses `await` to get `fetchPosts()` result and handles errors with `try/catch`.

---

## Converting promise chains to async/await

Theory
- Replace nested `.then()` chains with `await` to make flow linear and easier to read.

Promise chain:
```javascript
fetch("/token")
  .then(r => r.json())
  .then(t => fetch("/data", { headers: { Authorization: t.token } }))
  .then(r => r.json())
  .then(data => console.log(data))
  .catch(e => console.error(e));
```

Async/await equivalent:
```javascript
async function loadData() {
  try {
    const tokenRes = await fetch("/token");
    const token = await tokenRes.json();
    const dataRes = await fetch("/data", { headers: { Authorization: token.token } });
    const data = await dataRes.json();
    console.log(data);
  } catch (e) {
    console.error(e);
  }
}
```
Explain code
- Same logic expressed sequentially; easier to read, easier to add `try/catch` for error handling.

---

## Common pitfalls and best practices

1. Top-level await
   - Modern environments allow top-level `await` (modules). In other contexts, wrap code in an `async` IIFE:
   ```javascript
   (async () => {
     await doSomething();
   })();
   ```

2. Forgetting to check HTTP status
   - `fetch` resolves for non-2xx responses. Always check `response.ok` or `response.status` before parsing.

3. Not running independent tasks in parallel
   - Start promises first, then `await Promise.all(...)` for independent tasks.

4. Unhandled rejections
   - Always `await` Promises or attach `.catch()`; otherwise Node/browser may show unhandled rejection warnings.

5. Avoid `await` in loops when not necessary
   ```javascript
   // Bad: sequential
   for (const id of ids) {
     await process(id);
   }
   // Better: parallel
   await Promise.all(ids.map(id => process(id)));
   ```

6. Resource cleanup
   - Use `finally` to stop spinners or free resources regardless of success/failure.

7. Timeouts and cancellation
   - Native `fetch` has no built-in timeout; use `AbortController` to cancel slow requests.

   Example: timeout with AbortController
   ```javascript
   async function fetchWithTimeout(url, ms = 5000) {
     const controller = new AbortController();
     const id = setTimeout(() => controller.abort(), ms);
     try {
       const res = await fetch(url, { signal: controller.signal });
       return await res.json();
     } finally {
       clearTimeout(id);
     }
   }
   ```
   Explain code
   - `AbortController` aborts the fetch after `ms` milliseconds. `finally` clears the timeout.

8. Error semantics: network vs application errors
   - `fetch` network failure → rejected Promise.
   - HTTP errors (404, 500) → resolved Promise with `res.ok === false`. Decide how to handle (throw on bad status).

9. Use `Promise.allSettled` when you need all results regardless of individual failures:
   ```javascript
   const results = await Promise.allSettled(promises);
   results.forEach(r => {
     if (r.status === "fulfilled") use(r.value);
     else console.error("Failed:", r.reason);
   });
   ```

10. Avoid mixing paradigms carelessly
    - Prefer consistent style: either `async/await` or `.then/.catch` in a function/module for clarity.

---

## Conclusion

- `async` / `await` improve readability and error handling in asynchronous JavaScript by making code appear synchronous while remaining non‑blocking.
- Use `try/catch/finally` for clear error handling and cleanup.
- Run independent async operations in parallel with `Promise.all` (or `allSettled`) instead of awaiting each sequentially.
- Check HTTP responses (`res.ok`) before parsing, handle timeouts/cancellation with `AbortController`, and avoid unhandled rejections.
- Prefer `async/await` for control flow and `.then` for simple single-expression chains or library interop when needed.

---

If you'd like, I can:
- convert this into a one‑page printable cheat sheet,
- add short practice exercises with solutions (e.g., refactor promise chain to async/await; implement parallel fetch with error handling),
- produce slide‑friendly bullets, or
- generate concrete examples using `AbortController`, `Promise.allSettled`, and error-wrapping utilities.

Which would you like next?
