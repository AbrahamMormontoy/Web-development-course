# Audio Object — Concepts with Code and Explanations

Short, lecture‑style notes that emphasize theory and concise JavaScript/HTML examples. Each section shows a core concept, a minimal code snippet, and a short "Explain code" commentary linking theory → code.

---

## Table of contents
- Overview
- Creating an Audio object
- Accessing an existing `<audio>` element
- Important properties
- Useful methods
- Events & handling playback state
- Small example: simple player (JS + HTML)
- Notes, best practices, and gotchas
- Conclusion

---

## Overview

Theory
- The Audio object is the programmatic interface to HTML audio — it mirrors the `<audio>` element and allows scripts to control playback, inspect metadata, and react to playback events.
- You can create Audio elements with HTML or programmatically in JavaScript.
- Modern browsers enforce autoplay/user gesture policies and return Promises from `audio.play()`.

---

## Creating an Audio object

Theory
- Two common ways to create audio elements: via HTML markup or with JavaScript.

HTML (declarative)
```html
<audio id="myAudio" src="song.mp3" preload="metadata" controls></audio>
```
Explain code
- `<audio>` element in HTML with an id, source, `preload="metadata"` (fetches duration/metadata), and `controls` so the browser shows a native UI.

JavaScript — createElement
```javascript
let audio = document.createElement("audio");
audio.src = "path/to/song.mp3";
audio.preload = "metadata";
document.body.appendChild(audio);
```
Explain code
- Creates an `<audio>` element, sets its `src` and `preload`, and appends it to the document. You can further control and style it.

JavaScript — constructor shortcut
```javascript
let audio = new Audio("path/to/song.mp3");
```
Explain code
- `new Audio(src)` is a convenient shorthand to create an audio element with the provided source.

---

## Accessing an existing `<audio>` element

Theory
- Use standard DOM lookups to get a reference to an audio element created in HTML.

Example
```javascript
const audio = document.getElementById("myAudio");
console.log(audio.src); // absolute URL to the source
```
Explain code
- Retrieves the audio element with id `myAudio` and logs its resolved `src` attribute.

---

## Important properties

Theory
- Audio elements expose properties to read and change playback and metadata.

List and examples
```javascript
audio.src          // string — source URL
audio.currentTime  // number — current playback position in seconds (read/write)
audio.duration     // number — total duration in seconds (NaN until metadata loaded)
audio.paused       // boolean — true when not playing
audio.volume       // number 0.0..1.0
audio.muted        // boolean
audio.loop         // boolean — whether playback repeats
audio.playbackRate // number — speed (1.0 normal)
audio.paused       // boolean
audio.readyState   // number — loading/ready state
```
Explain code
- Use `currentTime` to seek, `duration` to show total time (available after metadata), `volume` to adjust loudness, and `playbackRate` to speed up or slow down playback.

---

## Useful methods

Theory
- Methods let you control playback and loading.

Examples
```javascript
audio.load();   // reloads source & starts loading (useful after changing .src)
audio.play();   // starts playback — returns a Promise in modern browsers
audio.pause();  // pauses playback
audio.pause();  // pause() doesn't return a Promise
```

Explain code
- `play()` may return a Promise that resolves when playback begins or rejects if browser blocks autoplay (or other errors). Always handle or ignore the Promise to avoid unhandled rejections.

Usage with Promise:
```javascript
audio.play()
  .catch(err => {
    console.warn("Playback failed:", err);
    // show play button or prompt user to interact
  });
```
Explain code
- Handling the Promise helps detect autoplay-blocking or other playback errors and lets you react (e.g., show a UI hint).

Other helpful methods/properties:
```javascript
audio.addTextTrack(kind, label); // captions/subtitles (advanced)
audio.cloneNode(true);           // clone audio element with attributes
```

---

## Events & handling playback state

Theory
- Audio elements fire many events: `loadedmetadata`, `canplay`, `timeupdate`, `ended`, `play`, `pause`, `error`, etc. Use them to update UI.

Common events:
- `loadedmetadata` — metadata (duration) available.
- `canplay` / `canplaythrough` — ready to start playback.
- `timeupdate` — currentTime changed; use to update progress bar.
- `ended` — playback finished.
- `play` / `pause` — playback started/paused.
- `error` — loading or decoding error.

Example — wiring events:
```javascript
audio.addEventListener("loadedmetadata", () => {
  console.log("Duration (s):", audio.duration);
});

audio.addEventListener("timeupdate", () => {
  // update a progress UI: fraction = audio.currentTime / audio.duration
  // but check if duration is finite
});

audio.addEventListener("ended", () => {
  console.log("Playback finished");
});
```
Explain code
- Use `loadedmetadata` to safely read `audio.duration`. `timeupdate` fires periodically while playing to update progress indicators.

---

## Small example: simple player (HTML + JS)

HTML:
```html
<div id="player">
  <button id="playBtn">Play</button>
  <span id="time">0:00 / 0:00</span>
  <input id="seek" type="range" min="0" max="100" value="0">
</div>
<audio id="a" src="song.mp3" preload="metadata"></audio>
```

JavaScript:
```javascript
const audio = document.getElementById("a");
const playBtn = document.getElementById("playBtn");
const timeLabel = document.getElementById("time");
const seek = document.getElementById("seek");

playBtn.addEventListener("click", async () => {
  try {
    if (audio.paused) {
      await audio.play(); // handle promise
      playBtn.textContent = "Pause";
    } else {
      audio.pause();
      playBtn.textContent = "Play";
    }
  } catch (err) {
    console.error("Play failed:", err);
  }
});

audio.addEventListener("loadedmetadata", () => {
  seek.max = Math.floor(audio.duration);
  updateTime();
});

audio.addEventListener("timeupdate", updateTime);

seek.addEventListener("input", () => {
  audio.currentTime = seek.value;
});

function updateTime() {
  const cur = formatTime(audio.currentTime);
  const dur = isFinite(audio.duration) ? formatTime(audio.duration) : "0:00";
  timeLabel.textContent = `${cur} / ${dur}`;
  if (isFinite(audio.duration)) seek.value = Math.floor(audio.currentTime);
}

function formatTime(seconds = 0) {
  const s = Math.floor(seconds % 60).toString().padStart(2, "0");
  const m = Math.floor(seconds / 60);
  return `${m}:${s}`;
}
```
Explain code
- Small UI toggles playback, displays time, updates a seek slider, and safely handles `play()`'s Promise. `loadedmetadata` sets the seek range when duration becomes available.

---

## Notes, best practices, and gotchas

- Autoplay restrictions: Many browsers block autoplay with sound until the user interacts with the page. Use `muted` for silent autoplay or wait for a user gesture.
- `audio.play()` returns a Promise — always handle rejection to avoid unhandled promise rejections.
- `duration` is `NaN` until metadata loads; use `loadedmetadata` to read it safely.
- Use `audio.preload = "metadata"` if you only need duration without preloading full audio.
- Respect bandwidth: avoid preloading many large audio files simultaneously.
- Use `audio.crossOrigin` when fetching cross-origin media and serving with appropriate CORS headers.
- For accessibility, pair audio controls with keyboard focus and labels; prefer native `controls` when appropriate.

---

## Conclusion

- The Audio object (and `<audio>` element) let you embed and control audio in web pages programmatically.
- Create audio elements in HTML or JS (`new Audio()` / `createElement("audio")`), control them with properties/methods (`src`, `currentTime`, `play()`, `pause()`), and respond to events (`loadedmetadata`, `timeupdate`, `ended`).
- Handle `play()`'s Promise and browser autoplay policies, and use events to build robust, user-friendly players.

---

If you want, I can:
- convert this into a one‑page printable cheat‑sheet,
- add a more advanced example (playlist, volume control, keyboard shortcuts),
- or produce a short exercise with a solution (implement a seekable player or a small playlist).

Which would you like next?