# Notes on Simple Array Methods

## Introduction

- This section covers basic array methods in JavaScript to expand your toolkit for working with arrays.

## Understanding Array Methods

- **Definition**: Methods are functions that can be called on objects. Arrays in JavaScript are objects, which is why they have methods.
- All arrays have access to built-in methods that act as tools.

## Example Test Array

```javascript
const testArray = ["A", "B", "C", "D", "E"];
```

---

## 1. **Slice Method**

- **Purpose**: Extracts a part of an array without modifying the original array.
- **Syntax**: `array.slice(begin, end)`
  - `begin`: index at which to start extraction (inclusive).
  - `end`: index at which to end extraction (exclusive).

### Example:

```javascript
const slicedArray = testArray.slice(2); // Returns ['C', 'D', 'E']
console.log(slicedArray);

const slicedRange = testArray.slice(1, 4); // Returns ['B', 'C', 'D']
console.log(slicedRange);
```

### Negative Indices:

- Use negative indices to count from the end of the array.

```javascript
const lastElement = testArray.slice(-1); // Returns ['E']
console.log(lastElement);

const sliceNegativeRange = testArray.slice(1, -1); // Returns ['B', 'C', 'D']
console.log(sliceNegativeRange);
```

### Shallow Copy:

- An empty slice creates a shallow copy of the array.

```javascript
const copyArray = testArray.slice(); // Returns ['A', 'B', 'C', 'D', 'E']
// Remeber : we can also use Spread oprator for shallow copy
const copyArraySecond = [...testArray];
```

---

## 2. **Splice Method**

- **Purpose**: Like slice but **changes the original array** by adding/removing elements.
- **Syntax**: `array.splice(start, deleteCount, item1, item2, ...)`
  - `start`: index at which to start changing the array.
  - `deleteCount`: number of elements to remove.
  - `itemN`: items to add to the array.

### Example:

```javascript
const arr = ["A", "B", "C", "D", "E"];
const splicedArray = arr.splice(1, 2); // Removes ['B', 'C']
console.log(arr); // ['A', 'D', 'E']
console.log(splicedArray); // ['B', 'C']
```

### Removing Last Element:

```javascript
arr.splice(-1); // Removes 'E'
console.log(arr); // ['A', 'D']
```

### Adding Elements:

```javascript
arr.splice(1, 0, "X", "Y"); // Adds 'X' and 'Y' at index 1
console.log(arr); // ['A', 'X', 'Y', 'D']
```

---

## 3. **Reverse Method**

- **Purpose**: Reverses the order of elements in the array.
- **Syntax**: `array.reverse()`
- Note: This method mutates the original array.

### Example:

```javascript
const arr2 = ["A", "B", "C", "D"];
arr2.reverse();
console.log(arr2); // ['D', 'C', 'B', 'A']
```

---

## 4. **Concat Method**

- **Purpose**: Merges two or more arrays.
- **Syntax**: `array1.concat(array2, array3, ...)`
- Does not mutate the original arrays.

### Example:

```javascript
const arr3 = ["A", "B"];
const arr4 = ["C", "D"];
const combinedArray = arr3.concat(arr4);
console.log(combinedArray); // ['A', 'B', 'C', 'D']
// Remeber : we can also concat with Spread operator
const combinedArraySpread = [...arr3, ...arr4];
```

---

## 5. **Join Method**

- **Purpose**: Joins all elements of an array into a string.
- **Syntax**: `array.join(separator)`
- `separator`: optional; specifies a string to separate the elements.

### Example:

```javascript
const arr3 = ["A", "B", "C", "D"];
const joinedString = arr3.join("-"); // 'A-B-C-D'
console.log(joinedString);
```

---

## Conclusion

- You now have a growing toolkit of array methods.
- Remember that some methods mutate the original array while others do not.
- For detailed information on each method, refer to the MDN documentation.

# the New `at` Method

## Introduction

- The `at` method is a new array method introduced in ES2022.
- It provides a modern way to access elements in an array.

## Creating a Dummy Array

```javascript
const array = [23, 11, 64]; // Example array
```

## Accessing Array Elements

### Traditional Method

- To access the first element:

```javascript
const firstElement = array[0]; // Gets the first element (23)
```

### Using the `at` Method

- Using the `at` method:

```javascript
const firstElementUsingAt = array.at(0); // Also gets the first element (23)
```

## Accessing Last Element

### Traditional Approach

- To get the last element without knowing the length:

```javascript
const lastElement = array[array.length - 1]; // Gets the last element (64)
```

### Using the `at` Method

- With the `at` method, you can use negative indices:

```javascript
const lastElementUsingAt = array.at(-1); // Gets the last element (64)
```

## Negative Indexing

- The `at` method allows negative indexing, counting from the end of the array:

```javascript
const secondLastElement = array.at(-2); // Gets the second last element (11)
```

## Comparison with Other Methods

- Another way to access the last element using the `slice` method:

```javascript
const lastElementUsingSlice = array.slice(-1)[0]; // Also returns 64
```

## Benefits of Using `at`

- The `at` method simplifies accessing elements, particularly when using negative indices.
- It makes code more readable when chaining methods.

## Method Chaining Example

- The `at` method can be useful in method chaining:

```javascript
const element = array.slice(0, 2).at(-1); // Gets the last element of the sliced array
```

## Performance Consideration

- For quick access to specific elements (like the first element), traditional bracket notation is still valid:

```javascript
const firstElementQuick = array[0]; // Quick access
```

## `at` Method with Strings

- The `at` method can also be used with strings:

```javascript
const name = "jonas";
const firstCharacter = name.at(0); // Gets 'j'
const lastCharacter = name.at(-1); // Gets 's'
```

## Conclusion

- Use the `at` method for readability and ease of access, especially with negative indices.
- Continue using traditional indexing for straightforward access to specific elements.

# Looping Arrays with `forEach` in JavaScript

## Introduction

- This section covers how to loop over arrays using the `forEach` method.
- The `forEach` method is fundamentally different from traditional loops, such as the `for...of` loop.

## Example Context: Bank Account Data

- The focus will be on an array representing bank account movements, where positive values indicate deposits and negative values indicate withdrawals.

## Creating an Example Array

```javascript
const movements = [200, -150, 450, -400, 300]; // Example movements array
```

## Using the `for...of` Loop

### Traditional Approach

- First, let's see how to loop through the array using a `for...of` loop:

```javascript
for (const movement of movements) {
  if (movement > 0) {
    console.log(`You deposited ${Math.abs(movement)}`);
  } else {
    console.log(`You withdrew ${Math.abs(movement)}`);
  }
}
```

### Explanation

- The loop iterates over each movement.
- It checks if the movement is positive (deposit) or negative (withdrawal) and logs the appropriate message using `Math.abs()` to get the absolute value.

## Transition to `forEach`

- Now, we will learn how to achieve the same result using the `forEach` method.

### Using `forEach`

```javascript
movements.forEach(function (movement) {
  if (movement > 0) {
    console.log(`You deposited ${Math.abs(movement)}`);
  } else {
    console.log(`You withdrew ${Math.abs(movement)}`);
  }
});
```

### Key Points

- `forEach` requires a callback function that defines what to do with each element.
- The `forEach` method automatically calls this function for each element in the array.

## Callback Function Details

- The `forEach` method passes the current element as an argument to the callback function.

### Example with Arrow Function

```javascript
movements.forEach((movement) => {
  if (movement > 0) {
    console.log(`You deposited ${Math.abs(movement)}`);
  } else {
    console.log(`You withdrew ${Math.abs(movement)}`);
  }
});
```

## Accessing Index and Array

- The `forEach` method can also provide access to the index of the current element and the entire array.

### Example with Index

```javascript
movements.forEach((movement, index, array) => {
  const type = movement > 0 ? "deposited" : "withdrew";
  console.log(`Movement ${index + 1}: You ${type} ${Math.abs(movement)}`);
});
// same instruction with for...of loop
for (const [index, movement] of movements.entries()) {
  const type = movement > 0 ? "deposited" : "withdrew";
  console.log(`Movement ${index + 1}: You ${type} ${Math.abs(movement)}`);
}
```

- In this example:
  - The first parameter is the current element (`movement`).
  - The second parameter is the index of that element.

## Summary of Differences

- **Breaking out of Loops**:
  - You cannot use `break` or `continue` with `forEach`. It always iterates through the entire array.
- **Index Access**:
  - In `forEach`, the index is automatically provided as an argument.

## When to Use Each Loop

- Use `forEach` for cleaner, more readable code when you need to perform an action on each element.
- Use `for...of` if you need more control, such as breaking out of the loop or using indices more flexibly.

## Conclusion

- The `forEach` method is a powerful tool for iterating over arrays.
- Understanding how it operates with callbacks will help you with other array methods in JavaScript.

### Final Thoughts

- Practice using `forEach` and other looping methods to become more comfortable with JavaScript's array handling capabilities.

# `forEach` with Maps and Sets in JavaScript

## Introduction

- The `forEach` method is not only available for arrays but also for maps and sets.
- This lecture explores how `forEach` works with these two data structures.

## `forEach` with Maps

### Overview of Maps

- A map is a collection of key-value pairs.
- Each entry in a map consists of a key and a value.

### Using `forEach` with Maps

```javascript
const currencies = new Map([
  ["USD", "United States Dollar"],
  ["EUR", "Euro"],
  ["GBP", "British Pound"],
]);

currencies.forEach((value, key, map) => {
  console.log(`Key: ${key}, Value: ${value}`);
});
```

### Parameters of the Callback Function

- The `forEach` method for maps calls the callback function with three arguments:
  1. **Current Value**: The value of the current entry.
  2. **Key**: The key of the current entry.
  3. **Map**: The entire map being iterated over.

### Example Output

- This will log each key-value pair in the map.

## `forEach` with Sets

### Overview of Sets

- A set is a collection of unique values and does not have keys or indexes.

### Creating a Set

```javascript
const currenciesUnique = new Set(["USD", "EUR", "GBP", "USD"]); // 'USD' is duplicated and will be ignored
console.log(currenciesUnique); // Output: Set { 'USD', 'EUR', 'GBP' }
```

### Using `forEach` with Sets

```javascript
currenciesUnique.forEach((value, key, set) => {
  console.log(`Value: ${value}, Key: ${key}`); // Here key is the same as value
});
```

### Explanation

- The second parameter (`key`) in the `forEach` method for sets is identical to the first parameter (`value`), since sets do not have distinct keys.

### Reasoning Behind Parameters

- The `forEach` method signature for sets retains the same structure as for arrays and maps to maintain consistency across different data structures.
- The key parameter in the set is effectively redundant, as it does not provide any additional information.

### Using an Underscore for Clarity

- To avoid confusion, we can use an underscore for the key parameter:

```javascript
currenciesUnique.forEach((value, _, set) => {
  console.log(`Value: ${value}`);
});
```

- The underscore signifies that this parameter is unused.

## Conclusion

- The `forEach` method is straightforward for both maps and sets, similar to its implementation with arrays.
- Understanding the parameters and their roles across different data structures helps maintain consistency in JavaScript programming.

### Key Takeaways

- **Maps**: `forEach` works with key-value pairs.
- **Sets**: `forEach` uses the same signature but the key is the same as the value.
- Using an underscore for unnecessary parameters keeps code clean and understandable.

# Data Transformations: `map`, `filter`, and `reduce` in JavaScript

## Introduction

- JavaScript provides three key array methods for data transformations:
  - **`map`**
  - **`filter`**
  - **`reduce`**
- These methods create new arrays based on transformations applied to existing arrays, making code cleaner and more expressive.

## Side Effects

- **Definition**: A side effect occurs when a function modifies a variable or interacts with the outside world (e.g., logging to the console, modifying a global variable).
- **Importance**: Functions without side effects (pure functions) are easier to test, debug, and reason about.

### Example of Side Effects with `forEach`

```javascript
const numbers = [1, 2, 3];
let sum = 0;

numbers.forEach((num) => {
  sum += num; // Side effect: modifying the external variable `sum`
});

console.log(sum); // Output: 6
```

- This example demonstrates a side effect because `sum` is modified outside of the function's scope.

## Overview of `map`

- **Purpose**: The `map` method transforms each element of an array and returns a new array.
- **Functionality**: It applies a specified callback function to each element.

### Example of `map`

```javascript
const numbers = [1, 2, 3, 4, 5];
const doubled = numbers.map((num) => num * 2);
console.log(doubled); // Output: [2, 4, 6, 8, 10]
```

- Here, each element is multiplied by 2, resulting in a new array of doubled values.

### Equivalent Implementation with `forEach`

```javascript
const doubledWithForEach = [];
numbers.forEach((num) => {
  doubledWithForEach.push(num * 2); // Side effect: modifying the external array
});
console.log(doubledWithForEach); // Output: [2, 4, 6, 8, 10]
```

## Overview of `filter`

- **Purpose**: The `filter` method creates a new array containing elements that satisfy a certain condition.
- **Functionality**: It tests each element with a specified condition and includes those that return true.

### Example of `filter`

```javascript
const numbers = [1, 2, 3, 4, 5];
const greaterThanTwo = numbers.filter((num) => num > 2);
console.log(greaterThanTwo); // Output: [3, 4, 5]
```

- This example filters the array to include only elements greater than 2.

### Equivalent Implementation with `forEach`

```javascript
const greaterThanTwoWithForEach = [];
numbers.forEach((num) => {
  if (num > 2) {
    greaterThanTwoWithForEach.push(num); // Side effect: modifying the external array
  }
});
console.log(greaterThanTwoWithForEach); // Output: [3, 4, 5]
```

## Overview of `reduce`

- **Purpose**: The `reduce` method reduces an array to a single value by applying a function cumulatively to its elements.
- **Functionality**: It maintains an accumulator that stores the intermediate result.

### Example of `reduce`

```javascript
const numbers = [1, 2, 3, 4, 5];
const sum = numbers.reduce((accumulator, current) => accumulator + current, 0);
console.log(sum); // Output: 15
```

- Here, `reduce` sums up all the elements in the array, returning the total.

```javascript
const movements = [200, 450, 70, 1300];

// Calculating the maximum value of an array
const max = movements.reduce((acc, mov) => {
  if (mov > acc) {
    return mov;
  } else {
    return acc;
  }
}, movements[0]);
```

- Here, `reduce` initializes with the first element of the array and then iterates through the rest of the elements, comparing each to find the maximum value.

### Explanation of `reduce` Process

- The `reduce` method takes two parameters:
  1. A callback function with three arguments: the accumulator and the current value of array and the array itself .
  2. An initial value for the accumulator (optional).

### Snowball Effect Analogy

- The `reduce` method can be likened to a snowball rolling down a hill, growing larger as it accumulates more snow (values).

### Equivalent Implementation with `forEach`

```javascript
let sumWithForEach = 0;
numbers.forEach((num) => {
  sumWithForEach += num; // Side effect: modifying the external variable `sumWithForEach`
});
console.log(sumWithForEach); // Output: 15
```

## Conclusion

- While you can achieve similar results with `forEach`, using `map`, `filter`, and `reduce` is preferred for several reasons:

  - **Readability**: Code is often more readable and expressive.
  - **Immutability**: These methods return new arrays instead of modifying existing ones, reducing side effects.
  - **Functional Programming**: They promote a functional programming style, which can lead to fewer side effects and more predictable code.

- Understanding side effects and how to manage them is crucial for writing effective JavaScript code.

---

# Method Chaining in JavaScript Arrays

In JavaScript, many array methods (like `.map()`, `.filter()`, `.reduce()`, `.sort()`, etc.) return a new array or a value, making them suitable for chaining. Chaining these methods allows you to perform multiple transformations on an array in a concise and readable way.

---

## **Common Array Methods for Chaining**

1. **`map()`**: Transforms each element of the array.
2. **`filter()`**: Filters elements based on a condition.
3. **`reduce()`**: Reduces the array to a single value.

---

## **Example: Chaining Array Methods**

```javascript
const numbers = [1, 2, 3, 4, 5];

// Chaining: Filter, Map, and Reduce
const result = numbers
  .filter((num) => num % 2 === 0) // Step 1: Keep even numbers [2, 4]
  .map((num) => num * 2) // Step 2: Double each number [4, 8]
  .reduce((sum, num) => sum + num, 0); // Step 3: Sum them up (4 + 8 = 12)

console.log(result); // Output: 12
```

---

## **How It Works**

1. **`filter(num => num % 2 === 0)`**:

   - Keeps only even numbers from the original array: `[2, 4]`.

2. **`map(num => num * 2)`**:

   - Doubles each remaining number: `[4, 8]`.

3. **`reduce((sum, num) => sum + num, 0)`**:
   - Calculates the sum of the transformed numbers: `4 + 8 = 12`.

---

## **Example: Breaking for Clarity**

Instead of chaining everything:

```javascript
const evenNumbers = numbers.filter((num) => num % 2 === 0);
const doubled = evenNumbers.map((num) => num * 2);
const sum = doubled.reduce((sum, num) => sum + num, 0);

console.log(sum); // Output: 12
```

## **Caution: When Not to Chain**

1. **Too Many Steps**:

   - If the chain becomes too long, it can reduce readability. Break it into intermediate steps if necessary.

2. **Debugging**:

   - Debugging can be harder in chains. Use intermediate variables to inspect results if needed.

3. **Mutating Arrays**:

   We shouldn't use chaining when the methods mutate the array because it can lead to unexpected side effects and make the code harder to understand and debug. It's not a good practice to rely on chaining with mutating methods like `sort()`, `reverse()`, or `splice()` since they modify the original array, potentially causing issues elsewhere in the code if the original array is reused.

---

# the `find` Method

## Introduction

- The `find` method is an important array method in JavaScript, used to retrieve a single element from an array based on a specified condition.

## Key Points

- **Purpose**: The `find` method returns the first element in an array that satisfies a given condition.
- **Callback Function**: Just like `filter` and `map`, `find` accepts a callback function that is executed for each element in the array.
- **Return Value**: Unlike `filter`, which returns an array of all matching elements, `find` returns only the first element that matches the condition or `undefined` if no match is found.

## Basic Usage

1. **Example with Numbers**:
   - Suppose we have an array of movements (transactions).
   ```javascript
   const movements = [200, -400, 300, -200];
   const firstWithdrawal = movements.find((movement) => movement < 0);
   console.log(firstWithdrawal); // Output: -400
   ```
   - In this example, `find` retrieves the first negative number from the array, indicating the first withdrawal.

### Differences from `filter`

- **Filter**: Returns all elements that match the condition and creates a new array.
- **Find**: Returns only the first matching element and does not create a new array.

### Example with Objects

- The `find` method is particularly useful when working with arrays of objects.

1. **Example with Accounts**:

   - Consider an array of account objects:

   ```javascript
   const accounts = [
     { owner: "Jessica Davis", balance: 5000 },
     { owner: "John Doe", balance: 3000 },
     { owner: "Sarah Smith", balance: 7000 },
   ];

   const account = accounts.find((acc) => acc.owner === "Jessica Davis");
   console.log(account);
   // Output: { owner: 'Jessica Davis', balance: 5000 }
   ```

### How It Works

- The `find` method loops through the `accounts` array and checks each account’s `owner` property against 'Jessica Davis'. When it finds a match, it returns that account object.

### Important Considerations

- When using `find`, ensure that the property you are checking (like `owner`) is unique within the array. This ensures that `find` will return one specific object.
- If there are no matches, `find` will return `undefined`.

### Practical Use Case

- The `find` method can be used to implement functionalities such as login features or searching for specific items in a collection.

### Challenge

- As a challenge, implement a similar functionality using a `for...of` loop to see the differences in iteration methods.

```javascript
let foundAccount;
for (const acc of accounts) {
  if (acc.owner === "Jessica Davis") {
    foundAccount = acc;
    break; // Stop the loop once the account is found
  }
}
console.log(foundAccount);
// Output: { owner: 'Jessica Davis', balance: 5000 }
```

### Conclusion

- The `find` method is a powerful tool for retrieving a single item from an array based on specific criteria, especially when dealing with complex data structures like arrays of objects. Understanding its differences from other array methods like `filter` is crucial for effective coding in JavaScript.

Here are the complete notes from the lecture on the `findIndex` method in JavaScript, along with code examples.

# `findIndex` Method

## Introduction

- The `findIndex` method is closely related to the `find` method. While `find` returns the element itself, `findIndex` returns the index of the element that satisfies a given condition.

## Key Points

- **Purpose**: The `findIndex` method is used to locate the index of the first element in an array that meets a specified condition.
- **Return Value**: It returns the index of the found element or `-1` if no matching element is found.

## Basic Usage

1. **Example with Numbers**:
   - Suppose we have an array of movements (transactions).
   ```javascript
   const movements = [200, -400, 300, -200];
   const indexFirstWithdrawal = movements.findIndex((movement) => movement < 0);
   console.log(indexFirstWithdrawal); // Output: 1
   ```
   - In this example, `findIndex` retrieves the index of the first negative number from the array, indicating the index of the first withdrawal.

## Use Case Scenario

- A practical use case for `findIndex` is where you need to delete an element from an array.

### Example: Closing an Account

1. **Array of Account Objects**:

   ```javascript
   const accounts = [
     { owner: "Jessica Davis", balance: 5000 },
     { owner: "John Doe", balance: 3000 },
     { owner: "Sarah Smith", balance: 7000 },
   ];
   ```

2. **Function to Close an Account**:

   ```javascript
   function closeAccount(username) {
     const index = accounts.findIndex((acc) => acc.owner === username);
     if (index !== -1) {
       accounts.splice(index, 1); // Remove the account
       console.log(`Account of ${username} closed.`);
     } else {
       console.log(`Account of ${username} not found.`);
     }
   }

   closeAccount("John Doe");
   console.log(accounts); // Output: Remaining accounts
   ```

### How It Works

- The `findIndex` method loops through the `accounts` array, checking each account's `owner` property against the provided username. When it finds a match, it returns the index of that account.

## Differences from `indexOf`

- **`indexOf`**: Searches for a specific value in the array and returns its index. It can only check for exact matches.
- **`findIndex`**: Allows for complex conditions and returns the index based on the criteria defined in the callback function.

### Example Comparing `indexOf` and `findIndex`

1. **Using `indexOf`**:

   ```javascript
   const numbers = [1, 2, 3, 4];
   const index = numbers.indexOf(2);
   console.log(index); // Output: 1
   ```

2. **Using `findIndex` for a Condition**:
   ```javascript
   const indexGreaterThanTwo = numbers.findIndex((num) => num > 2);
   console.log(indexGreaterThanTwo); // Output: 2
   ```

## Common Use Cases

- **Finding the Index of an Object**: Useful when working with arrays of objects to identify the position of an object based on specific criteria.
- **Deleting Elements**: As shown in the account closure example, `findIndex` helps to locate the index for deletion.

## Additional Notes

- Both `find` and `findIndex` methods provide access to the current index and the entire array within the callback function, although these parameters are rarely used.
- These methods were introduced in ES6, so they may not be supported in very old browsers.

## Conclusion

- The `findIndex` method is a powerful tool for finding the index of an element in an array that matches a specific condition. It enhances the ability to manipulate arrays, especially when combined with methods like `splice` for deletion. Understanding the differences between `find`, `findIndex`, and `indexOf` is essential for effective JavaScript programming.

#Here are the complete notes from the lecture covering the `some` and `every` array methods, along with relevant code examples.

Here are the updated notes with the additional information regarding the similarities between `includes` and `some`.

# Lecture Notes: Array Methods - `some` and `every`

## Overview

In this lecture, we explore two important array methods in JavaScript: `some` and `every`. These methods are useful for testing conditions in arrays.

## 1. The `some` Method

- **Definition**: The `some` method tests whether at least one element in the array passes the provided function's condition. It returns `true` if the condition is met for any element, and `false` otherwise.

### Example Usage

```javascript
const movements = [200, -150, 300, -50, 700];

// Check if there are any deposits (positive values)
const anyDeposits = movements.some((movement) => movement > 0);
console.log(anyDeposits); // true

// Check for deposits above 5000
const anyHighDeposits = movements.some((movement) => movement > 5000);
console.log(anyHighDeposits); // false
```

## 2. The `every` Method

- **Definition**: The `every` method tests whether all elements in the array pass the provided function's condition. It returns `true` if all elements satisfy the condition; otherwise, it returns `false`.

### Example Usage

```javascript
const movements = [200, 150, 300, 50, 700];

// Check if all movements are positive
const allDeposits = movements.every((movement) => movement > 0);
console.log(allDeposits); // false

// Example with an account that has only positive movements
const account4Movements = [200, 150, 300];
const allAccount4Deposits = account4Movements.every((movement) => movement > 0);
console.log(allAccount4Deposits); // true
```

## 3. Key Differences Between `includes`, `some`, and `every`

- **`includes`**: Checks for equality to see if a specific value exists in the array. It returns `true` if the value is found, and `false` otherwise.

  ```javascript
  const movements = [200, -150, 300];
  console.log(movements.includes(200)); // true
  console.log(movements.includes(-100)); // false
  ```

- **`some`**: Similar to `includes`, but allows you to specify a condition. It returns `true` if any element satisfies the condition.
- **`every`**: Returns `true` only if all elements satisfy the condition.

## 4. Practical Application: Loan Request Example

In a banking application, we may want to implement a feature to check if a loan can be granted based on deposit conditions.

### Implementation

```javascript
const currentAccount = {
  movements: [2000, -500, 7000, -400], // Example account movements
};

const requestLoan = function (amount) {
  // Condition: There needs to be at least one deposit >= 10% of the loan amount
  const hasDeposit = currentAccount.movements.some(
    (movement) => movement >= amount * 0.1
  );

  if (amount > 0 && hasDeposit) {
    console.log("Loan granted");
    currentAccount.movements.push(amount); // Add the loan to movements
  } else {
    console.log("Loan denied");
  }
};

requestLoan(50000); // Loan denied
requestLoan(2000); // Loan granted
```

## 5. Callback Functions

You can also define the condition as a separate function for reusability.

### Example of Separate Callback

```javascript
const isDeposit = (movement) => movement > 0;

const anyDeposits = movements.some(isDeposit);
console.log(anyDeposits); // true

const allDeposits = movements.every(isDeposit);
console.log(allDeposits); // false
```

## 6. Conclusion

The `some` and `every` methods are powerful tools for working with arrays in JavaScript, allowing for concise and readable code when testing conditions. Understanding these methods helps in implementing complex logic in applications, such as financial calculations and user validations. Additionally, recognizing the difference between `includes` and `some`—where `includes` checks for equality and `some` allows for condition testing—enhances our ability to manipulate and evaluate arrays effectively.

Here are the complete notes from the lecture covering the `flat` and `flatMap` array methods, along with relevant code examples.

# Array Methods - `flat` and `flatMap`

## Overview

In this lecture, we learn about two array methods in JavaScript: `flat` and `flatMap`, which are used for handling nested arrays. These methods were introduced in ES2019 and are straightforward to understand.

## 1. The `flat` Method

- **Definition**: The `flat` method creates a new array with all sub-array elements concatenated into it recursively up to the specified depth. By default, it flattens the array one level deep.

### Example Usage

```javascript
const nestedArray = [1, 2, [3, 4], [5, 6]];

// Flattening the array one level deep
const flatArray = nestedArray.flat();
console.log(flatArray); // Output: [1, 2, 3, 4, 5, 6]

// Flattening a deeper nested array
const deeperNestedArray = [
  1,
  2,
  [
    [3, 4],
    [5, 6],
  ],
];
const flatDeeperArray = deeperNestedArray.flat(2);
console.log(flatDeeperArray); // Output: [1, 2, 3, 4, 5, 6]
```

## 2. Flattening with Depth

- The `flat` method takes a depth argument to specify how deep a nested array should be flattened.

### Example of Depth Argument

```javascript
const arrDeep = [1, [2, [3, 4]], [5, 6]];

// Default depth (1)
const flatOnce = arrDeep.flat();
console.log(flatOnce); // Output: [1, 2, [3, 4], 5, 6]

// Flattening two levels deep
const flatTwice = arrDeep.flat(2);
console.log(flatTwice); // Output: [1, 2, 3, 4, 5, 6]
```

## 3. Practical Application: Calculating Overall Balance

To calculate the overall balance of all movements in bank accounts, we first need to flatten the nested arrays of movements.

### Implementation

```javascript
const accounts = [
  { owner: "Alice", movements: [200, -100, 300] },
  { owner: "Bob", movements: [500, -200, 100] },
];

// Extracting movements and flattening them
const allMovements = accounts.map((acc) => acc.movements).flat();
console.log(allMovements); // Output: [200, -100, 300, 500, -200, 100]

// Calculating total balance
const overallBalance = allMovements.reduce((acc, mov) => acc + mov, 0);
console.log(overallBalance); // Output: 800
```

## 4. Using `flatMap`

- **Definition**: The `flatMap` method maps each element using a mapping function, then flattens the result into a new array. It combines the functionality of `map` and `flat` in one method, operating at one level of depth.

### Example Usage

```javascript
const accounts = [
  { owner: "Alice", movements: [200, -100, 300] },
  { owner: "Bob", movements: [500, -200, 100] },
];

// Using flat and map to extract and flatten movements in one go
const allMovementsFlatMap = accounts.map((acc) => acc.movements).flat();

// Using flatMap to extract and flatten movements in one go
const allMovementsFlatMap = accounts.flatMap((acc) => acc.movements);
console.log(allMovementsFlatMap); // Output: [200, -100, 300, 500, -200, 100]

// Calculating total balance using flatMap
const overallBalanceFlatMap = allMovementsFlatMap.reduce(
  (acc, mov) => acc + mov,
  0
);
console.log(overallBalanceFlatMap); // Output: 800
```

## 5. Key Differences Between `flat` and `flatMap`

- **`flat`**: Flattens an array by a specified depth. Does not involve mapping.
- **`flatMap`**: Combines mapping and flattening into a single operation, flattening only one level deep.

## 6. Conclusion

The `flat` and `flatMap` methods are powerful tools for working with nested arrays in JavaScript. They allow for efficient manipulation of data structures commonly found in applications, particularly when dealing with arrays of objects, such as bank accounts. Understanding these methods can significantly enhance code readability and performance when handling nested arrays.

---

# Sorting Arrays in JavaScript

## Introduction

- Sorting is a crucial feature in applications, allowing users to organize data efficiently.
- JavaScript provides a built-in `sort` method for arrays.

## Sorting Strings

1. **Example with Strings**
   - Create an array of strings:
     ```javascript
     const owners = ["Jonas", "Zach", "Adam", "Martha"];
     owners.sort();
     console.log(owners); // ['Adam', 'Jonas', 'Martha', 'Zach']
     ```
   - The `sort` method mutates the original array.

## Sorting Numbers

2. **Example with Numbers**
   - Create an array of numbers:
     ```javascript
     const movements = [10, 5, 15, 3, -5];
     movements.sort();
     console.log(movements); // [-5, 10, 15, 3, 5] (not sorted as expected)
     ```
   - The `sort` method sorts numbers as strings, leading to unexpected results. basically converts eveything to strings and then it does the sorting itself .

## Custom Sorting

3. **Using a Compare Function**

   - To sort numbers correctly, use a compare function:
     ```javascript
     movements.sort((a, b) =>
     if (a > b) return(1) // If first number greater than second => switch order of them
     if (a < b) return(-1) // If first number smaller than second => Keep order
     );
     // Same as :
     movements.sort((a, b) => a - b);
     console.log(movements); // [-5, 3, 5, 10, 15] (sorted correctly)
     ```

4. **Understanding the Compare Function**

   - If the compare function returns:
     - A negative number: `a` comes before `b` (Keep order).
     - Zero: `a` and `b` are equal.
     - A positive number: `b` comes before `a` (Switch order)

5. **Example with Ascending and Descending Order**
   - Ascending order:
     ```javascript
     movements.sort((a, b) => a - b); // Ascending
     ```
   - Descending order:
     ```javascript
     movements.sort((a, b) => b - a); // Descending
     ```

## Shallow copy

6. **Create copy before sorting**

   - Many times, when we want to sort an array, we don't want to mutate the original array. In such cases, we can use the slice() method to create a copy of the array and then apply the sort() method to the copy.

   ```javascript
   const numbers = [5, 2, 8, 1, 4];

   // Create a sorted copy without mutating the original array
   const sortedNumbers = numbers.slice().sort((a, b) => a - b);

   console.log("Original array:", numbers); // [5, 2, 8, 1, 4]
   console.log("Sorted array:", sortedNumbers); // [1, 2, 4, 5, 8]
   ```

## Summary

- Use the `sort` method for sorting arrays in JavaScript, but remember that it sorts as strings by default.
- Always use a compare function for numeric arrays to ensure correct ordering.
- Implement sorting features carefully to enhance user experience in applications.

These notes summarize the key points and code examples from the lecture on sorting arrays in JavaScript.

---

Here are the notes from the lecture on creating and filling arrays programmatically, including code examples:

# Creating and Filling Arrays Programmatically

## Overview

- The lecture focuses on how to create and fill arrays in JavaScript programmatically, rather than manually.

## Creating Arrays

1. **Manual Creation**:

   - Arrays can be created by explicitly defining their elements:
     ```javascript
     const arr = [1, 2, 3, 4, 5, 6, 7];
     ```

2. **Using the `Array` Constructor**:
   - You can create an array using the `Array` constructor:
     ```javascript
     const arr = new Array(1, 2, 3, 4, 5, 6, 7);
     ```

## Understanding the `Array()` Constructor Behavior

- **Single Argument**:
  - Passing a single argument to `Array()` creates an array of that length with empty elements:
    ```javascript
    const x = new Array(7); // x is now [empty × 7]
    ```

## Filling Arrays

1. **Using the `fill()` Method**:

   - The `fill()` method can fill an array with a specified value:
     ```javascript
     const x = new Array(7).fill(5); // x is now [5, 5, 5, 5, 5, 5, 5]
     ```

2. **Filling with a Range**:
   - You can specify a start and end index:
   - `Syntax` : arr.fill (value , start , end)
   - End value not included
     ```javascript
     const arr = new Array(7).fill(0);
     arr.fill(1, 3, 5); // arr is now [0, 0, 0, 1, 1, 0, 0]
     ```

## Creating Arrays Programmatically with `Array.from()`

- **Using `Array.from()`**:

  - `syntax` : Array.from(arrayLike, mapFn)
  - `mapFn` : aruguments are `(element , index)`. It's like map method of arrays
  - `arrayLike` : An iterable or array-like object to convert to an array.

  - This method creates a new array instance from an array-like or iterable object.
  - Example to create an array of seven ones:
    ```javascript
    const ones = Array.from({ length: 7 }, () => 1); // [1, 1, 1, 1, 1, 1, 1]
    ```

- **Creating a Range from 1 to 7**:
  - You can use the index to create a sequence:
    ```javascript
    const arr = Array.from({ length: 7 }, (element, index) => index + 1); // [1, 2, 3, 4, 5, 6, 7]
    ```

## Handling Array-Like Structures

- **Converting NodeLists to Arrays**:
  - Remember that `querySelectorAll()` doesn't resturn array , instead it returns NodeLists that it doesn't have most of the array methodes like map() or reduce() so we can convert it to array with `Array.from()`
  - Example of converting a NodeList returned by `querySelectorAll()`
    ```javascript
    const movementsUI = Array.from(
      document.querySelectorAll(".movements_value")
    );
    // And now we can use map() on it
    movementsUI.map((element) => element * 2);
    // We can use map function immediately as second argument of Array.from(array-like , mapfn)
    const movementsUI = Array.from(
      document.querySelectorAll(".movements_value"),
      (element) => element * 2
    );
    ```

## Conclusion

- Programmatically creating and filling arrays is essential for dynamic data handling in JavaScript. The `Array.from()` method provides a powerful way to work with iterable objects and create arrays based on custom logic.

These notes encapsulate the key concepts and examples from the lecture, providing a solid foundation for understanding array creation and manipulation in JavaScript.

# Array methodes summary

Here’s an updated summary table of the 23 array methods, now including a syntax column:

## Methods That Mutate the Original Array

| **Method**  | **Description**                                                       | **Syntax**                                            |
| ----------- | --------------------------------------------------------------------- | ----------------------------------------------------- |
| `push()`    | Adds one or more elements to the end of an array.                     | `array.push(element1, element2, ...)`                 |
| `unshift()` | Adds one or more elements to the beginning of an array.               | `array.unshift(element1, element2, ...)`              |
| `pop()`     | Removes the last element from an array and returns it.                | `const lastElement = array.pop()`                     |
| `shift()`   | Removes the first element from an array and returns it.               | `const firstElement = array.shift()`                  |
| `splice()`  | Adds or removes elements from an array at a specified index.          | `array.splice(start, deleteCount, item1, item2, ...)` |
| `reverse()` | Reverses the order of the elements in an array.                       | `array.reverse()`                                     |
| `sort()`    | Sorts the elements of an array in place and returns the sorted array. | `array.sort(compareFunction)`                         |
| `fill()`    | Fills all the elements of an array with a static value.               | `array.fill(value, start, end)`                       |

## Methods That Return a New Array

| **Method**  | **Description**                                                                                           | **Syntax**                                 |
| ----------- | --------------------------------------------------------------------------------------------------------- | ------------------------------------------ |
| `map()`     | Creates a new array by applying a function to each element of the original array.                         | `const newArray = array.map(callback)`     |
| `filter()`  | Creates a new array with all elements that pass a test implemented by the provided function.              | `const newArray = array.filter(callback)`  |
| `slice()`   | Returns a shallow copy of a portion of an array into a new array.                                         | `const newArray = array.slice(start, end)` |
| `concat()`  | Merges two or more arrays, returning a new array without changing the existing arrays.                    | `const newArray = array1.concat(array2)`   |
| `flat()`    | Creates a new array with all sub-array elements concatenated into it recursively up to a specified depth. | `const newArray = array.flat(depth)`       |
| `flatMap()` | Maps each element using a mapping function, then flattens the result into a new array.                    | `const newArray = array.flatMap(callback)` |

## Methods for Finding Indexes

| **Method**    | **Description**                                                                            | **Syntax**                                |
| ------------- | ------------------------------------------------------------------------------------------ | ----------------------------------------- |
| `indexOf()`   | Returns the first index at which a given element can be found, or -1 if it is not present. | `const index = array.indexOf(value)`      |
| `findIndex()` | Returns the index of the first element that satisfies the provided testing function.       | `const index = array.findIndex(callback)` |

## Methods for Finding Elements

| **Method** | **Description**                                                                      | **Syntax**                             |
| ---------- | ------------------------------------------------------------------------------------ | -------------------------------------- |
| `find()`   | Returns the value of the first element that satisfies the provided testing function. | `const element = array.find(callback)` |

## Methods for Checking Inclusion

| **Method**   | **Description**                                                                                       | **Syntax**                                |
| ------------ | ----------------------------------------------------------------------------------------------------- | ----------------------------------------- |
| `includes()` | Determines whether an array includes a certain value among its entries, returning true or false.      | `const exists = array.includes(value)`    |
| `some()`     | Tests whether at least one element in the array passes the test implemented by the provided function. | `const hasElement = array.some(callback)` |
| `every()`    | Tests whether all elements in the array pass the test implemented by the provided function.           | `const allMatch = array.every(callback)`  |

## Methods for Transforming Arrays

| **Method** | **Description**                                                                               | **Syntax**                                            |
| ---------- | --------------------------------------------------------------------------------------------- | ----------------------------------------------------- |
| `join()`   | Joins all elements of an array into a string.                                                 | `const string = array.join(separator)`                |
| `reduce()` | Executes a reducer function on each element of the array, resulting in a single output value. | `const result = array.reduce(callback, initialValue)` |

## Methods for Looping Over Arrays

| **Method**  | **Description**                                                                      | **Syntax**                |
| ----------- | ------------------------------------------------------------------------------------ | ------------------------- |
| `forEach()` | Executes a provided function once for each array element, without returning a value. | `array.forEach(callback)` |
