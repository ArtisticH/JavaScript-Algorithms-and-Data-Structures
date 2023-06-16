# Debugging
Issues in code generally come in three forms: syntax errors that prevent your program from running,  
runtime errors where your code has unexpected behavior, or logical errors where your code doesn't do what you intended.  

### Use the JavaScript Console to Check the Value of a Variable

The `console.log()` method, which "prints" the output of what's within its parentheses to the console, will likely be the most helpful debugging tool.  
Placing it at strategic points in your code can show you the intermediate values of variables.  
It's good practice to have an idea of what the output should be before looking at what it is.  
Having check points to see the status of your calculations throughout your code will help narrow down where the problem is.  
  
There are many methods to use with console to output messages.`log`, `warn`, and `clear` to name a few. 

### Use typeof to Check the Type of a Variable
This is useful in debugging when working with multiple data types. If you think you're adding two numbers, but one is actually a string, the results can be unexpected.  
Type errors can lurk in calculations or function calls. Be careful especially when you're accessing and working with external data in the form of a JavaScript Object Notation (JSON) object.  
  
JavaScript recognizes seven primitive (immutable) data types: `Boolean`, `Null`, `Undefined`, `Number`, `String`, `Symbol` (new with ES6), and `BigInt` (new with ES2020), and one type for mutable items: `Object`.  
Note that in JavaScript, arrays are technically a type of object.

### Catch Mixed Usage of Single and Double Quotes
```
const grouchoContraction = "I've had a perfectly wonderful evening, but this wasn't it.";
const quoteInString = "Groucho Marx once said 'Quote me as saying I was mis-quoted.'";
const uhOhGroucho = 'I've had a perfectly wonderful evening, but this wasn't it.';
```
The first two are correct, but the third is incorrect.  
  
Of course, it is okay to use only one style of quotes. You can escape the quotes inside the string by using the backslash (`\`) escape character:
```
const allSameQuotes = 'I\'ve had a perfectly wonderful evening, but this wasn\'t it.';
```

### Catch Use of Assignment Operator Instead of Equality Operator
The code below assigns x to be 2, which evaluates as true.  
Almost every value on its own in JavaScript evaluates to true, except what are known as the "falsy" values:  
`false`, `0`, `""` (an empty string), `NaN`, `undefined`, and `null`.
```
let x = 1;
let y = 2;
if (x = y) {

} else {

}
```

### Catch Missing Open and Closing Parenthesis After a Function Call
```
function myFunction() {
  return "You rock!";
}
let varOne = myFunction;
let varTwo = myFunction();
```
Here `varOne` is the function `myFunction`, and `varTwo` is the string `You rock!`.  
  
Also, Make sure to supply all required arguments, in the proper order to avoid these issues.
  
### Catch Off By One Errors When Using Indexing
If you try to access an index equal to the length, the program may throw an "index out of range" reference error or print `undefined`.  
```
let alphabet = "abcdefghijklmnopqrstuvwxyz";
let len = alphabet.length;
for (let i = 0; i <= len; i++) {
  console.log(alphabet[i]);
}
for (let j = 1; j < len; j++) {
  console.log(alphabet[j]);
}
for (let k = 0; k < len; k++) {
  console.log(alphabet[k]);
}
```
The first example here loops one too many times, and the second loops one too few times (missing the first index, 0). The third example is correct.

### Use Caution When Reinitializing Variables Inside a Loop
Sometimes it's necessary to save information, increment counters, or re-set variables within a loop.  
A potential issue is when variables either should be reinitialized, and aren't, or vice versa.  
This is particularly dangerous if you accidentally reset the variable being used for the terminal condition, causing an infinite loop.

### Prevent Infinite Loops with a Valid Terminal Condition
Infinite loops are likely to freeze or crash the browser, and cause general program execution mayhem, which no one wants.  
  
One error is incrementing or decrementing a counter variable in the wrong direction from the terminal condition.  
Another one is accidentally resetting a counter or index variable within the loop code, instead of incrementing or decrementing it.

