# How the DOM Really Works

## Introduction to the DOM

- The DOM serves as the interface between JavaScript and HTML documents rendered in the browser.
- Understanding the internal organization of the DOM is crucial for effective web development.

## DOM Overview

- The DOM allows JavaScript to interact with the browser, enabling the creation, modification, and deletion of HTML elements.
- Key operations include:
  - Creating and modifying elements
  - Setting styles, classes, and attributes
  - Listening to and responding to events

## DOM Tree Structure

- The DOM represents an HTML document as a tree structure composed of nodes. Each node can be:
  - An HTML element
  - Text
  - Comments
- Interaction with this tree allows developers to manipulate web pages dynamically.

## DOM API

- The DOM is a complex API (Application Programming Interface) with numerous methods and properties. For example:
  - **Methods**: `querySelector`, `addEventListener`, `createElement`
  - **Properties**: `innerHTML`, `textContent`, `children`

## Node Types and Their Hierarchy

- Every node in the DOM tree is of type `Node`. Each node is represented by an object in JavaScript.
- Different types of nodes include:
  - **Element nodes** (e.g., `<div>`, `<p>`)
  - **Text nodes** (e.g., text inside elements)
  - **Comment nodes** (e.g., HTML comments)
  - **Document nodes** (the entire document itself)

## Node Representation

- Element nodes provide useful properties such as:
  - `innerHTML`: Gets or sets the HTML content.
  - `classList`: Provides methods to manipulate classes.
  - `children`: Returns child elements.

## Example of Node Manipulation

```javascript
// Creating a new element
const newDiv = document.createElement("div");
newDiv.innerHTML = "Hello, World!";
document.body.appendChild(newDiv); // Adding the new element to the body
```

## Inheritance in the DOM

- Inheritance allows child node types to access methods and properties of their parent types.
- For example, an HTML button element inherits properties from both `Element` and `Node` types.

## Example of Inheritance

```javascript
const button = document.createElement("button");
button.innerHTML = "Click Me";
button.addEventListener("click", () => alert("Button clicked!"));
document.body.appendChild(button);
```

## Document Node

- The `Document` node type provides essential methods for DOM manipulation:
  - `querySelector`: Selects the first matching element.
  - `createElement`: Creates a new element.
  - `getElementById`: Retrieves an element by its ID.

## Event Handling

- All node types can listen for events through the `addEventListener` method.
- The `EventTarget` type serves as a parent for both `Node` and `Window` types, allowing event handling capabilities across different node types.

## Example of Event Handling

```javascript
const div = document.createElement("div");
div.innerHTML = "Hover over me!";
div.addEventListener("mouseover", () => {
  div.style.backgroundColor = "lightblue";
});
div.addEventListener("mouseout", () => {
  div.style.backgroundColor = "";
});
document.body.appendChild(div);
```

## Conclusion

- The DOM API is structured into different types of nodes, each with unique properties and methods.
- Understanding this structure and the concept of inheritance is essential for effective DOM manipulation in JavaScript.
- The lecture emphasizes the importance of these concepts for creating dynamic web applications.

## Further Learning

- For deeper understanding, refer to the MDN (Mozilla Developer Network) documentation on the DOM.

Here is the final version of the notes on selecting, creating, and deleting elements with JavaScript:

# Selecting, Creating, and Deleting Elements with JavaScript

## 1. Selecting Elements

### a. Document Element

To select the entire document, use:

```javascript
const docElement = document.documentElement;
```

### b. Head and Body

You can easily select the head and body:

```javascript
const head = document.head;
const body = document.body;
```

### c. Query Selector

To select a single element:

```javascript
const header = document.querySelector("header");
```

### d. Query Selector All

To select multiple elements:

```javascript
const sections = document.querySelectorAll(".section");
```

This returns a NodeList of all elements with the class `section`.

### e. Get Element by ID

Select an element by its ID:

```javascript
const sectionOne = document.getElementById("section-one");
```

### f. Get Elements by Tag Name

To select all elements of a specific tag:

```javascript
const buttons = document.getElementsByTagName("button");
```

**Note:** This method returns an HTMLCollection.

- An HTMLCollection is a "live" collection, meaning it updates automatically when the DOM changes. For example, if you remove a button from the DOM, the count in the HTMLCollection will immediately reflect that change.

- **Note:** NodeLists are not live collections. They are static snapshots of the DOM at the time of selection. This means that if the DOM changes (such as adding or removing elements), the NodeList will not update to reflect these changes.

### g. Get Elements by Class Name

To select elements by class name:

```javascript
const buttonElements = document.getElementsByClassName("button");
```

**Note:** This method also returns a live HTMLCollection, which updates automatically with changes to the DOM.

## 2. Creating Elements

### a. Creating an Element

To create a new DOM element:

```javascript
const message = document.createElement("div");
```

### b. Adding Classes

You can add classes to the created element:

```javascript
message.classList.add("cookie-message");
```

### c. Adding Text Content

To add text to the element:

```javascript
message.textContent =
  "We use cookies for improved functionality and analytics.";
```

### d. Adding HTML Content

To set HTML content:

```javascript
message.innerHTML = "<button>Got it!</button>";
```

### e. Inserting into the DOM

To insert the created element into the DOM:

```javascript
const header = document.querySelector("header");
header.prepend(message); // Adds as the first child
// or
header.append(message); // Adds as the last child
```

**Note:** When you use `prepend` or `append`, you're moving the element within the DOM rather than creating a duplicate. If you `prepend` an element that has already been appended elsewhere, it will be removed from its previous position and placed in the new position. This is because both methods operate on live collections, meaning the DOM reflects the current structure without duplicating elements. Thus, you will only have one instance of that element in the DOM at any given time.We can solve it by cloning the element .

## 3. Cloning Elements

If you want to create a copy of an existing element:

```javascript
const clone = message.cloneNode(true); // true copies child elements
header.append(clone);
```

## 4. Additional Insertion Methods

To insert elements relative to others:

```javascript
header.insertAdjacentElement("beforebegin", message); // Before the header
header.insertAdjacentElement("afterend", message); // After the header
```

## 5. Deleting Elements

### a. Removing Elements

To remove an element from the DOM:

```javascript
const button = document.querySelector("button");
button.remove();
```

### Conclusion

These methods provide a quick reference for selecting, creating, and deleting elements in JavaScript. You can revisit this guide whenever you need to recall how to manipulate the DOM efficiently.

Here are the complete notes from the lecture on styles, attributes, and classes, including code examples:

# Styles, Attributes, and Classes

## Introduction

- The lecture covers styles, attributes, and classes in web development.
- Focus on CSS styles and how to manipulate them using JavaScript.

#### Styles

1. **Setting Styles**

   - To set a style on an element, use `element.style.propertyName`.
   - Properties should be in camelCase (e.g., `backgroundColor`).

   ```javascript
   // Example: Set background color
   message.style.backgroundColor = "darkblue";
   ```

2. **Setting Width**

   - Remember to include units when setting dimensions.

   ```javascript
   // Example: Set width
   message.style.width = "80%";
   ```

3. **Inline Styles**

   - Styles applied directly in the DOM are called inline styles.

   ```javascript
   // Checking inline styles
   console.log(message.style.backgroundColor); // Outputs: darkblue
   ```

4. **Reading Styles**

   - You can read inline styles using `element.style`, but only for styles you've set.

   ```javascript
   console.log(message.style.backgroundColor); // Outputs: darkblue
   ```

5. **Computed Styles**

   - To get styles applied via CSS or from classes, use `getComputedStyle`.

   ```javascript
   const computedStyles = getComputedStyle(message);
   console.log(computedStyles.color); // Outputs the computed color
   ```

6. **Modifying Height**

   - To modify the height of an element, first retrieve the current height, convert it from a string to a number, then add the desired value.

   ```javascript
   // Increase height by 40 pixels
   // This doesn't work because we out height is a string (120px) and we can add it to number , so we should first parse it
   const currentHeight = getComputedStyle(message).height;
   message.style.height = currentHeight + 40 + "px";

   const currentHeight = parseFloat(getComputedStyle(message).height);
   message.style.height = currentHeight + 40 + "px";
   ```

7. **CSS Custom Properties (Variables)**

   - CSS variables can be modified in JavaScript using `setProperty`.

   ```javascript
   // Variables are defined in the document
   document.documentElement.style.setProperty("--primary-color", "orangered");
   ```

#### Attributes

1. **Setting and getting Standard Attributes**

   - Access standard attributes directly as properties of the element.

   ```javascript
   const logo = document.querySelector(".nav__logo");
   // Getting style
   console.log(logo.alt); // Outputs the alt text
   console.log(logo.src); // Outputs the source URL
   // Setting style
   logo.alt = "logo";
   ```

2. **Setting and getting Custom Attributes**

   - Use `getAtrribute` to get custom attributes.
   - Use `setAttribute` to add custom attributes.

   ```javascript
   logo.setAttribute("data-designer", "Jonas");
   logo.getAttribute("data-designer"); // Jonas
   ```

   - The class name is accessed via `className` not `class`.

     2.1. **getting src and href attribute**

   - Use `getAtrribute` : Returns relative url
   - Use `elementName.src` : Return absolute url

   ```js
   const logo = document.querySelector(".nav__logo");
   console.log(logo.src); // http://127.0.0.1:5500/img/logo.png
   console.log(logo.getAttribute("src")); // img/logo.png
   ```

3. **Data Attributes**

   - We can store data in the DOM with `dataset-optinalName = value` .
   - Data attributes start with `data-` can be accessed using `getAttribute`.

   ```html
   <li data-animal-type="bird">Owl</li>
   ```

   ```javascript
   const animal = document.querySelector("li");
   // Getting data Attribute
   animal.dataset.animalType; // animal-type should be in camelCase here
   animal.getAttribute("data-animal-type");

   // Setting data Attribute
   animal.dataset.animalType = "Lion";
   animal.setAttribute("data-animal-type", "Lion");
   ```

### Classes

1. **Working with Classes**

   - Use `classList` to manipulate classes on an element.
   - Key methods include:
     - `add(className)`: Adds a class.
     - `remove(className)`: Removes a class.
     - `toggle(className)`: Toggles a class on or off.
     - `contains(className)`: Checks if a class is present.

   ```javascript
   // Example: Adding classes
   logo.classList.add("new-class", "another-class");
   ```

2. **Reading Class Names**

   - Use `className` to read or set class names, but be cautious as it overrides existing classes.

   ```javascript
   // Example: Setting a class name (overrides existing classes)
   logo.className = "new-class"; // Avoid this unless necessary
   ```

3. **Best Practices**

   - Prefer using `classList` methods to avoid overriding existing classes.
   - `contains` is used for checking class presence (Not include)

   ```javascript
   // Example: Check if a class exists
   if (logo.classList.contains("existing-class")) {
     console.log("Class is present");
   }
   ```

### Conclusion

- The lecture provided a comprehensive overview of how to work with styles and attributes in JavaScript.
- Understanding both inline styles and computed styles is crucial for dynamic styling.
- Attributes allow for more flexible and interactive web applications.

By following these notes and examples, you can effectively manage styles and attributes in your web development projects.

---

# Implementing Smooth Scrolling

## Introduction

In this lecture, we will implement smooth scrolling functionality on the Bankist website, allowing users to smoothly scroll to specific sections when buttons are clicked. We will explore two methods: an older approach and a modern approach.

## Setup

### HTML Structure

Assuming you have an HTML structure similar to this:

```html
<button class="btn-scroll-to">Scroll to Section 1</button>
<section id="section--1">Section 1 Content...</section>
```

## Step 1: Selecting Elements

First, we need to select the button and the section we want to scroll to.

### Code Example

```javascript
const btnScrollTo = document.querySelector(".btn-scroll-to");
const section1 = document.querySelector("#section--1");
```

## Step 2: Adding Event Listener

We will add an event listener to the button to listen for clicks.

### Code Example

```javascript
btnScrollTo.addEventListener("click", function () {
  // Smooth scrolling functionality will go here
});
```

## Step 3: Getting Coordinates

To implement smooth scrolling, we need the coordinates of the section we want to scroll to.

### Code Example

```javascript
const s1coords = section1.getBoundingClientRect();
```

### Explanation

- `getBoundingClientRect()` provides the size of an element and its position relative to the viewport.

## Step 4: Current Scroll Position

To scroll to the correct position, we need to consider the current scroll position.

### Code Example

```javascript
const currentScrollY = window.pageYOffset;
```

## Step 5: Calculating the Scroll Position

We combine the section's top position with the current scroll position to get the absolute position.

### Code Example

```javascript
const scrollToPosition = s1coords.top + currentScrollY;
```

## Step 6: Smooth Scrolling

To scroll smoothly, we use the `window.scrollTo()` method.

### Code Example (Old School Method)

```javascript
window.scrollTo({
  top: scrollToPosition,
  behavior: "smooth",
});
```

## Modern Approach

The modern approach uses `Element.scrollIntoView()`.

### Code Example (Modern Method)

```javascript
section1.scrollIntoView({
  behavior: "smooth",
});
```

## Full Implementation Example

Here’s the complete code combining all the above steps:

```javascript
const btnScrollTo = document.querySelector(".btn-scroll-to");
const section1 = document.querySelector("#section--1");

btnScrollTo.addEventListener("click", function () {
  // Old School Scroll
  const s1coords = section1.getBoundingClientRect();
  const currentScrollY = window.pageYOffset;
  const scrollToPosition = s1coords.top + currentScrollY;

  // Using Old School Method
  window.scrollTo({
    top: scrollToPosition,
    behavior: "smooth",
  });

  // OR Using Modern Method
  // section1.scrollIntoView({
  //     behavior: 'smooth'
  // });
});
```

## Conclusion

- We explored two methods for implementing smooth scrolling on a webpage.
- The older method includes calculating positions manually, while the modern method simplifies the process using `scrollIntoView()`.
- It's important to note that the modern method works only in modern browsers.

## Tips for Practice

- Experiment with different sections and buttons to see how the scrolling behaves.
- Try adjusting the viewport size to observe changes in scrolling behavior.

---

# Types of Events and Event Handlers

## Introduction

In this lecture, we will explore events in JavaScript, their significance, and different ways to handle them using event listeners.

## What is an Event?

- An event is a signal generated by the DOM (Document Object Model) when something occurs, such as:
  - A user clicking a button
  - Mouse movements
  - Triggering full-screen mode
- Events can be handled using event listeners to perform specific actions in response to those events.

## Types of Events

### Mouse Events

- Common mouse events include:
  - `click`
  - `mouseenter`
  - `mouseleave`

### Example: Using `mouseenter`

1. **Selecting an Element**:

   ```javascript
   const heading = document.querySelector("h1");
   ```

2. **Adding an Event Listener**:
   ```javascript
   heading.addEventListener("mouseenter", function () {
     alert("You are reading the heading.");
   });
   ```

### Testing the Event

- When the mouse enters the `<h1>` element, the alert will pop up.

## Event Reference

- A comprehensive list of events can be found on MDN (Mozilla Developer Network).
- Important events include:
  - Mouse events (e.g., `click`, `mouseenter`, `mouseleave`)
  - Keyboard events
  - Clipboard events
  - Scroll events

## Alternative Ways to Add Event Listeners

### 1. Using `on-event` Properties

- You can directly use properties like `onmouseenter` to handle events.

#### Example:

```javascript
heading.onmouseenter = function () {
  alert("You are reading the heading via onmouseenter.");
};
```

### 2. Using HTML Attributes

- Although not recommended, you can define event handlers directly in HTML.

#### Example:

```html
<h1 onclick="alert('Hello from HTML!')">Click me!</h1>
```

## Why Use `addEventListener`?

1. **Multiple Event Listeners**:

   - You can attach multiple listeners to the same event without overriding previous ones.

   #### Example:

   ```javascript
   heading.addEventListener("mouseenter", function () {
     alert("First alert.");
   });

   heading.addEventListener("mouseenter", function () {
     alert("Second alert.");
   });
   ```

2. **Removing Event Listeners**:

   - You can remove an event listener when it is no longer needed.

   #### Example:

   ```javascript
   function handleMouseEnter() {
     alert("Mouse entered.");
     heading.removeEventListener("mouseenter", handleMouseEnter);
   }

   heading.addEventListener("mouseenter", handleMouseEnter);
   ```

#### Example with `setTimeout`:

```javascript
function handleMouseEnter() {
  alert("Mouse entered.");
}

heading.addEventListener("mouseenter", handleMouseEnter);

// Remove the event listener after 3 seconds
setTimeout(() => {
  heading.removeEventListener("mouseenter", handleMouseEnter);
}, 3000);
```

## Conclusion

- We explored various ways to handle events in JavaScript, including using `addEventListener`, `on-event` properties, and HTML attributes.
- The preferred method is `addEventListener`, as it allows flexibility in managing multiple listeners and removing them when necessary.

## Next Steps

- In the next lecture, we will learn about event bubbling, an essential concept in event handling.

# Event Propagation - Bubbling and Capturing

## Introduction

JavaScript events have two important phases: **capturing** and **bubbling**. Understanding these phases is crucial for effectively managing event handling in web applications.

## Event Propagation Phases

1. **Capturing Phase**:

   - The event starts from the root of the DOM and travels down to the target element.
   - The event is generated at the root and passes through all parent elements until it reaches the target.

2. **Target Phase**:

   - The event reaches the target element where it can be handled. Event listeners defined on the target will respond here.

3. **Bubbling Phase**:
   - After reaching the target, the event bubbles back up to the root, passing through all parent elements again.
   - Both capturing and bubbling allow for event listeners to be triggered at different levels.

## Visualizing the Event Propagation

- Assume we have the following HTML structure:
  ```html
  <html>
    <body>
      <section>
        <p>
          <a href="#">Click me</a>
        </p>
      </section>
    </body>
  </html>
  ```

### Event Flow Example:

- **Click Event**:
  - When the link is clicked, the event travels from the root `<html>` down to the `<a>` element during the capturing phase.
  - Upon reaching the `<a>` element, the target phase executes any event listeners attached to it.
  - Next, the event bubbles back up through the `<p>`, `<section>`, and `<body>`.

## Handling Events

### Adding Event Listeners

- You can add event listeners to elements for both the capturing and bubbling phases.

#### Example: Handling a Click Event

```javascript
const anchor = document.querySelector("a");

// Event Listener for the target phase (bubbling)
anchor.addEventListener("click", function () {
  alert("Link clicked!");
});

// Event Listener for the capturing phase
document.body.addEventListener(
  "click",
  function () {
    alert("Body clicked (capturing phase)");
  },
  true
); // The third parameter 'true' enables capturing
```

### Bubbling Behavior

- If multiple event listeners are attached to parent elements, they will also respond to the same event due to bubbling.

#### Example: Handling Bubbling

```javascript
const section = document.querySelector("section");

section.addEventListener("click", function () {
  alert("Section clicked!");
});
```

- If you click the link, you will see alerts for the link, section, and body due to bubbling.

## Importance of Event Propagation

- Understanding event propagation allows you to implement powerful patterns:
  - You can handle the same event at different levels of the DOM.
  - This can help in creating more complex interactions without needing to duplicate code.

## Capturing Phase

- By default, events are handled in the target and bubbling phases. However, you can listen to events in the capturing phase by setting the third argument of `addEventListener` to `true`.

### Example: Capturing Event

```javascript
anchor.addEventListener(
  "click",
  function () {
    alert("Link clicked during capturing phase!");
  },
  true
); // Enables capturing
```

## Conclusion

- JavaScript events propagate through two main phases: capturing and bubbling. Understanding these phases is essential for effective event handling in web applications.
- You can add event listeners to handle events in both phases, allowing for flexible interaction designs.

## Next Steps

- In the next lecture, we will see practical implementations of event propagation in action.

##

##

##

##

##

##

####

####

####

####

#### Later

####

####

####

####

# Complete Notes on DOM Traversing

## Overview

- **DOM Traversing**: The process of navigating through the Document Object Model (DOM) to select elements based on their relationship to other elements.
- **Importance**: Necessary for selecting elements relative to a certain other element, especially when the structure of the DOM is unknown at runtime.

## Key Concepts

## Going Downwards

### 1. Selecting Child Elements

- **querySelector**: Selects the first matching child element.
- **querySelectorAll**: Selects all matching child elements.

**Example**:

```javascript
const highlights = h1.querySelectorAll(".highlight");
console.log(highlights); // Logs all elements with class 'highlight' that are children of h1
```

- **childNodes**: Retrieves all child nodes (including text, comments, and elements).

**Example**:

```javascript
const childNodes = h1.childNodes;
console.log(childNodes); // Logs all child nodes including text and comments
```

- **children**: Retrieves only child elements (returns an HTMLCollection).
- This one only return direct children

**Example**:

```javascript
const children = h1.children;
console.log(children); // Logs only child elements of h1
```

- **firstElementChild** & **lastElementChild**: Selects the first and last child elements respectively.

**Example**:

```javascript
const firstChild = h1.firstElementChild;
const lastChild = h1.lastElementChild;
firstChild.style.color = "white"; // Changes color of the first child
lastChild.style.color = "orange"; // Changes color of the last child
```

## Going Upwards

### 2. Selecting Parent Elements

- **parentNode**: Retrieves the direct parent node.
- **parentElement**: Retrieves the direct parent element.

**Example**:

```javascript
const parent = h1.parentNode; // or h1.parentElement
console.log(parent);
```

- **closest()**: Finds the closest ancestor that matches a specified selector.
- `closest()` is oppiste of querySelectory() : querySelectory finds children no matter how deep in the dom tree , closest finds parent no matter how far is in the dom tree . both of them recieve a query string as an input

**Example**:

```javascript
const closestHeader = h1.closest(".header"); // if h1 element has .header class select itself
closestHeader.style.backgroundColor = "lightblue"; // Changes background color of the closest header
```

## Go sideways : selecting siblings

### 3. Selecting Siblings

- **previousElementSibling**: Selects the immediate previous sibling element.
- **nextElementSibling**: Selects the immediate next sibling element.

- **previousSibling**: Selects the immediate previous sibling node.
- **nextSibling**: Selects the immediate next sibling node.

**Example**:

```javascript
const prevSibling = h1.previousElementSibling; // Gets the previous sibling element
const nextSibling = h1.nextElementSibling; // Gets the next sibling element
```

- **Getting all siblings**: Move up to the parent and access all children.

**Example**:

```javascript
const siblings = Array.from(h1.parentElement.children); // Notice that .children returns HTMLCollection and for using array methodes we convert collection to array
// convert to array using spread opertor
const siblings = [...h1.parentElement.children)];
siblings.forEach((sibling) => {
  if (sibling !== h1) {
    sibling.style.transform = "scale(0.5)"; // Scales down all siblings except h1
  }
});
```

### 4. Key Points

- **`querySelector` vs `closest`**:
  - `querySelector` finds child elements.
  - `closest` finds ancestor elements.
- **Traversal Direction**:
  - Downward: Selecting child elements.
  - Upward: Selecting parent elements.
  - Sideways: Selecting sibling elements.

### 5. Important Methods

- **querySelector**: Finds the first matching element.
- **querySelectorAll**: Finds all matching elements.
- **childNodes**: Retrieves all child nodes.
- **children**: Retrieves only child elements.
- **firstElementChild**: Selects the first child element.
- **lastElementChild**: Selects the last child element.
- **parentNode**: Retrieves the direct parent node.
- **parentElement**: Retrieves the direct parent element.
- **closest()**: Finds the nearest ancestor matching a selector.
- **previousElementSibling**: Gets the previous sibling element.
- **nextElementSibling**: Gets the next sibling element.

## Conclusion

- Understanding DOM traversing is crucial for dynamic web applications, especially for event delegation and manipulation.
- Traversing methods provide flexibility and powerful interactions with the document structure, allowing developers to navigate between elements as needed.

Here are the complete notes including CSS examples for the classes used in the tabbed component:

# Building a Tabbed Component

## Overview

- Tabbed components are widely used in web design.
- They allow users to switch between different content sections by clicking on tabs.

### Component Structure

- A typical tabbed component consists of:
  - Tabs (buttons) that users click to reveal content.
  - Content areas that display information associated with each tab.

### HTML Structure

Here’s an example of the basic structure:

```html
<div class="operations">
  <div class="tabs-container">
    <button class="operations-tab" data-tab="1">Tab 1</button>
    <button class="operations-tab" data-tab="2">Tab 2</button>
    <button class="operations-tab" data-tab="3">Tab 3</button>
  </div>
  <div class="operations-content operations-content-1 active">Content 1</div>
  <div class="operations-content operations-content-2">Content 2</div>
  <div class="operations-content operations-content-3">Content 3</div>
</div>
```

### CSS Styles

Here are examples of CSS classes that style the component:

```css
/* General styles for the tabbed component */
.operations {
  width: 100%;
  border: 1px solid #ccc;
  border-radius: 8px;
  overflow: hidden;
}

/* Style for the tabs container */
.tabs-container {
  display: flex;
  background-color: #f1f1f1;
}

/* Style for the individual tabs */
.operations-tab {
  flex: 1; /* Equal width for all tabs */
  padding: 10px;
  border: none;
  background: none;
  cursor: pointer;
  transition: background-color 0.3s;
}

/* Change background color on hover */
.operations-tab:hover {
  background-color: #ddd;
}

/* Active tab style */
.operations-tab-active {
  font-weight: bold;
  background-color: #ccc; /* Highlighted color for active tab */
}

/* General styles for content areas */
.operations-content {
  display: none; /* Hide all contents by default */
  padding: 15px;
  border-top: 1px solid #ccc; /* Separate content from tabs */
}

/* Style for the active content area */
.operations-content.active {
  display: block; /* Show the active content */
}
```

### JavaScript Functionality

1. **Selecting Elements**

   - Use `document.querySelectorAll` to select tabs and content areas.

   ```javascript
   const tabs = document.querySelectorAll(".operations-tab");
   const tabsContainer = document.querySelector(".tabs-container");
   const contents = document.querySelectorAll(".operations-content");
   ```

2. **Event Delegation**

   - Attach a single event listener to the parent container instead of each tab.

   ```javascript
   tabsContainer.addEventListener("click", (e) => {
     const clicked = e.target.closest(".operations-tab");
     if (!clicked) return; // Guard clause to ignore clicks outside tabs
   });
   ```

3. **Handling Clicks**

   - Determine which tab was clicked and show the associated content.

   ```javascript
   const tabIndex = clicked.dataset.tab; // Get the data-tab attribute
   contents.forEach((content) => {
     content.classList.remove("active"); // Hide all contents
   });
   document
     .querySelector(`.operations-content-${tabIndex}`)
     .classList.add("active"); // Show the selected content
   ```

4. **Updating Active Tab Style**
   - Update the active tab's style by adding/removing classes.
   ```javascript
   tabs.forEach((tab) => {
     tab.classList.remove("operations-tab-active"); // Remove active class from all
   });
   clicked.classList.add("operations-tab-active"); // Add to the clicked tab
   ```

### Complete Example

Here’s the complete code including HTML, CSS, and JavaScript:

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Tabbed Component</title>
    <style>
      .operations {
        width: 100%;
        border: 1px solid #ccc;
        border-radius: 8px;
        overflow: hidden;
      }
      .tabs-container {
        display: flex;
        background-color: #f1f1f1;
      }
      .operations-tab {
        flex: 1;
        padding: 10px;
        border: none;
        background: none;
        cursor: pointer;
        transition: background-color 0.3s;
      }
      .operations-tab:hover {
        background-color: #ddd;
      }
      .operations-tab-active {
        font-weight: bold;
        background-color: #ccc;
      }
      .operations-content {
        display: none;
        padding: 15px;
        border-top: 1px solid #ccc;
      }
      .operations-content.active {
        display: block;
      }
    </style>
  </head>
  <body>
    <div class="operations">
      <div class="tabs-container">
        <button class="operations-tab" data-tab="1">Tab 1</button>
        <button class="operations-tab" data-tab="2">Tab 2</button>
        <button class="operations-tab" data-tab="3">Tab 3</button>
      </div>
      <div class="operations-content operations-content-1 active">
        Content 1
      </div>
      <div class="operations-content operations-content-2">Content 2</div>
      <div class="operations-content operations-content-3">Content 3</div>
    </div>
    <script>
      const tabs = document.querySelectorAll(".operations-tab");
      const tabsContainer = document.querySelector(".tabs-container");
      const contents = document.querySelectorAll(".operations-content");

      tabsContainer.addEventListener("click", (e) => {
        const clicked = e.target.closest(".operations-tab");
        if (!clicked) return;

        const tabIndex = clicked.dataset.tab;
        contents.forEach((content) => {
          content.classList.remove("active");
        });
        document
          .querySelector(`.operations-content-${tabIndex}`)
          .classList.add("active");

        tabs.forEach((tab) => {
          tab.classList.remove("operations-tab-active");
        });
        clicked.classList.add("operations-tab-active");
      });
    </script>
  </body>
</html>
```

### Conclusion

This implementation allows users to interactively switch between different content sections using a tabbed interface. Event delegation improves performance by reducing the number of event listeners, and CSS styles enhance the user experience by providing visual feedback.

Sure! Here are the complete notes from the lecture on "Passing Arguments to Event Handlers," including key concepts and code examples.

---

# Passing Arguments to Event Handlers (navigation effect)

## Overview

- The lecture demonstrates a navigation effect where links fade out when hovered over, except for the hovered link.
- The main focus is on how to pass arguments into event handler functions.

### Key Concepts

1. **Event Delegation**: Instead of attaching event listeners to each link, attach one to a common parent element.
2. **Event Bubbling**: Events bubble up from their target, allowing a parent element to listen for events triggered on its children.
3. **Mouse Events**:
   - `mouseover`: Triggers when the mouse enters an element.
   - `mouseout`: Triggers when the mouse leaves an element.
   - `mouseenter`: Similar to `mouseover`, but does not bubble.
   - `mouseleave`: Similar to `mouseout`, but does not bubble.

### Implementation Steps

1. **Select the Parent Element**:

   - Use `document.querySelector()` to select the navigation container.
   - Example:
     ```javascript
     const nav = document.querySelector(".nav");
     ```

2. **Attach Event Listeners**:

   - Use `mouseover` and `mouseout` to manage the hover effects.
   - Example:

     ```javascript
     nav.addEventListener("mouseover", (e) => {
       // Handle mouse over
     });

     nav.addEventListener("mouseout", (e) => {
       // Handle mouse out
     });
     ```

3. **Identifying the Target**:

   - Check if the event target has a specific class (e.g., `nav_link` here is our `<a></a>` links on navbar).
   - Example:
     ```javascript
     if (e.target.classList.contains("nav_link")) {
       // Proceed with the effect
     }
     ```

4. **Managing Sibling Elements**:

   - Get siblings by selecting children from the parent.
   - Example:
     ```javascript
     if (e.target.classList.contains("nav_link")) {
       // Proceed with the effect
       const siblings = e.target.closest(".nav").querySelectorAll(".nav__link"); // Get all links
     }
     ```

5. **Changing Opacity**:

   - Loop through siblings and change their opacity.
   - Example:
     ```javascript
     siblings.forEach((sibling) => {
       if (sibling !== e.target) {
         sibling.style.opacity = "0.5"; // Fade out
       }
     });
     ```

6. **Resetting Opacity on Mouse Out**:
   - Use the `mouseout` event to reset opacity back to 1.
   - Example:
     ```javascript
     siblings.forEach((sibling) => {
       sibling.style.opacity = "1"; // Reset opacity
     });
     ```

### Refactoring for Reusability

- We wrote same codes for mousout and mouseover .But we can create a function to handle opacity changes, allowing for DRY (Don't Repeat Yourself) code.
- Example function:

  ```javascript
  function setOpacity(event, opacity) {
    const siblings = event.target.closest(".nav").querySelectorAll(".nav_link");
    siblings.forEach((sibling) => {
      if (sibling !== event.target) {
        sibling.style.opacity = opacity;
      }
    });
  }
  ```

- Use the function in event listeners:
- Incorrect way of passing a function as an argument because here the function is called immediately, and its return value is passed instead of the function reference.
  ```javascript
  addEventListener("mouseover", setOpacity(e, "0.5"));
  ```

Here's the updated explanation with a note about where the `event` argument comes from:

---

### Passing Arguments to Event Handlers (First Method)

#### Explanation:

- When you need to pass additional arguments to an event handler function, directly calling the function will execute it immediately instead of waiting for the event.
- To avoid this, wrap the function call inside an **arrow function** or a **regular anonymous function**. This ensures the function is only invoked when the event occurs.
- **Where the `event` argument comes from**:  
  When an event occurs (e.g., `mouseover`), the browser automatically provides an `Event` object that contains information about the event (e.g., the target element, type of event, etc.). This `event` object is passed to the event handler function as its first argument. In this case, it is passed to the arrow function and then forwarded to the `setOpacity` function.
- **Example**:
  ```javascript
  nav.addEventListener("mouseover", (e) => setOpacity(e, "0.5"));
  nav.addEventListener("mouseout", (e) => setOpacity(e, "1"));
  ```
  - **What happens here**:
    - `(e) => setOpacity(e, "0.5")` is a function definition that waits for the `mouseover` event.
    - When the event occurs, the browser provides the `event` object (`e`) automatically.
    - The `setOpacity` function is then called with the `event` object and the additional argument (`"0.5"` or `"1"`).

### Passing Arguments to Event Handlers (Second Method)

#### Explanation:

- You can use the `.bind()` method to pass arguments to an event handler function. The `.bind()` method creates a new function where the first parameter is explicitly set as the `this` value of the function. The value of `this` can then be used to access the argument inside the function.
- **Where the `event` argument comes from**:  
  Even though `.bind()` changes the `this` context, the browser still provides the `event` object as the first argument to the event handler. Inside the `setOpacity` function, the `event` object will be the first parameter, while the value of `this` will be the argument passed using `.bind()`.
- **Example**:
  ```javascript
  // Change function
  function setOpacity(event) {
    const siblings = event.target.closest(".nav").querySelectorAll(".nav_link");
    siblings.forEach((sibling) => {
      if (sibling !== event.target) {
        sibling.style.opacity = this; // 'this' is bound to the value passed via .bind()
      }
    });
  }
  nav.addEventListener("mouseover", setOpacity.bind("0.5")); // 'this' inside setOpacity will be "0.5"
  ```
  - **What happens here**:
    - `setOpacity.bind("0.5")` creates a new version of `setOpacity` where the value of `this` is `"0.5"`.
    - When the `mouseover` event triggers, the browser provides the `event` object as the first argument to `setOpacity`.
    - Inside `setOpacity`, the `event` object contains information about the event (e.g., which element triggered it), and the value of `this` is `"0.5"`, as specified by `.bind()`.

---

### Key Point:

In both methods, the `event` object is provided automatically by the browser when the event occurs, and it always appears as the first argument in the handler function. The additional arguments (like `"0.5"`) are passed either explicitly (first method) or through the `this` context (second method).

### Conclusion

- The lecture successfully illustrates how to create an interactive navigation effect using JavaScript event handling.
- It emphasizes the importance of event delegation, bubbling, and passing parameters to functions.

---

Here are the complete notes from the lecture on the Intersection Observer API, including code examples:

# Intersection Observer API

## **Overview:**

The Intersection Observer API allows your code to observe changes in the intersection of a target element with another element (root) or the viewport It's useful for tasks such as :

- Implementing lazy loading.
- Adding animations when elements enter the viewport.
- Creating sticky navigation.
- Building infinite scrolling features.

---

### Understanding the Intersection Observer API

1. **Creating an Intersection Observer**:

   - Syntax: `new IntersectionObserver(callback, options)`
   - **Callback**: A function that gets called when the target intersects the root.
   - **Options**: An object that can specify root, rootMargin, and thresholds.

2. **Storing the Observer**:

   ```javascript
   const observer = new IntersectionObserver(observerCallback, obsOptions);
   ```

3. **Observing a Target**:
   ```javascript
   observer.observe(targetElement);
   ```

### Setting Up Observer Options

Sure! Here’s the completed section on the options object for the Intersection Observer API, including details for `rootMargin`:

- **Options Object**:
  - **root**:
    - The element used as the viewport for visibility checks.
    - If set to `null`, the browser viewport is used.
  - **threshold**:
    - Specifies when the observer callback should be triggered, based on the percentage of the target's visibility.
    - For example:
      - `0`: Trigger as soon as even one pixel is visible.
      - `1`: Trigger only when the entire element is visible.
  - **rootMargin**:
    - Defines a margin around the root element, which can be used to expand or contract the area for intersection checks.
    - It accepts values in pixels or percentages and can be specified for each side (top, right, bottom, left) in the format `"{top} {right} {bottom} {left}"`.
    - For example:
      - `10px`: Adds a 10-pixel margin around the viewport.
      - `0px 0px -50% 0px`: Triggers the observer when the target is halfway out of the viewport (negative value for the bottom margin).

### Example - Basic Intersection Observer

```javascript
const obsOptions = {
  root: null, // Use viewport
  threshold: 0.1, // 10% visibility of target
};
```

### Observing Multiple Thresholds

- You can specify multiple thresholds in an array:

```javascript
const obsOptions = {
  root: null,
  threshold: [0, 0.2], // 0% and 20%
};
```

### Understanding the Callback Function

- The callback function receives two parameters:
  - **entries**:
    - An array of `IntersectionObserverEntry` objects, one for each observed element.
    - Key properties of an entry:
      - `isIntersecting`: Whether the element is currently visible in the viewport.
      - `target`: The element being observed.
      - `intersectionRatio`: The proportion of the element visible in the viewport.
  - **observer**: The observer instance itself.

### Example - Logging Entry Information

```javascript
const observerCallback = (entries) => {
  entries.forEach((entry) => {
    if (entry.isIntersecting) {
      console.log("Element is intersecting:", entry);
    } else {
      console.log("Element is not intersecting:", entry);
    }
  });
};
```

### Implementing Sticky Navigation

1. **When to Make Navigation Sticky**: When the header goes out of view.
2. **Selecting the Header**:

   ```javascript
   const header = document.querySelector(".header");
   ```

3. **Creating Sticky navigation with Header Observer**:

```javascript
// Without observer method (bad performance)
const initialCoords = section1.getBoundingClientRect();

window.addEventListener("scroll", function () {
  if (window.scrollY > initialCoords.top) nav.classList.add("sticky");
  else nav.classList.remove("sticky");
});

// With observer method
const navHeight = nav.getBoundingClientRect().height;

function observerCallBack(entries, observer) {
  const [entry] = entries;
  if (entry.isIntersecting) {
    nav.classList.remove("sticky");
  } else {
    nav.classList.add("sticky");
  }
}

const obsOptions = {
  root: null,
  threshold: 0,
  rootMargin: `-${navHeight}px`,
};

const observer = new IntersectionObserver(observerCallBack, obsOptions);
observer.observe(header);
```

### Conclusion

- The Intersection Observer API provides a powerful way to optimize performance by reducing the number of events fired during scroll events.
- Experiment with different thresholds and targets to understand the API better.

Here are the complete notes from the lecture on revealing elements on scroll using the Intersection Observer API, including code examples:

# Revealing Elements on Scroll

## Introduction

- **Purpose**: Implement a feature that reveals elements as the user scrolls close to them, enhancing the user experience.
- **Effect**: Sections become visible as they approach the viewport, creating a smooth transition effect.

### Overview of Implementation

1. **CSS Setup**:

   - Each section starts hidden with an opacity of zero and is slightly moved down.
   - When the class is removed, the section slides into view.

2. **Adding the Hidden Class**:
   - All sections will initially have the class `section--hidden` to make them invisible.

### CSS Example

```css
.section--hidden {
  opacity: 0;
  transform: translateY(8rem);
}
```

### JavaScript Implementation

#### Step 1: Create an Intersection Observer

- **Observer Setup**:

  ```javascript
  const options = {
    root: null, // Use the viewport
    threshold: 0.15, // Trigger when 15% of the section is visible
  };

  const observerCallback = (entries, observer) => {
    const [entry] = entries;

    if (!entry.isIntersecting) return;

    entry.target.classList.remove("section--hidden");
    observer.unobserve(entry.target); // Stop observing
  };

  const observer = new IntersectionObserver(observerCallback, options);
  ```

#### Step 2: Select Sections and Observe

- **Selecting Sections**:
  ```javascript
  const sections = document.querySelectorAll(".section");
  sections.forEach((section) => {
    section.classList.add("hidden"); // Initially hide sections
    observer.observe(section); // Observe each section
  });
  ```

### Explanation of Code

- **Intersection Observer**:

  - The observer monitors the visibility of observed elements based on the defined threshold.
  - When a section becomes visible (15% in this case), the `visible` class is added to it, triggering the CSS transition.

- **Unobserving**:
  - After a section is revealed, it is unobserved to improve performance, preventing unnecessary calculations.

### Final Notes

- This technique allows for smooth animations when scrolling through a webpage.
- The Intersection Observer API provides an efficient way to manage visibility without relying on scroll events, improving performance.

### Summary

- **CSS**: Defines how sections are hidden and revealed.
- **JavaScript**: Sets up the Intersection Observer, observes sections, and handles visibility changes.
- The effect enhances user engagement and provides a modern look to web pages.

Here are the complete notes on "Lazy Loading Images," incorporating your provided code examples:

---

# Lazy Loading Images

## Importance of Performance

- Images significantly impact webpage loading times.
- Optimizing images is crucial for better performance.

## What is Lazy Loading?

- Lazy loading defers the loading of images until they are needed (i.e., when they come into the viewport).
- This strategy improves initial load time and reduces resource consumption.

## Implementation Overview

1. Use a low-resolution placeholder image initially.
2. When the image comes into the viewport, replace the placeholder with the actual high-resolution image.

## HTML Structure

Ensure your images have a `data-src` attribute for the high-resolution image:

```html
<img
  src="placeholder.jpg"
  data-src="high-res.jpg"
  class="lazy-img"
  alt="Description"
/>
```

## JavaScript Implementation

### Step 1: Select Image Targets

Select all images that require lazy loading:

```javascript
const imgTargets = document.querySelectorAll("img[data-src]");
```

### Step 2: Create Load Image Function

Define a function to load the image when it intersects:

```javascript
const loadImg = function (entries, observer) {
  const [entry] = entries;

  // Check if the image is in the viewport
  if (!entry.isIntersecting) return;

  // Replace src with data-src
  entry.target.src = entry.target.dataset.src;

  // Remove the blur filter once the image is loaded
  entry.target.addEventListener("load", function () {
    entry.target.classList.remove("lazy-img");
  });

  // Stop observing the target since it has been loaded
  observer.unobserve(entry.target);
};
```

### Step 3: Create Intersection Observer

Set up the Intersection Observer to act on the image targets:

```javascript
const imgObserver = new IntersectionObserver(loadImg, {
  root: null, // Use the viewport as the container
  threshold: 0, // Trigger when any part of the image is visible
  rootMargin: "200px", // Add margin to trigger loading before the image is in view
});

// Observe each image target
imgTargets.forEach((img) => {
  imgObserver.observe(img);
});
```

## CSS for Placeholder

Use CSS to apply a blur effect to the placeholder image:

```css
.lazy-img {
  filter: blur(20px);
  transition: filter 0.3s ease-in-out;
}
```

## Summary

- Lazy loading images enhances website performance, especially for users with slow connections or low data plans.
- Implementing lazy loading involves using the Intersection Observer API to detect when images enter the viewport and loading them accordingly.

---

Here are the complete notes from the lecture on Lifecycle DOM Events, along with code examples:

# Lifecycle DOM Events

## Overview

- This section covers different events that occur in the DOM during a webpage's lifecycle, starting from when the page is accessed until the user leaves.

### Key Events in the DOM Lifecycle

#### 1. DOMContentLoaded Event

- **Definition**: Fired when the HTML has been completely parsed and the DOM tree is constructed.
- **Execution**: All scripts must be downloaded and executed before this event is triggered.
- **Key Point**: This event does not wait for images or other external resources to load.
  In the context of the **DOMContentLoaded** event, the statement "All scripts must be downloaded and executed before this event is triggered" means that:

1. **HTML Parsing**: When a web page is accessed, the browser starts parsing the HTML document to construct the DOM (Document Object Model). This process involves reading the HTML tags and building a tree structure that represents the page.

2. **Script Execution**: If the HTML contains `<script>` tags, the browser must download the JavaScript files specified in those tags and execute them. This is crucial because scripts can manipulate the DOM. If the scripts are not executed, any JavaScript code that relies on the DOM being fully constructed may not work correctly.

3. **Event Timing**: The **DOMContentLoaded** event is fired after:

   - The entire HTML has been parsed.
   - All synchronous scripts (those without the `async` or `defer` attributes) have been executed.

   However, this event does **not** wait for other resources like images, stylesheets, or asynchronous scripts to load. This is why you might see the **DOMContentLoaded** event fire before the entire page appears visually ready (i.e., images might still be loading).

**Code Example**:

```javascript
document.addEventListener("DOMContentLoaded", (event) => {
  console.log("HTML parsed and DOM tree built:", event);
});
```

#### 2. Load Event

- **Definition**: Fired when the entire page is fully loaded, including all images, scripts, and CSS files.
- **Execution**: This event occurs after all resources are loaded.

**Code Example**:

```javascript
window.addEventListener("load", (event) => {
  console.log("Page fully loaded:", event);
});
```

#### 3. BeforeUnload Event

- **Definition**: Fired immediately before a user is about to leave the page (e.g., closing a tab).
- **Usage**: This event can be used to prompt users for confirmation before leaving the page.
- **Important**: In some browsers, you may need to call `preventDefault()` and set the `returnValue` to an empty string to show a confirmation dialog.

**Code Example**:

```javascript
window.addEventListener("beforeunload", (event) => {
  event.preventDefault(); // Some browsers may require this
  event.returnValue = ""; // Display a generic confirmation dialog
});
```

### Practical Implications

- **DOMContentLoaded**: Use this event to execute code that relies on the DOM being ready, especially if your script is in the `<head>` or before the `<body>`.
- **Load**: This event is useful for analytics tracking or operations that require all resources to be fully loaded.
- **BeforeUnload**: Use sparingly, primarily when data loss could occur, such as during form submissions.

### Summary

- **DOMContentLoaded**: Good for initial scripts after the DOM is ready.
- **Load**: Suitable for when all resources are needed.
- **BeforeUnload**: Useful for protecting user data, but should be used judiciously to avoid annoying prompts.

---

Here are the complete notes from the lecture on efficient script loading in HTML, including key concepts and code examples.

# Efficient Script Loading: `defer` and `async`

## Overview

- The lecture discusses different methods for including JavaScript in HTML.
- Focuses on the impact of loading strategies on page performance.

### Traditional Script Loading

- Scripts are typically included in HTML using the `<script>` tag.

```html
<head>
  <script src="script.js"></script>
</head>
```

### Problems with Traditional Loading

- When a script is included in the `<head>`, HTML parsing stops until the script is fetched and executed.
- This can lead to delays in rendering the page.

### Recommended Practice

- Place script tags at the end of the `<body>` to ensure that all HTML is parsed before script execution.

```html
<body>
  <!-- HTML content -->
  <script src="script.js"></script>
</body>
```

### Using `async`

- The `async` attribute allows the script to be downloaded while HTML parsing continues.
- However, once downloaded, the script executes immediately, potentially interrupting HTML parsing.

```html
<head>
  <script src="script.js" async></script>
</head>
```

### Using `defer`

- The `defer` attribute also allows for asynchronous downloading of the script.
- The key difference is that scripts with `defer` are executed in order **after** the HTML is fully parsed.

```html
<head>
  <script src="script.js" defer></script>
</head>
```

### Comparison of `async` and `defer`

1. **Execution Timing**:

   - **`async`**: Executes as soon as the script is downloaded, which may happen before HTML parsing is complete.
   - **`defer`**: Executes after the entire HTML is parsed.

2. **Order of Execution**:

   - **`async`**: No guarantee of execution order.
   - **`defer`**: Scripts are executed in the order they appear in the document.

3. **DOMContentLoaded Event**:
   - **`async`**: Does not wait for the script; fires as soon as HTML parsing is complete.
   - **`defer`**: Waits for all deferred scripts to finish executing before firing.

### Use Cases

- **For scripts that need to run in a specific order** (e.g., when one script depends on another), use `defer`.
- **For third-party scripts** that do not depend on your code (like analytics or ads), use `async`.

### Browser Support

- Only modern browsers support `async` and `defer`.
- In older browsers, scripts should be placed at the end of the `<body>` to ensure proper loading.

### Code Examples

1. **Using `async`**:

   ```html
   <head>
     <script src="analytics.js" async></script>
   </head>
   ```

2. **Using `defer`**:

   ```html
   <head>
     <script src="library.js" defer></script>
     <script src="main.js" defer></script>
   </head>
   ```

3. **Script at End of Body** (Legacy Approach):
   ```html
   <body>
     <!-- HTML content -->
     <script src="script.js"></script>
   </body>
   ```

### Conclusion

- Use `defer` for scripts in the head to optimize loading and maintain execution order.
- Use `async` for independent third-party scripts.
- Always consider browser compatibility when implementing these strategies.

These notes summarize the key points from the lecture and include relevant code snippets for practical application.

Here are comprehensive notes from the lecture on building a slider component, along with the provided code examples.

# Building a Slider Component

## Overview

In this lecture, we will create a slider component that allows users to navigate through slides using buttons and dots. This will involve the use of HTML, CSS, and JavaScript.

### Key Features

- **Slides**: The component will contain multiple slides displayed side by side.
- **Navigation Buttons**: Users can navigate to the previous or next slide.
- **Dots**: Dots indicate the current slide and allow direct navigation to any slide.

### JavaScript Code Structure

#### Slider Function

We define a main function called `slider` that encapsulates all the functionality.

```javascript
const slider = function () {
  const slides = document.querySelectorAll(".slide");
  const btnLeft = document.querySelector(".slider__btn--left");
  const btnRight = document.querySelector(".slider__btn--right");
  const dotContainer = document.querySelector(".dots");

  let curSlide = 0;
  const maxSlide = slides.length;

  // Functions will be defined here
};
```

#### Functions

1. **Create Dots**

   - Generates dots based on the number of slides.

   ```javascript
   const createDots = function () {
     slides.forEach(function (_, i) {
       dotContainer.insertAdjacentHTML(
         "beforeend",
         `<button class="dots__dot" data-slide="${i}"></button>`
       );
     });
   };
   ```

2. **Activate Dot**

   - Highlights the dot corresponding to the current slide.

   ```javascript
   const activateDot = function (slide) {
     document
       .querySelectorAll(".dots__dot")
       .forEach((dot) => dot.classList.remove("dots__dot--active"));

     document
       .querySelector(`.dots__dot[data-slide="${slide}"]`)
       .classList.add("dots__dot--active");
   };
   ```

3. **Go To Slide**

   - Translates the slides to show the selected slide.

   ```javascript
   const goToSlide = function (slide) {
     slides.forEach(
       (s, i) => (s.style.transform = `translateX(${100 * (i - slide)}%)`)
     );
   };
   ```

4. **Next Slide**

   - Advances to the next slide, looping back to the first if at the end.

   ```javascript
   const nextSlide = function () {
     if (curSlide === maxSlide - 1) {
       curSlide = 0;
     } else {
       curSlide++;
     }

     goToSlide(curSlide);
     activateDot(curSlide);
   };
   ```

5. **Previous Slide**

   - Returns to the previous slide, looping back to the last if at the beginning.

   ```javascript
   const prevSlide = function () {
     if (curSlide === 0) {
       curSlide = maxSlide - 1;
     } else {
       curSlide--;
     }
     goToSlide(curSlide);
     activateDot(curSlide);
   };
   ```

6. **Initialization**

   - Sets up the initial state of the slider.

   ```javascript
   const init = function () {
     goToSlide(0);
     createDots();
     activateDot(0);
   };
   init();
   ```

### Event Handlers

- **Button Clicks**: Listeners for the next and previous buttons.
- **Keyboard Navigation**: Listens for left and right arrow keys to navigate.
- **Dot Clicks**: Allows users to click dots to go to a specific slide.

```javascript
btnRight.addEventListener("click", nextSlide);
btnLeft.addEventListener("click", prevSlide);

document.addEventListener("keydown", function (e) {
  if (e.key === "ArrowLeft") prevSlide();
  e.key === "ArrowRight" && nextSlide();
});

dotContainer.addEventListener("click", function (e) {
  if (e.target.classList.contains("dots__dot")) {
    const { slide } = e.target.dataset;
    goToSlide(slide);
    activateDot(slide);
  }
});
```

### Execution

Finally, we invoke the `slider` function to initialize the slider when the script runs.

```javascript
slider();
```
