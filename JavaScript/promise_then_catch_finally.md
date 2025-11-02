# Promise Methods — .then, .catch, .finally, and Chaining (Concepts with Code and Explanations)

Short, practical lecture‑style notes that emphasize theory and concise JavaScript examples. Each section shows a core concept, a minimal code snippet, and a short explanation of what the code does and how it illustrates the theory.

---

## Table of contents
- Overview
- .then
  - two-argument form
  - returned value / chaining
- .catch
- .finally
- Promise chaining (sequential steps)
- Important notes & best practices
- Quick examples
- Conclusion

---

## Overview

Theory
- A Promise represents a value that may be available now, later, or never.
- After a Promise settles it is either fulfilled (resolved) or rejected.
- Handlers:
  - `.then(onFulfilled, onRejected)` — register success and/or failure handlers.
  - `.catch(onRejected)` — register failure handler (equivalent to `.then(null, onRejected)`).
  - `.finally(onFinally)` — run cleanup regardless of outcome; does not receive the value.
- `.then`, `.catch`, and `.finally` return new Promises — enabling composition and chaining.

---

## .then

Theory
- `.then()` attaches callbacks for fulfillment and (optionally) rejection.
- Both handlers are optional; `.then` always returns a new Promise whose result depends on the handler return:
  - Returning a plain value resolves the next promise with that value.
  - Returning a Promise makes the next promise adopt its state (wait for it).
  - Throwing or returning a rejected Promise rejects the next promise.

Example — exam date promise:
```javascript
const examDate = new Date(2020, 7, 5);
const promise = new Promise(function(resolve, reject) {
  const currentDate = new Date();
  if (currentDate < examDate) {
    resolve("You should prepare for the exam");
  } else {
    reject("Oops! You have missed your exam!");
  }
});
```
Explain code
- Creates a Promise that resolves with a reminder if the current date is before `examDate`, otherwise rejects with an error message.

.then with two handlers:
```javascript
promise.then(
  function successStatus(response) {
    console.log(response);
    return response;
  },
  function failStatus(error) {
    console.log(error);
    return error;
  }
);
```
Explain code
- First callback handles success, second handles failure. Each returns a value that becomes the resolution for the Promise returned by `.then`.

Chaining by returning values:
```javascript
Promise.resolve(2)
  .then(x => x * 3)             // returns 6
  .then(y => `Result: ${y}`)    // returns "Result: 6"
  .then(console.log);           // logs "Result: 6"
```
Explain code
- Each `.then` receives the previous result; returning a value passes it down the chain.

---

## .catch

Theory
- `.catch(onRejected)` registers a rejection handler for the chain.
- It is equivalent to `.then(null, onRejected)` but preferred because it captures errors thrown anywhere earlier in the chain.
- Use `.catch` to centralize error handling for a sequence of asynchronous steps.

Example:
```javascript
promise.catch(function failStatus(error) {
  console.log(error);
  return error;
});
```
Explain code
- Logs the rejection reason if the promise rejects. If the `.then` above threw an error, this `.catch` would catch it as well.

Combined `.then` + `.catch`:
```javascript
promise
  .then(function successStatus(response) {
    console.log(response);
    return response;
  })
  .catch(function failStatus(error) {
    console.log(error);
    return error;
  });
```
Explain code
- `.catch` handles any rejection from the original promise or errors thrown inside the `.then` handlers.

---

## .finally

Theory
- `.finally(onFinally)` runs after the promise settles (fulfilled or rejected).
- The `onFinally` callback receives no arguments and should be used for cleanup tasks (e.g., hide spinner).
- The original resolved value or rejection reason is forwarded to the next handler unless `finally` throws or returns a rejected Promise.

Example:
```javascript
promise
  .then(response => { console.log(response); return response; })
  .catch(error => { console.log(error); return error; })
  .finally(() => { console.log("The loader has stopped"); });
```
Explain code
- `"The loader has stopped"` is logged regardless of success/failure. The chain's final result remains the original resolution/rejection (unless `finally` throws).

Caveat — throwing in finally:
```javascript
Promise.resolve("ok")
  .finally(() => { throw new Error("boom"); })
  .then(v => console.log("won't run"))
  .catch(e => console.error("caught:", e.message)); // "caught: boom"
```
Explain code
- If `finally` throws, that error overrides the previous outcome and causes the chain to reject.

---

## Promise chaining (sequential steps)

Theory
- Return a Promise from each `.then` so the next step waits for it — this enforces sequential execution.
- If any step rejects (and the rejection isn't handled), the chain short-circuits to the nearest `.catch`.

Sequential loading example:
```javascript
loadData("https://mywebsite.com/loadRoles")
  .then(function() {
    return loadData("https://mywebsite.com/loadUserInfo");
  })
  .then(function(user) {
    return loadData(`https://mywebsite.com/loadBanner_${user.id}`);
  })
  .catch(function(error) {
    console.log("Oops! An error occured!");
  });
```
Explain code
- Each `loadData` must return a Promise. Returning the next Promise in `.then` causes the chain to wait for it. `.catch` catches errors from any step.

Important
- Forgetting to `return` a Promise in a `.then` will break the sequencing — the next `.then` will run immediately instead of waiting.

---

## Important notes & best practices

- Always `return` values or Promises from `.then` handlers when you expect the chain to wait or pass results.
- Prefer `.catch` at the end of a chain to handle errors from any earlier step, unless you need per-step recovery.
- Use `.finally` for cleanup tasks (stop loaders, hide progress bars). Avoid throwing inside `finally`.
- For independent asynchronous tasks run them in parallel with `Promise.all` (or `Promise.allSettled`) instead of chaining sequentially.
- When using `async/await`, the same rules apply: `await` pauses until the Promise resolves; use `try/catch/finally` for error handling and cleanup.

---

## Quick examples

1) then-only:
```javascript
fetch("/data")
  .then(res => res.json())
  .then(data => console.log("Data:", data));
```

2) then + catch (check HTTP status):
```javascript
fetch("/data")
  .then(res => {
    if (!res.ok) throw new Error(res.status);
    return res.json();
  })
  .then(data => console.log(data))
  .catch(err => console.error("Fetch failed:", err));
```

3) finally to stop a loader:
```javascript
showLoader();
fetch("/data")
  .then(r => r.json())
  .catch(err => console.error(err))
  .finally(() => hideLoader()); // always hide loader
```

4) chaining with dependent promises:
```javascript
authenticate()
  .then(token => fetch("/profile", { headers: { Authorization: token } }))
  .then(r => r.json())
  .then(profile => renderProfile(profile))
  .catch(err => showError(err));
```

---

## Conclusion

- `.then` handles fulfillment and can optionally handle rejection (two-arg form); it returns a new Promise enabling chaining.
- `.catch` is the canonical way to handle rejections and errors from earlier handlers.
- `.finally` is for unconditional cleanup after settlement and forwards the original outcome unless it itself throws.
- For sequential dependent operations return Promises inside `.then`; for independent operations use parallel composition.
- Use `async/await` for clearer control flow but remember error propagation and the same Promise semantics apply.

---

If you want, I can:
- convert this into a one‑page printable cheat‑sheet,
- add short exercises (e.g., refactor a promise chain to async/await; fix a broken chain),
- or provide slide‑friendly bullets for each section.

Which would you like next?
