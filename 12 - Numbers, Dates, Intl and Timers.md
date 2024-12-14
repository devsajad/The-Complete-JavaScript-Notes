# Converting and Checking Numbers in JavaScript

## 1. Overview

- This section covers how numbers work in JavaScript, including:
  - Converting values to numbers
  - Checking if values are numbers

## 2. Number Representation

- In JavaScript:
  - All numbers are represented as floating-point numbers (decimals).
  - Internally, they are stored in a 64-bit binary format.

## 3. Binary Representation Challenges

- Some fractions are difficult to represent in binary format, leading to precision issues.
  - For example, `0.1` cannot be accurately represented, resulting in unexpected outputs. Like we cannot show 3/10 in base 10 correctly (3.33333...)

### Example:

```javascript
console.log(0.1 + 0.2); // Output: 0.30000000000000004
console.log(0.1 + 0.2 === 0.3); // Output : false
```

## 4. Converting Strings to Numbers

- You can convert strings to numbers using the `Number()` function:

```javascript
const str = "23";
const num = Number(str);
console.log(num); // Output: 23
```

- A simpler method is using the unary `+` operator:

```javascript
const str = "23";
const num = +str; // Type coertion
console.log(num); // Output: 23
```

## 5. Parsing Numbers

- Use `parseInt()` to extract integers from strings:
- String should starts with number otherwise we will get `undefined`

```javascript
const str = "30px";
const num = parseInt(str);
console.log(num); // Output: 30

const str2 = "ef22";
const num2 = parseInt(str2);
console.log(num2); // Output : NaN
```

- Use `parseFloat()` to extract floating-point numbers:

```javascript
const str = "2.5rem";
const num = parseFloat(str);
console.log(num); // Output: 2.5
```

## 6. Using Base with `parseInt()`

- The `parseInt()` function accepts a second argument to specify the numeral system base:

```javascript
const binaryStr = "1010";
const num = parseInt(binaryStr, 2); // Base 2
console.log(num); // Output: 10
```

## 7. Checking if Values are Numbers

- To check if a value is `NaN` (Not a Number):

```javascript
console.log(Number.isNaN(NaN)); // Output: true
console.log(Number.isNaN(20)); // Output: false
console.log(Number.isNaN("20")); // Output: false
console.log(Number.isNaN(+"sajjad")); // Output: true
```

- To check if a value is a finite number:

```javascript
console.log(Number.isFinite(20)); // Output: true
// isFinit is better way to check if value is number
console.log(Number.isFinite("20")); // Output : false (It's not a number)
console.log(Number.isFinite(Infinity)); // Output: false
```

- To check if a value is a integer number: `isInteger()`

## 8. Summary

- JavaScript numbers are represented as floating-point.
- Conversion can be done with `Number()`, `parseInt()`, `parseFloat()`, or the unary `+`.
- Use `isNaN()` and `isFinite()` to check number validity.

## 9. Important Points

- Precision can be problematic in scientific and financial calculations.
- Always be aware of the underlying representation of numbers in JavaScript to avoid unexpected results.
