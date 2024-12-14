# Destructuring Arrays

_def_ Unpacking values from an array or object => into seprate variables

```js
const categories = ["Italian", "Pizzeria", "Vegetarian", "Organic"];
const [a, b, c] = categories; // Destructuring
console.log(a, b, c);
```

## Ommiting values

```js
const [a, , c] = categories; // Ommmit second value of array
```

## Muatating variables (Swaping values)

[a , b] = [b , a]

```js
let [a, b] = categories;
[a, b] = [b, a];
```

## Nested array destructuring

```js
const categories = ["Italian", "Pizzeria", ["Vegetarian", "Organic"]];
let [first, , [firstNested]] = categories;
console.log(first, firstNested);
```

## Default values for the variables

if we desctruct some index of array that it doesn't exist => undefined
solution => Default values for when there is not anythin for destructuring

```js
const categories = ["Italian", "Pizzeria"];
const [a, b, c = "defualt"] = categories;
```

# Destructuring Object

{prpertyName , propertyName} = objectName
in obj order doesn't matter => just provide the name and don't need to ommit like array

```js
const { mainMenu, defName } = restaurant;
```

## Different variable names from object proprty names

```js
const { mainMenu: NewName, defName } = restaurant;
```

## Default value for variables

for whene there is not such property the variable value will be default value

```js
const { kirekhar = [] } = restaurant;
```

## Mustating Varibales

use {} => otherwise in js you can't assign a block of code to variable and you will have error

```js
let a = 100;
let b = 200;
const obj = {
  a: 1,
  b: 2,
};
{ a, b } = obj;✖️
({ a, b } = obj);✔️
```

## Nested Object

{{}}

```js
const {
const {
  openingHours: {
    thu: { open, close },
  },
} = restaurant;

```

# Spread Operator

# Spread Operator Overview

- The spread operator allows expanding an array into its individual elements, effectively "unpacking" the array.
- Introduced in ES6, it simplifies array and object manipulation.

## Use Cases

1. **Creating New Arrays**:

   1.1 You can create a new array by adding new elements at the beginning or end and spreading the elements of an existing array.

   - **Example**:
     `javascript
const arr = [7, 8, 9];
const newArr = [1, 2, ...arr]; // [1, 2, 7, 8, 9]
`
     1.2 **Shallow Copies**:

   - Create shallow copies of arrays using the spread operator.
   - **Example**:

   ```javascript
   const copy = [...originalArray];
   ```

   1.3 **Merging Arrays**:

   - Easily join multiple arrays into one.
   - **Example**:

   ```javascript
   const combined = [...array1, ...array2];
   ```

2. **Function Arguments**:

   - The spread operator can be used to pass multiple elements of an array as arguments to a function.
   - **Example**:
     ```javascript
     const arr = [1, 2, 3];
     console.log(...arr); // Logs: 1 2 3
     ```

## Important Notes

- The spread operator works with all iterables (arrays, strings, maps, sets) but not objects(in es8 you can you use it for objects).

  - **Example**:

  ```js
  // using for string
  const string = "sajjad";
  const arrayOfLetters = [...string];

  // using for obejcts ( for shallow copy , merge , add property , ....)
  const newObject = { ...restaurant.openingHours, newProperty: "new name" };
  console.log(newObject);
  ```

- It cannot be used in contexts that do not expect multiple values separated by commas, such as in template literals.
- whenever needs elements of array individually and we want write seprated by comma we use spread (when we create new array or pass argumnet to function)

# Rest Opertaor

Destructuring => to Unpack and assing to variables => [a , b] = [1,2,3] // a=1 , b=2
spread => to UNPACK elements => [1,2,3] = Unpack => 1,2,3
Rest => to PACK elements => collect all elements into array => 1 , 2 , 3 = pack => [1,2,3]

## Use Cases

**Destructuring with Rest** : to pack all rest elements into array
The rest syntax must always be the last element in a destructuring assignment.
Only one rest element is allowed in any destructuring assignment.

```js
const array = [1, 2, 3, 4];
// Destructuring
const [a, b] = array; // a=1 , b =2
// Spread
const newArray = [...array];
// Rest
// Rest collect all the array elements after last valriable and put it into array
const [a, b, ...others] = array; // a=1 b=2 others = [3,4]
```

**Rest Parameters in Functions**
Allows functions to accept an arbitrary number of arguments and pack them into array

```js
function sumNumbers(...numbers) {
  let sum = 0;
  for (const i in numbers) {
    sum += numbers[i];
  }
  console.log(sum);
}

sumNumbers(1, 2, 3, 4, 5);
sumNumbers(1, 2, 3, 4, 5, 6, 7);
// Combining Spread and Rest
const numbersArray = [1, 2, 3, 4, 5, 6];
sumNumbers(...numbersArray);
```

# Logical Operators: Short Circuiting (AND and OR)

### Overview of Logical Operators

- logical oprators can use with any data types and return any data types
- **Short Circuiting**: A technique where the evaluation stops as soon as the result is determined.

### OR Operator (`||`)

- **Functionality**: Returns the first truthy value it encounters.
- **Non-Boolean Values**: Can work with any data type, not just Boolean values.
- **Short Circuiting with OR**:
  - If the first operand is truthy, the second operand is not evaluated.
  - Example: `3 || 'Jonas'` returns `3` because `3` is truthy.

### Examples of OR Operator

- `'' || 'Jonas'` returns `'Jonas'` (first is falsy).
- `true || 0` returns `true` (first is truthy).
- `undefined || null` returns `null` (both are falsy => last one will return).

### General Rule for OR

- Evaluates until it finds a truthy value, then returns that value.

### Practical Application of OR

- Setting default values using OR:

  ```javascript
  //let guests = restaurant.numGuests ? restaurant.numGuests : 4;

  //if (restaurant.numGuests) guests = restaurant.numGuests;
  //else guests = 4;

  let guests = restaurant.numGuests || 10;
  ```

### AND Operator (`&&`)

- **Functionality**: Returns the first falsy value it encounters or the last truthy value.
- **Short Circuiting with AND**:
  - If the first operand is falsy, the second operand is not evaluated.
  - Example: `0 && 'Jonas'` returns `0`.

### Examples of AND Operator

- `23 && null` returns `null` (short circuits at the first falsy value).
- `true && 'Jonas'` returns `'Jonas'` (continues to evaluate).

### Practical Application of AND

- To execute code in the second operand if the first one is true:
  ```javascript
  //if(restaurant.orderPizza){
  //  restaurant.orderPizza("mushrooms", "spinach")
  //}
  // if orderPizza exist then call it
  restaurant.orderPizza && restaurant.orderPizza("mushrooms", "spinach");
  ```

### Summary

- Both operators can simplify code by avoiding if statements.
- Understanding short circuiting helps in writing cleaner, more efficient JavaScript.

### Caveat

- When using these operators, be cautious with falsy values like `0`, which might lead to unintended behavior when setting default values.

---

# Nullish Coalescing Operator (??)

**Introduction**

- It is designed to set default values, addressing limitations of the OR (`||`) operator.

**Comparison with the OR Operator**

- **OR Operator (`||`)**:

  - Sets a default value if the first operand is a falsy value (e.g., `0`, `""`, `null`, `undefined`).
  - Example:
    - `let guests = restaurant.numGuests || 10;`
    - This returns `10` if `numGuests` is falsy (including `0`).

- **Nullish Coalescing Operator (`??`)**:
  - Only considers `null` and `undefined` as "nullish" values.
  - Does not treat `0` or `""` as nullish, thus preserving those values.
  - Example:
    - `let guests = restaurant.numGuests ?? 10;`
    - This returns `10` only if `numGuests` is `null` or `undefined`.

**Behavior of the Nullish Coalescing Operator**

- Nullish Values:
  - The operator evaluates to the right operand only if the left operand is `null` or `undefined`.
  - If the left operand is a valid value (including `0` or `""`), it is returned immediately.

**Practical Examples**

- If `numGuests` is `0`, using `??` will return `0`:

  - `let guests = restaurant.numGuests ?? 10;`
  - If `numGuests` is `0`, `guests` will be `0`.

- If `numGuests` is `undefined`, it will return the default value:
  - `let guests = restaurant.numGuests ?? 10;`
  - If `numGuests` is `undefined`, `guests` will be `10`.

**Conclusion**

- The nullish coalescing operator is a useful addition to JavaScript, allowing for more precise handling of default values.
- It effectively resolves issues that arise with using the OR operator when dealing with falsy values like `0` and empty strings.

Here are the notes on logical assignment operators in JavaScript:

---

# Logical Assignment Operators in JavaScript ( ||= , &&= , ??=)

- These operators combine logical operations with assignment.

## Overview of Logical Assignment Operators

1. **OR Assignment Operator (`||=`)**:

   - Assigns a value to a variable if the variable is currently falsy.
   - Syntax: `variable ||= value`
   - Example:
     ```javascript
     restaurant1.numGuests = restaurant1.numGuests || 10;
     // Same as :
     restaurant1.numGuests ||= 10; // Sets numGuests to 10 if it's falsy (e.g., undefined, 0).
     ```

2. **Nullish Assignment Operator (`??=`)**:

   - Assigns a value to a variable only if the variable is nullish (`null` or `undefined`).
   - Syntax: `variable ??= value`
   - Example:
     ```javascript
     restaurant2.numGuests ??= 10; // Sets numGuests to 10 only if it's null or undefined.
     ```

3. **AND Assignment Operator (`&&=`)**:
   - Assigns a value to a variable if the variable is currently truthy.
   - Syntax: `variable &&= value`
   - Example:
     ```javascript
     restaurant1.owner = restaurant1.owner && "Anonymous";
     // same as this but when restaurant1.owner is not defined it will not assign undefine to the restaurant1.owner
     restaurant1.owner &&= "Anonymous"; // Replaces owner with "Anonymous" if it exists.
     ```

## Practical Examples

- **Using the OR Assignment Operator**:

  - If `numGuests` is falsy (e.g., `0`), it gets assigned a default value (e.g., `10`).
  - Example:
    ```javascript
    restaurant1.numGuests ||= 10; // If numGuests is 0, it gets set to 10.
    ```

- **Using the Nullish Assignment Operator**:

  - Ensures that if `numGuests` is `null` or `undefined`, it gets a default value.
  - Example:
    ```javascript
    restaurant2.numGuests ??= 10; // Only assigns 10 if numGuests is null or undefined.
    ```

- **Using the AND Assignment Operator**:
  - Useful for setting values conditionally based on the current truthiness of a variable.
  - Example:
    ```javascript
    restaurant1.owner &&= "Anonymous"; // Changes owner to "Anonymous" if it exists.
    ```

# Overview of the `for-of` Loop

- **Introduction**: The `for-of` loop
- **Purpose**: It allows you to loop through the elements of an array without needing to manage counters or conditions.

## Basic Structure

- **Syntax**:
  ```javascript
  for (let item of array) {
    // Code to execute for each item
  }
  ```
- **Example**: To loop over a menu array:
  ```javascript
  let menu = [...]; // Assume this is an array
  for (let item of menu) {
      console.log(item);
  }
  ```

## Benefits of the `for-of` Loop

- **Simplicity**: No need to set up a counter or condition; just specify the variable and the array.
- **Direct Access**: Each iteration directly provides access to the current element, making the code cleaner and easier to read.
- **Continue and Break**: You can still use the `continue` and `break` keywords within a `for-of` loop.

## Accessing Indexes

- **Limitations**: The `for-of` loop does not provide the current index directly.
- **Workaround**: To access both the index and the element, use `Array.entries()`=> this method returns an array => each element of array is [index , value]
- **Destructuring**: You can destructure the entries to get both the index and element:

  ```javascript
  for (let [index, item] of menu.entries()) {
    console.log(index, item);
  }
  ```

## Conclusion

- The `for-of` loop greatly simplifies array iteration in JavaScript, making the code more readable and less error-prone.
- It is particularly useful when you only need access to the elements of an array without the need for the index.

# enhanced object literals

Here are the notes on Enhanced Object Literals in JavaScript:

### Introduction

- **Enhanced Object Literals**: A feature introduced in ES6 that simplifies the syntax for defining object literals.

### Key Enhancements

1. **Property Name Shorthand**:

   - If a property name is the same as the variable name, you can omit the key.
   - **Example**:
     ```javascript
     const openingHours = {
       /* ... */
     };
     const restaurant = { openingHours }; // Shorthand
     ```

2. **Method Definitions**:

   - You can define methods without using the `function` keyword.
   - **Example**:
     ```javascript
     const restaurant = {
       order() {
         /* ... */
       }, // Simplified method definition
     };
     ```

3. **Computed Property Names**:
   - You can use expressions in square brackets to define property names dynamically.
   - **Example**:
     ```javascript
     const weekdays = ["Mon", "Tue", "Wed", "Thu", "Fri"];
     const openingHours = {
       [weekdays[0]]: "9 AM - 5 PM", // Dynamically computed property name
       ["Day - " + (4 + 2)]: "10 AM - 6 PM",
     };
     ```

### Benefits

- **Reduced Redundancy**: Less boilerplate code, making it cleaner and more readable.
- **Dynamic Flexibility**: Ability to compute property names enhances the utility of objects.

### Conclusion

- Enhanced object literals streamline object creation in JavaScript, improving code efficiency and readability.

# Optional Chaining

- **Definition**: allows developers to access properties of objects or arrays safely, without the risk of encountering errors when properties are undefined or null.
  check value of right side exist (it's not null or undefined) ? =Yes=> execute right side | =NO=> return undefined

#### Understanding the Concept

- **Basic Usage**:
  - Instead of using traditional checks (e.g., `if` statements), optional chaining uses the `?.` operator.
  - Example: Accessing a restaurant's opening hours can be done with `restaurant.openingHours?.mon`, which returns `undefined` if `openingHours` or `mon` is not available.

#### Benefits of Optional Chaining

- **Error Prevention**: Prevents runtime errors when trying to access properties of `undefined` or `null`.
- **Cleaner Code**: Reduces clutter by eliminating the need for multiple checks.
- **Readability**: Makes the intention of the code clearer.

#### How It Works

- **Syntax**: The optional chaining operator is written as `?.`.
  - Example: `object.property?.subProperty` checks if `property` exists before accessing `subProperty`.
- **Nullish Concept**: A property is considered to exist if it is neither `null` nor `undefined`. Values like `0` or an empty string are valid.

#### Practical Examples

1. **Accessing Properties**:

   - Example of accessing restaurant opening hours for Monday Without ERROR:
     ```javascript
     r;
     // ERROR without chaining
     //  restaurant.openingHours be undefined we will read property of undefined value so we have error
     const hours = restaurant.openingHours.mon;
     // This will only read mon property if restaurant.openingHours is not undefined
     const hours = restaurant.openingHours?.mon; // Returns undefined if not present
     // Old school way
     if (restaurant.openingHours) hours = restaurant.openingHours.mon;
     ```

2. **Handling Nested Objects**:

   - Optional chaining is particularly useful with nested structures:
     ```javascript
     const openTime = restaurant.openingHours?.mon?.open; // Safely accesses
     // Old school way
     if (restaurant.openingHours && restaurant.openingHours.mon)
       openTime = restaurant.openingHours.mon.open;
     ```

3. **Method Calls**:

   - You can also call methods conditionally:
     ```javascript
     restaurant.order?.(0, 1); // Calls order only if it exists
     ```

4. **Using with Arrays**:
   - Check if an array is empty and access elements safely:
     ```javascript
     const firstUserName = users[0]?.name; // Returns undefined if users is empty or undefined
     // OLD SCHOOL WAY
     if (user.length > 0) console.log(user[0].name);
     else console.log("Array is Empty");
     ```

#### Combining with Other Operators

- **Nullish Coalescing Operator (`??`)**:

  - Use this in conjunction with optional chaining to provide default values:

    ```javascript
    const daysOfWeek = ["sat", "sun", "mon", "tue", "wed", "thu", "fri"];

    for (const i of daysOfWeek) {
      const open = restaurant.openingHours[i]?.open ?? "Closed"; // if undefiend value is closed
      console.log(`${i} ${open}`);
    }
    ```

#### Real-World Applications

- **Web APIs**: When fetching data from APIs, not all properties may be guaranteed. Optional chaining allows safe access without extensive checks.
- **Deeply Nested Structures**: Useful for applications with complex data structures where many properties might be optional.

Here are detailed notes on looping through objects in JavaScript based on the speech:

# Looping Over Objects in JavaScript

#### Introduction

- **For-of Loop**: Previously learned for looping over arrays (which are iterable).
- **Objects**: Unlike arrays, objects are not iterable directly, but we can loop over them indirectly.

#### Looping Options

- We can choose to loop over:
  - **Property Names (Keys)**
  - **Property Values**
  - **Both Keys and Values (Entries)**

### Looping Over Property Names (Keys)

- **Using Object.keys()**:
  - To loop over property names, we use `Object.keys(object)` which returns an array of the object's keys.
  - Example:
    ```javascript
    openingHours: {
    thu: {
      open: 12,
      close: 22,
    },
    fri: {
      open: 11,
      close: 23,
    },
    sat: {
      open: 0, // Open 24 hours
      close: 24,
    },
    },
    const days = Object.keys(openingHours);
    console.log(days); // Output: ["Thursday", "Friday", "Saturday"]
    ```
- **Counting Properties**:
  - We can count how many properties are in the object:
    ```javascript
    console.log(`We are open on ${days.length} days.`); // Output: "We are open on 3 days."
    ```

### Looping Over Property Values

- **Using Object.values()**:
  - To get the values of an object, we use `Object.values(object)` which returns an array of the object's values.
  - Example:
    ```javascript
    const values = Object.values(openingHours);
    console.log(values); // Output: [ { open: 12, close: 22 }, ... ]
    ```

### Looping Over Both Keys and Values (Entries)

- **Using Object.entries()**:
  - To get both keys and values, we use `Object.entries(object)` which returns an array of key-value pairs.
  - The key-value pairs are represented as arrays within the main array.
  - Example:
    ```javascript
    const entries = Object.entries(openingHours);
    console.log(entries); // Output: [["Thursday", { open: 12, close: 22 }], ...]
    ```

### Destructuring in Looping

- **Destructuring**:
  - While looping through entries, we can destructure the array to easily access keys and values:
    ```javascript
    for (const [day, { open, close }] of Object.entries(openingHours)) {
      console.log(`On ${day}, we open at ${open} and close at ${close}.`);
    }
    ```

### Summary

- **Key Methods**:
  - `Object.keys(object)`: Retrieves an array of property names.
  - `Object.values(object)`: Retrieves an array of property values.
  - `Object.entries(object)`: Retrieves an array of key-value pairs.
- **Looping**: Use `for-of` to iterate through arrays returned by these methods, allowing for easy access to keys and values through destructuring.

### Conclusion

- Understanding how to loop over objects using `Object.keys()`, `Object.values()`, and `Object.entries()` is crucial for effective manipulation of object data in JavaScript.

This overview covers the essential points regarding looping through objects and demonstrates how to access keys, values, and entries effectively.

Here are the complete notes from the speech about JavaScript, focusing on Sets:

# JavaScript Sets Overview

- **Introduction to Data Structures**:
  - Historically, JavaScript had limited built-in data structures (primarily objects and arrays).
  - ES6 introduced two new structures: **Sets** and **Maps**.

### What is a Set?

- A **Set** is a collection of unique values, meaning:
  - No duplicates are allowed.
  - Useful for situations where uniqueness is required.

### Creating a Set

- To create a Set:
  ```javascript
  const ordersSet = new Set(iterable);
  ```
- Commonly, an **array** is used as the iterable.
- Example of creating a Set with strings:
  ```javascript
  const orders = ["pasta", "pizza", "pizza", "risotto", "pasta", "pizza"];
  const ordersSet = new Set(orders);
  console.log(ordersSet); // Outputs: Set { "pasta", "pizza", "risotto" }
  ```

### Properties of Sets

- Sets resemble arrays but do not maintain order and do not have key-value pairs.
- Sets are **iterable** but do not allow indexing.

### Working with Sets

1. **Size of a Set**:

   - Use `set.size` to get the number of unique elements.
   - In array we use `array.length`

   - Example:
     ```javascript
     // we can also convert strings to sets => because they are iterable too
     const myName = "sajjad";
     const myNameUniqueLetters = new Set(myName).size;
     ```

2. **Checking for Existence**:

   - Use `set.has(value)` to check if a value exists in the Set.
   - In array we use `array.includes(value)`
   - Example:
     ```javascript
     console.log(ordersSet.has("pizza")); // true
     console.log(ordersSet.has("bread")); // false
     ```

3. **Adding Elements**:

   - Use `set.add(value)` to add new elements.
   - In array we use `array.push(value)`
   - Duplicates are ignored.
   - Example:
     ```javascript
     ordersSet.add("garlic bread"); // Adds garlic bread
     ```

4. **Deleting Elements**:

   - Use `set.delete(value)` to remove an element.
   - In array we use `array.pop(value)`
   - Example:
     ```javascript
     ordersSet.delete("risotto"); // Removes risotto
     ```

5. **Clearing a Set**:
   - Use `set.clear()` to remove all elements from the Set.

### Retrieving Values

- You cannot retrieve values by index (like arrays) because Sets do not maintain order.
- The only way to check for values is using `set.has(value)`.

### Practical Use Cases

- Sets are commonly used to remove duplicate values from arrays:
  ```javascript
  const staff = ["waiter", "chef", "waiter", "manager", "chef", "waiter"];
  const uniqueStaff = [...new Set(staff)]; // ["waiter", "chef", "manager"]
  ```

### Conclusion

- Sets are not a replacement for arrays; use arrays when order and duplicates matter.
- Sets are beneficial for handling unique values.
- Remember to leverage the straightforward methods provided by Sets for ease of use.

These notes summarize the key points from the speech regarding JavaScript Sets, their creation, properties, methods, and practical applications.

Here are the comprehensive notes from the speech about JavaScript Maps, including code examples:

# Introduction to Maps

- **Concept**: Maps are a new data structure in JavaScript that are more useful than sets.
- **Definition**: A map allows mapping values to keys, similar to how objects work but with key-value pairs.

## Key Features of Maps

- **Key Types**: In maps, keys can be of any data type (e.g., objects, arrays), whereas in objects, keys are typically strings.

### Creating Maps

- Use the `Map` constructor to create an empty map:
  ```javascript
  const rest = new Map();
  ```

### Adding Entries

- Use the `set` method to add key-value pairs:
  ```javascript
  rest.set("name", "Classico Italiano");
  rest.set(1, "Firenze, Italy");
  rest.set(2, "Lisbon, Portugal");
  ```

### Updating Maps

- The `set` method updates the map and returns it, allowing for method chaining:
  ```javascript
  rest
    .set("categories", ["Italian", "Pizzeria"])
    .set("open", 11)
    .set("close", 23);
  ```

## Reading from Maps

- Use the `get` method to retrieve values by key:
  ```javascript
  console.log(rest.get("name")); // Output: Classico Italiano
  ```

### Key Data Types

- The data type of the key matters:
  ```javascript
  console.log(rest.get(1)); // Output: Firenze, Italy
  console.log(rest.get("1")); // Output: undefined
  ```

## Using Boolean Keys

- You can use Boolean values as keys to determine if a restaurant is open:

  ```javascript
  const currentTime = 21; // 9 PM
  rest.set(true, "We are open");
  rest.set(false, "We are closed");

  const isOpen =
    currentTime > rest.get("open") && currentTime < rest.get("close");
  console.log(rest.get(isOpen)); // Output: We are open
  ```

## Additional Map Methods and Properties

1. **`has` Method**: Check if a specific key exists in the map:

   ```javascript
   console.log(rest.has("categories")); // Output: true
   ```

2. **`delete` Method**: Remove a key-value pair from the map:

   ```javascript
   rest.delete(2); // Removes Lisbon location
   ```

3. **`size` Property**: Get the number of elements in the map:

   ```javascript
   console.log(rest.size); // Output: 7
   ```

4. **`clear` Method**: Remove all elements from the map:
   ```javascript
   rest.clear(); // Now the map is empty
   console.log(rest.size); // Output: 0
   ```

## You Can use set Methods

    ```js
    gameEvents.entries(); //same as [...gameEvents]
    gameEvents.values(); // {value1 , value2 , ...}
    gameEvents.keys(); // {key1 , key2 , ...}
    ```

## Comparison with Objects

- **Performance**: Maps provide better performance for adding and removing elements compared to objects.
- **Object Deletion**: Objects use the `delete` operator, which is generally slower:
  ```javascript
  const obj = { name: "Classico Italiano" };
  delete obj.name; // Slower than using map.delete()
  ```

## Advanced Key Usage

- **Using Objects and Arrays as Keys**:

  ```javascript
  const keyArr = [1, 2];
  rest.set(keyArr, "Test Value");

  console.log(rest.get(keyArr)); // Output: Test Value
  ```

### Key Retrieval

- To retrieve values correctly, the same reference must be used:

  ```javascript
  // Incorrect way (Not the same reference)
  rest.set([1, 2], "Test Value");
  console.log(rest.get([1, 2])); // OUTPUT : Undefined

  // Correnct way (The same reference)
  const anotherArr = [1, 2];
  rest.set(anotherArr, "Test Value");
  console.log(rest.get(anotherArr)); // Output: undefined
  ```

## Practical Demonstrations

- **Using DOM Elements as Keys**:

  ```javascript
  const h1 = document.querySelector("h1"); // h1 is an object
  rest.set(h1, "heading"); // map key is object

  console.log(rest.get(h1)); // Output: heading
  ```

## Conclusion

- **Flexibility**: Maps offer flexibility and advanced functionality in JavaScript.
- **Summary**: The lecture covers the creation, manipulation, and various methods of maps, with practical examples and use cases.

## Populating Maps

- Alternative way to populate a map without using the `set` method.
- Preferred when dealing with many values, as `set` can be cumbersome.

## Creating a Quiz Map

- A new map can be created by passing an array of arrays.
- Each inner array consists of a key (first position) and a value (second position).

### Example

```javascript
const questionMap = new Map([
  ["Question", "What is the best programming language in the world?"],
  [1, "C"],
  [2, "Java"],
  [3, "JavaScript"],
  ["Correct", 3], // Correct answer
  [true, "Correct"],
  [false, "Try Again"],
]);
```

## Structure Similarity

- The structure of an array of arrays is similar to the output of `Object.entries()`.
- This structure allows easy conversion from objects to maps.

### Converting Objects to Maps

- The conversion can be performed using:

```javascript
const openingHours = {
  mon: "10:00-18:00",
  tue: "10:00-18:00",
};

const ourMap = new Map(Object.entries(openingHours));
```

## Iterating Over Maps

- Maps are iterable, allowing the use of loops.
- A `for` loop can print options from the map.
- Use destructuring to separate keys and values.

### Example

```javascript
for (let [key, value] of questionMap) {
  if (typeof key === "number") {
    console.log(`Answer ${key}: ${value}`);
  }
}
```

## Converting Maps to Arrays

- Maps can also be converted back to arrays (array of arrays) using the spread operator.

### Example

```javascript
const arrayFromMap = [...questionMap]; // Convert map to array
console.log(arrayFromMap);
```

## Conclusion

- Understanding when to use maps versus objects is crucial.
- Future lessons will cover the differences between various data structures, including arrays, maps, and sets.

These notes summarize the key points discussed in the speech regarding JavaScript maps, along with code examples to illustrate their usage.

# Working with Strings in JavaScript

### Introduction to Strings

- Strings are a fundamental data type in JavaScript used to represent text.
- Common operations include accessing individual characters, measuring length, and using various string methods.

### Key Concepts

1. **Accessing Characters**

   - Strings can be indexed like arrays.
   - Example:
     ```javascript
     let plane = "A320";
     console.log(plane[0]); // Outputs: A
     console.log(plane[1]); // Outputs: 3
     ```

2. **String Length**

   - Use the `.length` property to get the number of characters.
   - Example:
     ```javascript
     let airline = "TAP Air Portugal";
     console.log(airline.length); // Outputs: 15
     ```

3. **String Methods**
   - Strings have methods similar to arrays.

#### Common String Methods

- **`indexOf()`**: Finds the index of the first occurrence of a specified character or substring.

  - Example:
    ```javascript
    console.log(airline.indexOf("r")); // Outputs: 6\
    console.log(airline.indexOf("Air")); // Search for a word (Case sensitive)
    ```

- **`lastIndexOf()`**: Finds the index of the last occurrence of a specified character or substring.

  - Example:
    ```javascript
    console.log(airline.lastIndexOf("a")); // Outputs: 10
    ```

- **`slice()`**: Extracts a portion of a string based on start and end indices.

  - this does not change the underlying string.That's because it's actually impossible to mutate strings. They are primitives so you should store the return value in a new variable.
  - Example:

    ```javascript
    //slice(start , end)
    console.log(airline.slice(4)); // Outputs: "Air Portugal"
    console.log(airline.slice(0, 3)); // Outputs: "TAP" ( index of 0,1,2 and not 3)
    ```

- **Negative Indices**: You can use negative indices to start counting from the end of the string.
  - Example:
    ```javascript
    // last index is -1
    console.log(airline.slice(-8)); // Outputs: "Portugal"
    console.log(airline.slice(0, -8)); // Outputs: "TAP Air "
    ```

### Extracting Substrings

- To extract parts of a string without hard-coding indices, use `indexOf()` and `lastIndexOf()` to dynamically find positions.

#### Example: Extracting the First and Last Word

```javascript
let airline = "TAP Air Portugal";
let firstWord = airline.slice(0, airline.indexOf(" "));
let lastWord = airline.slice(airline.lastIndexOf(" ") + 1);
console.log(firstWord); // Outputs: "TAP"
console.log(lastWord); // Outputs: "Portugal"
```

### Practical Example: Checking Middle Seats

- A function that checks if a seat in an airplane is a middle seat (B or E).

```javascript
function checkMiddleSeat(seat) {
  const lastCharacter = seat.slice(-1);
  if (lastCharacter === "B" || lastCharacter === "E") {
    console.log("You got the middle seat 😬");
  } else {
    console.log("You got lucky! 😎");
  }
}

// Test the function
checkMiddleSeat("23C"); // Outputs: You got lucky! 😎
checkMiddleSeat("3E"); // Outputs: You got the middle seat 😬
```

## How premitive dataTypes have methodes ?

data types like strings are primitive. However, JavaScript allows you to use methods on strings because it temporarily wraps the string primitive in a `String` object when you call a method on it. Here's how it works under the hood:

### Example:

```javascript
let str = "Hello, World!";
console.log(str.toUpperCase()); // Output: "HELLO, WORLD!"
```

### How it Works:

1. **Temporary Object Creation**: When you call a method like `toUpperCase()`, JavaScript internally creates a `String` object from the primitive value.

   - For example, `"Hello, World!"` is wrapped in an object equivalent to `new String("Hello, World!")`.

2. **Method Execution**: The method, such as `toUpperCase()`, is executed on this temporary object and return string as result.

3. **Garbage Collection**: The temporary `String` object is discarded after the method execution, and you're left with the result of the method.

### Why This Design?

- JavaScript was designed to have primitive types like `string`, `number`, and `boolean` for simplicity and performance.
- Methods and properties associated with these types are implemented via their corresponding wrapper objects: `String`, `Number`, and `Boolean`.

### Wrapper Objects:

Each primitive type has a corresponding wrapper object that provides methods:

| Primitive Type | Wrapper Object |
| -------------- | -------------- |
| `string`       | `String`       |
| `number`       | `Number`       |
| `boolean`      | `Boolean`      |

### Example with Explicit Wrapper:

You can manually create a `String` object, but it's usually unnecessary:

```javascript
let strPrimitive = "Hello";
let strObject = new String("Hello");

console.log(typeof strPrimitive); // "string"
console.log(typeof strObject); // "object"

// Accessing a method
console.log(strPrimitive.toLowerCase()); // "hello"
console.log(strObject.toLowerCase()); // "hello"
```

**Note**: Avoid using `new String` unless you specifically need an object (which is rare), as it can lead to unexpected results when comparing values:

```javascript
let strPrimitive = "Hello";
let strObject = new String("Hello");

console.log(strPrimitive === strObject); // false (different types)
```

### Summary:

You can use methods on strings because JavaScript temporarily converts the string primitive into a `String` object to provide the functionality, ensuring a seamless experience.

Here are comprehensive notes based on the provided speech about JavaScript string methods, including examples:

# Working with Strings in JavaScript (Part 2)

### String Case Manipulation

1. **Changing Case**
   - **`toLowerCase`**: Converts a string to lowercase.
     ```javascript
     let airline = "AirlineName";
     console.log(airline.toLowerCase()); // Output: airline name
     ```
   - **`toUpperCase`**: Converts a string to uppercase.
     ```javascript
     console.log(airline.toUpperCase()); // Output: AIRLINE NAME
     ```

### Practical Example: Fixing Passenger Names

- **Fix Capitalization**
  1. Convert the entire name to lowercase.
     ```javascript
     let passenger = "jOhn DoE";
     const passengerLower = passenger.toLowerCase(); // "john doe"
     ```
  2. Capitalize the first letter and concatenate with the rest of the string.
     ```javascript
     const passengerCorrect =
       passengerLower[0].toUpperCase() + passengerLower.slice(1);
     console.log(passengerCorrect); // Output: John doe
     ```

### Checking User Input: Email Validation

1. **Normalize Email**
   - Convert to lowercase and trim spaces.
   - trim() method will remove all white spaces
   ```javascript
   let loginEmail = "  Hello@Jonas.IO  /n";
   const normalizedEmail = loginEmail.toLowerCase().trim();
   console.log(normalizedEmail); // Output: hello@jonas.io
   ```

### Replacing Parts of Strings

1. **Basic Replacement**

   - **`replace`**: Replaces the first occurrence of a substring.
     ```javascript
     let priceGreatBritain = "288,97 pounds";
     let priceUS = priceGreatBritain
       .replace("pounds", "dollars")
       .replace(",", ".");
     console.log(priceUS); // Output: 288.97 dollars
     ```

2. **Replacing All Occurrences**
   - **`replaceAll`**: Replaces the All occurrence of a substring.
   - Also you can use **Regular Expressions** for global replacements.
   ```javascript
   let announcement = "Door 23 ,All passengers come to boarding door 23.";
   let updatedAnnouncement = announcement.replace(/door/g, "gate");
   console.log(updatedAnnouncement); // Output: gate 23 ,All passengers come to boarding gate 23.
   ```

### Boolean Methods

1. **`includes`**: Checks if a string contains a substring.

   ```javascript
   let plane = "A320neo";
   console.log(plane.includes("A320")); // Output: true
   console.log(plane.includes("Boeing")); // Output: false
   ```

2. **`startsWith`**: Checks if a string starts with a specific substring.

   ```javascript
   console.log(plane.startsWith("Airbus")); // Output: false
   console.log(plane.startsWith("A320")); // Output: true
   ```

3. **`endsWith`**: Checks if a string ends with a specific substring.
   ```javascript
   console.log(plane.endsWith("neo")); // Output: true
   ```

### Summary

- JavaScript provides various methods to manipulate strings, including changing their case, normalizing user input, replacing parts of strings, and checking for specific conditions using boolean methods.
- These methods are essential for handling user input, formatting data, and ensuring the accuracy of string operations in applications.

# Working with Strings in JavaScript (Part 3)

Here are comprehensive notes on working with strings in JavaScript, based on the provided speech:

### 2. **Using the `split()` Method**

- **Definition**: `split()` divides a string into an array based on a specified divider.
- **Example**:
  ```javascript
  const str = "A+very+nice+string";
  const result = str.split("+");
  console.log(result); // Outputs: ["A", "very", "nice", "string"]
  ```

### 3. **Destructuring with `split()`**

- You can directly assign the results of `split()` to variables using destructuring.
- **Example**:
  ```javascript
  const myName = "John Doe";
  const [firstName, lastName] = myName.split(" ");
  console.log(firstName); // Outputs: John
  console.log(lastName); // Outputs: Doe
  ```

### 4. **Using the `join()` Method**

- **Definition**: `join()` combines elements of an array into a string with a specified separator.
- **Example**:
  ```javascript
  const nameArray = ["Mr.", "John", "DOE"];
  const fullName = nameArray.join(" ");
  console.log(fullName); // Outputs: "Mr. John DOE"
  ```

### 5. **Combining `split()` and `join()`**

- This combination allows for powerful string manipulations.
- **Example**:
  ```javascript
  const sentence = "Hello, how are you?";
  const words = sentence.split(" ");
  const newSentence = words.join("-");
  console.log(newSentence); // Outputs: "Hello,-how-are-you?"
  ```

### 6. **Capitalizing Names**

- To capitalize the first letter of each word in a name:
- **Example**:
  ```javascript
  function capitalizeName(name) {
    return name
      .split(" ")
      .map((word) => word[0].toUpperCase() + word.slice(1).toLowerCase())
      .join(" ");
  }
  console.log(capitalizeName("jessica ann smith")); // Outputs: "Jessica Ann Smith"
  ```

### 7. **Padding Strings**

- **Definition**: Padding adds characters to a string until it reaches a desired length.
- **Methods**: `padStart()` and `padEnd()`.
- **Example**:
  ```javascript
  const message = "go to gate 23";
  console.log(message.padStart(25, "+")); // Outputs: "++++++++++++go to gate 23" (25 charachters)
  console.log(message.padEnd(30, "+")); // Outputs: "go to gate 23++++++++++++++++++" (30 charachters)
  ```

### 8. **Masking Credit Card Numbers**

- Example function to mask credit card numbers, displaying only the last four digits:
- **Example**:
  ```javascript
  function maskCreditCard(number) {
    number = number + ""; // convert number to string(Type Coercion)
    visibleNumber = number.slice(-4);
    return visibleNumber.padStart(number.length, "*");
  }
  console.log(maskCreditCard(1234567812345678)); // Outputs: "************5678"
  ```

### 8. **Using the `repeat()` Method**

- **Definition**: `repeat()` creates a new string by repeating the original string a specified number of times.
- **Example**:
  ```javascript
  const str = "Hello ";
  const repeatedStr = str.repeat(3);
  console.log(repeatedStr); // Outputs: "Hello Hello Hello "
  ```

### 10. **Conclusion**

- The string manipulation methods in JavaScript, such as `split()`, `join()`, `padStart()`, `padEnd()`, repeat() and others, can be combined creatively to perform complex operations efficiently.

These notes summarize the key points and examples discussed in the speech, providing a clear overview of working with strings in JavaScript.

# summarizing the string methods

| **Method**        | **Syntax**                                          | **Definition**                                                                                     |
|-------------------|-----------------------------------------------------|----------------------------------------------------------------------------------------------------|
| `includes()`      | `string.includes(searchString)`                     | Determines whether a string contains a specified substring, returning `true` or `false`.          |
| `startsWith()`    | `string.startsWith(searchString)`                   | Checks if a string starts with a specified substring, returning `true` or `false`.                |
| `endsWith()`      | `string.endsWith(searchString)`                     | Checks if a string ends with a specified substring, returning `true` or `false`.                  |
| `indexOf()`       | `string.indexOf(searchValue)`                       | Returns the index of the first occurrence of a specified substring, or `-1` if not found.         |
| `lastIndexOf()`   | `string.lastIndexOf(searchValue)`                   | Returns the index of the last occurrence of a specified substring, or `-1` if not found.          |
| `split()`         | `string.split(separator)`                           | Divides a string into an array of substrings based on a specified separator.                      |
| `join()`          | `array.join(separator)`                             | Combines the elements of an array into a single string, using a specified separator between each element. |
| `replace()`       | `string.replace(searchValue, newValue)`            | Returns a new string with some or all matches of a pattern replaced by a replacement.            |
| `replaceAll()`    | `string.replaceAll(searchValue, newValue)`         | Returns a new string with all matches of a pattern replaced by a replacement.                     |
| `repeat()`        | `string.repeat(count)`                              | Creates a new string by repeating the original string a specified number of times.                |
| `padStart()`      | `string.padStart(targetLength, padString)`         | Pads the current string with another string (padString) from the start until the target length is reached. |
| `padEnd()`        | `string.padEnd(targetLength, padString)`           | Pads the current string with another string (padString) from the end until the target length is reached. |
| `slice()`         | `string.slice(start, end)`                          | Extracts a section of a string and returns it as a new string, without modifying the original string. |
| `toUpperCase()`   | `string.toUpperCase()`                              | Converts all the characters in a string to uppercase.                                            |
| `toLowerCase()`   | `string.toLowerCase()`                              | Converts all the characters in a string to lowercase.                                            |
| `trim()`          | `string.trim()`                                     | Removes whitespace from both ends of a string.                                                   |

