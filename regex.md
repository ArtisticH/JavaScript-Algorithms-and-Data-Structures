# Regular Expressions

### Using the Test Method
Regular expressions are used in programming languages to match parts of strings.  
You create patterns to help you do that matching.  
  
If you want to find the word `the` in the string `The dog chased the cat`, you could use the following regular expression: `/the/`.  
Notice that quote marks are not required within the regular expression.  
  
JavaScript has multiple ways to use regexes.One way to test a regex is using the `.test()` method.  
The `.test()` method takes the regex, applies it to a string (which is placed inside the parentheses), and returns `true` or `false` if your pattern finds something or not.
```
let testStr = "freeCodeCamp";
let testRegex = /Code/;
testRegex.test(testStr);
```

### Match Literal Strings
```
let testStr = "Hello, my name is Kevin.";
let testRegex = /Kevin/;
testRegex.test(testStr); // true
```
Any other forms of `Kevin` will not match. For example, the regex `/Kevin/` will not match `kevin` or `KEVIN`.
```
let wrongRegex = /kevin/;
wrongRegex.test(testStr); // false
```
  
You can search for multiple patterns using the `alternation` or `OR` operator: `|`.  
This operator matches patterns either before or after it. For example, if you wanted to match the strings `yes` or `no`, the regex you want is `/yes|no/`.  
Like `/yes|no|maybe/`, You can also search for more than just two patterns.

### Ignore Case While Matching
Case (or sometimes letter case) is the difference between uppercase letters and lowercase letters.  
You can match both cases using what is called a flag. There are other flags but here you'll focus on the flag that ignores case - the `i` flag.  
An example of using this flag is `/ignorecase/i`. This regex can match the strings `ignorecase`, `igNoreCase`, and `IgnoreCase`.  

### Extract Matches
So far, you have only been checking if a pattern exists or not within a string.  
You can also extract the actual matches you found with the `.match()` method.  
```
"Hello, World!".match(/Hello/); // ["Hello"]
let ourStr = "Regular expressions";
let ourRegex = /expressions/;
ourStr.match(ourRegex); // ["expressions"]
```
Note that the `.match` syntax is the "opposite" of the `.test` method you have been using thus far.  
    
To search or extract a pattern more than once, you can use the global search flag: `g`.
```
let testStr = "Repeat, Repeat, Repeat";
let repeatRegex = /Repeat/g;
testStr.match(repeatRegex); // ["Repeat", "Repeat", "Repeat"]
```
### Match Anything with Wildcard Period
The wildcard character `.` will match any *one* character. The wildcard is also called `dot` and `period`.  
You can use the wildcard character just like any other character in the regex.  
For example, if you wanted to match `hug`, `huh`, `hut`, and `hum`, you can use the regex `/hu./` to match all four words.  
  
### Match Single Character with Multiple Possibilities
