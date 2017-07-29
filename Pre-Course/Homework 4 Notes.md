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
- [Object Prototype](#12)
- [Closures](#13)
- [Recursion](#14)

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

#### Syntax
```javascript
arr.reduce(callback[, initialValue])
```

#### Common Use Cases
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
var new_array = arr.map(function callback(currentValue, index, array) {
    // Return element for new_array
}[, thisArg])
```

#### Common Use Cases

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

## <a name="12" />Object Prototype

Every object has a prototype. The prototype is also an object.

All JavaScript objects inherit their properties and methods from their prototype.

Objects created using an object literal, or with new Object(), inherit from a prototype called Object.prototype.

The Object.prototype is on the top of the prototype chain.

#### Using the `prototype` Property

The prototype property allows you to add new properties to an existing prototype:
```javascript
Cat.prototype.breed = 'American Shorthair';

console.log(snowballII.name + ' is an ' + snowballII.breed);  // "Snowball II is an American Shorthair"
```

It is best practice to put an object method in a separate `prototype` property:

```javascript
Cat.prototype.meow = function() {  
    console.log('meow! My name is ' + this.name);
}
```

Now all objects made with the Cat Constructor Function can use the `.meow` object method.

## <a name="13" />Closure

A ***closure*** is the combination of a function and the lexical environment within which that function was declared. This environment consists of any local variables that were in-scope at the time that the closure was created.
```javascript
function init() {
  var name = 'Mozilla'; // name is a local variable created by init
  function displayName() { // displayName() is the inner function, a closure
    alert(name); // use variable declared in the parent function    
  }
  displayName();    
}
init();
```
`init()` creates a local variable called `name` and a function called `displayName()`. The `displayName()` function is an inner function that is defined inside `init()` and is only available within the body of the `init()` function. The `displayName()` function has no local variables of its own. However, because inner functions have access to the variables of outer functions, `displayName()` can access the variable `name` declared in the parent function, `init()`.

The following code illustrates how to use closures to define public functions that can access private functions and variables. Using closures in this way is known as the module pattern:
```javascript
var counter = (function() {
  var privateCounter = 0;
  function changeBy(val) {
    privateCounter += val;
  }
  return {
    increment: function() {
      changeBy(1);
    },
    decrement: function() {
      changeBy(-1);
    },
    value: function() {
      return privateCounter;
    }
  };   
})();

console.log(counter.value()); // logs 0
counter.increment();
counter.increment();
console.log(counter.value()); // logs 2
counter.decrement();
console.log(counter.value()); // logs 1
```

In previous examples, each closure has had its own lexical environment. Here, though, we create a single lexical environment that is shared by three functions: `counter.increment`, `counter.decrement`, and `counter.value`.

The shared lexical environment is created in the body of an anonymous function, which is executed as soon as it has been defined. The lexical environment contains two private items: a variable called `privateCounter` and a function called `changeBy`. Neither of these private items can be accessed directly from outside the anonymous function. Instead, they must be accessed by the three public functions that are returned from the anonymous wrapper.

Those three public functions are closures that share the same environment. Thanks to JavaScript's lexical scoping, they each have access to the `privateCounter` variable and `changeBy` function.

You'll notice we're defining an anonymous function that creates a counter, and then we call it immediately and assign the result to the counter variable. We could store this function in a separate variable `makeCounter` and use it to create several counters.
```javascript
var makeCounter = function() {
  var privateCounter = 0;
  function changeBy(val) {
    privateCounter += val;
  }
  return {
    increment: function() {
      changeBy(1);
    },
    decrement: function() {
      changeBy(-1);
    },
    value: function() {
      return privateCounter;
    }
  }  
};

var counter1 = makeCounter();
var counter2 = makeCounter();
alert(counter1.value()); /* Alerts 0 */
counter1.increment();
counter1.increment();
alert(counter1.value()); /* Alerts 2 */
counter1.decrement();
alert(counter1.value()); /* Alerts 1 */
alert(counter2.value()); /* Alerts 0 */
```
Notice how each of the two counters, `counter1` and `counter2`, maintains its independence from the other. Each closure references a different version of the `privateCounter` variable through its own closure. Each time one of the counters is called, its lexical environment changes by changing the value of this variable; however changes to the variable value in one closure do not affect the value in the other closure.

Using closures in this way provides a number of benefits that are normally associated with object oriented programming -- in particular, data hiding and encapsulation.

## <a name="14" />Recursions

Recursion is when a function calls itself.

```javascript
function nFibonacci(n) {
  if (n < 3) return 1; // base case so the recursion doesn't continue forever
  return nFibonacci(n - 2) + nFibonacci(n - 1); // recursion
}
console.log(nFibonacci(6)); // 8
```
 
```javascript
function factorial(n) {
  if(n < 0) {  // if the number is less than o, reject it
    return -1;
  } else if(n === 0) {  // if the number is 0, its factorial is 1
    return 1;
  } else  // otherwise, call this recursive procedure again
    return (n * factorial(n - 1)); 
}

console.log(factorial(5));
// 5 * 4 = 20
// 20 * 3 = 60
// 60 * 2 = 120
// 120 * 1 = 120
```
