## Useful Methodes

```js

//-----------SELECTING-----------------
// select element (if we have many same classes name => just select first class)
document.querySelector("like selecting in css");
// select all elements with same class
document.querySelectorAll("like selecting in css");
document.getElementById();

// --------- CHANGE STYLE ---------------
.style.styleNameCamelCase = "Value";

// manipulate classes
.classList.remove('className')
.classList.add('className')
.classList.contain('className')
.classList.toggle('className') // remove the class if there is or add the class if there isn't

// ----------- CHANGE CONTENT -------------
// change text content of element
.textContent ;
// change value of input
.value ;

.src

// ------------ DOM Manipulation -----------
const elementVariable = document.createElement('elementName')

// insert elements
.appendChild(elementVariable)
.insertAdjacentHTML("LocationParameter" , elementVariableWithHtmlCodes)

.innerHTML = ""
```

```js
// Clear Input field
inputLoginUsername.value = inputLoginPin.value = ""; 
inputLoginPin.blur(); // removes keyboard focus from the current element.

// ---------- EVENT HANDLING -------------
.addEventListener("eventName" , callbackFunction(event) )
// EVENT NAMES :
click
keyDown / keyUp / keyPress  // in event.key => we have the key that triggered
document.addEventListener("keyUp" , callbackFunction(event) // we use it on document object
// event for changing select inpute options
inputSelector.addEventListener('change', () => {
  inputCadence.closest('.form__row').classList.toggle('form__row--hidden');
  inputElevation.closest('.form__row').classList.toggle('form__row--hidden');
});
```
