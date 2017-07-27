# Advanced JavaScript Minicamp – Homework 4

### Summary
- [Truthy and Falsy](#1)
- [!!](#2)
- [`arguments`](#3)

## <a name="1" />Truthy and Falsy Values
Everything in JavaScript has an inherent Boolean value, generally known as truthy or falsy.
#### Falsy values:  
• `false`  
• `0` *(zero)*  
• `“”` *(empty string)*  
• `null`  
• `undefined`  
• `NaN` *(Number value meaning Not-a-Number)*  

#### All other values are Truthy, including:
• `true` 
• `function(){}` *(empty functions)*  
• `{}` *(empty objects)*  
• `[]` *(empty arrays)*	

#### Common Use Case
```javascript
function myFunction(x, y) {
  if (x) return 'error!';    // Returns "error!" if x === true
  if (!y) return 'error!';  // Returns "error!" if y === false
}
```

```javascript
function x(y) {
  !!y ? console.log(y + ' is truthy') : console.log(y + ' is falsy');
}  // checks to see if an argument is truthy or falsy

x(0)	// ‘0 is falsy’
```

## <a name="2" />!! (double-bang)

Is double negation. The first negation will convert the data to a Boolean value, the second negation reserves the value again. 

#### Syntax

```javascript
!!0 // Return false
```
## <a name="3" />`arguments`

`arguments` is a pseudo-array. Allows you to access an unknown number of arguments coming into a function. 

#### Syntax

```javascript
function sumNumbers() {
  var total = 0;
  for(var i = 0; i < arguments.length; i++) {
    total += arguments[i];
  }
  console.log(total);
}

sumNumbers(1, 2, 3, 4, 5, 6, 7, 8, 9);
```
