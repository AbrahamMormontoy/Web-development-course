# forEach — Concise Cheatsheet (Theory + Code)

- Short notes linking forEach theory to minimal JS examples.
- Emphasize sequential processing, callback parameters, and thisArg.

---

## Table of contents
- What is forEach
- Syntax
- Examples
- Conclusion

---

## What is forEach
- Purpose:
  - Perform the same action for each array element without manual indexing.
- Example (manual indexing):
```javascript
const arrayNames = ["Mike", "Alex", "Asya"];
console.log(arrayNames[0]);
console.log(arrayNames[1]);
```
- Use for arrays of unknown or large length:
```javascript
arrayNames.forEach(function(element) {
  console.log(element);
});
```
- Notes:
  - Outputs "Mike", then "Alex", then "Asya".
  - Processes elements sequentially; each element handled before moving on.
  - Skips deleted or uninitialized elements (e.g., ["Mike", , "Asya"] shows "Mike" and "Asya").

---

## Syntax
- Signature:
```javascript
forEach(callback, thisArg);
```
- callback parameters:
  - currentValue — element being processed.
  - index — index of currentValue.
  - array — the array being iterated.
- thisArg:
  - Value used as this inside callback.
- Example:
```javascript
const arrayFruit = ["pineapples", "oranges", "apples"];
arrayFruit.forEach(function(value) {
  console.log("Today I ate " + value);
});
```
- Result:
  - "Today I ate pineapples"
  - "Today I ate oranges"
  - "Today I ate apples"

---

## Examples
- Named callback:
```javascript
function showText(value) {
  console.log("Today I eat " + value);
}
arrayFruit.forEach(showText);
```
- Using index and array:
```javascript
function showItem(item, index, array) {
  console.log("My value is " + item + ". I’m the " + index + " element of array " + array);
}
arrayFruit.forEach(showItem);
```
- Example output:
  - "My value is pineapples. I'm the 0 element of array pineapples,oranges,apples"
  - "My value is oranges. I'm the 1 element of array pineapples,oranges,apples"
  - "My value is apples. I'm the 2 element of array pineapples,oranges,apples"
- Custom this:
```javascript
const customThis = { value: 10 };

function showThisValue() {
  console.log(this.value);
}

arrayFruit.forEach(showThisValue, customThis);
```
- Result: 10

---

## Conclusion
- forEach:
  - Iterates sequentially over array elements.
  - Uses a callback with (value, index, array).
  - Accepts a thisArg to set this in the callback.
- Good for applying the same operation to every element; skips holes in sparse arrays.
