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
```
// Function that returns a string representing a cup of green tea
const prepareGreenTea = () => 'greenTea';

// Function that returns a string representing a cup of black tea
const prepareBlackTea = () => 'blackTea';

/*
Given a function (representing the tea type) and number of cups needed, the
following function returns an array of strings (each representing a cup of
a specific type of tea).
*/
const getTea = (prepareTea, numOfCups) => {
  const teaCups = [];

  for(let cups = 1; cups <= numOfCups; cups += 1) {
    const teaCup = prepareTea();
    teaCups.push(teaCup);
  }
  return teaCups;
};

// Only change code below this line
const tea4GreenTeamFCC = getTea(prepareGreenTea, 27);
const tea4BlackTeamFCC = getTea(prepareBlackTea, 13);
// Only change code above this line

console.log(
  tea4GreenTeamFCC,
  tea4BlackTeamFCC
);
```

### 🌟Understand the Hazards of Using Imperative Code
Functional programming is a good habit. It keeps your code easy to manage, and saves you from sneaky bugs. But before we get there, let's look at an imperative approach to programming to highlight where you may have issues.

In English (and many other languages), the imperative tense is used to give commands. Similarly, an imperative style in programming is one that gives the computer a set of statements to perform a task.

Often the statements change the state of the program, like updating global variables. A classic example is writing a `for` loop that gives exact directions to iterate over the indices of an array.

In contrast, functional programming is a form of declarative programming. You tell the computer what you want done by calling a method or function.

JavaScript offers many predefined methods that handle common tasks so you don't need to write out how the computer should perform them. For example, instead of using the `for` loop mentioned above, you could call the `map` method which handles the details of iterating over an array. This helps to avoid semantic errors, like the "Off By One Errors" that were covered in the Debugging section.

Consider the scenario: you are browsing the web in your browser, and want to track the tabs you have opened. Let's try to model this using some simple object-oriented code.

A Window object is made up of tabs, and you usually have more than one Window open. The titles of each open site in each Window object is held in an array. After working in the browser (opening new tabs, merging windows, and closing tabs), you want to print the tabs that are still open. Closed tabs are removed from the array and new tabs (for simplicity) get added to the end of it.

The code editor shows an implementation of this functionality with functions for `tabOpen()`, `tabClose()`, and `join()`. The array tabs is part of the Window object that stores the name of the open pages.

```
// tabs is an array of titles of each site open within the window
const Window = function(tabs) {
  this.tabs = tabs; // We keep a record of the array inside the object
};

// When you join two windows into one window
Window.prototype.join = function(otherWindow) {
  this.tabs = this.tabs.concat(otherWindow.tabs);
  return this;
};

// When you open a new tab at the end
Window.prototype.tabOpen = function(tab) {
  this.tabs.push('new tab'); // Let's open a new tab for now
  return this;
};

// When you close a tab
Window.prototype.tabClose = function(index) {

  // Only change code below this line
  const tabsBeforeIndex = this.tabs.slice(0, index); // Get the tabs before the tab
  const tabsAfterIndex = this.tabs.slice(index + 1); // Get the tabs after the tab

  this.tabs = tabsBeforeIndex.concat(tabsAfterIndex); // Join them together

  // Only change code above this line

  return this;
 };

// Let's create three browser windows
const workWindow = new Window(['GMail', 'Inbox', 'Work mail', 'Docs', 'freeCodeCamp']); // Your mailbox, drive, and other work sites
const socialWindow = new Window(['FB', 'Gitter', 'Reddit', 'Twitter', 'Medium']); // Social sites
const videoWindow = new Window(['Netflix', 'YouTube', 'Vimeo', 'Vine']); // Entertainment sites

// Now perform the tab opening, closing, and other operations
const finalTabs = socialWindow
  .tabOpen() // Open a new tab for cat memes
  .join(videoWindow.tabClose(2)) // Close third tab in video window, and join
  .join(workWindow.tabClose(1).tabOpen());
console.log(finalTabs.tabs);
// ['FB', 'Gitter', 'Reddit', 'Twitter', 'Medium', 'new tab', 'Netflix', 'YouTube', 'Vine', 'GMail', 'Work mail', 'Docs', 'freeCodeCamp', 'new tab']
```

### Avoid Mutations and Side Effects Using Functional Programming
If you haven't already figured it out, the issue in the previous challenge was with the `splice` call in the `tabClose()` function.  
Unfortunately, `splice` changes the original array it is called on, so the second call to it used a modified array, and gave unexpected results.

This is a small example of a much larger pattern - you call a function on a variable, array, or an object, and the function changes the variable or something in the object.

One of the core principles of functional programming is to not change things. Changes lead to bugs. It's easier to prevent bugs knowing that your functions don't change anything, including the function arguments or any global variable.

The previous example didn't have any complicated operations but the splice method changed the original array, and resulted in a bug.

Recall that in functional programming, changing or altering things is called *mutation*, and the outcome is called a *side effect*. A function, ideally, should be a pure function, meaning that it does not cause any side effects.

Let's try to master this discipline and not alter any variable or object in our code.

```
// The global variable
let fixedValue = 4;

function incrementer() {
  // Only change code below this line
 let copy = fixedValue;
 copy++;
 return copy;

  // Only change code above this line
}
console.log(fixedValue);
console.log(incrementer())
```

### Pass Arguments to Avoid External Dependence in a Function
The last challenge was a step closer to functional programming principles, but there is still something missing.

We didn't alter the global variable value, but the function `incrementer` would not work without the global variable `fixedValue` being there.

Another principle of functional programming is to always declare your dependencies explicitly. This means if a function depends on a variable or object being present, then pass that variable or object directly into the function as an argument.

There are several good consequences from this principle. The function is easier to test, you know exactly what input it takes, and it won't depend on anything else in your program.

This can give you more confidence when you alter, remove, or add new code. You would know what you can or cannot change and you can see where the potential traps are.

Finally, the function would always produce the same output for the same set of inputs, no matter what part of the code executes it.

```
// The global variable
let fixedValue = 4;

// Only change code below this line
function incrementer(arg) {
  arg++;
  return arg;
  // Only change code above this line
}
console.log(fixedValue, incrementer(fixedValue)); // 4 5
```

### Refactor Global Variables Out of Functions

So far, we have seen two distinct principles for functional programming:

- Don't alter a variable or object - create new variables and objects and return them if need be from a function. Hint: using something like `const newArr = arrVar`, where `arrVar` is an array will simply create a reference to the existing variable and not a copy. So changing a value in `newArr` would change the value in `arrVar`.
- Declare function parameters - any computation inside a function depends only on the arguments passed to the function, and not on any global object or variable.

Adding one to a number is not very exciting, but we can apply these principles when working with arrays or more complex objects.  

***
Rewrite the code so the global array bookList is not changed inside either function. The add function should add the given bookName to the end of the array passed to it and return a new array (list). The remove function should remove the given bookName from the array passed to it.

Both functions should return an array, and any new parameters should be added before the bookName parameter.
***
```
// The global variable
const bookList = ["The Hound of the Baskervilles", "On The Electrodynamics of Moving Bodies", "Philosophiæ Naturalis Principia Mathematica", "Disquisitiones Arithmeticae"];

// Change code below this line
function add(bookList, bookName) {
  let newList = [...bookList];
  newList.push(bookName);
  return newList;
  
  // Change code above this line
}

// Change code below this line
function remove(bookList, bookName) {
  let newList = [...bookList];
  const book_index = newList.indexOf(bookName);
  if (book_index >= 0) {

    newList.splice(book_index, 1);
    return newList;
    // Change code above this line
    }
}

console.log(add(bookList, "A Brief History of Time"));
console.log(bookList);
console.log(remove(bookList, "On The Electrodynamics of Moving Bodies"));
console.log(remove(add(bookList, "A Brief History of Time"), "On The Electrodynamics of Moving Bodies"));
```

### Use the map Method to Extract Data from an Array
So far we have learned to use pure functions to avoid side effects in a program. Also, we have seen the value in having a function only depend on its input arguments.

This is only the beginning. As its name suggests, functional programming is centered around a theory of functions.

It would make sense to be able to pass them as arguments to other functions, and return a function from another function. Functions are considered first class objects in JavaScript, which means they can be used like any other object. They can be saved in variables, stored in an object, or passed as function arguments.

Let's start with some simple array functions, which are methods on the array object prototype. In this exercise we are looking at `Array.prototype.map()`, or more simply `map`.

The `map` method iterates over each item in an array and returns a new array containing the results of calling the callback function on each element. *It does this without mutating the original array*.

When the callback is used, it is passed three arguments. The first argument is the current element being processed. The second is the index of that element and the third is the array upon which the `map` method was called.

See below for an example using the `map` method on the `users` array to return a new array containing only the names of the users as elements. For simplicity, the example only uses the first argument of the callback.  
```
const users = [
  { name: 'John', age: 34 },
  { name: 'Amy', age: 20 },
  { name: 'camperCat', age: 10 }
];

const names = users.map(user => user.name);
console.log(names); // [ 'John', 'Amy', 'camperCat' ]
```
```
// The global variable
const watchList = [
  {
    "Title": "Inception",
    "Year": "2010",
    "Rated": "PG-13",
    "Released": "16 Jul 2010",
    "Runtime": "148 min",
    "Genre": "Action, Adventure, Crime",
    "Director": "Christopher Nolan",
    "Writer": "Christopher Nolan",
    "Actors": "Leonardo DiCaprio, Joseph Gordon-Levitt, Elliot Page, Tom Hardy",
    "Plot": "A thief, who steals corporate secrets through use of dream-sharing technology, is given the inverse task of planting an idea into the mind of a CEO.",
    "Language": "English, Japanese, French",
    "Country": "USA, UK",
    "Awards": "Won 4 Oscars. Another 143 wins & 198 nominations.",
    "Poster": "http://ia.media-imdb.com/images/M/MV5BMjAxMzY3NjcxNF5BMl5BanBnXkFtZTcwNTI5OTM0Mw@@._V1_SX300.jpg",
    "Metascore": "74",
    "imdbRating": "8.8",
    "imdbVotes": "1,446,708",
    "imdbID": "tt1375666",
    "Type": "movie",
    "Response": "True"
  },
  {
    "Title": "Interstellar",
    "Year": "2014",
    "Rated": "PG-13",
    "Released": "07 Nov 2014",
    "Runtime": "169 min",
    "Genre": "Adventure, Drama, Sci-Fi",
    "Director": "Christopher Nolan",
    "Writer": "Jonathan Nolan, Christopher Nolan",
    "Actors": "Ellen Burstyn, Matthew McConaughey, Mackenzie Foy, John Lithgow",
    "Plot": "A team of explorers travel through a wormhole in space in an attempt to ensure humanity's survival.",
    "Language": "English",
    "Country": "USA, UK",
    "Awards": "Won 1 Oscar. Another 39 wins & 132 nominations.",
    "Poster": "http://ia.media-imdb.com/images/M/MV5BMjIxNTU4MzY4MF5BMl5BanBnXkFtZTgwMzM4ODI3MjE@._V1_SX300.jpg",
    "Metascore": "74",
    "imdbRating": "8.6",
    "imdbVotes": "910,366",
    "imdbID": "tt0816692",
    "Type": "movie",
    "Response": "True"
  },
  {
    "Title": "The Dark Knight",
    "Year": "2008",
    "Rated": "PG-13",
    "Released": "18 Jul 2008",
    "Runtime": "152 min",
    "Genre": "Action, Adventure, Crime",
    "Director": "Christopher Nolan",
    "Writer": "Jonathan Nolan (screenplay), Christopher Nolan (screenplay), Christopher Nolan (story), David S. Goyer (story), Bob Kane (characters)",
    "Actors": "Christian Bale, Heath Ledger, Aaron Eckhart, Michael Caine",
    "Plot": "When the menace known as the Joker wreaks havoc and chaos on the people of Gotham, the caped crusader must come to terms with one of the greatest psychological tests of his ability to fight injustice.",
    "Language": "English, Mandarin",
    "Country": "USA, UK",
    "Awards": "Won 2 Oscars. Another 146 wins & 142 nominations.",
    "Poster": "http://ia.media-imdb.com/images/M/MV5BMTMxNTMwODM0NF5BMl5BanBnXkFtZTcwODAyMTk2Mw@@._V1_SX300.jpg",
    "Metascore": "82",
    "imdbRating": "9.0",
    "imdbVotes": "1,652,832",
    "imdbID": "tt0468569",
    "Type": "movie",
    "Response": "True"
  },
  {
    "Title": "Batman Begins",
    "Year": "2005",
    "Rated": "PG-13",
    "Released": "15 Jun 2005",
    "Runtime": "140 min",
    "Genre": "Action, Adventure",
    "Director": "Christopher Nolan",
    "Writer": "Bob Kane (characters), David S. Goyer (story), Christopher Nolan (screenplay), David S. Goyer (screenplay)",
    "Actors": "Christian Bale, Michael Caine, Liam Neeson, Katie Holmes",
    "Plot": "After training with his mentor, Batman begins his fight to free crime-ridden Gotham City from the corruption that Scarecrow and the League of Shadows have cast upon it.",
    "Language": "English, Urdu, Mandarin",
    "Country": "USA, UK",
    "Awards": "Nominated for 1 Oscar. Another 15 wins & 66 nominations.",
    "Poster": "http://ia.media-imdb.com/images/M/MV5BNTM3OTc0MzM2OV5BMl5BanBnXkFtZTYwNzUwMTI3._V1_SX300.jpg",
    "Metascore": "70",
    "imdbRating": "8.3",
    "imdbVotes": "972,584",
    "imdbID": "tt0372784",
    "Type": "movie",
    "Response": "True"
  },
  {
    "Title": "Avatar",
    "Year": "2009",
    "Rated": "PG-13",
    "Released": "18 Dec 2009",
    "Runtime": "162 min",
    "Genre": "Action, Adventure, Fantasy",
    "Director": "James Cameron",
    "Writer": "James Cameron",
    "Actors": "Sam Worthington, Zoe Saldana, Sigourney Weaver, Stephen Lang",
    "Plot": "A paraplegic marine dispatched to the moon Pandora on a unique mission becomes torn between following his orders and protecting the world he feels is his home.",
    "Language": "English, Spanish",
    "Country": "USA, UK",
    "Awards": "Won 3 Oscars. Another 80 wins & 121 nominations.",
    "Poster": "http://ia.media-imdb.com/images/M/MV5BMTYwOTEwNjAzMl5BMl5BanBnXkFtZTcwODc5MTUwMw@@._V1_SX300.jpg",
    "Metascore": "83",
    "imdbRating": "7.9",
    "imdbVotes": "876,575",
    "imdbID": "tt0499549",
    "Type": "movie",
    "Response": "True"
  }
];

// Only change code below this line

const ratings = watchList.map(item => ({
  title: item.Title,
  rating: item.imdbRating
}));
// Only change code above this line
console.log(JSON.stringify(ratings));
// [{"title":"Inception","rating":"8.8"},{"title":"Interstellar","rating":"8.6"},{"title":"The Dark Knight","rating":"9.0"},{"title":"Batman Begins","rating":"8.3"},{"title":"Avatar","rating":"7.9"}]
```

### Implement map on a Prototype
As you have seen from applying `Array.prototype.map()`, or simply `map()` earlier, the `map` method returns an array of the same length as the one it was called on. It also doesn't alter the original array, as long as its callback function doesn't.

In other words, `map` is a pure function, and its output depends solely on its inputs. Plus, it takes another function as its argument.

You might learn a lot about the `map` method if you implement your own version of it. It is recommended you use a `for` loop or `Array.prototype.forEach()`.  
***
Write your own `Array.prototype.myMap()`, which should behave exactly like `Array.prototype.map()`. You should not use the built-in map method. The `Array` instance can be accessed in the `myMap` method using `this`.
***
```
Array.prototype.myMap = function(callback) {
  const newArray = [];
  // Only change code below this line
  let copyArray = [...this];
  for(let i = 0; i < copyArray.length; i++) {
    let changedElements = callback(copyArray[i], i, copyArray);
    newArray.push(changedElements);
  }
  // Only change code above this line
  return newArray;
};

[23, 65, 98, 5, 13].myMap(item => item * 2); // [46, 130, 196, 10, 26]
["naomi", "quincy", "camperbot"].myMap(element => element.toUpperCase()); // [ 'NAOMI', 'QUINCY', 'CAMPERBOT' ]
[1, 1, 2, 5, 2].myMap((element, index, array) => array[index + 1] || array[0]); //  [1, 2, 5, 2, 1]
```
👇 답안 1
```
Array.prototype.myMap = function(callback) {
  const newArray = [];
  // Only change code below this line
  for (let i = 0; i < this.length; i++) {
    newArray.push(callback(this[i], i, this));
  }
  // Only change code above this line
  return newArray;
};
```
### Use the filter Method to Extract Data from an Array
Another useful array function is `Array.prototype.filter()`, or simply `filter()`.

`filter` calls a function on each element of an array and returns a new array containing only the elements for which that function returns a truthy value - that is, a value which returns `true` if passed to the `Boolean()` constructor. In other words, it filters the array, based on the function passed to it. Like `map`, it does this without needing to modify the original array.

The callback function accepts three arguments. The first argument is the current element being processed. The second is the index of that element and the third is the array upon which the `filter` method was called.

See below for an example using the `filter` method on the `users` array to return a new array containing only the users under the age of 30. For simplicity, the example only uses the first argument of the callback.
```
const users = [
  { name: 'John', age: 34 },
  { name: 'Amy', age: 20 },
  { name: 'camperCat', age: 10 }
];

const usersUnder30 = users.filter(user => user.age < 30);
console.log(usersUnder30); // [ { name: 'Amy', age: 20 }, { name: 'camperCat', age: 10 } ]
```
### Implement the filter Method on a Prototype
***
Write your own `Array.prototype.myFilter()`, which should behave exactly like `Array.prototype.filter()`. You should not use the built-in filter method. The Array instance can be accessed in the `myFilter` method using `this`.
***
```
Array.prototype.myFilter = function(callback) {
  const newArray = [];
  // Only change code below this line
  for(let i = 0; i < this.length; i++) {
    if (callback(this[i], i, this)) {
      newArray.push(this[i]);
    }
  }
  console.log(newArray);
  // Only change code above this line
  return newArray;
};

[23, 65, 98, 5, 13].myFilter(item => item % 2); // [23, 65, 5, 13]
["naomi", "quincy", "camperbot"].myFilter(element => element === "naomi"); // ["naomi"]
[1, 1, 2, 5, 2].myFilter((element, index, array) => array.indexOf(element) === index); // [1, 2, 5]
```
### Return Part of an Array Using the slice Method

The `slice` method returns a copy of certain elements of an array.  
It can take two arguments, the first gives the index of where to begin the slice, the second is the index for where to end the slice (and it's non-inclusive).  
If the arguments are not provided, the default is to start at the beginning of the array through the end, which is an easy way to make a copy of the entire array.  
The `slice` method does not mutate the original array, but returns a new one.
```
const arr = ["Cat", "Dog", "Tiger", "Zebra"];
const newArray = arr.slice(1, 3); // ["Dog", "Tiger"]
```

### Remove Elements from an Array Using slice Instead of splice
A common pattern while working with arrays is when you want to remove items and keep the rest of the array.  
JavaScript offers the `splice` method for this, which takes arguments for the index of where to start removing items, then the number of items to remove.  
If the second argument is not provided, the default is to remove items through the end.  
However, the `splice` method mutates the original array it is called on.  

As we saw in the last challenge, the `slice` method does not mutate the original array, but returns a new one which can be saved into a variable.  
Recall that the slice method takes two arguments for the indices to begin and end the slice (the end is non-inclusive), and returns those items in a new array.  
Using the `slice` method instead of `splice` helps to avoid any array-mutating side effects.

### Combine Two Arrays Using the concat Method
Concatenation means to join items end to end. JavaScript offers the `concat` method for both strings and arrays that work in the same way.  
For arrays, the method is called on one, then another array is provided as the argument to concat, which is added to the end of the first array.  
It returns a new array and does not mutate either of the original arrays.
```
[1, 2, 3].concat([4, 5, 6]);
// [1, 2, 3, 4, 5, 6]
```

### Add Elements to the End of an Array Using concat Instead of push

Functional programming is all about creating and using non-mutating functions.

The last challenge introduced the `concat` method as a way to merge arrays into a new array without mutating the original arrays.  
Compare `concat` to the `push` method. `push` adds items to the end of the same array it is called on, which mutates that array.  

`concat` offers a way to merge new items to the end of an array without any mutating side effects.  

### Use the reduce Method to Analyze Data

