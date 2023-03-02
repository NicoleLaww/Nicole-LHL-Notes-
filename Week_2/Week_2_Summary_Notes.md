# Notes 

## Primitives
* undefined 
* null 
* boolean
* string 
* number 
* symbol 
* Primitives are essential building blocks of data because they represent the simplest possible type of data that our software can have.

## Objects  
* Objects are NOT primitives
* Anything not in a list is an Object 
* Arrays & Functions are a sub-category of objects 
* Objects have properties 
* Objects are used to define more complex data types 
* Contains key-value paris, each key maps to a value 
  * Keys which are always strings or symbols (less common)
  * Have unique keys, cannot appear twice in an object 
  * Have their keys point to values which can be of any type  
* Object Literals 
  *  Object literal with a single key-value pair:
```javascript
const tinyObject = { size: "Tiny" };
```
* Object Values: While it's perfectly valid to use undefined as an object value, it's not typically done. As you'll see in a moment, undefined has a special meaning when accessing values in an object.
  * Notice that we get back undefined! The key "foo" doesn't exist in myObject, so it returns undefined to tell us that, well, the key is not defined.
* Accessing an object property:
  * Using the square brackets ([]) syntax, the key must be quoted (as a string). Otherwise it would be considered a variable name instead of a string literal.
```javascript
const person = { firstName: "Khurram" };
person[firstName]; 
// ReferenceError: firstName is not defined
```
  * If that variable name instead points to a string, then that can be an interesting way of accessing a key:
```javascript 
const person = { firstName: "Khurram" };
const propertyName = "firstName";
const firstName = person[propertyName]; // interpreted as person["firstName"], and therefore works fine :)
```
  * An alternative way to access the same value would be person.firstName.
* Accessing a Key That Doesn't Exist
  * undefined
* Assigning a New Value to a Key
  * Square-bracket notation can also be used to assign new values to new or existing keys.
```javascript 
const mary = { name: "Mary Sue" };
mary["name"] = "Mary Jane";
mary["age"]  = 22;
mary // shows the resulting object with both properties
```
* Objects as Values 
```javascript
const person = {
  name: "Paul",
  address: {
    street: "310 W 95th",
    city: "New York",
    zipCode: 10027
  }
};
``` 
  * Node typeof person["address"] -> object 
```javascript
person["address"]["city"]; // => "New York"
```
* SUMMARY 
  * Keys are always strings
  * Each key is unique (can only occur once in the object)
  * Each key is associated with exactly one value. (Note that technically, an array or another object would count as "one value" here, even though they contain other values.)
* When writing out object literals, like { myKey: "some value" }, the key is always interpreted as a literal string, even if it's unquoted. It's only necessary to use quotes around the key if the key contains spaces, hyphens or periods. For instance: { "my-hyphenated-key": "some value" }.
* The following example shows two ways of specifying the same value in an object literal: using a literal string for the value, or using a variable.
```javascript
const spam = "spam";
person["dislikes"] = { food: spam, "e-mail": "spam" };
```
* Object.keys - To inspect an object's keys, there is a method Object.keys(...) that returns an array of keys.
* PRO TIP
  * Common way to create objects (const o = {})
  * Accessing and setting properties on objects using string keys (o["key"]) 
  * How to get a list of all the keys in an object (Object.keys(o)

### Objects and Iteration 
* For ... in statement 
```javascript 
var planetMoons = {
  mercury: 0,
  venus: 0,
  earth: 1,
  mars: 2,
  jupiter: 67,
  saturn: 62,
  uranus: 27,
  neptune: 14
};

for (var planet in planetMoons) {
  var numberOfMoons = planetMoons[planet];
  console.log("Planet: " + planet + ", # of Moons: "+ numberOfMoons);
}

for (var planet in planetMoons) {
  // additional filter for object properties:
  if (planetMoons.hasOwnProperty(planet)) {
    //  ...
  }
}
```
* We should be careful with this looping technique, as it can produce some unexpected results. For reasons which we'll cover in later activities, objects can sometimes have properties that they inherit from their prototype chain as well as method names. An additional filtering step is sometimes necessary -> hasOwnProperty ^^ 

## First Class Object/Citizen 
* An object with no restrictions on its creation, destruction, or usage. This includes the ability to be passed as an argument, returned from a function, and assigned to a variable

## countOnly 
* Why did we not use assertEqual to compare the resulting object (result1) directly? Why did we need to instead break our test case into three different assertion checks?
  * Our assertEqual function can only compare primitive values. We ran into this issue when comparing arrays and ended up implementing assertArraysEqual, if you recall. The same will need to be done with objects to make our test code cleaner. Until we have that specialized assertion function, we will do it this, more cumbersome way.

## countLetters 
* Perhaps this function could return an object where each unique character encountered in the string is a property of the object and the value for that property/key should be the number of occurrences for that character.

Therefore countLetters("lighthouse in the house") would return:
```javascript
{
  l: 1,
  i: 2,
  g: 1,
  h: 4,
  t: 2,
  o: 2,
  u: 2,
  s: 2,
  e: 3,
  n: 1,
}
```

## Functions 
* Functions are first class objects 
* Functions can be store in variables and passed around
* Functions can do everything that other objects can do (like having properties assigned to them)
```javascript 
const myFn = function() {
  console.log("I am function.");
}

myFn.someAttribute = 42;
console.log(myFn.someAttribute);

function runner(f) {
  f();
}

runner(myFn);
```
* We assign a function to our variable myFn
* An attribute someAttribute is assigned to that function object
* A runner function is defined that runs the argument f that we pass it
* We pass a reference to our myFn, which gets invoked by the runner function

### Callback Functions 
* Functions you send into other functions are called Callback Functions 
* Is a function passed (by reference) into another function (let's call that one the "receiver" function)
* The receiver function is therefore accepting behavior to perform by calling the callback function that it now has access to
* The receiver function can decide to call the callback function at any time, as many times as it wants
```javascript
// The second argument/parameter is expected to be a (callback) function
const findWaldo = function(names, found) {
  for (let i = 0; i < names.length; i++) {
    let name = names[i];
    if (name === "Waldo") {
      found();   // execute callback
    }
  }
}

const actionWhenFound = function() {
  console.log("Found him!");
}

findWaldo(["Alice", "Bob", "Waldo", "Winston"], actionWhenFound);
```
* This code illustrates how a function can be treated as an ordinary value and passed around to another function. We pass a reference to the function named actionWhenFound as an argument to another function findWaldo.
* The function actionWhenFound is known as a callback function. It is first defined, then passed as an argument to another function, and finally executed once a specific event occurs.

### Anonymous Functions 
* Often a callback function would not be declared or assigned to a variable, but rather would be inline like this:
```javascript 
findWaldo(["Alice", "Bob", "Waldo", "Winston"], function(index) {
  console.log("Waldo is located at:", index);
});
```
* Anonymous functions are often declared while being passed in as callbacks to other functions. Why? Because the receiving function that takes in the anonymous function will give that parameter a name anyway.

### Arrow Functions 
```javascript 
// BEFORE: anonymous callback as function expression 
[1,2,3].forEach(function (num) {
  console.log('num: ', num);
});

// AFTER: anonymous callback as arrow function
[1,2,3].forEach((num) => {
  console.log('num: ', num);
});

// In fact, for one liners JS allows us to further remove some characters: 
[1,2,3].forEach(num => console.log('num: ', num));

```
* Can't be names 
* Normally in line 
* Small, inline & single purpose 

### Higher Order Functions 
* Functions that take in callbacks are referred to Higher Order Functions 
* Higher-Order functions are any functions which operate on other functions.
* This includes, but is not limited to, functions which take in functions (callbacks) as arguments.
* This means that built-in functions such as forEach, filter, and others can be called "Higher-Order Functions".
* Filter returns true or false, filters what you want 
* Map returns a transformed object 
* Function that takes a function as an argument, or returns a function as a result. Higher-order functions make use of other functions either as arguments or by returning them
* Rationale behind using them: 
  * They allow for creation of more powerful and generalized functions. A Higher-order function's job is reduced in scope when you allow it to interact with other functions. 

## Vim 
* Vim modes
  * Vim operates in two modes - edit and command mode. Edit mode is the state in which the keys you type on are actually inserted into your document, whereas the command mode allows you to navigate through the document, search and replace text, copy and paste, etc. By default when you open a file, you're placed in command mode.
* Moving around
  * You can use the H, K, J and L keys to move around. Here's how it breaks down: "H" moves left; "K" moves up; "L" moves right; "J" moves down. You can, of course, use the arrow keys as well, although using arrow keys is apparently the non-ninja style of using vim.
* Create/open a file
  * Create a new file and open it in vim by typing vim tutorial.txt.
* Edit a file 
  * VIM launches into the command mode by default.
  * To switch to edit mode (also called "insert mode") you need to give VIM a command to tell it to switch modes. There are two ways to do this:
  * "i" to begin inserting text at the current cursor position
  * "a" to begin inserting after the current cursor position 
  * ESC to make sure you are back to command mode.
  * Y copies a line of text to the buffer.
  * P pastes it to the cursor's current position.
  * dd will delete the whole line of text. This will also effectively "cut" a line of text as well. When you delete a line, it's placed in the buffer.
  * yy copies a whole line of text.
* Saving 
  * Make sure you are in command mode 
  * :w
* Quit Vim 
  * :wq - write (save) and quit file (and vim)
* :q! - quit and ignore changes made since last file save.
