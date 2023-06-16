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

### Factorialize a Number
```
function factorialize(num) {
  if(num <= 1) {
    return 1;
  } else {
    return num * factorialize(num-1);
  }
}

// function factorialize(num) {
//   let product = 1;
//   for(let i = num; i >= 1; i--) {
//     product *= i;
//   }
//   return product;
// }

console.log(factorialize(5));
console.log(factorialize(10));
console.log(factorialize(20));
console.log(factorialize(1));
```

### Find the Longest Word in a String
```
function findLongestWordLength(str) {
  let arr = str.match(/[^\s]+/g);
  for(let i = 0; i < arr.length; i++) {
    arr[i] = arr[i].length;
  }
  return Math.max(...arr);
}

console.log(findLongestWordLength("The quick brown fox jumped over the lazy dog"));
console.log(findLongestWordLength("May the force be with you"));
console.log(findLongestWordLength("Google do a barrel roll"));
console.log(findLongestWordLength("What is the average airspeed velocity of an unladen swallow"));
console.log(findLongestWordLength("What if we try a super-long word such as otorhinolaryngology"));
```

### Return Largest Numbers in Arrays
```
function largestOfFour(arr) {
  let newArr = [];
  for(let i = 0; i < arr.length; i++) {
    let max = Math.max(...arr[i]);
    newArr.push(max);
  }
  console.log(newArr);
  return newArr;
}

largestOfFour([[4, 5, 1, 3], [13, 27, 18, 26], [32, 35, 37, 39], [1000, 1001, 857, 1]]);
largestOfFour([[13, 27, 18, 26], [4, 5, 1, 3], [32, 35, 37, 39], [1000, 1001, 857, 1]]);
largestOfFour([[4, 9, 1, 3], [13, 35, 18, 26], [32, 35, 97, 39], [1000000, 1001, 857, 1]]);
largestOfFour([[17, 23, 25, 12], [25, 7, 34, 48], [4, -10, 18, 21], [-72, -3, -17, -10]]);
```
### Confirm the Ending
```
function confirmEnding(str, target) {
  let arr = str.split('');
  let num = str.length - target.length;
  let piece = arr.splice(num, target.length);
  return target === piece.join('');

}

console.log(confirmEnding("Bastian", "n"));
console.log(confirmEnding("Congratulation", "on"));
console.log(confirmEnding("Walking on water and developing software from a specification are easy if both are frozen", "specification"));
console.log(confirmEnding("He has to give me a new name", "name"));
console.log(confirmEnding("Connor", "n"));
console.log(confirmEnding("Abstraction", "action"));
```
👇 답안 1
```
function confirmEnding(str, target) {
  // "Never give up and good luck will find you."
  // -- Falcor

  return str.slice(str.length - target.length) === target;
}
```

### Repeat a String Repeat a String
```
function repeatStringNumTimes(str, num) {
  let i = 1;
  let str2 = '';
  while (i <= num) {
    str2 = str2.concat(str);
    i++;
  }
  console.log(str2);
  return str2;
}

repeatStringNumTimes("abc", 3);
repeatStringNumTimes("abc", 0);
repeatStringNumTimes("abc", -2);
repeatStringNumTimes("*", 3);
repeatStringNumTimes("abc", 4);
repeatStringNumTimes("*", 8);
```
### Truncate a String
```
function truncateString(str, num) {
  if (str.length <= num) {
    return str;
  } else {
    let subStr = [...str].splice(0, num).join(''); // str에 그냥 slice써도 된다.
    return `${subStr}...`;
  }
}

truncateString("A-tisket a-tasket A green and yellow basket", 8);
truncateString("Peter Piper picked a peck of pickled peppers", 11);
truncateString("A-tisket a-tasket A green and yellow basket", "A-tisket a-tasket A green and yellow basket".length);
truncateString("A-tisket a-tasket A green and yellow basket", "A-tisket a-tasket A green and yellow basket".length + 2);
truncateString("A-", 1);
truncateString("Absolutely Longer", 2);
```
slice는 배열과 문자열에서 모두 사용 가능하지만, splice는 문자열에서 사용 불가.  

### Finders Keepers
```
function findElement(arr, func) {
  for(let i = 0; i < arr.length; i++) {
    if(func(arr[i])) return arr[i];
  } 
}

console.log(findElement([1, 2, 3, 4], num => num % 2 === 0)); // 2
console.log(findElement([1, 3, 5, 8, 9, 10], function(num) { return num % 2 === 0; })); // 8
console.log(findElement([1, 3, 5, 9], function(num) { return num % 2 === 0; })); // undefined
```

### Boo who
```
function booWho(bool) {
  if(typeof bool === 'boolean') {
    return true;
  } else {
    return false;
  }
}

console.log(booWho(null)); // false
```

### Title Case a Sentence

```
function titleCase(str) {
  let arr = str.split('');
  let newStr = '';
  for(let i = 0; i < arr.length; i++) {
    if(i === 0 || arr[i-1] === ' ') {
      newStr += arr[i].toUpperCase();
    } else {
      newStr += arr[i].toLowerCase();
    }
  }
  console.log(newStr);
  return newStr;
}

titleCase("I'm a little tea pot"); // I'm A Little Tea Pot
titleCase("sHoRt AnD sToUt"); // Short And Stout
titleCase("HERE IS MY HANDLE HERE IS MY SPOUT"); 
// Here Is My Handle Here Is My Spout
```
👇 답안 1
```
function titleCase(str) {
  const newTitle = str.split(" ");
  const updatedTitle = [];
  for (let st in newTitle) {
    updatedTitle[st] = newTitle[st][0].toUpperCase() + newTitle[st].slice(1).toLowerCase();
  }
  return updatedTitle.join(" ");
}
```
👇 답안 2
```
function titleCase(str) {
  return str
    .toLowerCase()
    .split(" ")
    .map(val => val.replace(val.charAt(0), val.charAt(0).toUpperCase()))
    .join(" ");
}

titleCase("I'm a little tea pot");
```
👇 답안 3
```
function titleCase(str) {
  return str
    .toLowerCase()
    .replace(/(^|\s)\S/g, L => L.toUpperCase());
}
```
### Slice and Splice
```
function frankenSplice(arr1, arr2, n) {
  let second = arr2.slice(0);
  second.splice(n, 0, ...arr1);
  return second;
}
// The second array should remain the same after the function runs.
frankenSplice([1, 2, 3], [4, 5, 6], 1);
frankenSplice([1, 2, 3], [4, 5], 1) ;
frankenSplice([1, 2], ["a", "b"], 1);
frankenSplice(["claw", "tentacle"], ["head", "shoulders", "knees", "toes"], 2);
frankenSplice([1, 2, 3, 4], [], 0);
```
### Falsy Bouncer
```
function bouncer(arr) {
  let newarr = arr.filter(item => !item !== true);
  return newarr;
}

bouncer([7, "ate", "", false, 9]);
bouncer(["a", "b", "c"]);
bouncer([false, null, 0, NaN, undefined, ""]);
```
### Where do I Belong
```
function getIndexToIns(arr, num) {
  arr.push(num);
  arr.sort((a,b) => a-b);
  console.log(arr.indexOf(num));
  return arr.indexOf(num);
}

getIndexToIns([40, 60], 50);
getIndexToIns([10, 20, 30, 40, 50], 35);
getIndexToIns([10, 20, 30, 40, 50], 30);
getIndexToIns([3, 10, 5], 3);
getIndexToIns([5, 3, 20, 3], 5);
```
### Mutations
```
function mutation(arr) {
  let first = arr[0].toLowerCase().split('').sort(); 
  let second = arr[1].toLowerCase().split('').sort();
  let count = 0;
  for(let i = 0; i < second.length; i++) {
    if(first.includes(second[i])) {
      count++;
    }
  }
  console.log(count === second.length);
  return count === second.length;
}

mutation(["hello", "hey"]);
mutation(["Mary", "Aarmy"]);
mutation(["zyxwvutsrqponmlkjihgfedcba", "qrstu"]);
mutation(["Alien", "line"]);
```
👇 답안 1
```
function mutation(arr) {
  const test = arr[1].toLowerCase();
  const target = arr[0].toLowerCase();
  for (let i = 0; i < test.length; i++) {
    if (target.indexOf(test[i]) < 0) return false;
  }
  return true;
}
```
👇 답안 2
```
function mutation(arr) {
  return arr[1]
    .toLowerCase()
    .split("")
    .every(function(letter) {
      return arr[0].toLowerCase().indexOf(letter) !== -1;
    });
}
```

### Chunky Monkey
```
function chunkArrayInGroups(arr, size) {
  let newarr = [];
  let length = Math.ceil(arr.length / size);
  for(let i = 0; i < length; i++) {
    let piece = arr.splice(0, size);
    newarr.push(piece);
  }
  console.log(newarr);
  return newarr;
}

chunkArrayInGroups(["a", "b", "c", "d"], 2);
chunkArrayInGroups([0, 1, 2, 3, 4, 5, 6], 3)
```
👇 답안 1
```
function chunkArrayInGroups(arr, size) {
  // Break it up.
  const newArr = [];
  for (let i = 0; i < arr.length; i += size) {
    newArr.push(arr.slice(i, i + size));
  }
  return newArr;
}
```
