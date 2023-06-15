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
You learned how to match literal patterns (`/literal/`) and wildcard character (`/./`).  
Those are the extremes of regular expressions, where one finds exact matches and the other matches everything.  
There are options that are a balance between the two extremes.  
  
You can search for a literal pattern with some flexibility with *character classes*.  
Character classes allow you to define a group of characters you wish to match by placing them inside square (`[` and `]`) brackets.  
For example, you want to match `bag`, `big`, and `bug` but not `bog`.  
You can create the regex /`b[aiu]g`/ to do this. The `[aiu]` is the character class that will only match the characters `a`, `i`, or `u`.
  
Inside a character set, you can define a range of characters to match using a hyphen character: `-`.  
For example, to match lowercase letters a through e you would use `[a-e]`.  
Not limited to letters. It also works to match a range of numbers.  
For example, /`[0-5]`/ matches any number between 0 and 5, including the 0 and 5.  
Also, it is possible to combine a range of letters and numbers in a single character set.
```
let jennyStr = "Jenny8675309";
let myRegex = /[a-z0-9]/ig;
jennyStr.match(myRegex);
// [ 'J', 'e', 'n', 'n', 'y', '8', '6', '7', '5', '3', '0', '9' ]
```

### Match Single Characters Not Specified
you could also create a set of characters that you do not want to match. These types of character sets are called negated character sets.  
To create a negated character set, you place a caret character (`^`) after the opening bracket and before the characters you do not want to match.  
  
For example, `/[^aeiou]/gi` matches all characters that are not a vowel.  
Note that characters like `.`, `!`, `[`, `@`, `/` and white space are matched - the negated vowel character set only excludes the vowel characters.
```
let quoteSample = "3 blind mice.";
let myRegex = /[^aeiou0-9]/gi; // Change this line
let result = quoteSample.match(myRegex); // Change this line
console.log(result);
// [ ' ', 'b', 'l', 'n', 'd', ' ', 'm', 'c', '.' ]
```

### Match Characters that Occur One or More Times
You can use the `+` character to check if that is the case.  
Remember, the character or pattern has to be present consecutively. That is, the character has to repeat one after the other.

For example, `/a+/g` would find one match in `abc` and return `["a"]`. Because of the `+`, it would also find a single match in `aabc` and return `["aa"]`.

If it were instead checking the string `abab`, it would find two matches and return `["a", "a"]` because the a characters are not in a row - there is a b between them.  
Finally, since there is no a in the string `bcd`, it wouldn't find a match.
```
let difficultSpelling = "Mississippi";
let myRegex = /s+/g; // Change this line
let result = difficultSpelling.match(myRegex);
console.log(result); // [ 'ss', 'ss' ]
```

### Match Characters that Occur Zero or More Times
There's also an option that matches characters that occur zero or more times.
```
let soccerWord = "gooooooooal!";
let gPhrase = "gut feeling";
let oPhrase = "over the moon";
let goRegex = /go*/;
soccerWord.match(goRegex); // ["goooooooo"]
gPhrase.match(goRegex); // ["g"]
oPhrase.match(goRegex); // null
```

### Find Characters with Lazy Matching
In regular expressions, a *greedy* match finds the longest possible part of a string that fits the regex pattern and returns it as a match.  
The alternative is called a *lazy* match, which finds the smallest possible part of the string that satisfies the regex pattern.

You can apply the regex `/t[a-z]*i/` to the string `"titanic"`. This regex is basically a pattern that starts with `t`, ends with `i`, and has some letters in between.
Regular expressions are by default greedy, so the match would return `["titani"]`. It finds the largest sub-string possible to fit the pattern.

However, you can use the `?` character to change it to *lazy matching*. `"titanic"` matched against the adjusted regex of `/t[a-z]*?i/` returns `["ti"]`.
?는 최소한의 문자열을 매칭하려고 한다. 
```
let text = "<h1>Winter is coming</h1>";
let myRegex = /<.*?>/; // Change this line
let result = text.match(myRegex);
console.log(result);
```
### Find One or More Criminals in a Hunt



