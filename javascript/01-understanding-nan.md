# Understanding NaN

`NaN` (Not a Number) is a special value in JavaScript that represents the result of an operation that cannot produce a **meaningful numeric value**. It's often used to indicate errors or invalid calculations. While NaN itself is a peculiar concept, what makes it truly strange is its behavior when compared to other values.

```javascript
console.log(NaN === NaN); // false
console.log(NaN == NaN); // false
```

The reason behind this behavior is rooted in the [IEEE 754 floating-point standard](https://en.wikipedia.org/wiki/IEEE_754), which JavaScript follows for numeric operations. According to the standard, NaN is considered **unordered and not equal to any value**, including itself. This design choice was made to avoid potential ambiguities when dealing with NaN values in complex numerical computations.

There is a built-in function called isNaN(). But also, JavaScript provides the Number.isNaN() method to check for NaN. Unlike isNaN(), which considers non-numeric strings as NaN, Number.isNaN() only returns true if the value is specifically NaN.

```javascript
console.log(Number.isNaN(NaN)); // true
console.log(isNaN(NaN)); // true

console.log(Number.isNaN(42)); // false
console.log(isNaN(42)); // false

console.log(Number.isNaN('Hello')); // false
console.log(isNaN('Hello')); // true

console.log(Number.isNaN('123')); // false
console.log(isNaN('123')); // false

console.log(Number.isNaN(undefined)); // false
console.log(isNaN(undefined)); // true

console.log(Number.isNaN(null)); // false
console.log(isNaN(null)); // false
```
