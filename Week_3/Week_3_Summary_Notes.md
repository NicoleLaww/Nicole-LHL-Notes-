# Notes 

## Object Methods & This 
* this refers to the object the method (function) was called on

## Recursion 
* Recursion in a nutshell: A function that calls itself until it doesn't.
* RangeError: Maximum call stack size exceeded. This is known as a stack overflow. 
* Every recursive function must stop calling itself at one point 
* The recursive case is when the function will continue to call itself. Every time the function calls itself, the input gets closer and closer to the base case. The base case is when the function no longer calls itself. In a properly designed recursive function, with each recursive call, the input must gradually resolve toward the base case.
* A function must have at least one recursive case and at least one base case in order to be recursive.
* Alt for while and for loops 
* Each recursive call should break down the current problem into a smaller, simpler one.

## Modules 
* Every File In Node Is A Module
* In Node: 
  * Modules are its way of organizing code into individual files 
  * Every js file in node is implicity a module
    * We can console.log(module) and see its details 
  * module.exports tells node what to export from a file 
    * deafults to {} - empty object
  * We can use require with relative paths (like ./myModule)
    * it doesn't need the .js extension, implied already  

## Packages 
* Packages are self-contained code libraries that we can install and use in our projects.
* [package.json Reading Link](https://docs.npmjs.com/cli/v9/configuring-npm/package-json)

## Library 
* A "library" is a collection of pre-written code. Libraries can be private, but many are packaged up nicely, branded and made publicly available for other developers to use in their own projects.

### QUIZ 
* Library: an independent collection of code that can be used by programs (not JS specific) 
* Module: JS code in a separate file, that can be required by other JS programs - * Package: a collection of JS modules, with a package.json, usually published on NPM
* Should the node_modules directory be committed to your project's git repo? NO
  * package.json should be committed because it contains the information necessary to recreate node_modules. Including node_modules would be redundant and would cause giant git commits every time a library is updated.

## Installing Packages 
* package.json
* Basic attributes such as project name, description, author 
* Custom scripts in package.json
  * The scripts portion allows us to run commands using an alias
* Dependencies in package.json
  * Lists the packages that need to be installed for the project to run properly 

## Testing
* Manual Testing - How we tested before?
  * Repeatitive
  * Not efficient/sufficient 
* Automated Testing 
  * Practice of writing code to programmatically test the actual code we want to write 
* Unit Testing - do often 
* Integration Testing - not isolated from other components, verify that two seperate systems work together, fewer
* Functional Testing - user perspective, fewer
* Happy Path - 20 percent on when it works, 80 off it, find anomalies/break it

## Mocha & Chai Intro 
* BDD - Behavior Driven Development 
  * BDD encourages you to specify the behaviour of your app in terms of user stories which are broken down into scenarios that can be built and tested.
* BDD Frameworks
  * When we write tests, we are testing the behaviour of our code. If you were to test a function that sums two numbers together, you would create some numbers, call the function with those numbers, then write an assertion for what the function should return.
  * Some tests are more complicated than others, but every test will involve setting up some data, running some code that should do something, and asserting that it does that thing.
* MOCHA - Naming our test folder test tells mocha where to find our test files. While you could name your code folder anything you want (src is a common choice), you should keep your mocha test files in a test folder to keep things simple.
* CHAI 
```javascript 
const chai = require('chai');  // import the chai library
const assert = chai.expect;  // establish a variable to be used in our tests
const validator = require('../javascript/groupValidator.js'); // import the file where our function lives
describe("The function groupValidator()", () => {
    // this is where we put our tests.
});
```
  * The describe line begins our testing block, and within its callback function, we’ll be writing our tests. Our tests themselves will follow a very similar pattern: a keyword, a string description, and then a callback function.
```javascript 
 it("should return true if there are between 2 and 5 group members", () => {
    assert(validator.isGroupValid(["a", "b", "c"])).to.be.true
  });
```
  * The it line gives a description of the test, then runs a callback function. That function finds our validator file and then runs the groupValidator function inside with the parameters we pass it. Since we’re testing a group that should work, we’ve given it an array with three strings inside.
* Modular means that pieces of code, files, or libraries form building blocks that, when put together, make a functioning app/page.

## Object Oriented Programming
* An object is a little bundle of information, also known as state. Each property that an object has, can represent the state of that object
```javascript 
const dog = {
  sound: "woof", // Property
  breed: "shih tzu" // Property
};
```
* An object is not just state; an object also has some stuff it can do known as behaviour. This behaviour takes the form of methods, which is just the name we give to functions when they're tied to an object. Some methods might modify the object, some methods might ask the object for information, etc.
* this 
  * We use this within a line of code as if it were a variable, but it's actually a keyword, like for or function. 
  * The value of this is determined at the time of the call and depends on how and where it was called.
  * All we really need to know for OO in JavaScript, is that when you use this inside a method, this refers to the object that the method was called on.
* In the context of object orientation, an object is a little bundle of information. Actually, it's not just information (a.k.a. "state"); an object also has some stuff it can do (a.k.a. "behaviour"). Typically this behaviour takes the form of "methods", which is just the name we give to functions when they're tied to an object. Some methods might modify the object, some methods might ask the object for information, etc. OO bundles (groups) together related state and logic into an object that can be passed around as a single entity.

## Classes
* Classes are blueprints (templates) we use to create objects 
  * Describes what the object is going to be and we can create objects using the class
  * Can use any name for a class, but should always be a noun and the first letter should be capitalized 
```javascript
  class Pizza {

}//nothing inside, just an empty object
```
  * To create a new object from a class, we use the new keyword:
```javascript
  let pizza1 = new Pizza();
  let pizza2 = new Pizza();
```
  * Both Pizza objects 
    * When you create an object using a class, it is an instance of that class. ^^Both instances. They are not the same. 
  * 
```javascript
class Pizza {

  constructor() {
    this.toppings = ["cheese"];
  }

  addTopping(topping) {
    this.toppings.push(topping);
  }

}
```
  * You can add a method to a class with the following syntax:
```javascript
class SomeClass {
  methodName(parameters) {
    // this is a method
  }
}
```
  * To add properties to a class, simply use the this keyword followed by the property name, then assign it a value:
```javascript 
class SomeClass {
  someMethod() {
    this.hello = "hi"; // Created a property called hello
  }
}
```
  * Since a class is just a blueprint for creating objects, methods like addTopping will exist on the instances created from the class, but not on the class itself.
```javascript
// This will **NOT** work.
// That's because addTopping is a method only available to actual instances of Pizza
// Give it a try!
Pizza.addTopping();
```
* Intro to Constructor  
  * Constructor is a special kind of method that gets executed when an object instance is created from a class. Everything inside the Pizza's constructor method will get run for the new instance of the class when we call new Pizza();. This is a great place to setup default state for new instances. In other words, the constructor is for setting default values for any new object's properties.
```javascript
class Pizza {

  constructor(size, crust) {
    this.size = size;
    this.crust = crust;
    this.toppings = ["cheese"];
  }

  addTopping(topping) {
    this.toppings.push(topping);
  }

}
```
  * Now every time we use this class to create a new object, we can pass in the parameters of size and crust 
```javascript
let pizza = new Pizza('large', 'thin');
```
* An object constructor can be invoked with the word new

## Inheritance 
* Build a new class based on an existing class
* Now there is a general Person class that contains the shared code. Student and Mentor inherit behaviour and state information from Person using the keyword extends.
* Student and Mentor are subclasses of Person 
* Person is a superclass 
```javascript
// This class represents all that is common between Student and Mentor
class Person {
  // moved here b/c it was identical
  constructor(name, quirkyFact) {
    this.name = name;
    this.quirkyFact = quirkyFact;
  }

  // moved here b/c it was identical
  bio() {
    return `My name is ${this.name} and here's my quirky fact: ${this.quirkyFact}`;
  }
}

class Student extends Person {
  // stays in Student class since it's specific to students only
  enroll(cohort) {
    this.cohort = cohort;
  }
}

class Mentor extends Person {
  // specific to mentors
  goOnShift() {
    this.onShift = true;
  }

  // specific to mentors
  goOffShift() {
    this.onShift = false;
  }
}
```
