# Basic Data Structures
you'll learn more about the differences between arrays and objects, and which to use in different situations.
 
### Use an Array to Store a Collection of Data
This is known as a one-dimensional array, meaning it only has one level, or that it does not have any other arrays nested within it.  
Notice it contains booleans, strings, and numbers, among other valid JavaScript data types:
```
let simpleArray = ['one', 2, 'three', true, false, undefined, null];
console.log(simpleArray.length);
```
All arrays have a length property, which as shown above, can be very easily accessed with the syntax`Array.length`.  
A more complex implementation of an array is known as a multi-dimensional array, or an array that contains other arrays.

### Arrays are mutable!
push, unshift은 여러 요소를 넣을 수 있지만 pop, shift는 하나의 요소만 remove 가능.

### Remove Items Using splice()
원하는 곳 어디에서 원하는 만큼 remove하고 싶을때
what if we want to remove an element from somewhere in the middle? Or remove more than one element at once?  
Well, that's where `splice()` comes in. `splice()` allows us to do just that: **remove any number of consecutive elements** from anywhere in an array.  
  
`splice()` can take up to 3 parameters, but for now, we'll focus on just the first 2.  
The first two parameters of `splice()` are integers which represent indexes, or positions, of items in the array that `splice()` is being called upon.  
splice()'s first parameter represents the *index* on the array from which to begin removing elements, while the second parameter indicates *the number of elements to delete*. 
```
let array = ['today', 'was', 'not', 'so', 'great'];

array.splice(2, 2);
```
`splice()` not only modifies the array it's being called on, but it also returns a new array containing the value of the removed elements:  
원본 수정 뿐만 아니라 삭제한 요소를 배열로 반환. 
```
let array = ['I', 'am', 'feeling', 'really', 'happy'];

let newArray = array.splice(3, 2); // ['really', 'happy']
```
### Add Items Using splice()
삽입도 가능
Well, you can use the third parameter, comprised of one or more element(s), to add to the array. 
```
const numbers = [10, 11, 12, 12, 15];
const startIndex = 3;
const amountToDelete = 1;

numbers.splice(startIndex, amountToDelete, 13, 14);
console.log(numbers); // [ 10, 11, 12, 13, 14, 15 ]
```
Note that there can be any number of elements (separated by commas) following `amountToDelete`, each of which gets inserted.  
splice는 삭제 + 삽입  

### Copy Array Items Using slice()
Rather than modifying an array, `slice()` copies or extracts a given number of elements to a new array, leaving the array it is called upon untouched.  
`slice()` takes only 2 parameters — the first is the index at which to begin extraction, and the second is the index *at which to stop extraction (extraction will occur up to, but not including the element at this index)*. Consider this:  
지정한 요소를 copy해서 새로운 배열에 반환, 원본 배열은 안 건드림. 마지막 index는 미포함임. 
```
let weatherConditions = ['rain', 'snow', 'sleet', 'hail', 'clear'];
let todaysWeather = weatherConditions.slice(1, 3); // ['snow', 'sleet']
```
In effect, we have created a new array by extracting elements from an existing array.

### Copy an Array with the Spread Operator
While `slice()` allows us to be selective about what elements of an array to copy, among several other useful tasks,  
ES6's new *spread operator* allows us to easily copy *all* of an array's elements, *in order*, with a simple and highly readable syntax. The spread syntax simply looks like this: `...`
```
let thisArray = [true, true, undefined, false, null];
let thatArray = [...thisArray];
```

### Combine Arrays with the Spread Operator
Another huge advantage of the spread operator is the ability to combine arrays, or to insert all the elements of one array into another, at any index.  
With more traditional syntaxes, we can concatenate arrays, but this only allows us to combine arrays at the end of one, and at the start of another.  
Spread syntax makes the following operation extremely simple:
```
let thisArray = ['sage', 'rosemary', 'parsley', 'thyme'];

let thatArray = ['basil', 'cilantro', ...thisArray, 'coriander'];
```

### Check For The Presence of an Element With indexOf()
`indexOf()` takes an element as a parameter, and when called, it returns the position, or index, of that element, or -1 if the element does not exist on the array.  
  
### Iterate Through All an Array's Items Using For Loops
JavaScript offers several built in methods that each iterate over arrays in slightly different ways to achieve different results (such as `every()`, `forEach()`, `map()`, etc.),  
however the technique which is most flexible and offers us the greatest amount of control is a simple for loop.  
```
function greaterThanTen(arr) {
  let newArr = [];
  for (let i = 0; i < arr.length; i++) {
    if (arr[i] > 10) {
      newArr.push(arr[i]);
    }
  }
  return newArr;
}

greaterThanTen([2, 12, 8, 14, 80, 0, 1]);
```
### Create complex multi-dimensional arrays
```
let nestedArray = [
  ['deep'],
  [
    ['deeper'], ['deeper'] 
  ],
  [
    [
      ['deepest'], ['deepest']
    ],
    [
      [
        ['deepest-est?']
      ]
    ]
  ]
];
```
The `deep` array is nested 2 levels deep. The `deeper` arrays are 3 levels deep. The `deepest` arrays are 4 levels, and the `deepest-est?` is 5.(the outer-most array is level 1)

### Add Key-Value Pairs to JavaScript Objects
At their most basic, objects are just collections of key-value pairs.  
In other words, they are pieces of data (values) mapped to unique identifiers called properties (keys). 
```
tekkenCharacter.origin = 'South Korea';
tekkenCharacter['hair color'] = 'dyed orange';

const eyes = 'eye color';
tekkenCharacter[eyes] = 'brown';

{
  player: 'Hwoarang',
  fightingStyle: 'Tae Kwon Doe',
  human: true,
  origin: 'South Korea',
  'hair color': 'dyed orange',
  'eye color': 'brown'
};

```
Bracket notation is required if your property has a space in it or if you want to use a variable to name the property.  
In the above case, the property is enclosed in quotes to denote it as a string and will be added exactly as shown.  
Without quotes, it will be evaluated as a variable and the name of the property will be whatever value the variable is. 

### Access Property Names with Bracket Notation
For instance, imagine that our `foods` object is being used in a program for a supermarket cash register. We have some function that sets the `selectedFood` and we want to check our `foods` object for the presence of that food. This might look like:
```
let selectedFood = getCurrentFood(scannedItem);
let inventory = foods[selectedFood];
```
This code will evaluate the value stored in the `selectedFood` variable and return the value of that key in the `foods` object, or `undefined` if it is not present.  
Bracket notation is very useful because *sometimes object properties are not known before runtime* or we need to access them in a more dynamic way.
```
let foods = {
  apples: 25,
  oranges: 32,
  plums: 28,
  bananas: 13,
  grapes: 35,
  strawberries: 27
};

function checkInventory(scannedItem) {
  // Only change code below this line
  return foods[scannedItem];
  // Only change code above this line
}

console.log(checkInventory("apples"));
```
### Use the delete Keyword to Remove Object Properties
In short, objects are key-value stores which provide a flexible, intuitive way to structure data, and, they provide very fast lookup time.  

```
delete foods.apples;
```

### Check if an Object has a Property
One uses the `hasOwnProperty()` method and the other uses the `in` keyword. If we have an object users with a property of Alan, we could check for its presence in either of the following ways:
```
users.hasOwnProperty('Alan');
'Alan' in users;
```

### Iterate Through the Keys of an Object with a for...in Statement
Sometimes you need to iterate through all the *keys* within an object. You can use a for...in loop to do this. 
```
const refrigerator = {
  'milk': 1,
  'eggs': 12,
};

for (const food in refrigerator) {
  console.log(food, refrigerator[food]);
}
```
This code logs `milk 1` and `eggs 12`, with each key-value pair on its own line.  
We defined the variable `food` in the loop head and this variable was set to each of the object's keys on each iteration, resulting in each food's name being printed to the console.

NOTE: Objects do not maintain an ordering to stored keys like arrays do; thus a key's position on an object, or the relative order in which it appears, is irrelevant when referencing or accessing that key.

```
const users = {
  Alan: {
    online: false
  },
  Jeff: {
    online: true
  },
  Sarah: {
    online: false
  }
}

function countOnline(allUsers) {
  // Only change code below this line
  let count = 0;
  for(const user in allUsers) {
    if(allUsers[user].online) { // [user]임에 주의
      count++;
    }
  }
  return count;
  // Only change code above this line
}

console.log(countOnline(users));
```

### Generate an Array of All Object Keys with Object.keys()
We can also generate an array which contains all the keys stored in an object with the `Object.keys()` method.  
This method takes an object as the argument and returns an array of strings representing each property in the object.  
Again, there will be no specific order to the entries in the array.

### Modify an Array Stored in an Object
Now you've seen all the basic operations for JavaScript objects. You can add, modify, and remove key-value pairs, check if keys exist, and iterate over all the keys in an object. As you continue learning JavaScript you will see even more versatile applications of objects.  
  
Additionally, the Data Structures lessons located in the Coding Interview Prep section of the curriculum also cover the ES6 Map and Set objects, both of which are similar to ordinary objects but provide some additional features. 




