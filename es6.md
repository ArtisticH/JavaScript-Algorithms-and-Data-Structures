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
