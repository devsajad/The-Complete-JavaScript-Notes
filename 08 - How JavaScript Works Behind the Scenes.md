## Regular Functions vs. Arrow Functions
whene we have a regular function and function call inside a method => when we use 'this' it will be undefined
### solution 
1. self variable that store this value
2. modern way : use arrow function to inherit this from parent

```js
const jonas = {
  firstName: "Jonas",
  year: 1991,
  calcAge: function () {

    // Solution 1
    // const self = this; // self or that
    // const isMillenial = function () {
    //   console.log(self); 
    //   console.log(self.year >= 1981 && self.year <= 1996);
    // };

    // Solution 2
    const isMillenial = () => {
      console.log(this); 
      console.log(this.year >= 1981 && this.year <= 1996);
    };
    isMillenial();
  },
};
jonas.calcAge();
```
### Arguments
Arrow functions dont have arguments = unlike => other function types

```js

// arguments keyword
const addExpr = function (a, b) {
  console.log(arguments);
  return a + b;
};
addExpr(2, 5);
addExpr(2, 5, 8, 12); // we can call funtion with additional parameters and access to them with arguments object

var addArrow = (a, b) => {
  console.log(arguments);
  return a + b;
};
addArrow(2, 5, 8); // arrow functions dont have arguments object

```

## Primitives vs. Objects
### copying objects 

1. Object.assign({},) => shollow copy : only copy properties in the first level => if we have objects or array as property in that object they will not copy



```js
// Copying objects
const jessica2 = {
  firstName: 'Jessica',
  lastName: 'Williams',
  age: 27,
  family: ['Alice', 'Bob'],
};

const jessicaCopy = Object.assign({}, jessica2);
```