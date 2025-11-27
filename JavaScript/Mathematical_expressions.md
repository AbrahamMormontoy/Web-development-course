# Mathematical Expressions — JavaScript Examples

- Practical examples of evaluating mathematical expressions in JavaScript.
- Demonstrates arithmetic operators and comparison for polynomial expressions.

---

## Table of contents
- Evaluating Polynomial Expressions
- Comparing Expressions: x³ + x + 3 > x⁵
- Conclusion

---

## Evaluating Polynomial Expressions
- Theory:
  - JavaScript uses `**` for exponentiation (e.g., `x ** 3` for x³).
  - Arithmetic operators: `+`, `-`, `*`, `/`, `**`, `%`.
- Example:
```javascript
function evaluatePolynomial(x) {
  return x ** 3 + x + 3;
}

console.log(evaluatePolynomial(2)); // 8 + 2 + 3 = 13
console.log(evaluatePolynomial(0)); // 0 + 0 + 3 = 3
```

---

## Comparing Expressions: x³ + x + 3 > x⁵
- Question: Is x³ + x + 3 > x⁵ possible?
- Answer: **Yes, it is possible** for certain values of x.
- Example:
```javascript
function isInequalityTrue(x) {
  const left = x ** 3 + x + 3;
  const right = x ** 5;
  return left > right;
}

// Testing various values
console.log(isInequalityTrue(0));   // true: 3 > 0
console.log(isInequalityTrue(1));   // true: 5 > 1
console.log(isInequalityTrue(1.5)); // true: 7.875 > 7.594
console.log(isInequalityTrue(2));   // false: 13 < 32
```
- Explanation:
  - When x = 0: 0³ + 0 + 3 = 3, and 0⁵ = 0; since 3 > 0, the inequality holds.
  - When x = 1: 1³ + 1 + 3 = 5, and 1⁵ = 1; since 5 > 1, the inequality holds.
  - When x = 1.5: 3.375 + 1.5 + 3 = 7.875, and 1.5⁵ = 7.59375; since 7.875 > 7.59375, the inequality holds.
  - When x = 2: 8 + 2 + 3 = 13, and 2⁵ = 32; since 13 < 32, the inequality does not hold.
- Note: The inequality is true for values roughly in the range (-∞, ~1.53).

---

## Conclusion
- JavaScript can evaluate and compare polynomial expressions using arithmetic and comparison operators.
- The inequality x³ + x + 3 > x⁵ **is possible** and holds true for many values of x.
- Use functions to encapsulate mathematical expressions for reusability and clarity.
