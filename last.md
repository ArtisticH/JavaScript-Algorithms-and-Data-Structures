# JavaScript Algorithms and Data Structures Projects

### Palindrome Checker
Return `true` if the given string is a palindrome. Otherwise, return `false`.  
A palindrome is a word or sentence that's spelled the same way both forward and backward, ignoring punctuation, case, and spacing.  
Note: You'll need to remove all non-alphanumeric characters (punctuation, spaces and symbols) and turn everything into the same case (lower or upper case) in order to check for palindromes.  
We'll pass strings with varying formats, such as `racecar`, `RaceCar`, and `race CAR` among others.  
We'll also pass strings with special symbols, such as `2A3*3a2`, `2A3 3a2`, and `2_A3*3#A2`.
```
function palindrome(str) {
  // 숫자와 알파벳만 남기기.
  str = str.replace(/[^a-zA-Z0-9]+/g, '').toLowerCase();
  let copy = str.split('').reverse().join('');
  return str === copy;
}

palindrome("eye");
palindrome("_eye");
palindrome("race car");
palindrome("not a palindrome");
palindrome("A man, a plan, a canal. Panama");
palindrome("never odd or even");
palindrome("My age is 0, 0 si ega ym.");
palindrome("0_0 (: /-\ :) 0-0");
palindrome("five|\_/|four");
```

### Roman Numeral Converter

### Caesars Cipher
One of the simplest and most widely known ciphers is a Caesar cipher, also known as a shift cipher.  
In a shift cipher the meanings of the letters are shifted by some set amount.  
A common modern use is the ROT13 cipher, where the values of the letters are shifted by 13 places. Thus `A ↔ N`, `B ↔ O` and so on.  
Write a function which takes a ROT13 encoded string as input and returns a decoded string.  
All letters will be uppercase. Do not transform any non-alphabetic character (i.e. spaces, punctuation), but do pass them on.  
```
function rot13(str) {
  let answer = str.split('').map(item => {
    let code = item.charCodeAt(0);
    return !/[A-Z]/.test(item)
            ? item : code >= 78
            ? String.fromCharCode(code-13)
            : String.fromCharCode(code+13)
    }
  );
  return answer.join('');
}

rot13("SERR PBQR PNZC");
rot13("SERR CVMMN!");
rot13("SERR YBIR?");
rot13("GUR DHVPX OEBJA SBK WHZCF BIRE GUR YNML QBT.");
```

### Telephone Number Validator

