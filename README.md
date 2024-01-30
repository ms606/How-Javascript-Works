# How-Javascript-Works

Section 1 --------------------------------- Basic Knowledge <br />
Section 2 --------------------------------- About Javascript Engine <br />
Section 3 --------------------------------- Fundaments II ( Context / IIFE ) <br />
Section 4 --------------------------------- Types <br />
Section 5 --------------------------------- The 2 Pillars: Closure and Prototypal Inheritance <br />
Section 6 --------------------------------- Object Oriented Programming <br />
Section 7 --------------------------------- Upcoming <br />
Section 8 --------------------------------- Upcoming <br />
Section 9 --------------------------------- Asynchronous Javascript <br />
Section 10 -------------------------------- Bugs & Error handling <br />

#### Section 1: 
Basic knowledge: 
###### 1. About Javascript V8 engine
The V8 engine is an open-source high-performance JavaScript engine, written in C++ and used in the Chrome browser, and powers Node JS. In the V8 engine, the interpreter outputs bytecode. It is used in Chrome and Node.js, among others. It implements ECMAScript and WebAssembly and runs on Windows 7 or later, macOS 10.12+, and Linux systems that use x64, IA-32, ARM, or MIPS processors. 

###### 2. Parser
Parsing is the process of analyzing the source code, checking it for errors, and breaking it up into parts.
When JavaScript parses code, it does two things:

It breaks down the code into tokens, which are the smallest units of the code (like a single word in a sentence).
It organizes these tokens into a structure that shows the relationships between them. This is known as an Abstract Syntax Tree (AST). Think of it as a family tree that defines how each part of the code relates to the others.

``` javascript

function sum(a, b) {
  return a + b;
}

```
In the first step, the parser would break this down into tokens such as ```function```, ```sum```, ```(```, ```a```, ```,```, ```b```, ```)```, ```{```, ```return```, ```a```, ```+```, ```b```, ```;```, and ```}```.

In the second step, it would create an AST. At the top of the tree would be the function keyword, with branches leading to sum, a, b, and the body of the function. In the function body, another branch would lead to the return keyword, which would have its own branches to a, +, and b.

More detailed Visual Representation can be found here <a href=https://dev.to/lydiahallie/javascript-visualized-the-javascript-engine-4cdf> JavaScript Visualized: the JavaScript Engine </a>

###### 3. eval() 
 A function in js that evaluates a string of JavaScript code in the context of the current execution scope. It takes the valid javascript arguments as an expression, statements, and strings of js statements and executes the code dynamically. 

``` javascript
  function greet(name) {
    console.log('Hello, ' + name + '!');
  }
  
  let functionName = 'greet';
  let userName = 'Alice';
  
  eval(functionName + '("' + userName + '")'); // Outputs: Hello, Alice!
``` 

## Section 2: 
#### 1. Javascript Engine:
    a. Parser 
    b. AST (Abstract syntax tree)
    c. Interpreter & Compilers: Int.. reads the code line by line, Com .. takes the complete code, understand it and create a new type of code in a different language. Usually creates a machine code. They both of pros and cons when compiling the code. 
   The engineers build something which combines both interpreter and compilier into  called JIT Complier (just in time) in V8 engine.
   d. Profiler, watches the code and sees what we can do to optimise it, sees what code runs how many times. 
#### 2. Bytecode: code interpreted by js engine to run. You can not run the byte code just itself you need an engine. 
#### 3. Javascript is not just an intepreted language, but alot of it depends on the implementation. 
#### 4. Optimising js code:
    1. HIDDEN CLASSES: Writing a predictable code for machines and humans both like it. Helps work faster. 
    2. INLINE CACHING: Simple terms inline caching relies upon the observation that repeated calls to the same method tend to occur on the same type of object.
After two successful calls of the same method to the same hidden class, V8 omits the hidden class lookup and simply adds the offset of the property to the object pointer itself. 
If you create two objects of the same type, but with different hidden classes (as we did in the example earlier), V8 won’t be able to use inline caching because even though the two objects are of the same type, their corresponding hidden classes assign different offsets to their properties.

https://richardartoul.github.io/assets/hidden-classes/diffHiddenClasses.jpg

Optimization takeaways
Always instantiate your object properties in the same order so that hidden classes, and subsequently optimized code, can be shared.
Adding properties to an object after instantiation will force a hidden class change and slow down any methods that were optimized for the previous hidden class. Instead, assign all of an object’s properties in its constructor.
Code that executes the same method repeatedly will run faster than code that executes many different methods only once (due to inline caching).
    3. Managing /*arguments*/ key words, try to avoid using that.
    4. Call Stack: Call stack stores functions and variables as your code executes. There is a state stack, or called state frame, which lets us know where we are in the code. Runs like filo, first in & last out. & we use a memory heap to point different variables, object and data that we store so we know where to look.  
    5. Call stack and memory heaps are two important location which js remembers. 

Not everytime garbage collector works perfectly, so we can't just rely on that. 

#Memory Leaks: the pcs of memory that the application has used in the past but not needed anymore but its has/won't be returned back to us to reuse as free memory. 

Three common ways for memory leak:

1. Global variable
    var a = 1;
    var b = 1;
    var c = 1;

2. Event listner
    you create an event but then you don't remove it, and you keep on adding events on events eg
    var element = document.getElementById('button')
    element.addEventListner('click', onClick)

3. Set Interval
    If we don't clear or remove setInterval's callback functions, they will never be cleared by garbage collector and always be there creating memory leak.
    setInterval(() => {
        // referencing objects
    })

##### Single threaded: Js stack is a single threaded, can only perform one calculations at a time meaning a synchronous. 
To make it async it works with the browser enviornment and uses Web API, there is a callback queue and event loop. 

##### hoisting: happening in global execution context, js code takes a pass through the complete file code and when it finds either var keyword or function it creates a func and that variable into global like var abc = undefined 
so js page doesnt prompts any error just undefined. it goes into memory heap and asks to assign the value to it. 


* WHEN TO USE FUNCTION EXPRESSION AND FUNC DECLARATION. 
* Functional scope and block scope: 
Js is a functional scope language. e.g if you use functional scoping var, variable declared you can access the variable from anywhere in the code but when using the const or let keyword you turn that into block scope and won’t be able to access from anywhere
* its bad to write variables in global space. It pollutes the global environment and there is a change of overriding the variable names and values.
* Methods: they are the function inside of the object.
  This is a simple method:
```javascript
    var rabbit = {};
    rabbit.speak = function(line) {
      console.log("The rabbit says" + line + );
    }
    rabbit.speak("I am alive.");
``` 
* This: this keyword, 
    * Gives methods access to their data objects. 
    * Execute same code for multiple objects.  
* Function currying, refers to partially passing the parameters into the functions 
* Functions and arrays are both type object in JavaScript. 
* A value of a primitive type directly contains value of a primitive type there is no ambiguity eg var a = 5  
* In a non primitive data type the value is store somewhere else in the data and the reference or pointer is stored somewhere else. 

## Section 3:
###### 1. Execution context
 Whenever js engine scans a script, it makes an environment call Execution Context that handles the entire transformation and execution of the code. 
 There are two types of execution contexts: global and function. The global execution context is created when a JavaScript script first starts to run, and it represents the global scope in JavaScript. A function execution context is created whenever a function is called, representing the function's local scope.

###### 2. Global Context 
  In js global context refers to the outermost context in the execution stack. 
  ``` javascript
    var outerVariable = 'I am in the outer scope';
    
    function outerFunction() {
      var innerVariable = 'I am in the inner scope';
      console.log(innerVariable);
      console.log(outerVariable); // Accessible because of the scope chain
    }
    
    outerFunction();

  ```

###### 3. IIFE
``` javascript
      (function () {
      function square ( x ) { return x * x ; }
      var hundred = 100;
      console.log ( square(hundred) ) ;
      })();
```
  IIFE, Immediately Invoked Function Expression.
  How IIFE helps us in writing a clean code.
  1. Encapsulation: It helps encapsulate code within a block, preventing the global scope (Avoiding global pollution). 
  2. Local Scope: The function inside will be only accessible there and not outside, this will help eliminate the naming conflicts and unintended variable exposure.
  3. Isolation: This isolates the function and any other variable or other app behavior doesn't affect it or anything else in the code base.
  4. One-time execution: It is useful for situations where you want to execute a code block once.
  5. Closure: It creates a closure, as the inner function (square) has access of the outer variable even if the function is executed. 


## Section 4: Types in Javascript
    ` 1. Statically typed language: Declare the variables before using them. (usually prevent bugs and usually helps in error handling)
            e.g. int a;
                 a = 100; `
                                    
    ` 2. Dynamically typed language: You can declare the variables without really specifying in that strictness / boundness. Here the type checking is done on the run time.    (allows to be more flexible and write the code faster)
            e.g. var a = 100; `

## Section 5: The 2 Pillars: Closure and Prototypal Inheritance

### Functions properties:
1. Assign a function to a variable. 
    var stuff = function(){}
2. Pass a function into an arguments. 
    function a(fn) {
        fn()
    }
3. Return a function as values from another function.
    function b() {
        return function c() {console.log('bye'))
    }
    
### HOF Higher Order Functions:
    They are just functions that can take a function as an argument or returns another function. Higher order function usually returns another function that performs some task.
    
### Closures: 
    Combination of functions and lexical enviornment from which it has declared. When a HOF function is created or when a function has inner more functions, js on the first phase creates a lexical scoping creates a closure box and saves all the variables and stuff that is refernced in the inner functions, so after executing functions one by one, the last function has all the values reference of the parent ones.
    In js where we write the function matters not where we call/invoke. 
    
``` Javascript
    const boo = (string) => (name) => (name2) => console.log(`${string} ${name} ${name2}`);
    
    boo('hi')('tim')('becca');
```

**In closusres the parameters are treated as a local variables** example below 
``` Javascript
    const boo = (string) => (name) => (name2) => console.log(`${string} ${name} ${name2}`);
    
    const booString = boo('hi');
    // waiting 5 years, & js engine is running 
    const booStringName = booString();
    // we will still have the `hi` parameters
    
```


#### closure memory management:
In JavaScript, every time a function is called, a new execution context is created, which includes a new variable environment. When the function completes execution, this variable environment is typically destroyed, and any variables defined within it are garbage collected by the browser.

However, if a function creates a closure by referencing a variable from its outer lexical environment, that variable and its surrounding scope are not destroyed when the function completes execution. Instead, they are retained in memory as part of the closure.

*use cases*
 1. Encapsulation
 2. Data privacy 
 3. Creating functions with persistent state 
 4. Asynchronous programming
 5. Event handling

 1. Encapsualtion EX Code

```javascript
function createCounter() {
    let count = 0; // This variable will be captured by the closure.

    // This is a closure that captures the 'count' variable.
    function increment() {
        count++;
        console.log(count);
    }

    return increment;
}

const counter = createCounter(); // Create a closure
counter(); // Logs 1
counter(); // Logs 2

// At this point, the 'createCounter' function has finished executing,
// but the 'count' variable is still accessible via the 'counter' closure.

// Garbage collection is not performed because 'count' is still in use.

// Suppose you no longer need the counter:
counter = null;

// Now, 'counter' no longer references the closure.

// If there are no other references to the closure, it can be garbage collected.

// The closure still holds a reference to 'count', preventing it from being garbage collected.

```


#### Prototypal inheritance: 
Prototypal inheritance is a fundamental concept in JavaScript that allows objects to inherit properties and methods from other objects. In js how the array and the function has been created with some base fuctions, which we can view by calling the function.__proto__.
 In JavaScript, objects have an internal property called [[Prototype]] which points to another object from which the object inherits properties and methods. This object is known as the object's prototype.

```javascript
    
```

##### Prototypal Inheritance:
We have an array, called arr, if we want to check its prototype we can do arr.__proto__, it will show the list of values/functions in an array, which is equal to Array.prototype, these both will have the same result if you see in log of inspect element. Now, if we do arr.__proto___.___proto___ it will show the object which is equal to Object.prototype , if we now do arr.__proto__.__proto__.__proto__ you will get "null", this is call protoype chaining. 
So as we have saying that everything in the javascript is an object, it maybe coming from this only. 

## Section 6: OOP (Object-oriented programming)

##### History of objects
  One philosophy is that complexity can be manageable by separating it into small compartments that are isolated from each other. These compartments can be named *objects*. An object offers methods that present an *interface* through which the object is to be used. 

##### OOP (Object-oriented programming)
Bringing together the data and its functionality into the single box called an object is the main focus in OOP, orgranizing code into units is also called as OOP. A box containing information and operations that are suppose to refer to the same concept, these operation inside an object is called atributes or state.  

In FP: The data and behaviour is two differnet things and should be kept seperately

### OOP1: 
How do we start, first we create a simple json object and give it some of the objects properties, may be add some functions in it.  
Example: 
```javascript
    const elf = {
        name: 'Orwell',
        weapon: 'bow',
        attack() {
            return 'attack with' + elf.weapon
    }
   
    const elf2 = {
        name: 'Canoppy',
        weapon: 'bow',
        attack() {
            return 'attack with' + elf.weapon
    }
    
    elf.attack();
    elf2.attack();
```    
but now if we want to create another elf we will have to redo the whole objects, so instead of that we will perform encapsulation. The state, data inside the object and then we group the functions/method seperately.
So, here comes the factory functions (*Functions that creates an object for us*.)

```javascript
    function createElf(name, weapon) {
     return {
        name: name,
        weapon: weapon,
        attack() {
            return 'attack with ' + weapon
    }
    
    const peter = createElf('peter','stones');
    petter.attack();
```
Or we can use the Object.create() 

```javascript 
    const elfFunction = {
     attack() {
      return 'attack with ' + this.weapon 
     }
    }
    
    function createElf(name, weapon){
      let newElf = Object.create(elfFunctions)
      newElf.name = name;
      newElf.weapon = weapon;
      return newElf;
    } 
    
    const peter = createElf('peter','stones');
    petter.attack();
```


#### Factory functions: 
Functions that create an object for us. 

### OOP2: 

### OOP3 Constructor Function: 
 Anything called with new is called a contructor function. All the starting with capital letters like Function(), Object(), Number() are constructor functions. We innvoke them using NEW. *All construction function should start from a capital letter as a general rule*. They are the older ways to create replaced by Object.Create now a days. THe new keyword returns the object for the func.
You can not use arrow function in Contructor function because arrow functions do not have their own this binding.
If you want to add any property to a construnctor function you will have to do it through ```this``` keyword 
e.g 
function Elf(name, weapon) {
 * this.name = name;
  this.weapon = weapon; *
}
 
``` Note: When in JS we assign the number to any variable (var a = 5), internal it creates a constructor function and saves it in an object like [Number 5]. In JS everything besides null and undefined is an object and has a constructor function ```

### Implicit binidng: 
Implicit Binding is applied when you invoke a function in an Object using the dot notation. this in such scenarios will point to the object using which the function was invoked. Or simply the object on the left side of the dot.

### Explicit binding:

### Inheritance
    This how we can extend the class Object in JS, add a constructor to a new class, call the parameters we want to use in the new class, and if you want something newly created into this new class, do the ```this.newVariable = newVariable``` so you can use that further. Eg. 
```javascript    
    class Character {
  constructor(name, weapon) {
    this.name = name;
    this.weapon = weapon;
  }
  attack() {
    return 'atack with ' + this.weapon
  }
}

class Elf extends Character { 
  constructor(name, weapon, type) {
    // console.log('what am i?', this); this gives an error
    super(name, weapon) 
    console.log('what am i?', this);
    this.type = type;
  }
}
```javascript    
    
    
    
    
 ### 4 pillars of oop: 
1. Encapsulation 

2. Abstraction: meaning hiding the complexity from the user. You insntantiate the class and poof you have a var with all the properties. 

3. Inheritance: By inheriting from other classes we aboid writing same code again and again & save memory.
 

Exactly what new keyword does: ?? 

 1. anabhsd


## Section 7: Functional Programming
 Concept is there is a data and the interaction of data. Generally the focus of functional programming is simplicity by seperating the data and functions. 
 * There is only one pillar of FP, **** Pure Functions ****
 * All objects created in FP are immutable. 

#### Pure Functions (No communication with outside world at all):
1. No Side effects: they will not effect anything outside their function state, or mutate the global values/variables, only work with their own function. EG, koyi bahir array hai andar uski values ya index pey data hai woh update na hojaye. 
2. Input ---> Output: Meaning however times we call it with a same input, the answer/ return will always be with the same output. E.G. function a(num1, num2) { 
    return num1 + num2
   }
   It should have a refrential dependency/transparency ?. 
```` Esence of function programming is to build a program with very small, useable, predictable pure functions. ````

##### What to remember when programing in FP.
1. Perform singlular Task
2. Should have a return statement, always an input and output.
3. Pure, quality mentioned above.
4. No shared state with outer world or global values.
5. Imutable state, always return the new state and not update anything of outer parameters.
6. Composable. 
7. Predictable... self explainatory. 

##### 6. Composable: 
 Meaning the ability to combine small, reusable function into one larger complex function. These can be combined into different complex ways.
JS, is a fp emphasizes to use a higher order functions, which are func that can take other func as an arg or return func as a values. 
``` javascript
 const double = x => x * 2; 
 const add = y => x => x + y; 
 
 const doubleAndAdd = add(5)(double(3));
 console.log(doubleAndAdd);
````

#### Idempotence
Idempotence is any function that can be executed several times without changing the final result beyond its first iteration.
EX Math.abs(Math.abs(-50))

#### Imperative 
    A code that tells the machine what to do & how to do it. The kind where computer likes it. 
    ``` EX for (i=1; i < 99; i++) {
    console.log(i)
    }
    
#### Declarative 
    A code that tells what to do and what should happen, doesn't tells how to do it. The kind how human operates. Always goes through something machine code or imperative process. 
    ``` EX [1,2,3].forEach( item => console.log(item) ) 
    
#### Immutability 

#### Structural sharing

### HOF
Does one of two things it either One of more functions as an argument OR returns a function as a result (often calls as callback). 
const hof = () => () => 5; 
        OR
const hof = (fn) => fn(5);
hof(function a(x){return x});

#### Closure 
EG
const closure = function(){
 let count = 0;
 return function increment() 
  count++
  return count;
  }
}
    
#### Currying 
It is a function that takes multiple parameters one by one (it has closure kinda element in them)
EG. 
const curriedMultiply = (a) => (b) => a * b ; 
curriedMultiply(5)(2); //10

#### Memoization 

Sometimes, function calls can be an expensive task as they involve high processing and performing it many times. But there is a way we can optimize that and it is called caching.
For example, let's say we have to perform the factorial of number 50. We build a function in Js that does it and gives the answer, perfect. Now lets say we have then to perform the factorial of 51. Boom, the computer runs the function again and gets the factorial of 51. Now, imagine if we can save the value of earlier factorial of 50, and get that value in between the factorial of 51. We can get the factorial result in a very less time. 

Let's say here is a simple factorial function in Js 

```javascript
    function fac(x:any){
        let a = 1; 
        for(var n = x; n > 0; n--){
           a = a * n;
        }
        console.log(a);
        return a  
      }
    
      fac(8)  
```
Now converting that into a recursive function 

```javascript
  function factorial(num:number): number{
    if (num === 0){
      return 1;
    }else {
      console.log(num,num * factorial(num- 1),';');
      return num * factorial(num- 1)
    }
  }

  const facr = factorial(8)
```

#### Here's what a simple memoized function look like. 

``` javascript
  const memoizeAdd = () => {
    let cache: any = []
    return (n: any) => {
      console.log(cache, 'cache check' , n);

      if (n in cache) {
        console.log("fetching data");
        return cache[n];
      } else {
        console.log("calculating result");
        let result = n + 50;
        cache[n] = result;
        return result;
      }
    };
  };

  const newAdd = memoizeAdd();
  console.log(newAdd(4));
  console.log(newAdd(44));
  console.log(newAdd(44333));
  console.log(newAdd(1));
  console.log(newAdd(4));

```

#### Compose   

#### Difference between FP and OOP
1. FP is about performing many different operation when data is fixed.  
   OOP performs few operation on common data. 
   
2. FP stateless, state is immuteable. 
   OOP statefull, we are modifying state. 

3. Pure functions, only update stuff inside the function, can run parellel programs altogethor as it wont update the global states. 
   OOP, side effect, methods manilpulate inside state. 

4. Declarative, its about what we are doing. Better in performing large data for our applications eg. machine learning, becuase you can run on multiple processors
   Imperative, How about it we want to done. EG GAME 

## Section 9: Asynchronous Javascript
### Javascript Notes
    * Promises: An object that may produce single value sometime in the future. Either its a resolved value or a reason that it's not resolved (rejected). 
      A promise can be in total three possible states, Fullfilled, Rejected or Pending. 
    * Promises is the replacement of callback, it was messy and there were alot of nested callbacks for alot of scenarios. 
    * Async await: A function that returns a promise. One benifit is that more easily readable. 
    * Async uses "async" keyword before function and "await" keyword after an executed func.
    * In javascript runtime we have three two different queues *1. Callback Queue - Task Queue (
    2. Job Queue - Microtask Queue (It has more priority than the callback queue). 


    Promises sample code 
   
    ``` javascript
          const myPromise = new Promise((resolve, reject) => {
    const success = fetch(
      "http://103.164.49.101:2626/api/salesProductProcessedBoxes/5"
    )
      .then((response) => {
        if (response.ok) {
          // console.log(response.text())
          return response.text();
        } else {
          throw new Error("Error in API: no data found");
        }
      })
      .then((result) => {
        //console.log(result, 'inside result');
        resolve(result);
      })
      .catch((error) => {
        // console.log(error,'error inside catch')
        reject(error);
      });
    console.log(success, "success");
  });

  myPromise
    .then((result) => {
      console.log(result, "inside result");
    })
    .catch((reject) => {
      console.log(reject, "inside reject");
    });


## Section 10: Modules In Javascript
##### General Intro: 
  Modules divide programs into clusters of code that, by some criterion belong together. 
    1. There is module scope which lies between global scope and function scope. 
    2. We can combine multiple function scope in Module Scope but still not pollute the global scope
    3. Module Pattern code eg
        var anyName // anyName is a global variable
              = (function(){ 
          .... // the code we need to write
          }
          return {
           .... // public return api, this will be accessible on public scope
          }
        }) ( ... Pass here the dependencies )
    4. AMD Moduler helps loading the js async, which other moduler like common js etc doesnt

## Section 15: Intermediate Javascript
#### Chaining Operator: 

#### Nullish coalesing operator



<div style="page-break-after: always;"></div> 


#### Anti-Patters
Examples of anti-patters in JavaScript are the following:
1. Polluting the global namespaces by defining large numbers of variables in a global context.
2. Passing strings rather than functions to either setTimeout or setInterval as this triggers the use of eval() internally.
3. Modifying the Object class prototype.
4. Using JavaScript in an inline form as this is inflexible.
5. The use of document.write where native DOM alternatives such as document.createElement are more appropriate.

#### Section 10: Bugs & Error Handling  
1. Strict mode
   Adding  "use strict" at the top of a function or a js file, makes sure to check the types, it will not declare any global variables if you forget to create your self.
2. Debugging
   We know that our program is malfunctioning, and we want to find out why. This is where you must resist the urge to start making random changes to the code.     Instead, think. Analyze what is happening and come up with a theory of why it might be happening. Then, make additional observations to test this theory—or, if you don’t yet have a theory, make additional observations that might help you come up with one. Putting a few strategic console.log calls into the program is a good way
to get additional information about what the program is doing.
3. Error Propagation
   Understanding the difference between throwing an exception and an error. Exceptions are not errors, exceptions are anomalous or exceptional conditions that require special processing. There are two types of such conditions: *operational* and *non-operational*.
   * The input validation errors are operational errors. A failed login attempt is an *operational* situation. This is expected and can be handled.
   * Non-operational condition is when an application cannot automatically resolve and error and then it should be ended. EX. An App should store data in a DB as some of the functionality has been lost which is supposed to be critical and is in non *operational state*. So, the app has to be terminated and the restarted.
   - There are two ways to propagate an error in JavaScript and TypeScript:
   1. Throw an exception. It terminates the process if not handled. It should be used when the intention is to stop an application when something goes wrong.
   2. Return an error. It denotes an expected error case scenario and does not require an application termination.

##### Exception Handling


###### Some considerations where to use try-catch blocks.
1. Critical Operations: Use a try-catch block for code where it calls API, database queries, or any operations that depend on external resources. This helps prevent unhandled errors from crashing your applications.
```javascript
  async function fetchData(){
  try {
   const response = await fetch('https://api.example.com/data');
   const data = await response.json();
  } catch(error){
   console.log(error,'Error fetching data');
   // Show more friendly data
  }
``` 
