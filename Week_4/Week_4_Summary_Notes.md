# Notes 

## Introduction to Asynchronous Control Flow
* Asynchronous Concepts 
  * JavaScript has a few parts that work together to facilitate multitasking: the Call Stack, the Web APIs, the Callback Queue, and then the Event Loop.
  * Event Loop 
    * Call Stack
      * Code that might call another function 
      * New function might show up on the call stack 
    * Web APIs 
      * Reading a file 
      * Calling a network API request
    * Callback Queue 
      * Seperate stack of callbacks that can then be called in the function when JS is ready to run those 
    * Event Loop 
      * Takes callbacks from the callback queue and runs them `
* Order of Execution 
  * Function calls always execute right away. But the setTimeout method schedules a callback for later execution on the event loop 
  * The main thread has to finish first before the event loop can even start 
  * We use callbacks when we are writing asynchronous code, but it also helps with modularity. We now know that callback chaining means writing nested callback functions.
* Using Async Functions 
  * Other ways it might be used 
    * Making a network API request 
    * Connecting to a chat server 
    * Anything that takes time and where we want users to know that the code is still running,  like showing a basic loading animation 
* Asynchronous programming is when a unit of work is run separately from the main thread of the program and notifies the program of its completion.
* Order in which async finishes is not always the same 
* Can order with nested 

## User Events 
* Common requirement of user-facing software is the ability to handle user input. 
  * Action events -> when a user does something
  * These are asynchronous 
* process.stin -> standard input 
* process.stout -> standard output
```javascript 
// on any input from stdin (standard input), output a "." to stdout
process.stdin.on('data', (key) => {
  process.stdout.write('.');
});

console.log('after callback');
```
  * We use the on method on stdin to register a callback. Unlike setTimeout, this callback is not scheduled to run x seconds later. No delay information is provided for this reason. Instead, it is meant to run any time the user provides input to the program.
  * The on function is a very common method name for registering callbacks to handle events.
```javascript 
const stdin = process.stdin;
// don't worry about these next two lines of setup work.
stdin.setRawMode(true);
stdin.setEncoding('utf8');

////////////
// Event Handling for User Input
////////////

// on any input from stdin (standard input), output a "." to stdout
stdin.on('data', (key) => {
  if (key === '\u0003') {//acts like control + c, stops it 
    process.exit();
  }
  process.stdout.write('.');
});

console.log('after callback');
```

## OOP Super 
* Method Overriding and Super
  * When a subclass implements a method that already exists in the superclass, it is called method overriding. This is because it is indeed overriding the superclass's method.
```javascript
// Superclass
class Person {
  constructor(name, quirkyFact) {
    this.name = name;
    this.quirkyFact = quirkyFact;
  }

  bio() {
    return `My name is ${this.name} and here's my quirky fact: ${this.quirkyFact}`;
  }
}

// Subclass
class Mentor extends Person {
  // Completely re-define the bio method since it has more to say
  bio() {
    return `I'm a mentor at Lighthouse Labs. My name is ${this.name} and here's my quirky fact: ${this.quirkyFact}`;
  }
}

// The Student class doesn't need to define bio since it can just use the one from Person

// DRIVER CODE

const bob = new Mentor('Bob Ross', 'I like mountains way too much');
console.log(bob.bio());
```
  * Super - OOP languages allow subclasses to have a reference on the parent class. This is usually done via the super keyword, and JavaScript supports it too!
  
```javascript
// Super class
class Person {
  constructor(name, quirkyFact) {
    this.name = name;
    this.quirkyFact = quirkyFact;
  }

  bio() {
    return `My name is ${this.name} and here's my quirky fact: ${this.quirkyFact}`;
  }
}

class Mentor extends Person {
  // Mentor bios need to include a bit more info
  bio() {
    return `I'm a mentor at Lighthouse Labs. ${super.bio()}`;
  }
}

// DRIVER CODE

const bob = new Mentor('Bob Ross', 'I like mountains way too much');
console.log(bob.bio());
```

## OOP Getters & Setters 
* In this activity, we explored the concept of getters and setters and how to use the get and set keywords in JavaScript. Setters allow us to validate data before assigning it to a property and getters allow us to compute a value on the fly instead of simply pulling it out of a property. The get and set keywords just make our object's interface more simple.
```javascript 
class Pizza {

  // ...

  // replace our custom getters / setters with these ones!
  get price() {
    const basePrice = 10;
    const toppingPrice = 2;
    return basePrice + this.toppings.length * toppingPrice;
  }

  set size(size) {
    if (size === 's' || size === 'm' || size === 'l') {
      this._size = size;
    }
  }
}

let pizza = new Pizza();

pizza.price;      // instead of getPrice()
pizza.size = 's'; // instead of setSize(size)

```
* Setters - have to change property we store value into, to a different name from the setter. Otherwise we'll end up with an infinite loop where the setter calls this.size which then calls the setter. 

## OOP 
* Java isn't private, if you use _ it signals to other developers to not access something directly; 
* Classes should only have one job! 
