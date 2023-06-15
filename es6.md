# 2. ES6

### Compare Scopes of the var and let Keywords

When you declare a variable with the `var` keyword, it is declared globally, or locally if declared inside a function.(전역 혹은 함수만을 scope으로 인정)  
하지만 When you declare a variable with the `let` keyword inside a `block, statement, or expression`, its scope is limited to that block, statement, or expression.  
(let은 전역, 함수 뿐만 아니라 이들도 scope으로 인정한다)
```
var numArray = [];
for (var i = 0; i < 3; i++) {
  numArray.push(i);
}
console.log(numArray);
console.log(i);
```
Here the console will display the values `[0, 1, 2]` and `3`.  
With the var keyword, i is declared globally. So when i++ is executed, it updates the global variable.  
  
This behavior will cause problems if you were to create a function and store it for later use inside a for loop that uses the i variable.  
This is because the stored function will always refer to the value of the updated global i variable.
```
var printNumTwo;
for (var i = 0; i < 3; i++) {
  if (i === 2) {
    printNumTwo = function() {
      return i;
    };
  }
}
console.log(printNumTwo());
```
Here the console will display the value `3`.  
This is because the value assigned to i was updated and the printNumTwo() returns the global i and not the value i had when the function was created in the for loop.  
  
The `let` keyword does not follow this behavior:
```
let printNumTwo;
for (let i = 0; i < 3; i++) {
  if (i === 2) {
    printNumTwo = function() {
      return i;
    };
  }
}
console.log(printNumTwo());
console.log(i);
```
Here the console will display the value `2`(*클로저*), and an error that `i is not defined`.
`i` is not defined because it was not declared in the global scope. (for루프의 block 스코프에 해당)
It is only declared within the for loop statement.  
`printNumTwo()` returned the correct value because three different i variables with unique values (0, 1, and 2) were created by the let keyword within the loop statement.

var는 전역, 함수 스코프만을 인정하고, let은 block scope도 인정. 

### Mutate an Array Declared with const
Some developers prefer to assign all their variables using `const` by default, unless they know they will need to reassign the value.  
Only in that case, they use `let`.  
  
However, it is important to understand that objects (including arrays and functions) assigned to a variable using `const` are still mutable. 
```
const s = [5, 6, 7];
s = [1, 2, 3];
s[2] = 45;
console.log(s);
```
`s = [1, 2, 3]` will result in an error. After commenting out that line, the console.log will display the value `[5, 6, 45]`.
As you can see, you can mutate the object `[5, 6, 7]` itself and the variable `s` will still point to the altered array `[5, 6, 45]`.  
Like all arrays, the array elements in `s` are mutable, but because `const` was used, you cannot use the variable identifier `s` to point to a different array using the assignment operator.  
const라서 재할당은 안되지만 배열 값 변경은 가능.  
  
### Prevent Object Mutation
As seen in the previous challenge, const declaration alone doesn't really protect your data from mutation.  
To ensure your data doesn't change, JavaScript provides a function `Object.freeze` to prevent data mutation.  
Any attempt at changing the object will be rejected, with an error thrown if the script is running in strict mode.
```
let obj = {
  name:"FreeCodeCamp",
  review:"Awesome"
};
Object.freeze(obj);
obj.review = "bad";
obj.newProp = "Test";
console.log(obj); 
```
The obj.review and obj.newProp assignments will result in errors, because our editor runs in strict mode by default,  
and the console will display the value `{ name: "FreeCodeCamp", review: "Awesome" }`.    
  

```
function freezeObj() {
  const MATH_CONSTANTS = {
    PI: 3.14
  };
  // Only change code below this line
  Object.freeze(MATH_CONSTANTS);
  // Only change code above this line
  try {
    MATH_CONSTANTS.PI = 99;
  } catch(ex) {
    console.log(ex);
    // [TypeError: Cannot assign to read only property 'PI' of object '#<Object>']
  }
  return MATH_CONSTANTS.PI;
}
const PI = freezeObj();
console.log(PI); // 3.14
```

### Use Arrow Functions to Write Concise Anonymous Functions

In JavaScript, we often don't need to name our functions, especially when passing a function as an argument to another function.  
Instead, we create inline functions. We don't need to name these functions because we do not reuse them anywhere else.  
익명 함수
```
const myFunc = function() {
  const myVar = "value";
  return myVar;
}
```
ES6 provides us with the syntactic sugar to not have to write anonymous functions this way.  
Instead, you can use **arrow function syntax:**
```
const myFunc = () => {
  const myVar = "value";
  return myVar;
}
```
When there is no function body, and only a return value, arrow function syntax allows you to omit the keyword return as well as the brackets surrounding the code.  
This helps simplify smaller functions into one-line statements:
```
const myFunc = () => "value";
```
```
const doubler = (item) => item * 2;
doubler(4);
```
If an arrow function has a single parameter, the parentheses enclosing the parameter may be omitted.
```
const doubler = item => item * 2;
```
It is possible to pass more than one argument into an arrow function.  
  
- inline
 "inline"은 특정 요소나 기능을 다른 위치나 코드로부터 분리하여 독립적으로 사용하는 대신에, 해당 요소나 기능을 직접 포함하는 것을 의미.
 따라서 "inline CSS"는 스타일을 HTML 요소 자체에 포함시키는 것을, "inline Function"은 함수 정의를 호출하는 부분에 직접 작성하는 것을 의미.
 ```
 <div style="color: blue; font-size: 14px;">Hello</div>
 setTimeout(function() { console.log('Hello'); }, 1000);
 ```

### Set Default Parameters for Your Functions
```
const greeting = (name = "Anonymous") => "Hello " + name;

console.log(greeting("John")); // Hello John
console.log(greeting()); // Hello Anonymous
```
The default parameter kicks in when the argument is not specified (it is undefined). 

### Use the Rest Parameter with Function Parameters

With the rest parameter, you can create functions that take a variable number of arguments.  
These arguments are stored in *an array* that can be accessed later from inside the function.
```
function howMany(...args) {
  return "You have passed " + args.length + " arguments.";
}
console.log(howMany(0, 1, 2));
console.log(howMany("string", null, [1, 2, 3], { }));
```
The console would display the strings `You have passed 3 arguments.` and `You have passed 4 arguments.`.  
  
The rest parameter eliminates the need to use the `arguments` object and allows us to use array methods on the array of parameters passed to the function.

### Use the Spread Operator to Evaluate Arrays In-Place

ES6 introduces the spread operator, which allows us to expand arrays and other expressions in places where multiple parameters or elements are expected.  
  
The ES5 code below uses apply() to compute the maximum value in an array:
```
var arr = [6, 89, 3, 45];
var maximus = Math.max.apply(null, arr);
```
call은 인수를 쉼표로 구분하여 전달하고, apply는 배열 형태의 인수를 받고, 배열의 각 요소는 함수에 개별적인 인수로 전달된다. 
We had to use `Math.max.apply(null, arr)` because `Math.max(arr)` returns `NaN`. `Math.max()` expects comma-separated arguments, but not an array.  
The spread operator makes this syntax much better to read and maintain.
```
const arr = [6, 89, 3, 45];
const maximus = Math.max(...arr);
```
`...arr` returns an unpacked array. In other words, it spreads the array.  
However, the spread operator only works in-place, like in an argument to a function or in an array literal. For example:
```
const spreaded = [...arr];
```

### Use Destructuring Assignment to Extract Values from Objects
neatly assigning values taken directly from an object.  
  
Consider the following ES5 code:
```
const user = { name: 'John Doe', age: 34 };

const name = user.name;
const age = user.age;
```
Here's an equivalent assignment statement using the ES6 destructuring syntax:
```
const { name, age } = user;
```
`name` would have a value of the string `John Doe`, and `age` would have the number `34`.  
Here, the `name` and `age` variables will be created and assigned the values of their respective values from the `user` object.  
You can extract as many or few values from the object as you want.
```
const HIGH_TEMPERATURES = {
  yesterday: 75,
  today: 77,
  tomorrow: 80
};

// Only change code below this line
const {today, tomorrow } = HIGH_TEMPERATURES;
console.log(today, tomorrow);
// Only change code above this line
```
Destructuring allows you to assign a new variable name when extracting values.  
You can do this by putting the new name after a colon when assigning the value.
```
const user = { name: 'John Doe', age: 34 };
const { name: userName, age: userAge } = user;
```
You may read it as "get the value of `user.name` and assign it to a new variable named `userName`" and so on.    
  
You can use the same principles from the previous two lessons to destructure values from nested objects.
```
const user = {
  johnDoe: { 
    age: 34,
    email: 'johnDoe@freeCodeCamp.com'
  }
};

const { johnDoe: { age, email }} = user;

const { johnDoe: { age: userAge, email: userEmail }} = user;
```

### Use Destructuring Assignment to Assign Variables from Arrays

One key difference between the spread operator and array destructuring is that the spread operator unpacks all contents of an array into a comma-separated list.  
Consequently, you cannot pick or choose which elements you want to assign to variables.  
  
Destructuring an array lets us do exactly that:
```
const [a, b] = [1, 2, 3, 4, 5, 6];
console.log(a, b);
```
The console will display the values of `a` and `b` as `1, 2`.  
  
We can also access the value at any index in an array with destructuring by using *commas* to reach the desired index:
```
const [a, b,,, c] = [1, 2, 3, 4, 5, 6];
console.log(a, b, c);
```
The console will display the values of `a`, `b`, and `c` as `1, 2, 5`.  

```
let a = 8, b = 6;
// Only change code below this line
[a, b] = [b, a];
console.log(a, b); // 6 8
```

### Destructuring via rest elements
In some situations involving array destructuring, we might want to collect the rest of the elements into a separate array.  
  
The result is similar to `Array.prototype.slice()`, as shown below:
```
const [a, b, ...arr] = [1, 2, 3, 4, 5, 7];
console.log(a, b);
console.log(arr);
```
Variables a and b take the first and second values from the array.  
After that, because of the rest syntax presence, `arr` gets the rest of the values in the form of an array.  
The rest element only works correctly as the last variable in the list.  
As in, you cannot use the rest syntax to catch a subarray that leaves out the last element of the original array.  
  
### Use Destructuring Assignment to Pass an Object as a Function's Parameters
In some cases, you can destructure the object in a function argument itself.
```
const profileUpdate = (profileData) => {
  const { name, age, nationality, location } = profileData;

}
```
This effectively destructures the object sent into the function. This can also be done in-place:
```
const profileUpdate = ({ name, age, nationality, location }) => {

}
```
When `profileData` is passed to the above function, the values are destructured from the function parameter for use within the function.  

### Create Strings using Template Literals
Template literals allow you to create multi-line strings and to use string interpolation(문자열 내에 변수나 표현식 삽입) features to create strings.
```
const person = {
  name: "Zodiac Hasbro",
  age: 56
};

const greeting = `Hello, my name is ${person.name}!
I am ${person.age} years old.`;

console.log(greeting);
```
Similarly, you can include other expressions in your string literal, for example `${a + b}`. 

### Write Concise Object Literal Declarations Using Object Property Shorthand

```
const getMousePosition = (x, y) => ({
  x: x,
  y: y
});
```
return값이 객체이면 ()로 감싼다. 
`getMousePosition` is a simple function that returns an object containing two properties.  
ES6 provides the syntactic sugar to eliminate the redundancy of having to write `x: x`. You can simply write x once, and it will be converted to `x: x` (or something equivalent) under the hood.  
Here is the same function from above rewritten to use this new syntax:
```
const getMousePosition = (x, y) => ({ x, y });
```
key가 지워지고 value로 표기됌.

### Write Concise Declarative Functions with ES6
```
const person = {
  name: "Taylor",
  sayHello: function() {
    return `Hello! My name is ${this.name}.`;
  }
};
```
With ES6, you can remove the `function` keyword and colon altogether when defining functions in objects. Here's an example of this syntax:
```
const person = {
  name: "Taylor",
  sayHello() {
    return `Hello! My name is ${this.name}.`;
  }
};
```

### Use class Syntax to Define a Constructor Function
ES6 provides a new syntax to create objects, using the `class` keyword.  
  
In ES5, an object can be created by defining a `constructor` function and using the `new` keyword to instantiate the object.  
  
In ES6, a `class` declaration has a `constructor` method that is invoked with the `new` keyword.  
If the constructor method is not explicitly defined, then it is implicitly defined with no arguments.
```
class SpaceShuttle {
  constructor(targetPlanet) {
    this.targetPlanet = targetPlanet;
  }
  takeOff() {
    console.log("To " + this.targetPlanet + "!");
  }
}

// Implicit constructor 
class Rocket {
  launch() {
    console.log("To the moon!");
  }
}

const zeus = new SpaceShuttle('Jupiter');
// prints To Jupiter! in console
zeus.takeOff();

const atlas = new Rocket();
// prints To the moon! in console
atlas.launch();
```
It should be noted that the `class` keyword declares a new function, to which a constructor is added.  
This constructor is invoked when `new` is called to create a new object.  
  
UpperCamelCase should be used by convention for ES6 class names, as in `SpaceShuttle` used above.  
  
The `constructor` method is a special method for creating and initializing an object created with a class. 

### Use getters and setters to Control Access to an Object
You can obtain values from an object and set the value of a property within an object.  
These are classically called *getters* and *setters*.  
    
Getter functions are meant to simply return (get) the value of an object's *private variable* to the user without the *user directly accessing the private variable*.  
  
Setter functions are meant to modify (set) the value of an object's *private variable* based on the value passed into the setter function.  
This change could involve calculations, or even overwriting the previous value completely.
```
class Book {
  constructor(author) {
    this._author = author;
  }
  // getter
  get writer() {
    return this._author;
  }
  // setter
  set writer(updatedAuthor) {
    this._author = updatedAuthor;
  }
}
const novel = new Book('anonymous');
console.log(novel.writer);
novel.writer = 'newAuthor';
console.log(novel.writer);
```
The console would display the strings `anonymous` and `newAuthor`.  
  
Notice the syntax used to invoke the getter and setter.  
They do not even look like functions.  
**Getters and setters are important because they hide internal implementation details.**. 
  
It is convention to precede the name of a private variable with an underscore (_).  
However, the practice itself does not make a variable private.  
  
You are creating an API for another user, who can get the correct result regardless of which one you track.  
API 사용자는 내부에서 어떤 것을 추적하고 있는지에 관계없이 올바른 결과를 얻을 수 있다. 즉, 사용자는 *내부 구현 세부 사항에 대해 알 필요 없이 API를 사용할 수 있으며*, 항상 올바른 결과를 얻을 수 있게 된다.  
  
### Create a Module Script
In order to make JavaScript more modular, clean, and maintainable; ES6 introduced a way to easily share code among JavaScript files.  
This involves exporting parts of a file for use in one or more other files, and importing the parts you need, where you need them.  
In order to take advantage of this functionality, you need to create a script in your HTML document with a type of module. Here’s an example:
```
<script type="module" src="filename.js"></script>
```
A script that uses this module type can now use the `import` and `export` features.  
  
Imagine a file called `math_functions.js` that contains several functions related to mathematical operations.  
One of them is stored in a variable, add, that takes in two numbers and returns their sum.  
You want to use this function in several different JavaScript files. In order to share it with these other files, you first need to export it.
```
export const add = (x, y) => {
  return x + y;
}
```
The above is a common way to export a single function, but you can achieve the same thing like this:
```
const add = (x, y) => {
  return x + y;
}

export { add };
```
When you export a variable or function, you can import it in another file and use it without having to rewrite the code.  
You can export multiple things by repeating the first example for each thing you want to export, or by placing them all in the export statement of the second example, like this:
```
export { add, subtract };
```

### Reuse JavaScript Code Using import
```
import { add } from './math_functions.js';
import { add, subtract } from './math_functions.js';
```
The `./` tells the import to look for the `math_functions.js` file in the same folder as the current file.  
The relative file path (`./`) and file extension (`.js`) are required when using import in this way.  
  
Suppose you have a file and you wish to import all of its contents into the current file. This can be done with the import `*` as syntax.  
```
import * as myMathModule from "./math_functions.js";

myMathModule.add(2,3);
myMathModule.subtract(5,3);
```
The above import statement will create an object called `myMathModule`. This is just a variable name, you can name it anything.  
The object will contain all of the exports from math_functions.js in it, so you can access the functions like you would any other object property.  

### Create an Export Fallback with export default
In the export lesson, you learned about the syntax referred to as a *named export*.  
This allowed you to make multiple functions and variables available for use in other files.  
  
There is another export syntax you need to know, known as *export default*. Usually you will use this syntax if only one value is being exported from a file.  
It is also used to create a fallback value for a file or module.
Below are examples using `export default`:
```
export default function add(x, y) {
  return x + y;
}

export default function(x, y) {
  return x + y;
}
```
The first is a named function, and the second is an anonymous function.  
  
Since export default is used to declare a fallback value for a module or file, you can only have one value be a default export in each module or file.  
Additionally, you cannot use export default with `var`, `let`, or `const`.  

### Import a Default Export
```
import add from "./math_functions.js";
```
The imported value, `add`, is not surrounded by curly braces (`{}`).  
`add` here is simply a variable name for whatever the default export of the `math_functions.js` file is.  
You can use any name here when importing a default.

### JavaScript Promise
A promise in JavaScript is exactly what it sounds like - you use it to make a promise to do something, usually *asynchronously*.  
When the task completes, you either fulfill your promise or fail to do so.  
Promise is a `constructor` function, so you need to use the `new` keyword to create one.  
It *takes a function, as its argument*, with two parameters - `resolve` and `reject`.  
These are methods used to determine the outcome of the promise. The syntax looks like this:
```
const myPromise = new Promise((resolve, reject) => {

});
```
  
A promise has three states: `pending`, `fulfilled`, and `rejected`.  
The promise you created in the last challenge is forever stuck in the pending state because you did not add a way to complete the promise.  
The resolve and reject parameters given to the promise argument are used to do this.  
`resolve` is used when you want your promise to succeed, and `reject` is used when you want it to fail.  
These are methods that take an argument, as seen below.
```
const myPromise = new Promise((resolve, reject) => {
  if(condition here) {
    resolve("Promise was fulfilled");
  } else {
    reject("Promise was rejected");
  }
});
```
어떤 조건을 만족되서(주로 비동기 적인 일) resolve함수가 호출되면 pending -> fulfilled 상태로 변화, reject함수가 호출되면 pending -> rejected 상태로 변화.  
The example above uses strings for the argument of these functions, but it can really be anything.  
Often, it might be an object, that you would use data from, to put on your website or elsewhere.
```
const makeServerRequest = new Promise((resolve, reject) => {
  // responseFromServer represents a response from a server
  let responseFromServer; 
  if(responseFromServer) {
    // Change this line
    resolve('We got the data')
  } else {  
    // Change this line
    reject('Data not received')
  }
});
```
### Handle a Fulfilled Promise with then
Promises are most useful when you have a process that takes an unknown amount of time in your code (i.e. something asynchronous), often a server request.  
When you make a server request it takes some amount of time, and after it completes you usually want to do something with the response from the server.  
This can be achieved by using the `then` method. The `then` method is executed immediately after your promise is fulfilled with resolve. Here’s an example:
```
myPromise.then(result => {
  
});
```
`result` comes from the argument given to the `resolve` method.  
  
```
const makeServerRequest = new Promise((resolve, reject) => {
  // responseFromServer is set to true to represent a successful response from a server
  let responseFromServer = true;
    
  if(responseFromServer) {
    resolve("We got the data");
  } else {  
    reject("Data not received");
  }
});

makeServerRequest.then(result => {console.log(result)});
```

### Handle a Rejected Promise with catch
`catch` is the method used when your promise has been rejected.  
It is executed immediately after a promise's `reject` method is called. Here’s the syntax:
```
myPromise.catch(error => {
  
});
```
`error` is the argument passed in to the `reject` method.  
  
```
const makeServerRequest = new Promise((resolve, reject) => {
  // responseFromServer is set to false to represent an unsuccessful response from a server
  let responseFromServer = false;
    
  if(responseFromServer) {
    resolve("We got the data");
  } else {  
    reject("Data not received");
  }
});

makeServerRequest.then(result => {
  console.log(result);
}).catch(error => {console.log(error)});
```





