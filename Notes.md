# Notes

### Truthy and Falsy Values
Everything in JavaScript has an inherent Boolean value, generally known as truthy or falsy.
#### Falsy values:  
• false  
• 0 *(zero)*  
• “” *(empty string)*  
• null  
• undefined  
• NaN *(Number value meaning Not-a-Number)*  

#### Truthy values:
• true  
• *All other values are truthy*  
• Empty functions  
• Empty objects  
• Empty arrays	

#### Common Use Case
```javascript
function x(y) {
  !!y ? console.log(y + ' is truthy') : console.log(y + ' is falsy');
}	// checks to see if an argument is truthy or falsy

x(0)	// ‘0 is falsy’
```

### !! (double-bang)

Is double negation. The first negation will convert the data to a Boolean value, the second negation reserves the value again. 

#### Syntax

```javascript
!!0 // Return false
```

### Object Literal

```javascript
const user = {
  userName: 'echo',
  avatar: 'echo.png'
};
```

### Arrow Functions `=>`

Arrow functions have an implicit return feature: if the function body consists of a single expression, you can omit the `return` keyword: `() => 'foo'` is a function that takes no parameters, and returns the string, `'foo'`.

Be careful when you return object literals. By default, JavaScript assumes you want to create a function body when you use braces, e.g., `{ broken: true }`. If you want to use an implicit return for an object literal, you'll need to disambiguate by wrapping the object literal in parathesis:

```javascript
const noop = () => { foo: 'bar' }; // returning a function body 👎 
console.log(noop()); // undefined

const createFoo = () => ({ foo: 'bar' }); // returning an object literal 👍
console.log(createFoo()); // { foo: "bar" }
