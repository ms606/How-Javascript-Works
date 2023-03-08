# How-Javascript-Works

Section 2: 
1. Javascript Engine:
    a. Parser 
    b. AST (Abstract syntax tree)
    c. Interpreter & Compilers: Int.. reads the code line by line, Com .. takes the complete code, understand it and create a new type of code in a different language. Usually creates a machine code. They both of pros and cons when compiling the code. 
   The engineers build something which combines both interpreter and compilier into  called JIT Complier (just in time) in V8 engine.
   d. Profiler, watches the code and sees what we can do to optimise it, sees what code runs how many times. 
2. Bytecode: code interpreted by js engine to run. You can not run the byte code just itself you need an engine. 
3. Javascript is not just an intepreted language, but alot of it depends on the implementation. 
4. Optimising js code:
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
