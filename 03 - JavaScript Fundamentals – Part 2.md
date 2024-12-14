## Activating Sctrict mode

strict mode forbids us to do certain things and second, it will actually create visible errors for us in certain situations in which without strict mode JavaScript will simply fail silently without letting us know that we did a mistake.

1. without strtict mode we can create a variable without declaration but strict mode doesn't allow us
2. another thing that strict mode does is to introduce a short list of variable names that are reserved for features that might be added to the language a bit later. => interface , if , ...

## Functions

https://www.devsajjad.ir/posts/Function-Types-in-JavaScript

Arrow funtion (type of function expression)
one line functions => one parameter and one line of return statement

```js
const age = (birthYear) => date - birthYear;
const age = function (birthYear) {
  return date - birthYear;
};
```

## Array methodes

- Add elements
  push(); // Last
  unshift(); // First

- Remove elements
  pop(); // Last
  shift(); // First

- Elemenet Index
  indexOf('Steven')

- Check Exist an Element in Array
  includes('Steven')

## Dot vs. Bracket Notation OBJECTS

- objectName[expression||PropertyName] // with expression we ca execute propertyName
- objectName.propertyName

So when we need to first compute the property name, then of course we have to use the bracket notation in any other case, just use the dot notation

```js
const jonas = {
  lastName: "Schmedtmann",
  birthYeah : 1380
  calcAge: function () {
    this.age = 1403 - this.birthYeah;
    return this.age;
  },
};

// Access to property
console.log(jonas.lastName);
console.log(jonas["lastName"]);
console.log(jonas["calacAge"]());

// Use Expression in Bracket
const interestedIn = prompt("What do you want");
jonas.interestedIn; // Error : we dont have interestedIn property && we can not use expression
jonas[interestedIn]; // CORRECT

// Add property to object
jonas.location = "Portugal";
jonas["twitter"] = "@jonasschmedtman";
```

when using bracket notation to access an object property, what's inside the brackets should either be a :

1.  string
2.  variable that refers to a string

## While and For loop
whenever you do need a loop without a counter, you can reach for the while loop. So basically that happens whenever you do not know beforehand how many iterations the loop will have or you want to loop till a certain condition is true So in that situation the while loop is the right tool for the job.

```js
// Sample Example :
const correctPassword = "openSesame";
let userGuess = "";

while (userGuess !== correctPassword) {
  userGuess = prompt("Please enter the password:");
  if (userGuess === correctPassword) {
    console.log("Access granted!");
  } else {
    console.log("Wrong password. Try again.");
  }
}
```

