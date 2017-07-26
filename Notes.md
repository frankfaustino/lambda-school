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

The double-bang is a simple way to Typecast something to Boolean. The Boolean will cast true for truthy values and false for falsy values.

#### Syntax

```javascript
!!0 // Return false
```

### Arrow Functions `=>`

Arrow functions have an implicit return feature: if the function body consists of a single expression, you can omit the `return` keyword: ```javascript () => 'foo' ``` is a function that takes no parameters, and returns the string, `'foo'`.
