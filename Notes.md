# Notes

### Truthy and Falsy Values
Everything in JavaScript has an inherent Boolean value, generally known as truthy or falsy.
#### Falsy values:					#### Truthy values:
• false							• true
• 0 (zero)						• All other values are truthy
• “” (empty string)					• Empty functions
• null							• Empty objects
• undefined						• Empty arrays	
• NaN (Number value meaning Not-a-Number)

#### Common Use Case
```
function x(y) {
  !!y ? console.log(y + ' is truthy') : console.log(y + ' is falsy');
}	// checks to see if an argument is truthy or falsy

x(0)	// ‘0 is falsy’
````

### !! (double-bang)

The double-bang is a simple way to Typecast something to Boolean. The Boolean will cast true for truthy values and false for falsy values.

#### Syntax

`!!0 // Return false`
