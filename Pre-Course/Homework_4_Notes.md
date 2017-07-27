# Advanced JavaScript Minicamp – Homework 4

### Summary
- [Truthy and Falsy](#1)
- [!!](#2)
- [`arguments`](#3)
- [Callback Functions](#4)

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
  if (x) return 'truth!';    // Returns "truth!" if x === true
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

Is a double negation. The first negation will convert the data to a Boolean value, the second negation reserves the value again. 

Shortcut way to check a value's truthiness or falsiness.

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

## <a name="4" />Callback Function

A Callback function, aka **higher-order function** is a function that is passed as an argument to another function and the callback function is called (or executed) inside the other function.

*ref. [Understanding JavaScript Callback Functions](http://javascriptissexy.com/understand-javascript-callback-functions-and-use-them/)*

#### Syntax

```javascript
var friends = ['Troy', 'Chcuk', 'Paul', 'Mikey'];
friends.push('Justin');
friends.forEach(function(eachName, index) {  // an anonymous function being passed as an argument
  console.log(index + 1 + '. ' + eachName);  // 1. Troy, 2. Chcuk, 3. Paul, 4. Mikey, 5. Justin
});
```

### How do Callback Functions work?

When we pass a callback function as an argument to another function, we are only passing the function definition. We are not executing the function in the parameter. In other words, we aren't passing the function with the trailing pair of executing parenthesis `()` like we do when we are executing a function.

Since the containing function has the callback function in its parameter as a function definition, it can execute the callback anytime.

Note that the callback function is not executed immediately. It is "called back" at some specified point inside the containing function's body.

```javascript
$("#btn_1").click(function() {
  alert("Btn 1 Clicked");
  });
```

Here, the anonymous function will be called later inside the function body. Even without a name, the anonymous function can still be access later via the ***arguments*** object by the containing function.

### Callback Functions Are Closures

Since the callback function is executed at some point inside the containing function's body, it's just as if the callback were defined in the containing function. This means the callback is a closure.

Closures have access to the containing function's scope, so the callback function can access the containing functions' variables, and even the variables from the global scope.

### Named or Anonymous Functions as Callbacks

In the above two examples, I used an anonymous function that was defined in the parameter of the containing function.

You can also **declare a named function and pass the name of that function to the parameter**:

```javascript
var allUserData = [];

// generic function that logs data to console
function logStuff(userData) {
  if(typeof userData === 'string') 
  {
    console.log(userData);
  }
  else if (typeof userData === 'object') 
  {
    for(var item in userData) {
      console.log(item + ': ' + userData[item]);
    }
  }
}

// this function pushes options to the allUserData array and calls back a function as a parameter
function getInput(options, callback) {
  allUserData.push(options);
  callback(options);
}

// calls getInput that passes an object and logStuff as the parameter
// logStuff is the function that will be called back in getInput
getInput('{name:'Frank', specialty:'JavaScript'}', logStuff)
```

