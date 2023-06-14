# 1. Basic JavaScript

- A string literal, or string, is a *series of zero or more characters* enclosed in single or double quotes.
- If you do a mathematical operation on an `undefined` variable your result will be `NaN` which means "Not a Number".  
If you concatenate a string with an `undefined` variable, you will get a string of `undefined`.
- In JavaScript all variables and function names are case sensitive.  
Write variable names in JavaScript in camelCase.  
In camelCase, multi-word variable names have the first word in lowercase and the first letter of each subsequent word is capitalized.

### Explore Differences Between the var and let Keywords
One of the biggest problems with declaring variables with the `var` keyword is that you can easily overwrite variable declarations:
```
var camper = "James";
var camper = "David";
console.log(camper);
```
var로 선언한 변수는 같은 스코프 내에서 중복 선언이 허용된다. 따라서 위의 두 번째 코드에서 var가 없는 것처럼 행동한다.  
This behavior does not throw an error, searching for and fixing bugs becomes more difficult.

If you replace `var` with `let` in the code above, it results in an error:
```
let camper = "James";
let camper = "David";
```

So unlike `var`, when you use `let`, a variable with the same name can only be declared once.
`let`은 같은 스코프 내에서 중복 선언이 허용되지 않음.(!==재할당, 재할당은 가능)
  
  

### Declare a Read-Only Variable with the const Keyword
```
const FAV_PET = "Cats";
FAV_PET = "Dogs";
```
 `const` are read-only. They are a constant value, which means that once a variable is assigned with const, it cannot be reassigned
 It is common for developers to use uppercase variable identifiers for immutable values and lowercase or camelCase for mutable values (objects and arrays).  
   
   
 ### Increment/Decrement a Number
 ```
 i++;
 i = i + 1;
 ```
 
 ```
 i--;
 i = i - 1;
 ```  
 
 ### Decimal Numbers   
 We can store decimal numbers in variables too. Decimal numbers are sometimes referred to as floating point numbers or floats.  
 when you compute numbers, they are computed with finite precision. Operations using floating points may lead to different results than the desired outcome.  
 
 ###  Remainder
 The remainder operator `%` gives the remainder of the division of two numbers.  
 주로 홀수, 짝수 구분할 때 사용
   
   The remainder operator is sometimes incorrectly referred to as the modulus operator.  
   It is very similar to modulus, but does not work properly with negative numbers.  
   %는 양수 음수에 모두 적용 가능
   
### Compound Assignment

```
myVar = myVar + 5;
myVar += 5;
```

### Escaping Literal Quotes in Strings

When you are defining a string you must start and end with a single or double quote.  
What happens when you need a literal quote: `"` or `'` inside of your string?  
  
In JavaScript, you can escape a quote from considering it as an end of string quote by placing a backslash (\) in front of the quote.  
따옴표를 문자열의 끝으로 인식하는 것을 방지(탈출)하기 위해 백 슬래시(\) 사용

```
const sampleStr = "Alan said, \"Peter is learning JavaScript\".";
```
This signals to JavaScript that the following quote is not the end of the string, but should instead appear inside the string.  
So if you were to print this to the console, you would get:
```
Alan said, "Peter is learning JavaScript".
```

### Quoting Strings with Single Quotes

Unlike some other programming languages, single and double quotes work the same in JavaScript.
Remember, a string has the same kind of quote at the beginning and end.  
But if you have that same quote somewhere in the middle, the string will stop early and throw an error.
```
const goodStr = 'Jake asks Finn, "Hey, let\'s go on an adventure?"'; 
const badStr = 'Finn responds, "Let's go!"';
```

Here `badStr` will throw an error.

```
const myStr = '<a href="http://www.example.com" target="_blank">Link</a>';
```

### Escape Sequences in Strings
Quotes are not the only characters that can be escaped inside a string.
|Code|   Output   |
|----|------------|
|\\' |single quote|
|\\" |double quote|
|\\\ |backslash   |
|\n  |newline     |
|\t	 |tab         |
|\r	 |carriage return|
|\b  |backspace   |
|\f	 |form feed   |

Note that the backslash itself must be escaped in order to display as a backslash.

### Concatenating Strings with Plus Operator
In JavaScript, when the `+` operator is used with a String value, it is called the concatenation operator.  
Note: Watch out for spaces. Concatenation does not add spaces between concatenated strings, so you'll need to add them yourself.  

We can also use the `+=` operator to concatenate a string onto the end of an existing string variable.
```
let ourStr = "I come first. ";
ourStr += "I come second.";
```

By using the concatenation operator (+), you can insert one or more variables into a string you're building.
```
const ourName = "freeCodeCamp";
const ourStr = "Hello, our name is " + ourName + ", how are you?";
```
Just as we can build a string over multiple lines out of string literals, we can also append variables to a string using the plus equals (+=) operator.
```
const anAdjective = "awesome!";
let ourStr = "freeCodeCamp is ";
ourStr += anAdjective;
```

### Find the Length of a String
You can find the length of a String value by writing .length after the string variable or string literal.
space character between is also counted.  
  
In order to get the last letter of a string, you can subtract one from the string's length.  
  
You can use the same principle we just used to retrieve the last character in a string to retrieve the Nth-to-last character.(끝에서 n번째)
```
const firstName = "Augusta";
const thirdToLastLetter = firstName[firstName.length - 3];
```

### Use Bracket Notation to Find the Character in a String
Bracket notation is a way to get a character at a specific index within a string.(Zero-based indexing.)

### Understand String Immutability
In JavaScript, `String` values are immutable, which means that they cannot be altered once created.
Note that this does not mean that myStr could not be re-assigned.  
The only way to change would be to assign it with a new value, like this:

### Store Multiple Values in one Variable using JavaScript Arrays
```
const sandwich = ["peanut butter", "jelly", "bread"];
```
You can also nest arrays within other arrays, like below:
```
const teams = [["Bulls", 23], ["White Sox", 45]];
```
This is also called a multi-dimensional array.  
  
Array indexes are written in the same bracket notation that strings use, except that instead of specifying a character, they are specifying an entry in the array.  
Like strings, arrays use zero-based indexing, so the first element in an array has an index of 0.  
  
Unlike strings, the entries of arrays are `mutable` and can be changed freely, even if the array was declared with `const`.  
  
There shouldn't be any spaces between the array name and the square brackets, like array [0].  
Although JavaScript is able to process this correctly, this may confuse other programmers reading your code.  
  
One way to think of a multi-dimensional array, is as an array of arrays.  
When you use brackets to access your array, the first set of brackets refers to the entries in the outermost (the first level) array, and each additional pair of brackets refers to the next level of entries inside.  
```
const arr = [
  [1, 2, 3],
  [4, 5, 6],
  [7, 8, 9],
  [[10, 11, 12], 13, 14]
];

const subarray = arr[3];
const nestedSubarray = arr[3][0];
const element = arr[3][0][1];
```

### Manipulate Arrays
An easy way to append data to the end of an array is via the `push()` function.  
`.push()` takes one or more parameters and "pushes" them onto the end of the array.(원본변경)
```
const arr1 = [1, 2, 3];
arr1.push(4);

const arr2 = ["Stimpson", "J", "cat"];
arr2.push(["happy", "joy"]);
```

`.pop()` is used to pop a value off of the end of an array. (원본변경)
We can store this popped off value by assigning it to a variable.  
In other words, `.pop()` removes the last element from an array and returns that element.  
  
What if you want to remove the first?  
That's where `.shift()` comes in. It works just like `.pop()`, except it removes the first element instead of the last.  
  
`.unshift()` works exactly like `.push()`, but instead of adding the element at the end of the array, `unshift()` adds the element at the beginning of the array.  
  
  
### Write Reusable JavaScript with Functions
```
function functionName() {
  console.log("Hello World");
}
```
You can call or invoke this function by using its name followed by parentheses, like this: `functionName()`; 

### Passing Values to Functions with Arguments

Parameters are variables that act as placeholders for the values that are to be input to a function when it is called.  
When a function is defined, it is typically defined along with one or more parameters.  
The actual values that are input (or "passed") into a function when it is called are known as arguments. 매개변수와 인수  

### Return a Value from a Function with Return
We can pass values into a function with arguments.  
You can use a `return` statement to send a value back out of a function.

### Global Scope and Functions
In JavaScript, scope refers to the visibility of variables.  
Variables which are defined outside of a function block have Global scope.  
This means, they can be seen everywhere in your JavaScript code.  
  
Variables which are declared without the `let` or `const` keywords are automatically created in the global scope. (암묵적 전역)
This can create unintended consequences elsewhere in your code or when running a function again.  
You should always declare your variables with let or const.

### Local Scope and Functions
Variables which are declared within a function, as well as the function parameters, have local scope.  
That means they are only visible within that function.
```
function myTest() {
  const loc = "foo";
  console.log(loc);
}

myTest();
console.log(loc);
```

### Global vs. Local Scope in Functions
It is possible to have both local and global variables with the same name.  
When you do this, the local variable takes precedence over the global variable.

### Understanding Undefined Value returned from a Function
A function can include the `return` statement but it does not have to.  
In the case that the function doesn't have a `return` statement, when you call it, the function processes the inner code but the returned value is `undefined`.

### Assignment with a Returned Value
If you'll recall from our discussion about Storing Values with the Assignment Operator, everything to the right of the equal sign is resolved before the value is assigned.  
This means we can take the return value of a function and assign it to a variable.
```
ourSum = sum(5, 12);
```

### Stand in Line
In Computer Science a queue is an abstract Data Structure where items are kept in order.  
New items can be added at the back of the queue and old items are taken off from the front of the queue. (선입선출 , push+shift)

### Understanding Boolean Values
Boolean values are never written with quotes.  
The strings `"true"` and `"false"` are not Boolean and have no special meaning in JavaScript.

### Use Conditional Logic with If Statements
The keyword `if` tells JavaScript to execute the code in the curly braces under certain conditions, defined in the parentheses.  
These conditions are known as Boolean conditions and they may only be `true` or `false`.
```
function test (myCondition) {
  if (myCondition) {
    return "It was true";
  }
  return "It was false";
}

test(true);
test(false);
```

### Comparison 
There are many comparison operators in JavaScript.  
All of these operators return a boolean `true` or `false` value.  
  
The most basic operator is the equality operator `==`.  
The equality operator compares two values and returns true if they're equivalent or false if they are not.  
  
In order for JavaScript to compare two different data types (for example, `numbers` and `strings`), it must convert one type to another.  
This is known as Type Coercion.  
Once it does, however, it can compare terms as follows:
```
1   ==  1  // true
1   ==  2  // false
1   == '1' // true
"3" ==  3  // true
```

Strict equality (`===`) is the counterpart to the equality operator (`==`).  
However, unlike the equality operator, which attempts to convert both values being compared to a common type, the strict equality operator does not perform a type conversion.
  
If the values being compared have different types, they are considered unequal, and the strict equality operator will return false.
  
In JavaScript, you can determine the type of a variable or a value with the `typeof` operator, as follows:
```
typeof 3
typeof '3'
```

The inequality operator (`!=`) is the opposite of the equality operator.  
It means not equal and returns false where equality would return true and vice versa.  
Like the equality operator, the inequality operator will convert data types of values while comparing.
```
1 !=  2    // true
1 != "1"   // false
1 != '1'   // false
1 != true  // false
0 != false // false
```
The strict inequality operator (`!==`) is the logical opposite of the strict equality operator.  
  
The greater than operator (>) compares the values of two numbers.  
The greater than or equal to operator (>=) compares the values of two numbers.  
The less than operator (<) compares the values of two numbers.  
The less than or equal to operator (<=) compares the values of two numbers. 
Like the equality operator, these operators will convert data types of values while comparing.

### Comparisons with the Logical And Operator

Sometimes you will need to test more than one thing at a time.  
The logical and operator (`&&`) returns true if and only if the operands to the left and right of it are true.  
  
The same effect could be achieved by nesting an `if` statement inside another `if`.
```
if (num > 5) {
  if (num < 10) {
    return "Yes";
  }
}
return "No";

if (num > 5 && num < 10) {
  return "Yes";
}
return "No";
```

### Comparisons with the Logical Or Operator
The logical or operator (`||`) returns true if either of the operands is true.  
Otherwise, it returns false.
```
if (num > 10) {
  return "No";
}
if (num < 5) {
  return "No";
}
return "Yes";

if (num > 10 || num < 5) {
  return "No";
}
return "Yes";
```
### Introducing Else Statements
When a condition for an if statement is true, the block of code following it is executed.  
What about when that condition is false? Normally nothing would happen.  
With an else statement, an alternate block of code can be executed.
```
if (num > 10) {
  return "Bigger than 10";
} else {
  return "10 or Less";
}
```
### Introducing Else If Statements
If you have multiple conditions that need to be addressed, you can chain `if` statements together with `else if` statements.
```
if (num > 15) {
  return "Bigger than 15";
} else if (num < 5) {
  return "Smaller than 5";
} else {
  return "Between 5 and 15";
}
```

Order is important in if, else if statements.  
The function is executed from top to bottom so you will want to be careful of what statement comes first.

### Selecting from Many Options with Switch Statements

If you need to match one value against many options, you can use a switch statement.  
A `switch` statement compares the value to the `case` statements which define various possible values.  
Any valid JavaScript statements can be executed inside a case block and will run from the first matched case value until a `break` is encountered.
```
switch (fruit) {
  case "apple":
    console.log("The fruit is an apple");
    break;
  case "orange":
    console.log("The fruit is an orange");
    break;
}
```
case values are tested with strict equality (`===`).  
The break tells JavaScript to stop executing statements. If the break is omitted, the next statement will be executed.  
  
In a switch statement you may not be able to specify all possible values as case statements.  
Instead, you can add the `default` statement which will be executed if no matching case statements are found.  
Think of it like the final else statement in an if/else chain.
```
switch (num) {
  case value1:
    statement1;
    break;
  case value2:
    statement2;
    break;
...
  default:
    defaultStatement;
    break;
}
```

If the break statement is omitted from a switch statement's case, the following case statement(s) are executed until a break is encountered.  
If you have multiple inputs with the same output, you can represent them in a switch statement like this:
```
let result = "";
switch (val) {
  case 1:
  case 2:
  case 3:
    result = "1, 2, or 3";
    break;
  case 4:
    result = "4 alone";
}
```
  
if you have many options to choose from, a switch statement can be easier to write than many chained if/else if statements.
```
if (val === 1) {
  answer = "a";
} else if (val === 2) {
  answer = "b";
} else {
  answer = "c";
}

switch (val) {
  case 1:
    answer = "a";
    break;
  case 2:
    answer = "b";
    break;
  default:
    answer = "c";
}
```
### Returning Boolean Values from Functions
```
function isEqual(a, b) {
  if (a === b) {
    return true;
  } else {
    return false;
  }
}
```
But there's a better way to do this. Since `===` returns `true` or `false`, we can return the result of the comparison:
```
function isEqual(a, b) {
  return a === b;
}
```

### Object
Objects are similar to arrays, except that instead of using indexes to access and modify their data, you access the data in objects through what are called `properties`.  
Objects are useful for storing data in a structured way, and can represent real world objects.  
  
Properties are stored as strings. However, you can also use numbers as properties.  
You can even omit the quotes for single-word string properties, as follows:
```
const anotherObject = {
  make: "Ford",
  5: "five",
  "model": "focus"
};
```
However, if your object has any non-string properties, JavaScript will automatically typecast them as strings.  
  
There are two ways to access the properties of an object: dot notation (.) and bracket notation ([]), similar to an array.  
Dot notation is what you use when you know the name of the property you're trying to access ahead of time.(obj.legs처럼 quotes쓰지 않음!)
   
if the property of the object you are trying to access has a space in its name, you will need to use bracket notation.
However, you can still use bracket notation on object properties without spaces.  
Note that property names with spaces in them must be in quotes (single or double).  
```
const myObj = {
  "Space Name": "Kirk",
  "More Space": "Spock",
  "NoSpace": "USS Enterprise"
};

myObj["Space Name"];
myObj['More Space'];
myObj["NoSpace"];
```   
  
Another use of bracket notation on objects is to access a property which is stored as the value of a variable.  
This can be very useful for iterating through an object's properties or when accessing a lookup table.  
```
const dogs = {
  Fido: "Mutt",
  Hunter: "Doberman",
  Snoopie: "Beagle"
};

const myDog = "Hunter";
const myBreed = dogs[myDog];
console.log(myBreed);
```
Note that we do not use quotes around the variable name when using it to access the property because we are using the value of the variable, not the name.  
  
After you've created a JavaScript object, you can update its properties at any time just like you would update any other variable.  
You can use either dot or bracket notation to update.  
Also, You can add new properties to existing JavaScript objects the same way you would modify them.  
    
We can also delete properties from objects like this:  
You may use either dot or bracket notation.
```
delete ourDog.bark;
```
   
  
Objects can be thought of as a key/value storage, like a dictionary.  
If you have tabular data(표 형식의), you can use an object to lookup values rather than a switch statement or an if/else chain.  
This is most useful when you know that your input data is limited to a certain range.
```
// Setup
function phoneticLookup(val) {
  let result = "";

  // Only change code below this line
  switch(val) {
    case "alpha":
      result = "Adams";
      break;
    case "bravo":
      result = "Boston";
      break;
    case "charlie":
      result = "Chicago";
      break;
    case "delta":
      result = "Denver";
      break;
    case "echo":
      result = "Easy";
      break;
    case "foxtrot":
      result = "Frank";
  }

  // Only change code above this line
  return result;
}

phoneticLookup("charlie");
```
```
// Setup
function phoneticLookup(val) {
  let result = "";

  // Only change code below this line
  const lookup = {
    "alpha": "Adams",
    "bravo": "Boston",
    "charlie": "Chicago",
    "delta": "Denver",
    "echo": "Easy",
    "foxtrot": "Frank"
  }

  result = lookup[val];
  // Only change code above this line
  return result;
}

phoneticLookup("charlie");
```
To check if a property on a given object exists or not, you can use the `.hasOwnProperty()` method.  
`someObject.hasOwnProperty(someProperty)` returns true or false depending on if the property is found on the object or not.
```
function checkForProperty(object, property) {
  return object.hasOwnProperty(property);
}
```
   
Sometimes you may want to store data in a flexible Data Structure.  
A JavaScript object is one way to handle flexible data.  
They allow for arbitrary combinations of strings, numbers, booleans, arrays, functions, and objects.
```
const ourMusic = [
  {
    "artist": "Daft Punk",
    "title": "Homework",
    "release_year": 1997,
    "formats": [ 
      "CD", 
      "Cassette", 
      "LP"
    ],
    "gold": true
  }
];
```
Objects hold data in a property, which has a key-value format.  
*In the example above,` "artist": "Daft Punk"` is a property that has a key of `artist` and a value of `Daft Punk`.*

### Iterate with JavaScript Loops
You can run the same code multiple times by using a loop.  
  
The first type of loop we will learn is called a while loop because it runs while a specified condition is true and stops once that condition is no longer true.
```
const ourArray = [];
let i = 0;

while (i < 5) {
  ourArray.push(i);
  i++;
}
```
The most common type of JavaScript loop is called a `for` loop because it runs for a specific number of times.  
For loops are declared with three optional expressions separated by semicolons:  
`for (a; b; c)`, where `a` is the initialization statement, `b` is the condition statement, and `c` is the final expression.  
  
The initialization statement is executed one time only before the loop starts. It is typically used to define and setup your loop variable.  
  
The condition statement is evaluated at the beginning of every loop iteration and will continue as long as it evaluates to true. When the condition is false at the start of the iteration, the loop will stop executing. This means if the condition starts as false, your loop will never execute.  
  
The final expression is executed at the end of each loop iteration, prior to the next condition check and is usually used to increment or decrement your loop counter.  
```
const ourArray = [];

for (let i = 0; i < 5; i++) {
  ourArray.push(i);
}
```
  
For loops don't have to iterate one at a time. By changing our `final-expression`, we can count by even numbers.  
```
const ourArray = [];

for (let i = 0; i < 10; i += 2) {
  ourArray.push(i);
}
```
A for loop can also count backwards, so long as we can define the right conditions.  
```
const ourArray = [];

for (let i = 10; i > 0; i -= 2) {
  ourArray.push(i);
}
```
  
### Iterate Through an Array with a For Loop
```
const arr = [10, 9, 8, 7, 6];

for (let i = 0; i < arr.length; i++) {
   console.log(arr[i]);
}
```
If you have a multi-dimensional array, you can use the same logic as the prior waypoint to loop through both the array and any sub-arrays. Here is an example:
```
const arr = [
  [1, 2], [3, 4], [5, 6]
];

for (let i = 0; i < arr.length; i++) {
  for (let j = 0; j < arr[i].length; j++) {
    console.log(arr[i][j]);
  }
}
```
### Iterate with JavaScript Do...While Loops
It is called a do...while loop because it will first `do` one pass of the code inside the loop no matter what,  
and then continue to run the loop `while` the specified condition evaluates to true.  
```
const ourArray = [];
let i = 0;

do {
  ourArray.push(i);
  i++;
} while (i < 5);
```
what makes the `do...while` different from other loops is how it behaves when the condition fails on the first check.
```
const ourArray = []; 
let i = 5;

do {
  ourArray.push(i);
  i++;
} while (i < 5);
```
In this case, we initialize the value of i to 5, just like we did with the while loop.  
When we get to the next line, there is no condition to evaluate, so we go to the code inside the curly braces and execute it.  
We will add a single element to the array and then increment i before we get to the condition check.  
When we finally evaluate the condition i < 5 on the last line, we see that i is now 6, which fails the conditional check, so we exit the loop and are done.  
At the end of the above example, the value of ourArray is [5]. Essentially, a do...while loop ensures that the code inside the loop will run at least once. 

### Replace Loops using Recursion
Recursion is the concept that a function can be expressed in terms of itself.  
  
multiply the first n elements of an array to create the product of those elements.  
Using a for loop, you could do this:
```
function multiply(arr, n) {
    let product = 1;
    for (let i = 0; i < n; i++) {
      product *= arr[i];
    }
  return product;
}
```
***However, notice that `multiply(arr, n) == multiply(arr, n - 1) * arr[n - 1]`.***. 
That means you can rewrite multiply in terms of itself and never need to use a loop.  
```
  function multiply(arr, n) {
    if (n <= 0) {
      return 1;
    } else {
      return multiply(arr, n - 1) * arr[n - 1];
    }
 }
```
```
let arr = [2, 4, 5, 7, 8];
multiply(arr, 3) === multiply(arr, 2) * arr[2]
앞에서 3개 곱하기는 (앞에서 두개 * 세번째꺼 곱하기)와 같음
(더하기의 경우 마찬가지로 앞에 3개 더하기는 (앞에서 두개 + 세번째거 더하기)와 같음)
multiply(arr, 2) === multiply(arr, 1) * arr[1]
multiply(arr, 1) === multiply(arr, 0) * arr[0]
따라서
multiply(arr, 3) === multiply(arr, 0) * arr[0] * arr[1] * arr[2]
여기서 multiply(arr, 0)은 필요 없음, arr[0] * arr[1] * arr[2]이 원하는 결과. 
그래서 base case, 
if (n <= 0) {
      return 1;
}
```
```
function sum(arr, n) {
  // Only change code below this line
  if ( n<= 0) {
    return 0;
  } else {
    return sum(arr, n-1) + arr[n-1];
  }
  // Only change code above this line
}
```
Recursive functions must have a base case when they return without calling the function again (in this example, when `n <= 0`), otherwise they can never finish executing.  

### Generate Random Fractions with JavaScript
JavaScript has a `Math.random()` function that generates a random decimal number between 0 (inclusive) and 1 (exclusive).  
Thus Math.random() can return a 0 but never return a 1.

### Generate Random Whole Numbers with JavaScript
1. Use `Math.random()` to generate a random decimal number.
2. Multiply that random decimal number by `20`.(아무숫자)
3. Use `Math.floor()` to round this number down to its nearest whole number.(내려서 정수로 만듬)

0부터 19까지의 정수가 랜덤으로
```
Math.floor(Math.random() * 20);
```
This formula gives a random whole number in the range from `min` to `max`.
```
Math.floor(Math.random() * (max - min + 1)) + min
```

### Use the parseInt Function
The `parseInt()` function parses a *string* and returns an *integer.*
```
const a = parseInt("007");
```
The above function converts the string 007 to the integer 7.  
If the first character in the string can't be converted into a number, then it returns `NaN`.  
  
It takes a second argument for the radix, which specifies the base of the number in the string.  
The radix can be an integer between 2 and 36.
```
const a = parseInt("11", 2);
```
*The radix variable says that 11 is in the binary system, or base 2.*. 
This example converts the string 11 to an integer 3.(2^1 * 1 + 2^0 * 1 = 3)

### Use the Conditional (Ternary) Operator
The conditional operator, also called the ternary operator, can be used as a one line if-else expression.  
  
The syntax is `a ? b : c`, where `a` is the condition, `b` is the code to run when the condition returns `true`, and `c` is the code to run when the condition returns `false`.
```
function findGreater(a, b) {
  return a > b ? "a is greater" : "b is greater or equal";
}
```
You can also chain them together to check for multiple conditions.(들여쓰기 강추)
```
function findGreaterOrEqual(a, b) {
  return (a === b) ? "a and b are equal" 
    : (a > b) ? "a is greater" 
    : "b is greater";
}
```



  
