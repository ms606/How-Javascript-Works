# How-Javascript-Works

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
* This: this keyword, 
    * Gives methods access to their data objects. 
    * Execute same code for multiple objects.  
* Function currying, refers to partially passing the parameters into the functions 
* Functions and arrays are both type object in JavaScript. 
* A value of a primitive type directly contains value of a primitive type there is no ambiguity eg var a = 5  
* In a non primitive data type the value is store somewhere else in the data and the reference or pointer is stored somewhere else. 



## Section 4: Types in Javascript
    ` 1. Statically typed language: Declare the variables before using them. (usually prevent bugs and usually helps in error handling)
            e.g. int a;
                 a = 100; `
                                    
    ` 2. Dynamically typed language: You can declare the variables without really specifying in that strictness / boundness. Here the type checking is done on the run time.    (allows to be more flexible and write the code faster)
            e.g. var a = 100; `
            
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
    
#### closure memory management:
In JavaScript, every time a function is called, a new execution context is created, which includes a new variable environment. When the function completes execution, this variable environment is typically destroyed, and any variables defined within it are garbage collected by the browser.

However, if a function creates a closure by referencing a variable from its outer lexical environment, that variable and its surrounding scope are not destroyed when the function completes execution. Instead, they are retained in memory as part of the closure.

#### Prototypal inheritance: 
Prototypal inheritance is a fundamental concept in JavaScript that allows objects to inherit properties and methods from other objects. In js how the array and the function has been created with some base fuctions, which we can view by calling the function.__proto__.
 In JavaScript, objects have an internal property called [[Prototype]] which points to another object from which the object inherits properties and methods. This object is known as the object's prototype.


## Section 6: OOP (Object oriented programming)
Bringing together the data and its functionality into the single box called an object is the main focus in OOP, orgranizing code into units is also called as OOP. A box containing information and operations that are suppose to refer to the same concept, these operation inside an object is called atributes or state.  

In FP: In FP, the data and behaviour is two differnet things and should be kept seperately

#### Factory functions: 
Functions that creates an objects for us. 

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

### Implicit binidng

### Explicit binding

### Inheritance
    This how we can extend the class Object in JS, add a constructor to a new class, call the parameters we want to use in the new class, and if you want something newly created into this new class, do the ```this.newVariable = newVariable``` so you can use that further. Eg. 
````    
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
````    
    
    
    
    
 ### 4 pillars of oop: 
1. Encapsulation 

2. Abstraction: meaning hiding the complexity from the user. You insntantiate the class and poof you have a var with all the properties. 

3. Inheritance: By inheriting from other classes we aboid writing same code again and again & save memory.
 

Exactly what new keyword does: ?? 

 1. 


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
```` EG
 const double = x => x * 2; 
 const add = y => x => x + y; 
 
 const doubleAndAdd = add(5)(double(3));
 console.log(doubleAndAdd);
````

#### Idempotence
Idempotence is any function that can be executed several times without changing the final result beyond its first iteration.
EX Math.abs(Math.abs(-50))

#### Imperative 

#### Declarative 
Always goes through something machine code or imperative process. 

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
It is a function that takes multiple parameter one by one (it has closure kinda element in them)
EG. 
const curriedMultiply = (a) => (b) => a * b ; 
curriedMultiply(5)(2); //10

#### Memoization 

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
    2. Job Queue - Microtask Queue (It has more priority than the callback queue). * 

## Section 10: Modules In Javacript
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
