## Template Literals
```js
console.log(`we can use ${expression} inside Template literal`)
console.log(
  `${
    age > 18
      ? "You can access to the content"
      : "You can not access to the content"
  }`
);
```
multi line string : 
1. " this is /n multi line " 
2. `this is 
multi line`

## Type coercion
1.there is type conversion and type coercion.
type conversion is when we manually convert from one type to another.
type coercion is when automatically converts types behind the scenes for us.

type coercion happens whenever an operator is dealing with two values that have different types. So in that case, JavaScript will then, behind the scenes, convert one of the values to match the other value so that in the end,the operation can be executed.

```javascript
    const firstExample = 3 + "2" // + operator trigger type coersion and conver 3 to string then concat it with 2
    const secondExample = 3 - "2" // - operator trigger type coersion and conver "2" to number
```

2.what if we're trying to convert something to a number that is impossible to convert?
We get NaN, which stands for not a number. So JavaScript gives us this not a number value whenever an operation that involves numbers fails , to produce a new number.
So basically, not a number actually means invalid number.

typeof NaN = number

## Truthy and Fulsy values
5 falsy vlues : 0 , '' , undefined , null , NaN
When conver them to boolean result will be flase

A BUG
```js
    const number = 0;
    if(number){
        console.log("number defined")
    }else{
        console.log("Number is not defined")
    }
    // result : if(we have type coercion to boolean here) => 0 is falsy value => result will be "Number is not defined"
```

## Equality Operators == vs. ===

=== (strict equality) : it does not perform type coercion. so it only returns to when both values are exactly the same

== (loose equality) : loose equality operator does type coercion.

always use strict equality Even if we actually need type conversion.it's better to convert the value manually before the comparison than relying on the double equal operator.

## Statements and Expressions
expression is a piece of code that produces a value. = exp => 3+2 , 3 , true && false

statement is like a bigger piece of code that is executed and which does not produce a value on itself. And we can compare this with normal spoken language.

a declaration is like a complete sentence and expressions are like the words that make up the sentences.
example : 
```js
if(23 > 10){
    console.log("23 is bigger than 10") // the string is expression inside statement
}// if is statement
```
