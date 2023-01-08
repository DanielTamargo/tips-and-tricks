# Operators

There are many operators in JS and you don't have to memorize all of them, but it is really good to know the existence of them and how powerful they can be.  

- Assignment operators
  - Update variable if...
    - [**||=  ⬅ Logical OR Assignment**](#logical-or-assignment)
    - [**??=  ⬅ Logical Nullish Assignment**](#logical-nullish-assignment)
  - Math-involved operators
    - [**\*\*=  ⬅ Exponentiation assignment**](#exponentiation-assignment)


## Exponentiation assignment
We all used the addition assignment operator in our code `value += 2`, but did you know we can also use the [exponentiation assignment operator](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Exponentiation_assignment)?   
It's a fast way to apply an exponentiation and assing the result to the variable.    
```js
const value = 4
const exponent = 2
value **= exponent
console.log(value) // 16 (4 ** 2) 
```

You can get the same result using [**`Math.pow(base, exponent)`**](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Math/pow) method.
```js
// Using exponentiation assignment
const value = 4
value **= 2
console.log(value) // 16 (4 ** 2) 

// Using Math.pow and assigning the obtained value to the variable
const value_pow = Math.pow(4, 2)
console.log(value_pow) // 16 (4 ** 2) 
```

## Logical or assignment
It will assign a value to a variable **only** if that variable has a falsy value.  

In this code fragment you'll understand super fast how can it be used.
```js
// Long and classic way
let variable = 0
if (!variable) { // <- checking if it holds a falsy value
  a = 'new value!'
}

// Short way using logical or assignment operator
let variable = 0
varieble ||= 'new value!'
```

Here we have some examples of falsy or truthy values and the behaviour when using logical or assignment operator.
```js
let a = 0 // Falsy value
a ||= 'new value!' // a value is: 'new value!'

let b = '' // Falsy value
b ||= 'new value!' // b value is: 'new value!'

let c = 2 // Truthy value
c ||= 'new value!' // c value is: 2

let d = 'Hi!' // Truthy value
d ||= 'new value!' // d value is: 'Hi!'

// Falsy values are:
false, 0, 0n, "", null, undefined, NaN
```
Using this operator can be powerful, but you have to be aware about falsy and truthy values.  
[Learn more about falsy values here.](https://www.freecodecamp.org/news/falsy-values-in-javascript/)  
If you want to update the variable's value only if the variable contains a nullish (null or undefined value), you can use the [logical nullish assignment operator](#logical-nullish-assignment)!


## Logical Nullish Assignment
Updates a variable with a new value only if that variable has a nullish value.  
```js
let a = null // Nullish value
a ??= 'new value!' // a value is: 'new value!'

let b = undefined // Nullish value
b ??= 'new value!' // b value is: 'new value!'

let c = 0 // Falsy value
c ??= 'new value!' // c value is: 0

let d = 'Hi!' // Truthy value
d ??= 'new value!' // d value is: 'Hi!'
```
As we found out that when using [**logical or assignment operator**](#logical-or-assignment) you will assign a value to a variable **only if the variable holds a falsy value**. With the **logical nullish assignment operator** it's almost the same but **only with null or undefined**.