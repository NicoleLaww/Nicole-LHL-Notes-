# Notes 

## [Command Line Arguments](https://stackabuse.com/command-line-arguments-in-node-js/)
* Ex of syntax of command line arguments -> $ [runtime] [script_name] [argument-1 argument-2 argument-3 ... argument-n]
* IMP!! Using process.argv - the simplest way of retrieving arguments in Node.js 
* first index contains the path to our node executable 
* second index contains the path to the script file 
* rest of the indexes contain the arguments that we passed in their respective sequence 

## Library 
* Collection of pre-written code 
* Examples are jQuery and Bootstrap 
* Lotide - For JS 

## Template Literals 
```javascript 
const name = 'Alice';
console.log(`Hello, ${name}!`);
```

## Head & Tail 
* Head of the array -> first element of the array 

## Functions
* Name functions with the action, be consistent with your naming conventions, adapt to existing procedures if joining a project 
* Use camelCasedNames 
* Properly indent the function code 
* Functions should focus on a single task: returning a value or causing a side effect. Break your function into additional smaller functions if you find it doing two or more thing.
  * One single task could be to compute and return a value (eg: zeroPad)
  * Another single task could be to perform a side effect such as logging a message to the screen (eg: printFarmInventory)
* Global-scoped variable is available everywhere in the code  
* Local-scoped variable is available within the function it is defined
* It is ideal if functions try to avoid reading outer scope variables. If a function needs some information / data, then that data should instead be passed in as a parameter, making it available within the function's inner scope.
* Data needed by Functions should be passed in as parameters/arguments (i.e. local scope) instead of being accessed directly
```javascript 
const person = "Martha";

// BAD
const sayHelloBadly = function() {
  console.log(`Howdy, ${person}`);
}
sayHelloBadly(); // Works, but not ideal!

// GOOD
const sayHelloGoodly = function(name) {
  console.log(`Howdy, ${name}`);
}
sayHelloGoodly(person);
```
* What is the reason for this rule? Why is it better to pass the data into the function as a parameter/argument instead of letting the function simply access that data directly? After all, the latter approach takes fewer characters to write.
  * Correct Answer -> Functions that take in parameters are more reusable, since they are less dependent on their surroundings, (i.e. their outer scope). From the example above, we can extract the sayHelloGoodly function and plop drop it into another piece of code. We can't do that with sayHelloBadly because the person variable would have to come along for the ride. 

## Error Messages 

### Syntax Errors 

```javascript 
var rank = "Imperator";
var name = "Furiosa";

console.log(rank name);
```
/vagrant/focal/syntax-error.js:4

  * This tells us that the error happened in a file called /vagrant/focal/syntax-error.js, but more importantly, the :4 on the end of the file name tells us the error was thrown by line 4 in this file. This is very useful, because it helps us narrow down our search for the error. Looking back at our code, we find that line 4 is the following.
    
console.log(rank name);

  * Chances are our error is caused by something on this line. There are cases when that won't be true, which we'll see shortly, but it's not a bad assumption to start with. 

console.log(rank name);
                 ^^^^
SyntaxError: Unexpected identifier

  * This shows us where exactly in the code the error occurred and that we're dealing with a SyntaxError. There seems to be something wrong with name, which JavaScript is calling an Unexpected identifier. Because we're working out of a single file, we can be confident we've learned enough about our error to fix it. There's no trick for the next step; here we see that what we meant to do was log rank then name, separated by a space, which means we're missing a ,.

### Stack Traces 

at exports.runInThisContext (vm.js:73:16)
at Module._compile (module.js:443:25)
at Object.Module._extensions..js (module.js:478:10)
at Module.load (module.js:355:32)
at Function.Module._load (module.js:310:12)
at Function.Module.runMain (module.js:501:10)
at startup (node.js:129:16)
at node.js:814:3

  * This bit is called a stack trace, which shows the state of our program when the error occurred. In the future, we'll discuss the more technical details of what stack traces are and how they're determined, but for now, take a look at the file names printed out in the stack trace, in the parentheses at the end of each line: vm.js, module.js and node.js. We don't know anything about them. They're not even our code, we didn't write them! It's possible, as we'll see once we start working with modules, that the error didn't come from the exact file the error was thrown in (in our case /vagrant/focal/syntax-error.js) but that it came from one of these files. However, it's a safe bet to assume the error is not caused by someone elses (hopefully) well-tested code but by ours – it is a work in progress, after all. 

### Trickier Syntax Traces 

```javascript
   if (5 > 10) {
  console.log("Impossible!");

console.log("Phew, logical fallacies avoided.");
```
/vagrant/focal/syntax-error2.js:6
});
 ^
SyntaxError: Unexpected token )
    at exports.runInThisContext (vm.js:73:16)
    at Module._compile (module.js:443:25)
    at Object.Module._extensions..js (module.js:478:10)
    at Module.load (module.js:355:32)
    at Function.Module._load (module.js:310:12)
    at Function.Module.runMain (module.js:501:10)
    at startup (node.js:129:16)
    at node.js:814:3

  * This error message is weird... Firstly, there's no line 6 in our code - we only wrote four lines! Second, it's pointing to a snippet of code that doesn't even exist in our four lines.

});
 ^

   * In this case it's hard to use the information provided by the first few lines of the error message to our advantage. But the next line, SyntaxError: Unexpected token ) is a big hint. Unexpected token errors occur when JavaScript expected something that wasn't there, which frequently means we're missing a parenthesis, bracket or curly brace. In our case, we're missing a }.

```javascript 
if (5 > 10) {
  console.log("Impossible!");
}

console.log("Phew, logical fallacies avoided.");
```
### Reference Errors 
```javascript 
var firstName = "Jane";
var lastName = "Doe";

console.log(firstName, lasName);
```

node reference-error.js
/vagrant/focal/reference-error.js:4
console.log(firstName, lasName);
                       ^
ReferenceError: lasName is not defined
    at Object.<anonymous> (/vagrant/focal/reference-error.js:4:24)
    at Module._compile (module.js:460:26)
    at Object.Module._extensions..js (module.js:478:10)
    at Module.load (module.js:355:32)
    at Function.Module._load (module.js:310:12)
    at Function.Module.runMain (module.js:501:10)
    at startup (node.js:129:16)
    at node.js:814:3

* Let's read our error message line by line again.

/vagrant/focal/reference-error.js:4
  * This tells us our error is most likely coming from line 4, which is confirmed by the next couple lines of the error message.

console.log(firstName, lasName);
                       ^
  * Something is wrong with lasName – node tells us that it's not defined. ReferenceErrors are also common errors we see in day-to-day development, and they occur when we're trying to use the value of an undefined variable. In our case, this happened because we misspelled lastName.

### Type Errors 
```javascript 
var favouriteMeal = "BREAKFAST";

console.log(favouriteMeal.toLower());
```

node type-error.js
/vagrant/focal/type-error.js:3
console.log(favouriteMeal.toLower());
                          ^
TypeError: undefined is not a function
    at Object.<anonymous> (/vagrant/focal/type-error.js:3:27)
    at Module._compile (module.js:460:26)
    at Object.Module._extensions..js (module.js:478:10)
    at Module.load (module.js:355:32)
    at Function.Module._load (module.js:310:12)
    at Function.Module.runMain (module.js:501:10)
    at startup (node.js:129:16)
    at node.js:814:3
  
  * Let's start at the top of the error message again.

/vagrant/focal/type-error.js:3
console.log(favouriteMeal.toLower());
                          ^
  * It's telling us we broke something on line 3, and it has something to do with toLower. It looks fine at a glance, so let's check the error description. 

TypeError: undefined is not a function
  * Taking a look at line 3 of our code again, we see that we're trying to call two functions, console.log and favouriteMeal.toLower. JavaScript is telling us that one of them is undefined – and it's being helpful enough to draw our attention to toLower. Something must be wrong here. If we did a Google search for something like javascript convert string to lowercase and avoided the W3schools link in favour of the Mozilla Developer Network (MDN), we would find that we simply forgot the name of the prototype function that converts a string to lowercase. 

```javascript 
var favouriteMeal = "BREAKFAST";

console.log(favouriteMeal.toLowerCase());
```

## Truthy & Falsy 
* == -> 23 == "23" - TRUE 
  * Type coercion -> can produce unexpected results 
  * Same for != 
* === -> compares two values, including comparing the type of those values -> 23 === "23" FALSE 
  * Same for !==
* All of the following are inherently falsey:
  * False // False is False. Makes sense, right?
  * 0 // 0 is the only falsey Number
  * "" // an empty string is falsey
  * null // a null, or empty value, is falsey.
  * undefined // an object that has not been defined is considered falsey.
  * NaN // Not a Number. You'll learn more about NaN as we go on.

  ## Array.isArray 
  * Evaluate if it is an Array or not 
  * Can't use typeof on an Array because it will return obj
  ```javascript
  const flatten = (arr) => {
  let newArr = [];
  for (let i = 0; i < arr.length; i++) {
    //console.log(arr[i]);
    if (!Array.isArray(arr[i])) {
    //  console.log(Array.isArray(arr[i]));
      newArr.push(arr[i]);
    } else {
      let smallArr = arr[i];
      for (let j = 0; j < smallArr.length; j++) {
        newArr.push(smallArr[j]);
      }
    }
  }
  console.log(newArr);
};

flatten([1, 2, [3, 4], 5, [6]]); // => [1, 2, 3, 4, 5, 6]

```
