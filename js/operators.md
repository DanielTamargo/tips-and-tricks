# Operators

There are many operators in JS and you don't have to memorize all of them, but it is really good to know the existence of them and how powerful they can be.  

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