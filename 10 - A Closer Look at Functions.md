# Default Parameters in JavaScript

### 1. **Introduction to Default Parameters**

- Default parameters allow functions to have preset values for certain parameters. If no value is provided during the function call, the default value is used.

### 2. **Function Without Default Parameters**

- Initially, a basic function is created without default parameters. The parameters must be passed explicitly each time the function is called. and if we don't pass parameters to function they will be `undefined` .

```javascript
function createBooking(flightNumber, numPassengers, price) {
  const booking = {
    flightNumber,
    numPassengers,
    price,
  };
  return booking; // {flightNumber : LH23 , numPassengers : undefined , price : undefined}
}
createBooking("LH23");
```

### 3. **Short Circuiting for Default Values (Old Method)**

- Before ES6, default values were set using logical OR (`||`). For example:

```javascript
function createBooking(flightNumber, numPassengers, price) {
  numPassengers = numPassengers || 1; // Default to 1 if not provided
  price = price || 199; // Default to 199 if not provided
  const booking = { flightNumber, numPassengers, price };

  return booking;
}
```

### 4. **Using Default Parameters in ES6**

- In ES6, you can directly assign default values in the function parameter list:

```javascript
function createBooking(flightNumber, numPassengers = 1, price = 199) {
  const booking = { flightNumber, numPassengers, price };
  console.log(booking);
  return booking;
}
```

### 5. **Overriding Default Values**

- Default values can be overridden by providing arguments when calling the function:

```javascript
createBooking("LH 123", 2, 800); // Overrides defaults
// Outputs: { flightNumber: "LH 123", numPassengers: 2, price: 800 }
```

### 6. **Expressionss in Default Values**

- Default parameters can contain expressions, including calculations based on other parameters:

```javascript
function createBooking(
  flightNumber,
  numPassengers = 1,
  price = numPassengers * 199
) {
  const booking = { flightNumber, numPassengers, price };
  console.log(booking);
  return booking;
}
```

### 7. **Order of Parameters**

- When using default parameters, they must be defined in order. If `price` depends on `numPassengers`, `numPassengers` must be listed before `price`:

```javascript
createBooking("LH 123", 3); // Outputs: { flightNumber: "LH 123", numPassengers: 3, price: 597 }
```

### 8. **Skipping Parameters**

- You cannot skip parameters when calling a function. If you want to use a default value for a parameter while setting another, you can explicitly pass `undefined`:

```javascript
createBooking("LH 123", undefined, 800); // Keeps numPassengers at default
// Outputs: { flightNumber: "LH 123", numPassengers: 1, price: 800 }
```

# How Passing Arguments Works Value vs. Reference

Here are the updated notes, including the clarification about passing arguments in JavaScript:

### Notes: How Passing Arguments Works: Values vs. Reference

1. **Definitions**:

   - **Primitive Types**: For primitive data types (e.g., `number`, `string`, `boolean`, `null`, `undefined`, `symbol`, `bigint`), JavaScript always passes by value. This means that when you pass a primitive to a function, a copy of the value is made, and changes to the parameter inside the function do not affect the original variable.
   - **Reference Types**: JavaScript still uses pass-by-value, but the "value" being passed is a reference to the object. This means that if you modify the properties of the object inside a function, the changes are reflected in the original object because both the original variable and the function parameter point to the same object in memory.

2. **Code Example**:

   ```javascript
   const flight = "LH234";
   const jonas = {
     name: "Jonas Schmedtmann",
     passport: 24739479284,
   };
   ```

3. **Function: `checkIn`**:

   - Takes two parameters: `flightNum` (a primitive) and `passenger` (an object).
   - Modifies `flightNum` by assigning it a new value (`'LH999'`), but this does not affect the original `flight` variable.
   - Modifies the `name` property of the `passenger` object, which affects the original `jonas` object.
   - Checks the passport number and alerts based on its validity.

   ```javascript
   const checkIn = function (flightNum, passenger) {
     flightNum = "LH999"; // This change does not affect the flight variable
     passenger.name = "Mr. " + passenger.name; // This changes the original jonas object

     if (passenger.passport === 24739479284) {
       alert("Checked in");
     } else {
       alert("Wrong passport!");
     }
   };
   ```

4. **Effects of Function Call**:

   - If `checkIn(flight, jonas)` is called:
     - `console.log(flight)` will show `'LH234'` (unchanged).
     - `console.log(jonas)` will show `name: 'Mr. Jonas Schmedtmann'` (changed).

5. **Key Takeaways**:
   - **Clarification on JavaScript's Passing Mechanism**: JavaScript does not have true "pass-by-reference" behavior in the way some other programming languages (like C++ or Python) do. Instead, JavaScript employs pass-by-value semantics. When an object is passed, a reference to the object is passed, but the reference itself is a value that passed to the function.

# First-Class and Higher-Order Functions in JavaScript

## **First-Class Functions**:

- JavaScript has first-class functions, meaning functions are treated as first citizens.
- This means that function are simply values

1. **Functions as Objects**:

   - Functions are a type of object in JavaScript.
   - Since objects are values, functions can be stored in variables and object properties.
   - This property enables flexibility in how functions are used.

2. **Storing Functions**:

   - Functions can be assigned to variables, passed as arguments, and returned from other functions.
   - Example of storing a function:
     ```javascript
     const greet = function () {
       console.log("Hello!");
     };
     ```

3. **Passing Functions**:

   - Functions can be passed as arguments to other functions.
   - Example: `addEventListener` takes a function as an argument (callback function).
   - The callback function is executed later when an event occurs.
   -

4. **Returning Functions**:
   - Functions can also return other functions.
   - This allows for the creation of more complex and flexible code.
   - Example of a higher-order function returning another function:
     ```javascript
     const createGreeter = function (greeting) {
       return function (name) {
         console.log(greeting + ", " + name);
       };
     };
     // first createGreeter return a function and then we can store it or immediately call it
     // 1.Store returned funtion
     const = createGreeter("Hello")
     // 2.Call immediately
     createGreeter("Hello")("Sajjad")
     ```
     you can write functions with `arrow-function`
     ```js
     const createGreeter = (greeting) => (name) =>
       console.log(greeting + ", " + name);
     ```

## Higher-Order Functions:

- A higher-order function is one that either takes a function as an argument or returns a function.
- **Types of Higher-Order Functions**:
  - **Function that receives another function**: e.g., `addEventListener`.
  - **Function that returns a new function**: e.g., factory functions.

1. **Callback Functions**:

   - When a function is passed as an argument to another function, it is often called a callback function.
   - The higher-order function calls the callback function at a later time, typically in response to an event.

2. **Method Invocation**:
   - Functions can also have methods, similar to how objects have methods.
   - Example: The `bind` method allows you to set the value of `this` in a function.

## Distinction Between First-Class and Higher-Order Functions:

- **First-Class Functions**: A language feature indicating that functions are values.
- **Higher-Order Functions**: Practical implementations of functions that use other functions as arguments or return them.
- Understanding this distinction is important for mastering JavaScript.

**Importance of First-Class Functions**:

- The first-class nature of functions in programming langueg enables powerful functional programming techniques.
- Higher-order functions facilitate more abstract and modular code.

## **Conclusion**:

First-class functions are a fundamental concept in JavaScript, enabling higher-order functions.

# The call and apply Methods

Here are the complete notes from the speech about JavaScript's `this` keyword and the `call` and `apply` methods:

### Understanding the `this` Keyword

1. **Purpose of `this`**:

   - `this` refers to the object that is currently executing the function.
   - Understanding how `this` works is crucial for managing context in JavaScript.

2. **Example Scenario**:
   - Consider an airline object (e.g., Lufthansa) that has properties like `airline name`, `iataCode`, and an array for `bookings`.

### Creating an Airline Object

```javascript
const lufthansa = {
  airline: "Lufthansa",
  iataCode: "LH",
  bookings: [],
  book(flightNum, name) {
    console.log(
      `${name} booked a seat on ${this.airline} flight ${this.iataCode}${flightNum}`
    );
    this.bookings.push({ flight: `${this.iataCode}${flightNum}`, name });
  },
};
```

- **Method Explanation**:
  - The `book` method logs a message and adds a booking to the `bookings` array.
  - Uses `this` to access properties of the airline object.

### Booking Flights

```javascript
lufthansa.book(239, "Jonas Schmedtmann");
lufthansa.book(635, "John Smith");
```

- **Result**:
  - Two bookings are made for Lufthansa.

### Creating Another Airline Object

```javascript
const eurowings = {
  airline: "Eurowings",
  iataCode: "EW",
  bookings: [],
};
```

### Function Reference and the Problem with `this`

```javascript
const book = lufthansa.book;
// Does NOT work
book(23, "Sarah Williams");
```

- **Issue**:
  - `book` Function here it's now a copy of a method and not a method so we have just a regular function call so the `this` keyword points to `undefined`
  - Calling `book` directly loses the context of `this`, resulting in errors.

### Using the `call` Method

- **Syntax**: `function.call(thisArg, arg1, arg2, ...)`
- **Usage**:

```javascript
book.call(eurowings, 23, "Sarah Williams");
console.log(eurowings);
```

- **Result**:
  - Successfully books a flight for Eurowings by explicitly setting `this` to the `eurowings` object.

### Using the `apply` Method

- **Syntax**: `function.apply(thisArg, [argsArray])`
- **Example**:

```javascript
const flightData = [583, "George Cooper"];
book.apply(swiss, flightData);
console.log(swiss);
```

- **Result**:
  - Books a flight for Swiss by passing an array of arguments.

### Spread Operator with `call`

```javascript
book.call(swiss, ...flightData);
```

- **Explanation**:
  - The spread operator allows an array to be expanded into individual arguments, similar to `apply`. And nowdays we usually don't use `apply` method , we can just use `call` with spread

### Summary

- The `call` and `apply` methods are used to set the context (`this`) when calling functions.
- `call` accepts a list of arguments, while `apply` takes an array of arguments.
- Both methods enhance the flexibility of function calls, allowing the reuse of methods across different objects.

# The bind Method

### Overview of `bind`

- The `bind` method is used to set the `this` keyword for a function.
- Unlike `call`, which invokes the function immediately, `bind` returns a new function with `this` bound to a specific value.

### Key Differences Between `bind` and `call`

- **`call`**: Invokes the function immediately and sets `this`.
- **`bind`**: Returns a new function that can be called later, with `this` set to the specified value.

### Example: Using `bind` with Functions

```javascript
// Defining a function to book a flight
const book = function (flightNum, passengerName) {
  console.log(`Booking flight ${flightNum} for ${passengerName}`);
};

const eurowings = {
  airline: "Eurowings",
  iataCode: "EW",
  bookings: [],
};

// Bind the book function to specific airline objects
const bookEW = book.bind(eurowings);

// Using the bound function
bookEW(23, "Steven Williams");
```

### Using `bind` with Event Listeners

- When attaching event listeners, `this` may not refer to the expected object because in the event handler function the `this` always point to element on which that handler is attached to .
- Use `bind` to ensure `this` refers to the correct object.

```javascript
// Setting up an airline object
const lufthansa = {
  buyPlane() {
    this.planes++;
  },
};

//❎ Porblem : Here this refers to <button class="buy"></botton> and result is wrong
document.querySelector(".buy").addEventListener("click", lufthansa.buyPlane);

//✅ Solution : Use bind method to sepecify this value explicitly
document
  .querySelector(".buy")
  .addEventListener("click", lufthansa.buyPlane.bind(lufthansa));
```

#### Passing Arguments in Event Handlers

Event handlers receive only one argument: the `event` object. If you want to pass **additional arguments**, you can't directly pass them because the event handler is invoked by the browser with just the event argument.

To work around this, you can use `.bind()` to "preset" arguments or use a wrapper function.

---

**Example Using `.bind()`:**

```javascript
function handleClick(event, customMessage) {
  console.log(customMessage, event.type);
}

const button = document.createElement("button");
button.textContent = "Click me";

button.addEventListener(
  "click",
  handleClick.bind(null, "Button clicked!") // Bind preset argument
);

document.body.appendChild(button);
// When clicked: Output => "Button clicked! click"
```

Here:

- The first argument (`null`) is used because `this` isn't needed.
- `"Button clicked!"` is passed as the second argument, fixed in the bound function.

---

**Alternative Using a Wrapper Function:**

```javascript
function handleClick(event) {
  console.log("Button clicked!", event.type);
}

button.addEventListener("click", (event) => handleClick(event));
// This wrapper calls `handleClick` with the desired arguments.
```

---

**Incorrect Usage:**

If you directly call the function instead of passing it, the function is executed immediately, and whatever it returns is passed to the event listener, which is likely **not what you want**.

```javascript
function handleHover(event, opacity) {
  console.log(`Hovered with opacity: ${opacity}`);
}

navLinks.addEventListener("mouseover", handleHover(e, 0.5)); // Incorrect
```

This will not work because:

1. The `handleHover(e, 0.5)` function is **called immediately**, not passed as a reference.
2. Whatever `handleHover` returns (if anything) is passed as the event handler, which leads to incorrect behavior.

---

**Correct Approach Using `.bind()`:**

```javascript
function handleHover(event, opacity) {
  console.log(`Hovered with opacity: ${opacity}`);
}

navLinks.addEventListener("mouseover", handleHover.bind(null, 0.5)); // Correct
```

Here:

- `.bind(null, 0.5)` ensures that the function is passed as a reference and will be called with the `event` argument automatically provided by the browser.

---

**Correct Approach Using a Wrapper Function:**

```javascript
navLinks.addEventListener("mouseover", (event) => handleHover(event, 0.5));
```

Here:

- The wrapper function explicitly calls `handleHover` with both `event` and the additional argument (`0.5`).
- the `event` object is provided automatically by the browser when the event occurs, and it always appears as the first argument in the handler function.

---

### **Summary**

- Event handlers are invoked with only the `event` argument.
- Directly calling the handler function (e.g., `handleHover(e, 0.5)`) does not work because the function is executed immediately.
- Use `.bind()` to preset arguments or a wrapper function to explicitly call the handler with additional arguments.

### Partial Application

- `bind` can also be used for partial application, where some arguments are pre-set.
- **Syntax** `funtion.bind( ThisValue , FirstArgPreSet , secArgPreset , ... )`

```javascript
// Function to add tax
const addTax = (rate, value) => value + value * rate;

// Pre-setting first argument (tax rate) . now we have a new function that always "rate = 0.23"
const addVAT = addTax.bind(null, 0.23); // use null to don't specify any value for this
console.log(addVAT(100)); // Outputs: 123
```

### Conclusion

- The `bind` method is a powerful tool in JavaScript for controlling the context of `this` and for creating partially applied functions.
- Understanding how to use `bind` effectively can simplify code, especially when dealing with event listeners and functions that need specific context.

# Immediately Invoked Function Expressions (IIFE)

### Introduction to IIFE

- **Definition**: An Immediately Invoked Function Expression (IIFE) is a function that is executed right after it is defined.
- **Purpose**: It allows for the creation of a function that runs once and does not persist in memory.

### Why Use IIFE?

- **Single Execution**: Sometimes, we need a function that should only execute once and then disappear. This is useful for scenarios where we want to encapsulate code without polluting the global scope.

### Basic Structure of IIFE

1. **Function Expression**: An IIFE is not assigned to a variable; it is defined and executed immediately.
2. **Syntax**:
   ```javascript
   (function () {
     // Code to execute
   })();
   ```
   - The function is wrapped in parentheses to indicate it is an expression, not a declaration.

### Example of IIFE

- Running a simple IIFE that logs a message:
  ```javascript
  (function () {
    console.log("This will run immediately!");
  })();
  // we can also use funtion expression
  (() => {
    console.log("This will run immediately!");
  })();
  ```

### Error Handling

- If you try to define a function without wrapping it in parentheses, you will get an error:
  ```
  SyntaxError: Function statements require a function name
  ```

### Calling the IIFE

- After wrapping the function in parentheses, you can call it by adding another pair of parentheses:
  ```javascript
  (function () {
    console.log("Executed!");
  })();
  ```

### Benefits of IIFE

1. **Encapsulation**: Variables defined inside an IIFE are not accessible from the outside, providing data privacy.
2. **Scope Creation**: IIFEs create a new scope, preventing variable conflicts.

### Data Privacy

- Variables defined within an IIFE cannot be accessed from the global scope:
  ```javascript
  (function () {
    var privateVar = "I'm private";
  })();
  console.log(privateVar); // ReferenceError
  ```

### Comparison with Block Scope

- Since in ES6, `let` and `const` create their own scope inside a block An IIFE is not strictly necessary for creating a private scope anymore,but it is still useful for executing code immediately.
  ```js
  {
    const isPrivate : "Yes"
  }
  console.log(isPrivate) // We can't access it
  ```

### Modern Usage of IIFE

- While IIFEs were more common in older JavaScript, they are still valuable when you want to execute a function just once. For example, IIFEs are useful when initializing settings or configurations.

### Conclusion

- IIFEs are a powerful pattern in JavaScript for encapsulating code and creating private variables, especially useful when needing to execute a function immediately.
- This pattern helps protect variables from being overwritten and supports the concept of data encapsulation.Here are the complete notes from the speech about Immediately Invoked Function Expressions (IIFE) in JavaScript:

# Closure

Closures are one of the most powerful and fundamental concepts in JavaScript. Let’s break them down and explore them step by step with simple examples.

---

## **What is a Closure?**

A closure is a function that **remembers** the variables from its **outer scope** even after the outer function has finished executing. This means the function has "access to the variables of its parent scope."

---

## **Core Concepts**

1. **Lexical Scope:**
   JavaScript functions are executed in the scope where they were **defined**, not where they are **called**. This is the foundation of closures.

2. **Closure:**
   A function retains access to its lexical environment (the variables and functions in its outer scope) even after the outer scope has returned.

---

### **Example 1: Basic Closure**

```javascript
function outer() {
  let message = "Hello, I'm a closure!";

  function inner() {
    console.log(message); // Accesses `message` from `outer`
  }

  return inner;
}

const myClosure = outer(); // `outer` runs and returns `inner`
myClosure(); // Logs: "Hello, I'm a closure!"
```

**Explanation:**

- `inner` function is defined inside `outer`.
- Even though `outer` has finished executing, the returned `inner` function retains access to `message` because of closure.

---

### **Example 2: Counter with Closure**

Closures are often used to preserve state across function calls.

```javascript
function createCounter() {
  let count = 0; // Private variable

  return function () {
    count++; // Access and update the private variable
    console.log(count);
  };
}

const counter = createCounter(); // Returns the inner function
counter(); // Logs: 1
counter(); // Logs: 2
counter(); // Logs: 3
```

**Explanation:**

- The `createCounter` function creates a `count` variable and returns a function that increments it.
- The `count` variable is "remembered" by the returned function.

---

### **Example 3: Multiple Closures**

Each closure maintains its own separate copy of variables.

```javascript
function createAdder(x) {
  return function (y) {
    return x + y;
  };
}

const add5 = createAdder(5); // Creates a closure with `x = 5`
const add10 = createAdder(10); // Creates a closure with `x = 10`

console.log(add5(2)); // Logs: 7
console.log(add10(3)); // Logs: 13
```

**Explanation:**

- `createAdder` creates closures for each function call.
- Each closure "remembers" its own `x` value.

---

Here are the notes based on the provided speech and code examples:

## More examples for Closures

### Example 1: Function Reassignment and Closures

1. **Code Example**:

   ```javascript
   let f;

   const g = function () {
     const a = 23;
     f = function () {
       console.log(a * 2);
     };
   };

   const h = function () {
     const b = 777;
     f = function () {
       console.log(b * 2);
     };
   };

   g();
   f(); // Logs 46
   console.dir(f); // Shows function that logs a

   h();
   f(); // Logs 1554
   console.dir(f); // Shows function that logs b
   ```

2. **Execution Flow**:

   - Calling `g()` initializes `f`, allowing it to log `46` (23 \* 2).
   - Calling `h()` reassigns `f`, which now logs `1554` (777 \* 2).
   - The closure retains the reference to the variable `b` after `h()`.

3. **Explanation**:
   - `f` not defined inside of the `g` variable environment but then as we assigned it inside the `g` function it will be colesed-over variable environment of `g`
   - when you reassigned funtions even without return it also this will create a closure .

### Example 2: Using Timers and Closures

1. **Execution Flow**:

   - The console logs the boarding message after the `wait` period.
   - The closure allows the callback to access `n` and `perGroup` even after `boardPassengers` has executed.

   ```javascript
   const boardPassengers = function (n, wait) {
     const perGroup = n / 3;

     setTimeout(function () {
       console.log(`We are now boarding all ${n} passengers`);
       console.log(`There are 3 groups, each with ${perGroup} passengers`);
     }, wait * 1000);

     console.log(`Will start boarding in ${wait} seconds`);
   };

   const perGroup = 1000; // Global variable
   boardPassengers(180, 3);
   ```

   - When the callback function executes, its parent function has finished execution and is no longer on the stack. However, callback functions, such as those used in `setTimeout`, demonstrate how closures work by maintaining access to their parent scope's variables.

### Key Takeaways

- Closures allow functions to retain access to their lexical scope after they have been executed.
- Reassigning functions can change the closure, allowing access to new variables defined in the new function's scope.
- callback functions, such as those used in `setTimeout`, demonstrate how closures work by maintaining access to their parent scope's variables.
