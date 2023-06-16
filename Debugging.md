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

