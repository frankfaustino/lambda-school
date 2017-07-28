# Advanced JavaScript Minicamp – Homework 4

### Contents
- [Truthy and Falsy](#1)
- [`!!`](#2)
- [`arguments`](#3)
- [`forEach()`](#4)
- [Callback Functions](#5)
- [`reduce()`](#6)
- [`map()`](#7)
- Creating Objects
  - [Object Literals](#8)
  - [`new`](#9)
  - [Object Constructors](#10)
- [Object Methods](#11)

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
## <a name="4" />`forEach()`

The forEach() method executes a provided function once for each array element.

#### Syntax

```javascript
arr.forEach(function callback(currentValue, index, array) {
    //your iterator
}[, thisArg]);
```
**callback** Function to execute for each element, taking three arguments:  
- **currentValue** The value of the current element being processed in the array.  
- **index** The index of the current element being processed in the array.  
- **array** The array that forEach is being applied to.  

**thisArg** *optional* value to use as `this` (i.e. the reference to Object) when executing callback.

```javascript
var a = ['a', 'b', 'c'];

a.forEach(function(element) {
    console.log(element);
});

// a
// b
// c
```

## <a name="5" />Callback Function

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
## <a name="6" />`reduce()`

The reduce() method applies a function against an accumulator and each element in the array (from left to right) to reduce it to a single value.

```javascript
var arr = [0, 1, 2, 3];
var total = arr.reduce(function(sum, value) {
  return sum + value;
}, 0);
// total is 6
```
```javascript
var flattened = [[0, 1], [2, 3], [4, 5]].reduce(function(a, b) {
  return a.concat(b);
}, []);
// flattened is [0, 1, 2, 3, 4, 5]
```

## <a name="7" />`map()`

The map() method creates a new array with the results of calling a provided function on every element in the calling array.

#### Syntax

```javascript
var numbers = [1, 5, 10, 15];
var doubles = numbers.map(function(x) {
   return x * 2;
});
// doubles is now [2, 10, 20, 30]
// numbers is still [1, 5, 10, 15]
```
```javascript
var numbers = [1, 4, 9];
var roots = numbers.map(Math.sqrt);
// roots is now [1, 2, 3]
// numbers is still [1, 4, 9]
```

## Creating Objects

### <a name="8" />Object Literals

```javascript
var person = {firstName:"John", lastName:"Doe", age:50, eyeColor:"blue"};
```

### <a name="9" /> `new`

```javascript
var person = new Object();
person.firstName = "John";
person.lastName = "Doe";
person.age = 50;
person.eyeColor = "blue";
```

### <a name="10" /> Object Constructor Function

The examples above are limited in many situations. They only create a single object.

Sometimes we like to have an "object type" that can be used to create many objects of one type.

The standard way to create an "object type" is to use an object constructor function:

```javascript
function person(first, last, age, eye) {
    this.firstName = first;
    this.lastName = last;
    this.age = age;
    this.eyeColor = eye;
}
var myFather = new person("John", "Doe", 50, "blue");
var myMother = new person("Sally", "Rally", 48, "green")
```


```javascript
function encryptPassword(password) {
  return '$#$87sd' + password;
}

function User(options) {
  this.username = options.username;
  this.password = encryptPassword(options.password);
}

var frank = new User({
  username: 'frank',
  password: 'blah#1998'
});

var rey = new User({
  username: 'efozzie',
  password: 'blah$1999'
});

console.log(frank, rey);
```
## <a name="11" />Object Methods

A method is a property containing a function definition.

```javascript
function Cat(options) {
  this.name = options.name;
  this.age = options.age;
  this.meow = function() {  // ← method defined in constructor function
    console.log('meow! My name is ' + this.name);
  }
}

var snowballII = new Cat({
  name: 'Snowball II',
  age: 5
});

var snowballIII = new Cat({
  name: 'Snowball III',
  age: 1
});

snowballII.meow();  // ← method being accessed
snowballIII.meow();  // ← method being accessed
```
