# 📘 JavaScript Interview Questions (Beginner to Advanced)

A complete guide with **JavaScript Interview Questions** — from **core concepts** to **ES6+ features**, including **real-world scenarios**, **performance tips**, and **best practices**. This list is crafted to help you **revise**, **understand deeply**, and **crack your next frontend or MERN stack interview** with confidence.

---
#### 🔹 Section 1: Core Concepts & Syntax
<details>
  <summary>What are the differences between var, let, and const?</summary>
  
  **Scope:**
  - `var`: Function-scoped or globally-scoped
  - `let` & `const`: Block-scoped
  
  **Hoisting:**
  - `var`: Hoisted and initialized with `undefined`
  - `let` & `const`: Hoisted but not initialized (Temporal Dead Zone)
  
  **Re-declaration:**
  - `var`: Can be re-declared
  - `let` & `const`: Cannot be re-declared in same scope
  
  **Re-assignment:**
  - `var` & `let`: Can be re-assigned
  - `const`: Cannot be re-assigned (but objects/arrays can be mutated)
  
  ```javascript
  // var example
  function example() {
    if (true) {
      var x = 1;
    }
    console.log(x); // 1 (accessible outside block)
  }
  
  // let/const example
  function example2() {
    if (true) {
      let y = 1;
      const z = 2;
    }
    console.log(y); // ReferenceError
  }
  ```
</details>

<details>
  <summary>What is hoisting in JavaScript?</summary>
  
  Hoisting is JavaScript's behavior of moving variable and function declarations to the top of their scope during compilation phase.
  
  **Function Hoisting:**
  ```javascript
  console.log(myFunction()); // "Hello!" - works due to hoisting
  
  function myFunction() {
    return "Hello!";
  }
  ```
  
  **Variable Hoisting:**
  ```javascript
  console.log(x); // undefined (not ReferenceError)
  var x = 5;
  
  // Equivalent to:
  // var x;
  // console.log(x);
  // x = 5;
  ```
  
  **let/const Hoisting (Temporal Dead Zone):**
  ```javascript
  console.log(y); // ReferenceError
  let y = 10;
  ```
</details>

<details>
  <summary>What are truthy and falsy values?</summary>
  
  **Falsy values (8 total):**
  - `false`, `0`, `-0`, `0n`, `""`, `null`, `undefined`, `NaN`
  
  **Everything else is truthy**, including:
  - `"0"`, `"false"`, `[]`, `{}`, `function(){}`
  
  ```javascript
  // Examples
  if ("") console.log("won't run"); // falsy
  if ("0") console.log("will run"); // truthy
  if ([]) console.log("will run"); // truthy
  if ({}) console.log("will run"); // truthy
  
  // Practical use
  const name = user.name || "Anonymous";
  ```
</details>

<details>
  <summary>What is the difference between == and ===?</summary>
  
  **== (Loose Equality):**
  - Performs type coercion before comparison
  - Can lead to unexpected results
  
  **=== (Strict Equality):**
  - No type coercion
  - Compares both value and type
  
  ```javascript
  // == examples
  1 == "1"        // true (string coerced to number)
  true == 1       // true 
  null == undefined // true
  [] == ""        // true
  
  // === examples
  1 === "1"       // false
  true === 1      // false
  null === undefined // false
  
  // Best practice: always use ===
  ```
</details>

<details>
  <summary>How does JavaScript handle type coercion?</summary>
  
  JavaScript automatically converts types when needed (implicit coercion).
  
  **String Coercion:**
  ```javascript
  "5" + 3        // "53" (number to string)
  "5" + true     // "5true"
  "5" + null     // "5null"
  ```
  
  **Number Coercion:**
  ```javascript
  "5" - 3        // 2 (string to number)
  "5" * "2"      // 10
  +"42"          // 42 (unary + operator)
  ```
  
  **Boolean Coercion:**
  ```javascript
  Boolean("")    // false
  Boolean("0")   // true
  Boolean([])    // true
  Boolean({})    // true
  ```
</details>

<details>
  <summary>What are template literals and how are they useful?</summary>
  
  Template literals use backticks (`) and allow:
  - String interpolation with `${}`
  - Multi-line strings
  - Tagged templates
  
  ```javascript
  const name = "Deepak";
  const age = 25;
  
  // String interpolation
  const message = `Hello, ${name}! You are ${age} years old.`;
  
  // Multi-line strings
  const html = `
    <div>
      <h1>${name}</h1>
      <p>Age: ${age}</p>
    </div>
  `;
  
  // Expressions
  const result = `Total: ${10 + 20}`;
  
  // Tagged templates
  function highlight(strings, ...values) {
    return strings.reduce((result, string, i) => {
      return result + string + (values[i] ? `<mark>${values[i]}</mark>` : '');
    }, '');
  }
  
  const highlighted = highlight`Hello ${name}, you are ${age} years old!`;
  ```
</details>

<details>
  <summary>What are arrow functions and how do they differ from traditional functions?</summary>
  
  **Syntax:**
  ```javascript
  // Traditional function
  function add(a, b) {
    return a + b;
  }
  
  // Arrow function
  const add = (a, b) => a + b;
  
  // Various arrow function forms
  const single = x => x * 2;           // single parameter
  const multiple = (x, y) => x + y;    // multiple parameters
  const block = x => {                 // block body
    const result = x * 2;
    return result;
  };
  ```
  
  **Key Differences:**
  1. **`this` binding**: Lexically bound (inherited from enclosing scope)
  2. **No `arguments` object**
  3. **Cannot be used as constructors**
  4. **No hoisting** (function expressions)
  
  ```javascript
  // this binding example
  const obj = {
    name: "Deepak",
    traditional: function() {
      console.log(this.name); // "Deepak"
    },
    arrow: () => {
      console.log(this.name); // undefined (window.name)
    }
  };
  ```
</details>

<details>
  <summary>What is the typeof operator and what are some tricky results it returns?</summary>
  
  `typeof` returns a string indicating the type of operand.
  
  **Normal cases:**
  ```javascript
  typeof 42          // "number"
  typeof "hello"     // "string"
  typeof true        // "boolean"
  typeof undefined   // "undefined"
  typeof Symbol()    // "symbol"
  typeof 123n        // "bigint"
  typeof function(){} // "function"
  ```
  
  **Tricky cases:**
  ```javascript
  typeof null        // "object" (famous bug in JS)
  typeof []          // "object"
  typeof {}          // "object"
  typeof new Date()  // "object"
  typeof /regex/     // "object"
  typeof NaN         // "number"
  
  // Better type checking
  Array.isArray([])           // true
  Object.prototype.toString.call(null) // "[object Null]"
  ```
</details>

<details>
  <summary>What is the difference between primitive and reference types?</summary>
  
  **Primitive Types:**
  - `number`, `string`, `boolean`, `undefined`, `null`, `symbol`, `bigint`
  - Stored by value
  - Immutable
  - Passed by value
  
  **Reference Types:**
  - `object`, `array`, `function`
  - Stored by reference
  - Mutable
  - Passed by reference
  
  ```javascript
  // Primitives
  let a = 10;
  let b = a;
  a = 20;
  console.log(b); // 10 (unchanged)
  
  // References
  let obj1 = { x: 10 };
  let obj2 = obj1;
  obj1.x = 20;
  console.log(obj2.x); // 20 (changed)
  
  // Function parameters
  function modifyPrimitive(num) {
    num = 100;
  }
  function modifyObject(obj) {
    obj.x = 100;
  }
  
  let number = 10;
  let object = { x: 10 };
  
  modifyPrimitive(number);
  modifyObject(object);
  
  console.log(number); // 10 (unchanged)
  console.log(object.x); // 100 (changed)
  ```
</details>

<details>
  <summary>How does the this keyword work in different contexts?</summary>
  
  `this` refers to the object that is executing the current function.
  
  **Global Context:**
  ```javascript
  console.log(this); // Window object (browser) or global (Node.js)
  ```
  
  **Object Method:**
  ```javascript
  const obj = {
    name: "Deepak",
    greet() {
      console.log(this.name); // "Deepak"
    }
  };
  ```
  
  **Constructor Function:**
  ```javascript
  function Person(name) {
    this.name = name;
  }
  const person = new Person("Deepak");
  ```
  
  **Arrow Functions:**
  ```javascript
  const obj = {
    name: "Deepak",
    greet: () => {
      console.log(this.name); // undefined (lexical this)
    }
  };
  ```
  
  **Event Handlers:**
  ```javascript
  button.addEventListener('click', function() {
    console.log(this); // button element
  });
  
  button.addEventListener('click', () => {
    console.log(this); // Window object
  });
  ```
  
  **Explicit Binding:**
  ```javascript
  const obj = { name: "Deepak" };
  function greet() {
    console.log(this.name);
  }
  
  greet.call(obj);    // "Deepak"
  greet.apply(obj);   // "Deepak"
  greet.bind(obj)();  // "Deepak"
  ```
</details>

#### 🔹  Section 2: Functions, Scopes, Closures

<details>
  <summary>What is the difference between function declaration and function expression?</summary>
  
  **Function Declaration:**
  ```javascript
  // Hoisted - can be called before definition
  console.log(add(2, 3)); // 5
  
  function add(a, b) {
    return a + b;
  }
  ```
  
  **Function Expression:**
  ```javascript
  // Not hoisted - cannot be called before definition
  console.log(add(2, 3)); // TypeError
  
  const add = function(a, b) {
    return a + b;
  };
  ```
  
  **Named Function Expression:**
  ```javascript
  const factorial = function fact(n) {
    return n <= 1 ? 1 : n * fact(n - 1);
  };
  ```
  
  **Key Differences:**
  - **Hoisting**: Declarations are hoisted, expressions are not
  - **Conditional Creation**: Expressions can be created conditionally
  - **IIFE**: Only expressions can be immediately invoked
</details>

<details>
  <summary>What is a closure and how is it used?</summary>
  
  A closure is a function that has access to variables in its outer (enclosing) scope even after the outer function has returned.
  
  ```javascript
  function outerFunction(x) {
    // This is the outer function's scope
    
    function innerFunction(y) {
      // This inner function has access to x
      console.log(x + y);
    }
    
    return innerFunction;
  }
  
  const closure = outerFunction(10);
  closure(5); // 15
  ```
  
  **Practical Examples:**
  
  **1. Data Privacy:**
  ```javascript
  function createCounter() {
    let count = 0;
    
    return {
      increment: () => ++count,
      decrement: () => --count,
      getCount: () => count
    };
  }
  
  const counter = createCounter();
  console.log(counter.getCount()); // 0
  counter.increment();
  console.log(counter.getCount()); // 1
  ```
  
  **2. Function Factories:**
  ```javascript
  function multiplyBy(factor) {
    return function(number) {
      return number * factor;
    };
  }
  
  const double = multiplyBy(2);
  const triple = multiplyBy(3);
  
  console.log(double(5)); // 10
  console.log(triple(5)); // 15
  ```
</details>

<details>
  <summary>How does lexical scoping work in JavaScript?</summary>
  
  Lexical scoping means that the accessibility of variables is determined by where they are declared in the code structure.
  
  ```javascript
  const globalVar = "global";
  
  function outerFunction() {
    const outerVar = "outer";
    
    function innerFunction() {
      const innerVar = "inner";
      
      // Has access to all three variables
      console.log(globalVar); // "global"
      console.log(outerVar);  // "outer"
      console.log(innerVar);  // "inner"
    }
    
    innerFunction();
    // console.log(innerVar); // ReferenceError
  }
  
  outerFunction();
  ```
  
  **Scope Chain:**
  1. Local scope (current function)
  2. Enclosing scope (outer functions)
  3. Global scope
  
  ```javascript
  let x = 1;
  
  function a() {
    let x = 2;
    
    function b() {
      let x = 3;
      console.log(x); // 3 (local scope wins)
    }
    
    b();
    console.log(x); // 2
  }
  
  a();
  console.log(x); // 1
  ```
</details>

<details>
  <summary>What are higher-order functions? Can you give an example?</summary>
  
  Higher-order functions are functions that:
  - Take other functions as arguments, OR
  - Return functions as results
  
  **Examples:**
  
  **1. Functions that take functions as arguments:**
  ```javascript
  const numbers = [1, 2, 3, 4, 5];
  
  // map, filter, reduce are higher-order functions
  const doubled = numbers.map(x => x * 2);
  const evens = numbers.filter(x => x % 2 === 0);
  const sum = numbers.reduce((acc, x) => acc + x, 0);
  
  // Custom higher-order function
  function processArray(arr, callback) {
    const result = [];
    for (let i = 0; i < arr.length; i++) {
      result.push(callback(arr[i]));
    }
    return result;
  }
  
  const squared = processArray([1, 2, 3], x => x * x);
  ```
  
  **2. Functions that return functions:**
  ```javascript
  function createMultiplier(multiplier) {
    return function(x) {
      return x * multiplier;
    };
  }
  
  const double = createMultiplier(2);
  const triple = createMultiplier(3);
  
  console.log(double(5)); // 10
  console.log(triple(4)); // 12
  ```
  
  **3. Both (function composition):**
  ```javascript
  function compose(f, g) {
    return function(x) {
      return f(g(x));
    };
  }
  
  const addOne = x => x + 1;
  const double = x => x * 2;
  
  const addOneThenDouble = compose(double, addOne);
  console.log(addOneThenDouble(3)); // 8 (3 + 1 = 4, 4 * 2 = 8)
  ```
</details>

<details>
  <summary>What is currying in JavaScript?</summary>
  
  Currying is transforming a function with multiple arguments into a sequence of functions, each taking a single argument.
  
  **Basic Example:**
  ```javascript
  // Regular function
  function add(a, b, c) {
    return a + b + c;
  }
  
  // Curried version
  function curriedAdd(a) {
    return function(b) {
      return function(c) {
        return a + b + c;
      };
    };
  }
  
  // Usage
  console.log(add(1, 2, 3)); // 6
  console.log(curriedAdd(1)(2)(3)); // 6
  
  // Partial application
  const addOne = curriedAdd(1);
  const addOneAndTwo = addOne(2);
  console.log(addOneAndTwo(3)); // 6
  ```
  
  **Arrow Function Version:**
  ```javascript
  const curriedAdd = a => b => c => a + b + c;
  ```
  
  **Generic Curry Function:**
  ```javascript
  function curry(fn) {
    return function curried(...args) {
      if (args.length >= fn.length) {
        return fn.apply(this, args);
      }
      return function(...nextArgs) {
        return curried.apply(this, args.concat(nextArgs));
      };
    };
  }
  
  const add = (a, b, c) => a + b + c;
  const curriedAdd = curry(add);
  
  console.log(curriedAdd(1)(2)(3)); // 6
  console.log(curriedAdd(1, 2)(3)); // 6
  console.log(curriedAdd(1)(2, 3)); // 6
  ```
  
  **Practical Use Cases:**
  - Event handling
  - Reusable configuration functions
  - Functional composition
</details>

#### 🔹 Section 3: Objects, Arrays & DOM
<details>
  <summary>What's the difference between dot and bracket notation?</summary>
  
  **Dot Notation:**
  - Simpler and more concise
  - Cannot use reserved words or start with a number
  - Example: `obj.property`
  
  **Bracket Notation:**
  - More flexible, can use any string or variable
  - Useful for dynamic property access
  - Example: `obj["property"]` or `obj[varName]`
  
  ```javascript
  const obj = {
    "first-name": "Deepak",
    age: 25
  };
  
  console.log(obj.first-name); // SyntaxError
  console.log(obj["first-name"]); // "Deepak"
  
  const key = "age";
  console.log(obj[key]); // 25
  ```
</details>

<details>
  <summary>How does object destructuring work?</summary>
  
  Object destructuring allows unpacking values from objects into distinct variables.
  
  **Basic Syntax:**
  ```javascript
  const obj = { x: 1, y: 2 };
  const { x, y } = obj;
  
  console.log(x); // 1
  console.log(y); // 2
  ```
  
  **New Variable Names:**
  ```javascript
  const obj = { a: 1, b: 2 };
  const { a: alpha, b: beta } = obj;
  
  console.log(alpha); // 1
  console.log(beta); // 2
  ```
  
  **Default Values:**
  ```javascript
  const obj = { x: 1 };
  const { x, y = 10 } = obj;
  
  console.log(x); // 1
  console.log(y); // 10
  ```
  
  **Nested Destructuring:**
  ```javascript
  const obj = { p: 1, q: { r: 2 } };
  const { p, q: { r } } = obj;
  
  console.log(p); // 1
  console.log(r); // 2
  ```
  
  **Function Parameters:**
  ```javascript
  function logCoords({ x, y }) {
    console.log(`X: ${x}, Y: ${y}`);
  }
  
  const point = { x: 10, y: 20 };
  logCoords(point); // "X: 10, Y: 20"
  ```
</details>

<details>
  <summary>What are the different ways to clone an object?</summary>
  
  **1. Shallow Copy with Object.assign:**
  ```javascript
  const obj = { a: 1, b: 2 };
  const clone = Object.assign({}, obj);
  ```
  
  **2. Shallow Copy with Spread Operator:**
  ```javascript
  const obj = { a: 1, b: 2 };
  const clone = { ...obj };
  ```
  
  **3. Deep Copy with JSON.parse/JSON.stringify:**
  ```javascript
  const obj = { a: 1, b: { c: 2 } };
  const clone = JSON.parse(JSON.stringify(obj));
  ```
  
  **4. Deep Copy with Recursive Function:**
  ```javascript
  function deepClone(obj) {
    if (obj === null || typeof obj !== "object") {
      return obj;
    }
    
    if (Array.isArray(obj)) {
      const arrCopy = [];
      for (let item of obj) {
        arrCopy.push(deepClone(item));
      }
      return arrCopy;
    }
    
    const copy = {};
    for (let key in obj) {
      copy[key] = deepClone(obj[key]);
    }
    return copy;
  }
  
  const obj = { a: 1, b: { c: 2 } };
  const clone = deepClone(obj);
  ```
  
  **5. Using Libraries (e.g., Lodash):**
  ```javascript
  const _ = require('lodash');
  
  const obj = { a: 1, b: { c: 2 } };
  const clone = _.cloneDeep(obj);
  ```
</details>

<details>
  <summary>How do you merge two objects or arrays?</summary>
  
  **1. Merging Objects with Object.assign:**
  ```javascript
  const obj1 = { a: 1, b: 2 };
  const obj2 = { b: 3, c: 4 };
  
  const merged = Object.assign({}, obj1, obj2);
  // Merged: { a: 1, b: 3, c: 4 }
  ```
  
  **2. Merging Objects with Spread Operator:**
  ```javascript
  const obj1 = { a: 1, b: 2 };
  const obj2 = { b: 3, c: 4 };
  
  const merged = { ...obj1, ...obj2 };
  // Merged: { a: 1, b: 3, c: 4 }
  ```
  
  **3. Merging Arrays with concat:**
  ```javascript
  const arr1 = [1, 2, 3];
  const arr2 = [4, 5, 6];
  
  const merged = arr1.concat(arr2);
  // Merged: [1, 2, 3, 4, 5, 6]
  ```
  
  **4. Merging Arrays with Spread Operator:**
  ```javascript
  const arr1 = [1, 2, 3];
  const arr2 = [4, 5, 6];
  
  const merged = [...arr1, ...arr2];
  // Merged: [1, 2, 3, 4, 5, 6]
  ```
  
  **5. Deep Merge with Lodash:**
  ```javascript
  const _ = require('lodash');
  
  const obj1 = { a: 1, b: { x: 1 } };
  const obj2 = { b: { y: 2 }, c: 3 };
  
  const merged = _.merge({}, obj1, obj2);
  // Merged: { a: 1, b: { x: 1, y: 2 }, c: 3 }
  ```
</details>

<details>
  <summary>How do you loop over arrays vs objects?</summary>
  
  **Looping Over Arrays:**
  - Use `for`, `for...of`, or array methods (`forEach`, `map`, etc.)
  
  ```javascript
  const arr = [1, 2, 3];
  
  for (let i = 0; i < arr.length; i++) {
    console.log(arr[i]);
  }
  
  for (let value of arr) {
    console.log(value);
  }
  
  arr.forEach((value) => {
    console.log(value);
  });
  ```
  
  **Looping Over Objects:**
  - Use `for...in` or `Object.keys`/`Object.entries` with array methods
  
  ```javascript
  const obj = { a: 1, b: 2, c: 3 };
  
  for (let key in obj) {
    console.log(key, obj[key]);
  }
  
  Object.keys(obj).forEach((key) => {
    console.log(key, obj[key]);
  });
  
  Object.entries(obj).forEach(([key, value]) => {
    console.log(key, value);
  });
  ```
  
  **Key Differences:**
  - Arrays are ordered, objects are unordered
  - Arrays have a length property, objects do not
  - Use array methods for arrays, loop constructs for objects
</details>

<details>
  <summary>What are array methods like map(), filter(), reduce()?</summary>
  
  **map():**
  - Creates a new array by applying a function to each element
  - Does not modify the original array
  
  ```javascript
  const arr = [1, 2, 3];
  const doubled = arr.map(x => x * 2);
  // doubled: [2, 4, 6]
  ```
  
  **filter():**
  - Creates a new array with elements that pass the test implemented by the provided function
  - Does not modify the original array
  
  ```javascript
  const arr = [1, 2, 3, 4, 5];
  const evens = arr.filter(x => x % 2 === 0);
  // evens: [2, 4]
  ```
  
  **reduce():**
  - Executes a reducer function (that you provide) on each element of the array, resulting in a single output value
  - Does not modify the original array
  
  ```javascript
  const arr = [1, 2, 3, 4, 5];
  const sum = arr.reduce((acc, x) => acc + x, 0);
  // sum: 15
  ```
  
  **Chaining Example:**
  ```javascript
  const arr = [1, 2, 3, 4, 5];
  
  const result = arr
    .filter(x => x % 2 === 0)
    .map(x => x * 2)
    .reduce((acc, x) => acc + x, 0);
  
  // result: 20
  ```
</details>

<details>
  <summary>What is event delegation in the DOM?</summary>
  
  Event delegation is a technique that involves using a single event listener to manage events for multiple elements, typically by taking advantage of event bubbling.
  
  **Example Scenario:**
  - A list of items where each item has a button
  - Instead of adding a click event listener to each button, you add one to the parent element
  
  **Advantages:**
  - **Performance:** Fewer event listeners mean less memory usage and improved performance, especially with many elements
  - **Dynamic Elements:** Works for elements added in the future (e.g., via AJAX), as the event listener is on the parent
  
  **Example Code:**
  ```javascript
  // HTML structure
  <ul id="itemList">
    <li>Item 1 <button>Delete</button></li>
    <li>Item 2 <button>Delete</button></li>
    <li>Item 3 <button>Delete</button></li>
  </ul>
  
  // JavaScript
  document.getElementById('itemList').addEventListener('click', function(event) {
    if (event.target.tagName === 'BUTTON') {
      const listItem = event.target.parentNode;
      listItem.parentNode.removeChild(listItem);
    }
  });
  ```
</details>

<details>
  <summary>What is the difference between event.target and event.currentTarget?</summary>
  
  **event.target:**
  - Refers to the element that triggered the event (the "actual" target)
  - Could be a child element, if the event was triggered by a nested element
  
  **event.currentTarget:**
  - Refers to the element to which the event handler is attached (the "current" target)
  - Remains constant during the event propagation, unlike event.target
  
  **Example Code:**
  ```javascript
  // HTML structure
  <div id="parent">
    <button id="child">Click Me</button>
  </div>
  
  // JavaScript
  document.getElementById('parent').addEventListener('click', function(event) {
    console.log('event.target:', event.target.id);
    console.log('event.currentTarget:', event.currentTarget.id);
  });
  ```
  
  **In the example above:**
  - If the button is clicked:
    - `event.target` will be `"child"`
    - `event.currentTarget` will be `"parent"`
  - If the parent div is clicked:
    - Both `event.target` and `event.currentTarget` will be `"parent"`
</details>

<details>
  <summary>What are data attributes and how do you access them?</summary>
  
  Data attributes are custom attributes that start with `data-` and are used to store extra information on standard, semantic HTML elements.
  
  **Defining Data Attributes:**
  ```html
  <div id="myElement" data-user-id="123" data-role="admin"></div>
  ```
  
  **Accessing Data Attributes in JavaScript:**
  - Using `getAttribute` and `setAttribute` methods
  - Using the `dataset` property (modern browsers)
  
  **Example Code:**
  ```javascript
  // Using getAttribute
  const element = document.getElementById('myElement');
  const userId = element.getAttribute('data-user-id');
  const role = element.getAttribute('data-role');
  
  console.log(userId); // "123"
  console.log(role);   // "admin"
  
  // Using dataset
  const userId2 = element.dataset.userId;
  const role2 = element.dataset.role;
  
  console.log(userId2); // "123"
  console.log(role2);   // "admin"
  ```
  
  **Note:**
  - Data attributes are always stored as strings.
  - They are useful for embedding custom data attributes on all HTML elements.
  - They can be accessed and modified easily using JavaScript.
</details>

<details>
  <summary>How do you manipulate DOM elements using JS?</summary>
  
  JavaScript can manipulate DOM elements in several ways:
  
  **1. Selecting Elements:**
  - `getElementById`, `getElementsByClassName`, `getElementsByTagName`
  - `querySelector` and `querySelectorAll` (CSS selector syntax)
  
  **2. Modifying Elements:**
  - Changing `innerHTML`, `textContent`, or `innerText`
  - Modifying attributes with `setAttribute` or directly (e.g., `element.src = '...'`)
  - Changing styles with `style` property or `classList` methods
  
  **3. Creating and Inserting Elements:**
  - Creating elements with `document.createElement`
  - Inserting elements with `appendChild`, `insertBefore`, or `replaceChild`
  
  **4. Removing Elements:**
  - Removing with `removeChild` or `element.remove()`
  
  **Example Code:**
  ```javascript
  // HTML structure
  <div id="app"></div>
  
  // JavaScript
  const app = document.getElementById('app');
  
  // 1. Creating a new element
  const newElement = document.createElement('div');
  newElement.textContent = 'Hello, World!';
  newElement.setAttribute('data-role', 'message');
  
  // 2. Inserting the new element
  app.appendChild(newElement);
  
  // 3. Modifying the element
  newElement.style.color = 'blue';
  
  // 4. Removing the element
  // app.removeChild(newElement);
  ```
  
  **Note:**
  - Always ensure the DOM is fully loaded before manipulating it (e.g., place scripts at the end of the body or use `DOMContentLoaded` event).
  - Be cautious with `innerHTML` as it can expose your code to XSS attacks if used with untrusted content.
</details>

#### 🔹 Section 4: Asynchronous JS
<details>
  <summary>What is the event loop in JavaScript?</summary>
  
  The event loop is a mechanism that allows JavaScript to perform non-blocking I/O operations, despite being single-threaded, by offloading operations to the system kernel whenever possible.
  
  **How It Works:**
  1. Execute the top item in the stack (synchronous code).
  2. If the stack is empty, check the message queue.
  3. If there's a message in the queue, push its associated callback onto the stack.
  4. Repeat until the queue is empty or the stack is not empty.
  
  **Example:**
  ```javascript
  console.log('Start');
  
  setTimeout(() => {
    console.log('Timeout 1');
  }, 0);
  
  new Promise((resolve) => {
    console.log('Promise 1');
    resolve();
  }).then(() => {
    console.log('Promise 1 resolved');
  });
  
  setTimeout(() => {
    console.log('Timeout 2');
  }, 100);
  
  Promise.resolve().then(() => {
    console.log('Promise 2 resolved');
  });
  
  console.log('End');
  ```
  
  **Output Order:**
  1. Start
  2. Promise 1
  3. End
  4. Promise 1 resolved
  5. Promise 2 resolved
  6. Timeout 1
  7. Timeout 2
  
  **Note:**
  - The event loop enables JavaScript's concurrency model, allowing it to perform other tasks while waiting for I/O operations to complete.
  - Understanding the event loop is crucial for mastering asynchronous programming in JavaScript.
</details>

<details>
  <summary>What is the difference between setTimeout, setInterval, and requestAnimationFrame?</summary>
  
  **setTimeout:**
  - Executes a single callback after a specified delay (in milliseconds).
  - Does not repeat.
  
  **setInterval:**
  - Repeatedly executes a callback with a fixed time delay between each call.
  - Continues until cleared.
  
  **requestAnimationFrame:**
  - Tells the browser that you wish to perform an animation and requests that the browser calls a specified function to update an animation before the next repaint.
  - Optimized for animations, provides a smoother experience.
  
  **Example:**
  ```javascript
  console.log('Start');
  
  setTimeout(() => {
    console.log('setTimeout 1');
  }, 0);
  
  setInterval(() => {
    console.log('setInterval 1');
  }, 1000);
  
  requestAnimationFrame(() => {
    console.log('requestAnimationFrame 1');
  });
  
  setTimeout(() => {
    console.log('setTimeout 2');
  }, 0);
  
  requestAnimationFrame(() => {
    console.log('requestAnimationFrame 2');
  });
  
  console.log('End');
  ```
  ```
  **Output Order:**
  1. Start
  2. End
  3. requestAnimationFrame 1
  4. requestAnimationFrame 2
  5. setTimeout 1
  6. setTimeout 2
  7. setInterval 1 (after 1000ms)
  ```
  
  **Note:**
  - `setTimeout` and `setInterval` are part of the Web API, not the JavaScript language itself. They are provided by the browser (or Node.js) environment.
  - `requestAnimationFrame` is specifically designed for animations and should be preferred over `setTimeout`/`setInterval` for this purpose.
  - Always clear intervals with `clearInterval` to avoid potential memory leaks.
</details>

<details>
  <summary>What are Promises and how do they work?</summary>
  
  Promises are objects that represent the eventual completion (or failure) of an asynchronous operation and its resulting value.
  
  **States of a Promise:**
  - `pending`: Initial state, neither fulfilled nor rejected.
  - `fulfilled`: The operation completed successfully.
  - `rejected`: The operation failed.
  
  **Key Methods:**
  - `then(onFulfilled, onRejected)`: Adds fulfillment and rejection handlers to the promise, and returns a new promise resolving to the return value of the called handler.
  - `catch(onRejected)`: Adds a rejection handler callback to the promise and returns a new promise.
  - `finally(onFinally)`: Adds a handler to be called when the promise is settled, regardless of its outcome.
  
  **Example:**
  ```javascript
  const myPromise = new Promise((resolve, reject) => {
    setTimeout(() => {
      resolve('Success!');
      // or
      reject('Error!');
    }, 1000);
  });
  
  myPromise
    .then(result => {
      console.log(result); // 'Success!'
    })
    .catch(error => {
      console.log(error); // 'Error!'
    })
    .finally(() => {
      console.log('Promise settled');
    });
  ```
  
  **Note:**
  - Promises are a way to handle asynchronous operations in JavaScript, providing a cleaner alternative to callbacks.
  - They help in avoiding "callback hell" and make the code more readable and maintainable.
  - Understanding promises is crucial for working with asynchronous JavaScript, including modern features like `async`/`await`.
</details>

<details>
  <summary>How do async/await work under the hood?</summary>
  
  `async`/`await` are syntactic sugar built on top of promises, making asynchronous code look and behave like synchronous code.
  
  **How It Works:**
  - An `async` function always returns a promise. Other values are wrapped in a resolved promise automatically.
  - The `await` keyword can only be used inside `async` functions. It makes JavaScript wait until the promise is resolved or rejected, and returns the resolved value.
  
  **Example:**
  ```javascript
  function delay(ms) {
    return new Promise(resolve => setTimeout(resolve, ms));
  }
  
  async function asyncCall() {
    console.log('Calling');
    
    const result = await delay(2000);
    
    console.log('Resolved after 2 seconds');
    
    return 'Done';
  }
  
  asyncCall().then(result => console.log(result));
  ```
  
  **Output:**
  1. Calling
  2. (after 2 seconds) Resolved after 2 seconds
  3. Done
  
  **Note:**
  - `async`/`await` provides a more concise and readable way to work with asynchronous code compared to traditional promise chaining.
  - Error handling is also simplified, as you can use `try`/`catch` blocks around `await` expressions.
  - However, under the hood, `async`/`await` is still using promises, and the event loop continues to manage the asynchronous operations.
</details>

<details>
  <summary>What happens when you forget to await an async function?</summary>
  
  If you forget to `await` an `async` function, the function will return a promise immediately, and the code will continue executing without waiting for the promise to resolve or reject.
  
  **Example:**
  ```javascript
  async function foo() {
    console.log('Start');
    await delay(2000);
    console.log('End');
  }
  
  function bar() {
    console.log('Bar');
  }
  
  foo();
  bar();
  ```
  
  **Output:**
  1. Start
  2. Bar
  3. (after 2 seconds) End
  
  **Note:**
  - In the example, `bar()` is called before the promise inside `foo()` is resolved, because `foo()` is not awaited.
  - This can lead to unexpected behavior, especially if the subsequent code depends on the completion of the `async` function.
  - It's important to always `await` an `async` function or handle its returned promise appropriately.
</details>

<details>
  <summary>What is Promise chaining and error handling?</summary>
  
  Promise chaining is the process of linking multiple `.then()` calls together, allowing you to perform a series of asynchronous operations in sequence.
  
  **Example:**
  ```javascript
  asyncFunction1()
    .then(result1 => {
      // Handle result1
      return asyncFunction2(result1);
    })
    .then(result2 => {
      // Handle result2
      return asyncFunction3(result2);
    })
    .then(finalResult => {
      // Handle final result
    })
    .catch(error => {
      // Handle any error that occurred in the chain
    });
  ```
  
  **Error Handling:**
  - Errors in a promise chain can be caught using a `.catch()` method at the end of the chain.
  - If any promise in the chain is rejected, the control is passed to the nearest rejection handler.
  
  **Example:**
  ```javascript
  asyncFunction1()
    .then(result1 => {
      return asyncFunction2(result1);
    })
    .then(result2 => {
      return asyncFunction3(result2);
    })
    .catch(error => {
      // Handle error from any of the above functions
    });
  ```
  
  **Note:**
  - Promise chaining allows for cleaner and more readable asynchronous code, avoiding the "pyramid of doom" associated with nested callbacks.
  - Proper error handling in promise chains is crucial to avoid unhandled promise rejections and to ensure that errors are caught and managed appropriately.
</details>

<details>
  <summary>What is the difference between microtask and macrotask queue?</summary>
  
  Both microtasks and macrotasks are part of the JavaScript event loop, but they have different purposes and priorities.
  
  **Macrotask Queue (Task Queue):**
  - Contains tasks like `setTimeout`, `setInterval`, and I/O tasks.
  - Executes tasks in the order they were added, after the current stack is empty.
  
  **Microtask Queue (Job Queue):**
  - Contains tasks like promise callbacks (`.then`, `.catch`, `.finally`) and `MutationObserver` callbacks.
  - Has a higher priority than the macrotask queue. Microtasks are executed before the next repaint and before any macrotasks.
  
  **Example:**
  ```javascript
  console.log('Script start');
  
  setTimeout(() => {
    console.log('setTimeout 1');
  }, 0);
  
  Promise.resolve()
    .then(() => {
      console.log('Promise 1');
    })
    .then(() => {
      console.log('Promise 2');
    });
  
  setTimeout(() => {
    console.log('setTimeout 2');
  }, 0);
  
  console.log('Script end');
  ```
  
  **Output Order:**
  1. Script start
  2. Script end
  3. Promise 1
  4. Promise 2
  5. setTimeout 1
  6. setTimeout 2
  
  **Note:**
  - Understanding the difference between microtask and macrotask queues is important for mastering the JavaScript event loop and for writing efficient asynchronous code.
  - Microtasks are used for high-priority tasks that need to be executed immediately after the currently executing script and before any rendering or I/O tasks.
</details>

<details>
  <summary>How would you implement your own Promise?</summary>
  
  Implementing a basic version of a Promise involves creating an object with `pending`, `fulfilled`, and `rejected` states, and `then`, `catch`, and `finally` methods.
  
  **Basic Structure:**
  ```javascript
  class MyPromise {
    constructor(executor) {
      this.state = 'pending';
      this.value = undefined;
      this.reason = undefined;
      
      const resolve = (value) => {
        if (this.state === 'pending') {
          this.state = 'fulfilled';
          this.value = value;
        }
      };
      
      const reject = (reason) => {
        if (this.state === 'pending') {
          this.state = 'rejected';
          this.reason = reason;
        }
      };
      
      try {
        executor(resolve, reject);
      } catch (error) {
        reject(error);
      }
    }
    
    then(onFulfilled, onRejected) {
      // Handle fulfillment and rejection
      // Return a new promise
    }
    
    catch(onRejected) {
      // Handle rejection
      // Return a new promise
    }
    
    finally(onFinally) {
      // Add a handler to be called when the promise is settled
      // Return a new promise
    }
  }
  ```
  
  **Basic Usage:**
  ```javascript
  const myPromise = new MyPromise((resolve, reject) => {
    setTimeout(() => {
      resolve('Success!');
      // or
      reject('Error!');
    }, 1000);
  });
  
  myPromise
    .then(result => {
      console.log(result); // 'Success!'
    })
    .catch(error => {
      console.log(error); // 'Error!'
    })
    .finally(() => {
      console.log('Promise settled');
    });
  ```
  
  **Note:**
  - This is a very basic implementation and lacks many features and optimizations of native promises.
  - Implementing a full-fledged promise library is complex and requires handling various edge cases and ensuring compliance with the Promises/A+ specification.
  - However, this basic structure provides a starting point for understanding how promises work under the hood.
</details>

<details>
  <summary>What are use cases of Promise.all(), Promise.race()?</summary>
  
  **Promise.all():**
  - Waits for all promises to be resolved or for any to be rejected.
  - Useful for running multiple asynchronous operations in parallel and waiting for all of them to complete.
  - Returns a single promise that resolves to an array of the results.
  
  **Example:**
  ```javascript
  const promise1 = Promise.resolve(3);
  const promise2 = new Promise((resolve, reject) => {
    setTimeout(resolve, 100, 'foo');
  });
  const promise3 = 42;
  
  Promise.all([promise1, promise2, promise3]).then((values) => {
    console.log(values); // [3, "foo", 42]
  });
  ```
  
  **Promise.race():**
  - Returns a promise that resolves or rejects as soon as one of the promises in the iterable resolves or rejects, with the value or reason from that promise.
  - Useful for setting a timeout for a promise or for reacting to the first completed promise in a group.
  
  **Example:**
  ```javascript
  const promise1 = new Promise((resolve, reject) => {
    setTimeout(resolve, 500, 'one');
  });
  const promise2 = new Promise((resolve, reject) => {
    setTimeout(resolve, 100, 'two');
  });
  
  Promise.race([promise1, promise2]).then((value) => {
    console.log(value); // "two" (because it resolves first)
  });
  ```
  
  **Note:**
  - `Promise.all()` and `Promise.race()` are static methods of the `Promise` class and are used to handle multiple promises more easily.
  - They are part of the modern JavaScript (ES6+) promise implementation and are widely used in real-world applications for handling asynchronous operations.
</details>

<details>
  <summary>How does async code execute in JavaScript's single-threaded model?</summary>
  
  JavaScript executes async code in its single-threaded model using the event loop, which manages the execution of asynchronous tasks, allowing JavaScript to perform non-blocking I/O operations.
  
  **How It Works:**
  1. JavaScript engine starts and executes the script.
  2. When it encounters an async operation (like `setTimeout`, `Promise`, etc.), it offloads the operation to the system kernel or to a web API (in browsers).
  3. The engine continues executing the rest of the code without waiting for the async operation to complete.
  4. Once the async operation is complete, the callback associated with it is added to the message queue.
  5. The event loop continuously checks the call stack and the message queue.
  6. If the call stack is empty, it pushes the first callback from the message queue to the call stack, executing it.
  7. This process continues, allowing JavaScript to handle multiple async operations efficiently, despite being single-threaded.
  
  **Visual Representation:**
  ```
  Call Stack
  ┌─────────────┐
  │ Main Thread │
  └─────────────┘
         │
         ▼
  ┌─────────────┐
  │  Web APIs   │
  └─────────────┘
         │
         ▼
  ┌─────────────┐
  │  Message    │
  │    Queue     │
  └─────────────┘
  ```
  
  **Note:**
  - Understanding how async code executes in JavaScript's single-threaded model is crucial for mastering asynchronous programming and for writing efficient, high-performance JavaScript code.
  - It helps in avoiding common pitfalls and in leveraging JavaScript's concurrency model effectively.
</details>

#### 🔹 Section 5: ES6+ Features, Real-World & Optimization
<details>
  <summary>What are ES6 modules and how do they differ from CommonJS?</summary>
  
  ES6 modules are a standardized way to define and use modules in JavaScript, introduced in ECMAScript 2015 (ES6).
  
  **Key Features:**
  - **Syntax:** Uses `import` and `export` statements.
  - **Asynchronous Loading:** Modules are loaded asynchronously by default.
  - **Static Structure:** The structure of imports and exports is static and known at compile time.
  
  **Example:**
  ```javascript
  // lib.js
  export const pi = 3.14;
  export function add(x, y) {
    return x + y;
  }
  
  // app.js
  import { pi, add } from './lib.js';
  
  console.log(pi); // 3.14
  console.log(add(2, 3)); // 5
  ```
  
  **Differences with CommonJS:**
  - **Syntax:** CommonJS uses `require` and `module.exports`.
  - **Loading:** CommonJS modules are loaded synchronously, which can be a drawback for performance in some cases.
  - **Compilation:** CommonJS is a runtime module system, while ES6 modules are a compile-time module system.
  
  **Example of CommonJS:**
  ```javascript
  // lib.js
  const pi = 3.14;
  function add(x, y) {
    return x + y;
  }
  module.exports = { pi, add };
  
  // app.js
  const { pi, add } = require('./lib');
  
  console.log(pi); // 3.14
  console.log(add(2, 3)); // 5
  ```
  
  **Note:**
  - ES6 modules are now widely supported in modern JavaScript environments, including Node.js (from version 12 with the `--experimental-modules` flag, and stable from version 14).
  - They provide a more powerful and flexible way to work with modules in JavaScript, addressing many of the shortcomings of earlier module systems like CommonJS.
  - When working on modern JavaScript applications, especially with frameworks like React, Angular, or Vue, you'll be using ES6 modules.
</details>

<details>
  <summary>What are spread/rest operators and how do you use them?</summary>
  
  The spread and rest operators are represented by the same syntax: `...`. They are used for different purposes based on the context.
  
  **Spread Operator:**
  - Used to expand or spread iterables (like arrays) into individual elements.
  - Often used in function calls, array literals, or object literals.
  
  **Example:**
  ```javascript
  const arr = [1, 2, 3];
  const newArr = [4, 5, ...arr, 6];
  
  console.log(newArr); // [4, 5, 1, 2, 3, 6]
  ```
  
  **Rest Operator:**
  - Used to collect multiple elements and pack them into an array.
  - Often used in function parameters to handle variable numbers of arguments.
  
  **Example:**
  ```javascript
  function sum(...numbers) {
    return numbers.reduce((acc, num) => acc + num, 0);
  }
  
  console.log(sum(1, 2, 3, 4)); // 10
  ```
  
  **Differences:**
  - **Spread** is used to unpack elements, while **rest** is used to pack elements.
  - They look the same but are used in opposite situations.
  
  **Note:**
  - The spread and rest operators provide a more concise and readable way to work with arrays and objects in JavaScript.
  - They are part of the ES6+ feature set and are widely used in modern JavaScript development.
  - Understanding these operators is essential for working with modern JavaScript, especially in functional programming patterns and in frameworks like React.
</details>

<details>
  <summary>What are template literals and tagged templates?</summary>
  
  Template literals are string literals that allow embedded expressions, multi-line strings, and string interpolation. They are enclosed by backticks (`` ` ``) instead of single or double quotes.
  
  **Features:**
  - **String Interpolation:** Embed variables and expressions using `${expression}` syntax.
  - **Multi-line Strings:** Create strings that span multiple lines without using escape characters.
  - **Tagged Templates:** Call a function (a "tag") with the template literal and its interpolated values.
  
  **Example:**
  ```javascript
  const name = 'Deepak';
  const age = 25;
  
  // String interpolation
  const greeting = `Hello, ${name}. You are ${age} years old.`;
  
  // Multi-line string
  const message = `This is a string
  that spans multiple lines.`;
  
  // Tagged template
  function tag(strings, ...values) {
    console.log(strings); // Array of string parts
    console.log(values);  // Array of interpolated values
  }
  
  const result = tag`Hello, ${name}. You are ${age} years old.`;
  ```
  
  **Note:**
  - Template literals and tagged templates provide a powerful and flexible way to work with strings in JavaScript.
  - They are part of the ES6+ feature set and are widely used in modern JavaScript development.
  - Understanding these features is essential for working with modern JavaScript, especially in frameworks like React, where template literals are often used for defining styles and templates.
</details>

<details>
  <summary>How do you use optional chaining (?.) and nullish coalescing (??)?</summary>
  
  **Optional Chaining (?.):**
  - A syntax for accessing deeply nested properties of an object without having to explicitly check each level for existence.
  - If the value before `?.` is `null` or `undefined`, the expression short-circuits and returns `undefined` instead of throwing an error.
  
  **Example:**
  ```javascript
  const user = {
    profile: {
      name: 'Deepak',
      age: 25
    }
  };
  
  console.log(user.profile?.name); // 'Deepak'
  console.log(user.profile?.address?.city); // undefined
  ```
  
  **Nullish Coalescing (??):**
  - A logical operator that returns its right-hand side operand when its left-hand side operand is `null` or `undefined`, and otherwise returns its left-hand side operand.
  - It is similar to the logical OR (`||`) operator, but it only considers `null` and `undefined` as nullish values, not other falsy values like `0`, `''`, or `false`.
  
  **Example:**
  ```javascript
  const foo = null ?? 'default string';
  const bar = 0 ?? 42;
  
  console.log(foo); // 'default string'
  console.log(bar); // 0
  ```
  
  **Combining Both:**
  ```javascript
  const user = {
    name: 'Deepak',
    preferences: null
  };
  
  const userPreferences = user.preferences ?? 'default preferences';
  
  console.log(userPreferences); // 'default preferences'
  ```
  
  **Note:**
  - Optional chaining and nullish coalescing are part of the ES2020 feature set and are widely supported in modern JavaScript environments.
  - They provide a more concise and readable way to work with objects and handle default values, respectively.
  - Understanding these features is essential for working with modern JavaScript, especially in frameworks like React, where they are commonly used for handling props and state.
</details>

<details>
  <summary>How do you debounce or throttle a function in JavaScript?</summary>
  
  Debouncing and throttling are techniques to control the rate at which a function is executed, especially in the context of events that fire rapidly (like scrolling, resizing, or keypresses).
  
  **Debouncing:**
  - Ensures that a function is not called again until a certain amount of time has passed without it being called.
  - Useful for scenarios like validating input in a form, where you don't want to validate on every keystroke, but rather after the user has stopped typing for a certain period.
  
  **Example:**
  ```javascript
  function debounce(func, delay) {
    let timeout;
    return function(...args) {
      const context = this;
      clearTimeout(timeout);
      timeout = setTimeout(() => func.apply(context, args), delay);
    };
  }
  
  const handleInput = debounce((event) => {
    console.log('Input value:', event.target.value);
  }, 250);
  
  inputElement.addEventListener('input', handleInput);
  ```
  
  **Throttling:**
  - Ensures that a function is called at most once in a specified amount of time, regardless of how many times the event is triggered.
  - Useful for scenarios like handling scroll events, where you might want to execute a function at regular intervals as the user scrolls.
  
  **Example:**
  ```javascript
  function throttle(func, limit) {
    let lastFunc;
    let lastRan;
    return function(...args) {
      const context = this;
      if (!lastRan) {
        func.apply(context, args);
        lastRan = Date.now();
      } else {
        clearTimeout(lastFunc);
        lastFunc = setTimeout(() => {
          if ((Date.now() - lastRan) >= limit) {
            func.apply(context, args);
            lastRan = Date.now();
          }
        }, limit - (Date.now() - lastRan));
      }
    };
  }
  
  const handleScroll = throttle(() => {
    console.log('Scroll event fired');
  }, 1000);
  
  window.addEventListener('scroll', handleScroll);
  ```
  
  **Note:**
  - Debouncing and throttling are important techniques for optimizing performance and improving user experience in web applications.
  - They help in reducing the number of times a function is called, thus saving resources and preventing potential lag or unresponsiveness in the application.
  - Understanding and being able to implement these techniques is essential for modern JavaScript development, especially in performance-critical applications.
</details>

<details>
  <summary>How do you detect memory leaks in JavaScript apps?</summary>
  
  Detecting memory leaks in JavaScript applications can be challenging, but there are several tools and techniques that can help:
  
  **1. Chrome DevTools:**
  - The built-in Chrome DevTools provide a powerful set of tools for profiling and debugging JavaScript applications, including detecting memory leaks.
  - Use the "Memory" tab to take heap snapshots, record allocation timelines, and analyze memory distribution.
  
  **2. Heap Snapshots:**
  - Take heap snapshots at different times during the execution of your application to compare and analyze memory usage.
  - Look for objects that are not being garbage collected and are still referenced in memory.
  
  **3. Allocation Timeline:**
  - Record an allocation timeline to see how memory is allocated and freed over time.
  - Look for patterns of increasing memory usage that do not stabilize or decrease.
  
  **4. Performance Profiling:**
  - Use the "Performance" tab in Chrome DevTools to record and analyze the performance of your application.
  - Look for long-running scripts, excessive garbage collection, and other performance bottlenecks.
  
  **5. Third-Party Tools:**
  - There are several third-party tools and libraries that can help in detecting and diagnosing memory leaks in JavaScript applications, such as:
    - `memwatch-next`: A native addon for Node.js that detects memory leaks.
    - `node-inspector`: A debugger for Node.js applications that provides a web-based interface for debugging and profiling.
    - `clinic.js`: A suite of tools for diagnosing and fixing performance issues in Node.js applications.
  
  **Example of Using Chrome DevTools:**
  1. Open Chrome DevTools and go to the "Memory" tab.
  2. Take a heap snapshot by clicking on the "Take snapshot" button.
  3. Interact with your application to simulate the scenario where you suspect a memory leak.
  4. Take another heap snapshot.
  5. Compare the two snapshots to identify objects that are still in memory but should have been garbage collected.
  6. Analyze the retaining paths to understand why the objects are still referenced and not collected.
  7. Fix the identified memory leaks in your code and retest to ensure the leaks are resolved.
  
  **Note:**
  - Memory leaks can significantly impact the performance and stability of JavaScript applications, leading to increased memory usage, slowdowns, and crashes.
  - Detecting and fixing memory leaks is an essential part of JavaScript development, especially for long-running applications or applications with complex interactions and data flows.
  - Regularly profiling and monitoring the memory usage of your applications can help in early detection and prevention of memory leaks.
</details>

<details>
  <summary>What is garbage collection and how does it work?</summary>
  
  Garbage collection is the process of automatically identifying and reclaiming memory that is no longer in use by the program, in order to free up resources and prevent memory leaks.
  
  **How It Works:**
  - JavaScript uses a garbage collector to automatically manage memory.
  - The garbage collector runs in the background and periodically checks for objects in memory that are no longer reachable or needed by the program.
  - When an object is no longer reachable, its memory is reclaimed and made available for future allocations.
  
  **Reference Counting:**
  - One of the techniques used in garbage collection is reference counting.
  - Each object in memory has a reference count that tracks the number of references to it from other objects or variables.
  - When the reference count of an object drops to zero, it means the object is no longer reachable and can be garbage collected.
  
  **Mark-and-Sweep:**
  - Another common technique is the mark-and-sweep algorithm.
  - The garbage collector first "marks" all reachable objects by traversing the object graph from the root objects (like global variables or active function calls).
  - Then, it "sweeps" through the memory, reclaiming the memory of objects that were not marked (i.e., unreachable objects).
  
  **Example:**
  ```javascript
  let obj1 = { name: 'Deepak' };
  let obj2 = obj1;
  
  obj1 = null; // obj1 no longer references the object
  
  // The object is still reachable through obj2, so it won't be garbage collected yet
  
  obj2 = null; // Now the object is unreachable, and its memory can be reclaimed
  ```
  
  **Note:**
  - Garbage collection is an essential part of memory management in JavaScript, as it helps in preventing memory leaks and optimizing memory usage.
  - However, developers should not rely solely on garbage collection and should also follow best practices for memory management, such as avoiding global variables, nullifying references when no longer needed, and using tools like `WeakMap` and `WeakSet` for managing memory-sensitive data.
</details>

<details>
  <summary>How would you deep compare two objects in JavaScript?</summary>
  
  Deep comparing two objects means checking if they are equivalent in terms of structure and values, including nested objects and arrays.
  
  **1. Using JSON.stringify:**
  - A simple way to deep compare objects is to convert them to JSON strings and compare the strings.
  - This method works well for objects that can be serialized to JSON, but it has limitations (e.g., functions, `undefined`, and circular references are not supported).
  
  **Example:**
  ```javascript
  const obj1 = { a: 1, b: { c: 2 } };
  const obj2 = { a: 1, b: { c: 2 } };
  
  const isEqual = JSON.stringify(obj1) === JSON.stringify(obj2);
  
  console.log(isEqual); // true
  ```
  
  **2. Using Lodash's isEqual:**
  - The `isEqual` function from Lodash is a popular utility for deep comparing objects.
  - It handles many edge cases and provides a reliable way to compare objects.
  
  **Example:**
  ```javascript
  const _ = require('lodash');
  
  const obj1 = { a: 1, b: { c: 2 } };
  const obj2 = { a: 1, b: { c: 2 } };
  
  const isEqual = _.isEqual(obj1, obj2);
  
  console.log(isEqual); // true
  ```
  
  **3. Custom Recursive Function:**
  - You can also write a custom recursive function to deep compare objects, handling different types of values and structures.
  
  **Example:**
  ```javascript
  function deepEqual(obj1, obj2) {
    if (obj1 === obj2) return true;
    
    if (obj1 == null || obj2 == null || typeof obj1 !== 'object' || typeof obj2 !== 'object') {
      return false;
    }
    
    const keys1 = Object.keys(obj1);
    const keys2 = Object.keys(obj2);
    
    if (keys1.length !== keys2.length) return false;
    
    for (let key of keys1) {
      if (!keys2.includes(key) || !deepEqual(obj1[key], obj2[key])) {
        return false;
      }
    }
    
    return true;
  }
  
  const obj1 = { a: 1, b: { c: 2 } };
  const obj2 = { a: 1, b: { c: 2 } };
  
  console.log(deepEqual(obj1, obj2)); // true
  ```
  
  **Note:**
  - Deep comparing objects can be computationally expensive, especially for large and complex objects.
  - It's important to choose the right method or library for deep comparison based on the specific requirements and constraints of your project.
  - Understanding how to deep compare objects is essential for working with complex data structures and for ensuring data integrity in JavaScript applications.
</details>

<details>
  <summary>What are proxies in JavaScript and when would you use them?</summary>
  
  Proxies are objects that wrap another object (the target) and intercept operations (like property access, assignment, enumeration, function invocation, etc.) on the target object.
  
  **Key Features:**
  - Proxies are created using the `Proxy` constructor, which takes two arguments: the target object and a handler object.
  - The handler object defines the traps (interceptors) for the operations you want to intercept on the target object.
  
  **Example:**
  ```javascript
  const target = {
    message: 'Hello, World!'
  };
  
  const handler = {
    get: function(obj, prop) {
      return prop in obj ? obj[prop] : `Property "${prop}" does not exist.`;
    }
  };
  
  const proxy = new Proxy(target, handler);
  
  console.log(proxy.message); // 'Hello, World!'
  console.log(proxy.nonExistent); // 'Property "nonExistent" does not exist.'
  ```
  
  **Common Use Cases:**
  - **Validation:** Validate values before they are set on an object.
  - **Value Formatting:** Format or transform values when they are accessed or modified.
  - **Logging:** Log operations performed on an object for debugging or auditing purposes.
  - **Function Proxies:** Create function proxies that can modify the behavior of functions (e.g., logging, timing, caching).
  
  **Note:**
  - Proxies are a powerful and flexible feature of JavaScript, but they should be used judiciously, as they can introduce complexity and performance overhead.
  - Understanding proxies and their use cases is important for mastering advanced JavaScript programming and for working with modern JavaScript frameworks and libraries.
</details>

<details>
  <summary>How do you handle performance optimization in large-scale JavaScript apps?</summary>
  
  Performance optimization in large-scale JavaScript applications involves various strategies and techniques to improve the speed, responsiveness, and overall performance of the application.
  
  **1. Code Splitting:**
  - Split your code into smaller bundles that can be loaded on demand, rather than loading the entire application at once.
  - Use dynamic `import()` to load modules asynchronously.
  
  **2. Tree Shaking:**
  - Eliminate dead code and unused exports from your bundles, reducing the size of the JavaScript files that need to be loaded.
  - Use tools like Webpack or Rollup that support tree shaking.
  
  **3. Debouncing and Throttling:**
  - Use debouncing and throttling techniques to limit the rate at which functions are executed, especially for events that fire rapidly (like scrolling, resizing, or keypresses).
  
  **4. Memoization:**
  - Cache the results of expensive function calls and return the cached result when the same inputs occur again.
  
  **5. Web Workers:**
  - Offload heavy computations or blocking operations to web workers, which run in the background and do not block the main thread.
  
  **6. Performance Profiling:**
  - Use performance profiling tools (like Chrome DevTools' Performance tab) to identify and analyze performance bottlenecks in your application.
  
  **7. Efficient Data Structures and Algorithms:**
  - Choose the right data structures and algorithms for your specific use case, and optimize them for performance.
  
  **8. Avoiding Memory Leaks:**
  - Be vigilant about avoiding memory leaks, which can degrade performance over time.
  - Use tools like Chrome DevTools' Memory tab to detect and diagnose memory leaks.
  
  **9. Using Native Browser Features:**
  - Leverage native browser features and APIs (like `requestAnimationFrame`, `fetch`, etc.) that are optimized for performance.
  
  **10. Code Minification and Compression:**
  - Minify and compress your JavaScript code to reduce its size and improve loading times.
  
  **Note:**
  - Performance optimization is a critical aspect of JavaScript development, especially for large-scale applications with complex interactions and data flows.
  - It's important to regularly profile and monitor the performance of your application, and to be proactive in identifying and addressing performance issues.
  - Understanding and applying performance optimization techniques is essential for modern JavaScript development, and for building high-performance, scalable JavaScript applications.
</details>

