# Functional Programming
In Functional Programming, code is organized into smaller, basic functions that can be combined to build complex programs.

### Learn About Functional Programming
Functional programming is a style of programming where solutions are simple, isolated functions, without any side effects outside of the function scope: `INPUT -> PROCESS -> OUTPUT`.  
- Isolated functions - there is no dependence on the state of the program, which includes global variables that are subject to change  
- (전역 변수처럼 프로그램 상태에 의존하지 않음)
- Pure functions - the same input always gives the same output
- Functions with limited side effects - any changes, or mutations, to the state of the program outside the function are carefully controlled

```
// Function that returns a string representing a cup of green tea
const prepareTea = () => 'greenTea';

/*
Given a function (representing the tea type) and number of cups needed, the
following function returns an array of strings (each representing a cup of
a specific type of tea).
*/
const getTea = (numOfCups) => {
  const teaCups = [];

  for(let cups = 1; cups <= numOfCups; cups += 1) {
    const teaCup = prepareTea();
    teaCups.push(teaCup);
  }
  return teaCups;
};

// Only change code below this line
const tea4TeamFCC = getTea(40);
console.log(tea4TeamFCC);
// Only change code above this line
```

### Understand Functional Programming Terminology

The FCC Team had a mood swing and now wants two types of tea: green tea and black tea.  
General Fact: Client mood swings are pretty common.

With that information, we'll need to revisit the `getTea` function from last challenge to handle various tea requests.  
We can modify `getTea` to accept a function as a parameter to be able to change the type of tea it prepares.  
This makes getTea more flexible, and gives the programmer more control when client requests change.

But first, let's cover some functional terminology:  

Callbacks are the functions that are slipped or passed into another function to decide the invocation of that function. You may have seen them passed to other methods, for example in `filter`, the callback function tells JavaScript the criteria for how to filter an array.

Functions that can be assigned to a variable, passed into another function, or returned from another function just like any other normal value, are called *first class* functions. In JavaScript, all functions are first class functions.

The functions that take a function as an argument, or return a function as a return value, are called *higher order functions*.

When functions are passed in to or returned from another function, then those functions which were passed in or returned can be called a *lambda*.


