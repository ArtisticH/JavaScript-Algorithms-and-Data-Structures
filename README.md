# Basic JavaScript

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

 
 
