# Basic Algorithm Scripting
An algorithm is a series of step-by-step instructions that describe how to do something.
To write an effective algorithm, it helps to break a problem down into smaller parts and think carefully about how to solve each part with code.

### Reverse a String
```
function reverseString(str) {
  return str.split('').reverse().join('');
}

// function reverseString(str) {
//   let newstr = '';
//   for(let i = str.length - 1; i >= 0; i-- ) {
//     newstr += str[i];
//   }
//   return newstr;
// }

console.log(reverseString("hello"));
```

