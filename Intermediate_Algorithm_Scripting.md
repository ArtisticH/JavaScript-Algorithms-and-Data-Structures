# Intermediate Algorithm Scripting

### Sum All Numbers in a Range
```
function sumAll(arr) {
  // 오름차순 정렬
  arr.sort((a, b) => a === b ? 0 : a < b ? -1 : 1);
  let sum = 0;
  for(let i = arr[0]; i <= arr[1]; i++) {
    sum += i;
  }
  return sum;
}

sumAll([1, 4]);
sumAll([4, 1]);
sumAll([5, 10]);
```
### Diff Two Arrays
Compare two arrays and return a new array with any items only found in one of the two given arrays, but not both. In other words, return the symmetric difference of the two arrays.
```
// 서로의 배열에서 없는 요소 찾아서 합치기
function diffArray(arr1, arr2) {
  const first = arr1.filter(item => !arr2.includes(item));
  const second = arr2.filter(item => !arr1.includes(item));
  return first.concat(second);
}

console.log(diffArray([1, 2, 3, 5], [1, 2, 3, 4, 5]));
console.log(diffArray(["diorite", "andesite", "grass", "dirt", "pink wool", "dead shrub"], ["diorite", "andesite", "grass", "dirt", "dead shrub"]));
console.log(diffArray(["andesite", "grass", "dirt", "pink wool", "dead shrub"], ["diorite", "andesite", "grass", "dirt", "dead shrub"]));
console.log(diffArray(["andesite", "grass", "dirt", "dead shrub"], ["andesite", "grass", "dirt", "dead shrub"]));
console.log(diffArray([1, "calf", 3, "piglet"], [1, "calf", 3, 4]));
```

### Seek and Destroy
You will be provided with an initial array (the first argument in the destroyer function), followed by one or more arguments. Remove all elements from the initial array that are of the same value as these arguments.
```
function destroyer(arr) {
  // 인수들의 목록에서 배열 빼고 나머지를 배열로 만들고
  let args = [...arguments];
  let newArr = [];
  for(let i = 1; i < args.length; i++) {
    newArr.push(args[i]);
  }
  // 겹치지 않는 것들만 반환
  return arr.filter(item => !newArr.includes(item));
}

console.log(destroyer([1, 2, 3, 1, 2, 3], 2, 3));
console.log(destroyer([1, 2, 3, 5, 1, 2, 3], 2, 3));
console.log(destroyer([3, 5, 1, 2, 2], 2, 3, 5));
console.log(destroyer([2, 3, 2, 3], 2, 3));
console.log(destroyer(["tree", "hamburger", 53], "tree", 53));
console.log(destroyer(["possum", "trollo", 12, "safari", "hotdog", 92, 65, "grandma", "bugati", "trojan", "yacht"], "yacht", "possum", "trollo", "safari", "hotdog", "grandma", "bugati", "trojan"));
```
### Wherefore art thou
Make a function that looks through an array of objects (first argument) and returns an array of all objects that have matching name and value pairs (second argument). Each name and value pair of the source object has to be present in the object from the collection if it is to be included in the returned array.

For example, if the first argument is `[{ first: "Romeo", last: "Montague" }, { first: "Mercutio", last: null }, { first: "Tybalt", last: "Capulet" }]`, and the second argument is `{ last: "Capulet" }`, then you must return the third object from the array (the first argument), because it contains the name and its value, that was passed on as the second argument.
```
function whatIsInAName(collection, source) {
  let newArr = [];
  let legnth = Object.keys(source).length;
    for(let i = 0; i < collection.length; i++) {
      let count = 0;
      for(let property in source) {
        if (collection[i][property] === source[property]) {
          count++;
        }
      }
      if(count === legnth) {
        newArr.push(collection[i]);
      }
    }
  return newArr;
}

whatIsInAName([{ first: "Romeo", last: "Montague" }, { first: "Mercutio", last: null }, { first: "Tybalt", last: "Capulet" }], { last: "Capulet" });
whatIsInAName([{ "apple": 1 }, { "apple": 1 }, { "apple": 1, "bat": 2 }], { "apple": 1 });
whatIsInAName([{ "apple": 1, "bat": 2 }, { "bat": 2 }, { "apple": 1, "bat": 2, "cookie": 2 }], { "apple": 1, "bat": 2 }); 
whatIsInAName([{ "apple": 1, "bat": 2 }, { "apple": 1 }, { "apple": 1, "bat": 2, "cookie": 2 }], { "apple": 1, "cookie": 2 }) ;
whatIsInAName([{ "apple": 1, "bat": 2 }, { "apple": 1 }, { "apple": 1, "bat": 2, "cookie": 2 }, { "bat":2 }], { "apple": 1, "bat": 2 });
whatIsInAName([{"a": 1, "b": 2, "c": 3}], {"a": 1, "b": 9999, "c": 3});
whatIsInAName([{"a": 1, "b": 2, "c": 3, "d": 9999}], {"a": 1, "b": 9999, "c": 3});
```
👇답안 1
```
function whatIsInAName(collection, source) {
  const souceKeys = Object.keys(source);

  // filter the collection
  return collection.filter(obj => {
    for (let i = 0; i < souceKeys.length; i++) {
      if (obj[souceKeys[i]] !== source[souceKeys[i]]) {
        return false;
      }
    }
    return true;
  });
}
```
### Spinal Tap Case
Convert a string to spinal case. Spinal case is all-lowercase-words-joined-by-dashes.
```
function spinalCase(str) {
  // 대문자 앞에 공백 추가
  let newStr = '';
  for(let i = 0; i < str.length; i++) {
    if(/[A-Z]/.test(str[i])) {
      newStr += ` ${str[i]}`;
    } else {
      newStr += str[i];
    }
  }
  newStr = newStr.toLowerCase().trim().split(/\s+|_|-/).filter(item => item !== '');
  console.log(newStr.join('-'));
  return newStr.join('-');
}

spinalCase('This Is Spinal Tap');
spinalCase("thisIsSpinalTap");
spinalCase("The_Andy_Griffith_Show");
spinalCase("Teletubbies say Eh-oh");
spinalCase("AllThe-small Things");
```
👇답안 1
```
function spinalCase(str) {
  // Create a variable for the white space and underscores.
  var regex = /\s+|_+/g;

  // Replace low-upper case to low-space-uppercase
  str = str.replace(/([a-z])([A-Z])/g, "$1 $2");

  // Replace space and underscore with -
  return str.replace(regex, "-").toLowerCase();
}

// test here
spinalCase("This Is Spinal Tap");
```
### Pig Latin
Pig Latin is a way of altering English Words. The rules are as follows:

- If a word begins with a consonant, take the first consonant or consonant cluster, move it to the end of the word, and add `ay` to it.
- If a word begins with a vowel, just add `way` at the end.

```
function translatePigLatin(str) {
  if (/[aeiou]/.test(str[0])) {
    return `${str}way`
  } else {
    let notVowel = str.match(/[^aeiou]+/)[0];
    let arr = str.split('');
    arr.splice(0, notVowel.length);
    arr = arr.join('');
    return `${arr}${notVowel}ay`
  }
}

translatePigLatin("consonant");
translatePigLatin("paragraphs");
translatePigLatin("glove");
translatePigLatin("rhythm");
translatePigLatin("schwartz");
translatePigLatin("algorithm");
translatePigLatin("eight");
```
👇답안 1
```
function translatePigLatin(str) {
  let consonantRegex = /^[^aeiou]+/;
  let myConsonants = str.match(consonantRegex);
  return myConsonants !== null
    ? str
        .replace(consonantRegex, "")
        .concat(myConsonants)
        .concat("ay")
    : str.concat("way");
}

translatePigLatin("consonant");
```

### Search and Replace
Perform a search and replace on the sentence using the arguments provided and return the new sentence.
First argument is the sentence to perform the search and replace on.
Second argument is the word that you will be replacing (before).
Third argument is what you will be replacing the second argument with (after).
Note: Preserve the case of the first character in the original word when you are replacing it. For example if you mean to replace the word `Book` with the word `dog`, it should be replaced as `Dog`
```
function myReplace(str, before, after) {
  return before[0].toLowerCase() === before[0] ?
          str.replace(before, after[0].toLowerCase().concat(after.slice(1)))
            :str.replace(before, after[0].toUpperCase().concat(after.slice(1)));
}

console.log(myReplace("A quick brown fox jumped over the lazy dog", "jumped", "leaped"));
console.log(myReplace("He is Sleeping on the couch", "Sleeping", "sitting"));
```

### DNA Pairing
Pairs of DNA strands consist of nucleobase pairs. Base pairs are represented by the characters AT and CG, which form building blocks of the DNA double helix.

The DNA strand is missing the pairing element. Write a function to match the missing base pairs for the provided DNA strand. For each character in the provided string, find the base pair character. Return the results as a 2d array.

For example, for the input `GCG`, return `[["G", "C"], ["C","G"], ["G", "C"]]`
The character and its pair are paired up in an array, and all the arrays are grouped into one encapsulating array.
```
function pairElement(str) {
  return [...str].map(item => item === 'G' ? [item, 'C'] 
                        : item === 'C' ?  [item, 'G']
                        : item === 'T' ? [item, 'A']
                        : [item, 'T']);
}

console.log(pairElement("GCG"));
console.log(pairElement("ATCGA"));
console.log(pairElement("TTGAG"));
console.log(pairElement("CTCTA"));
```
### Missing letters
Find the missing letter in the passed letter range and return it.
If all letters are present in the range, return `undefined`.
```
function fearNotLetter(str) {
  let arr = 'abcdefghijklmnopqrstuvwxyz';
  let first = arr.indexOf(str[0]);
  let last = arr.indexOf(str[str.length-1]);
  arr = arr.slice(first, last+1)
  let answer = [...arr].filter(item => ![...str].includes(item));
  return answer[0];
}

fearNotLetter("abce");
fearNotLetter("abcdefghjklmno");
fearNotLetter("stvwx");
fearNotLetter("bcdf");
fearNotLetter("abcdefghijklmnopqrstuvwxyz");
```
👇답안 1
```
function fearNotLetter(str) {
  for (let i = 0; i < str.length; i++) {
    /* code of current character */
    const charCode = str.charCodeAt(i);

    /* if code of current character is not equal to first character + no of iteration
        then a letter was skipped */
    if (charCode !== str.charCodeAt(0) + i) {
      /* if current character skipped past a character find previous character and return */
      return String.fromCharCode(charCode - 1);
    }
  }
  return undefined;
}

// test here
fearNotLetter("abce");
```

### Sorted Union
Write a function that takes two or more arrays and returns a new array of unique values in the order of the original provided arrays.
In other words, all values present from all arrays should be included in their original order, but with no duplicates in the final array.
The unique numbers should be sorted by their original order, but the final array should not be sorted in numerical order.
```
function uniteUnique(arr) {
  const newArr = [];
  for(let i = 0; i < [...arguments].length; i++) {
    [...arguments][i].map(item => !newArr.includes(item)
                                    ? newArr.push(item)
                                    : null );
  }
  console.log(newArr);
  return newArr;
}

uniteUnique([1, 3, 2], [5, 2, 1, 4], [2, 1]);
uniteUnique([1, 2, 3], [5, 2, 1]);
uniteUnique([1, 2, 3], [5, 2, 1, 4], [2, 1], [6, 7, 8]);
uniteUnique([1, 3, 2], [5, 4], [5, 6]);
uniteUnique([1, 3, 2, 3], [5, 2, 1, 4], [2, 1]);
```

### Convert HTML Entities
Convert the characters `&`, `<`, `>`, `"` (double quote), and `'` (apostrophe), in a string to their corresponding HTML entities.
```
function convertHTML(str) {
  const entities = {
    '&': '&amp;',
    '<': '&lt;',
    '>': '&gt;',
    '"': '&quot;',
    "'": '&apos;'
  }

  let answer = [...str].map(item => item.match(/&|<|>|'|"/)
                  ? item.replace(item.match(/&|<|>|'|"/), entities[item.match(/&|<|>|'|"/)])
                  : item)
  return answer.join('');
}

convertHTML("Dolce & Gabbana");
convertHTML("Hamburgers < Pizza < Tacos");
convertHTML("Sixty > twelve");
convertHTML('Stuff in "quotation marks"');
convertHTML("Schindler's List");
convertHTML("<>");
```
👇답안 1
```
function convertHTML(str) {
  // Split by character to avoid problems.

  var temp = str.split("");

  // Since we are only checking for a few HTML elements, use a switch

  for (var i = 0; i < temp.length; i++) {
    switch (temp[i]) {
      case "<":
        temp[i] = "&lt;";
        break;
      case "&":
        temp[i] = "&amp;";
        break;
      case ">":
        temp[i] = "&gt;";
        break;
      case '"':
        temp[i] = "&quot;";
        break;
      case "'":
        temp[i] = "&apos;";
        break;
    }
  }

  temp = temp.join("");
  return temp;
}

//test here
convertHTML("Dolce & Gabbana");
```

### Sum All Odd Fibonacci Numbers
Given a positive integer `num`, return the sum of all odd Fibonacci numbers that are less than or equal to `num`.

The first two numbers in the Fibonacci sequence are 0 and 1. Every additional number in the sequence is the sum of the two previous numbers. The first seven numbers of the Fibonacci sequence are 0, 1, 1, 2, 3, 5 and 8.

For example, `sumFibs(10)` should return `10` because all odd Fibonacci numbers less than or equal to `10` are 1, 1, 3, and 5.
```
function sumFibs(num) {
  const fibs = [0, 1];
  let sum = 1;
  // 일단 1차망
  while(fibs[fibs.length - 1] <= num) {
    // 먼저 마지막 두 개 더해서 배열에 넣고
    fibs.push(fibs[fibs.length - 2] + fibs[fibs.length - 1]); 
    // 만약 마지막 숫자가 num보다 같거나 작고 odd일때만 더한다. 
    if(fibs[fibs.length - 1] <= num && fibs[fibs.length - 1] % 2 === 1) {
      sum += fibs[fibs.length - 1];
    } 
  }
  console.log(sum);
  return sum;
}

sumFibs(4);
sumFibs(1000);
sumFibs(4000000);
sumFibs(75024);
sumFibs(75025);
```
👇답안 1
```
function sumFibs(num) {
  let prevNumber = 0;
  let currNumber = 1;
  let result = 0;
  while (currNumber <= num) {
    if (currNumber % 2 !== 0) {
      result += currNumber;
    }
    currNumber += prevNumber;
    prevNumber = currNumber - prevNumber;
  }

  return result;
}

// test here
sumFibs(4);
```
### Sum All Primes
A prime number is a whole number greater than 1 with exactly two divisors: 1 and itself. For example, 2 is a prime number because it is only divisible by 1 and 2. In contrast, 4 is not prime since it is divisible by 1, 2 and 4.

Rewrite `sumPrimes` so it returns the sum of all prime numbers that are less than or equal to num.
```
function sumPrimes(num) {
  // 소수 판별 함수(약수가 1과 자기자신뿐)
  function isPrime(num) {
    let arr = [];
    for(let i = 1; i<= num; i++) {
      arr.push(i);
    }
    arr = arr.filter(item => num % item === 0);
    // 약수가 2개면 소수이고, 아니면 0 반환
    return arr.length === 2 ? num : 0;
  }
  let sum = 0;
  // 소수인 애들만 더해
  for(let i = 2; i <= num; i++) {
    sum += isPrime(i);
  }
  console.log(sum);
  return sum;
}

sumPrimes(10);
sumPrimes(5);
sumPrimes(977);
```
👇답안 1
```
function sumPrimes(num) {
  // Helper function to check primality
  function isPrime(num) {
    const sqrt = Math.sqrt(num);
    for (let i = 2; i <= sqrt; i++) {
      if (num % i === 0)
        return false;
    }
    return true;
  }

  // Check all numbers for primality
  let sum = 0;
  for (let i = 2; i <= num; i++) {
    if (isPrime(i))
      sum += i;
  }
  return sum;
}
```
### Smallest Common Multiple
Find the smallest common multiple of the provided parameters that can be evenly divided by both, as well as by all sequential numbers in the range between these parameters.

The range will be an array of two numbers that will not necessarily be in numerical order.

For example, if given 1 and 3, find the smallest common multiple of both 1 and 3 that is also evenly divisible by all numbers between 1 and 3. The answer here would be 6.
```
function smallestCommons(arr) {
  // 오름차순 정렬
  let sorted = arr.sort((a,b) => a === b ? 0 : a < b ? -1 : 1);
  // 배열 범위 만들기
  let seq = [];
  let multiple = 1;
  for (let i = arr[0]; i <= arr[1]; i++) {
    seq = seq.concat(i)
    multiple *= i;
  }
  // 가장 큰 수의 배수들 중에서 나머지 배열로 하나씩 나눌 때 나머지가 모두 0인 수
  for(let k = arr[1]; k <= multiple; k += arr[1]) {
    let count = 0;
    for(let d = 0; d < seq.length - 1; d++) {
      if(k % seq[d] === 0) count++;
      if(count === seq.length - 1) return k;
    }
  }
}

console.log(smallestCommons([1,5]));
console.log(smallestCommons([2, 10]));
console.log(smallestCommons([1, 13]));
console.log(smallestCommons([23, 18]));
```
👇답안 1
```
function smallestCommons(arr) {
  // Setup
  const [min, max] = arr.sort((a, b) => a - b);
  const numberDivisors = max - min + 1;
  // Largest possible value for SCM
  let upperBound = 1;
  for (let i = min; i <= max; i++) {
    upperBound *= i;
  }
  // Test all multiples of 'max'
  for (let multiple = max; multiple <= upperBound; multiple += max) {
    // Check if every value in range divides 'multiple'
    let divisorCount = 0;
    for (let i = min; i <= max; i++) {
      // Count divisors
      if (multiple % i === 0) {
        divisorCount += 1;
      }
    }
    if (divisorCount === numberDivisors) {
      return multiple;
    }
  }
}

smallestCommons([1, 5]);
```
👇답안 2
```
function smallestCommons(arr) {
  // Setup
  const [min, max] = arr.sort((a, b) => a - b);
  const range = Array(max - min + 1)
    .fill(0)
    .map((_, i) => i + min);
  // Largest possible value for SCM
  const upperBound = range.reduce((prod, curr) => prod * curr);
  // Test all multiples of 'max'
  for (let multiple = max; multiple <= upperBound; multiple += max) {
    // Check if every value in range divides 'multiple'
    const divisible = range.every((value) => multiple % value === 0);
    if (divisible) {
      return multiple;
    }
  }
}

smallestCommons([1, 5]);
```

