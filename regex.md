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
### Match Beginning String Patterns

Outside of a character set, the caret is used to search for patterns at the beginning of strings.
```
let firstString = "Ricky is first and can be found.";
let firstRegex = /^Ricky/;
firstRegex.test(firstString); // TRUE
let notFirst = "You can't find Ricky now.";
firstRegex.test(notFirst); // FALSE
```

### Match Ending String Patterns
You can search the end of strings using the dollar sign character `$` at the end of the regex.
```
let theEnding = "This is a never ending story";
let storyRegex = /story$/;
storyRegex.test(theEnding); // TRUE
let noEnding = "Sometimes a story will have to end";
storyRegex.test(noEnding); // FALSE
```
### Match All Letters and Numbers
Using character classes, you were able to search for all letters of the alphabet with `[a-z]`.  
This kind of character class is common enough that there is a shortcut for it, although it includes a few extra characters as well.

The closest character class in JavaScript to match the alphabet is `\w`.  
This shortcut is equal to `[A-Za-z0-9_]`. This character class matches upper and lowercase letters plus numbers.  
Note, this character class also includes the underscore character (`_`).  
These shortcut character classes are also known as *shorthand character classes*.  
  
You can search for the opposite of the `\w` with `\W`. Note, the opposite pattern uses a capital letter.  
This shortcut is the same as `[^A-Za-z0-9_]`.

### Match All Numbers
The shortcut to look for digit characters is `\d`, with a lowercase d.  
This is equal to the character class `[0-9]`, which looks for a single character of any number between zero and nine.  
  
The shortcut to look for non-digit characters is `\D`.  
This is equal to the character class `[^0-9]`, which looks for a single character that is not a number between zero and nine.

### Restrict Possible Usernames
1. Usernames can only use alpha-numeric characters.
2. The only numbers in the username have to be at the end. There can be zero or more of them at the end. Username cannot start with the number.
3. Username letters can be lowercase and uppercase.
4. Usernames have to be at least two characters long. A two-character username can only use alphabet letters as characters.
```
let username = "JackOfAllTrades";
let userCheck = /^[a-zA-Z]([a-zA-Z]+|\d{2,})\d*$/; // Change this line
let result = userCheck.test(username);
```

👇 답안 1
```
let username = "JackOfAllTrades";
let userCheck = /^[a-z][a-z]+\d*$|^[a-z]\d\d+$/i;
let result = userCheck.test(username);
console.log(result)
```

### Match Whitespace
You can search for whitespace using `\s`, which is a lowercase s.  
This pattern not only matches whitespace, but also carriage return, tab, form feed, and new line characters.  
You can think of it as similar to the character class `[ \r\t\f\n\v]`.  
  
Search for non-whitespace using `\S`, which is an uppercase s.  
This pattern will not match whitespace, carriage return, tab, form feed, and new line characters.  
You can think of it being similar to the character class `[^ \r\t\f\n\v]`.  
  
### Specify Upper and Lower Number of Matches
You can specify the lower and upper number of patterns with quantity specifiers.  
Quantity specifiers are used with curly brackets (`{` and `}`). You put two numbers between the curly brackets - for the lower and upper number of patterns.  
  
For example, to match only the letter `a` appearing between 3 and 5 times in the string ah, your regex would be `/a{3,5}h/`.

### Specify Only the Lower Number of Matches
For example, to match only the string hah with the letter `a` appearing at least 3 times, your regex would be `/ha{3,}h/`.

### Specify Exact Number of Matches
For example, to match only the word hah with the letter a 3 times, your regex would be `/ha{3}h/`.  

### Check for All or None
You can specify the possible existence of an element with a question mark, `?`.  
This checks for zero or one of the preceding element.  
You can think of this symbol as saying the previous element is optional.  
  
```
let american = "color";
let british = "colour";
let rainbowRegex= /colou?r/;
rainbowRegex.test(american); // true
rainbowRegex.test(british); // true
```

### Positive and Negative Lookahead
Lookaheads(전방탐색) are patterns that tell JavaScript to look-ahead in your string to check for patterns further along. This can be useful when you want to search for multiple patterns over the same string.  
  
There are two kinds of lookaheads: positive lookahead and negative lookahead.  
  
A *positive* lookahead will look to make sure the element in the search pattern is there, but won't actually match it.  
A positive lookahead is used as `(?=...)` where the `...` is the required part that is not matched.
```
let quit = "qu";
let quRegex= /q(?=u)/;
quit.match(quRegex); // ["q"]
```
전방탐색은 패턴이 일치하는 위치를 찾을 때 다음 패턴이 뒤따라오는 경우에만 일치하는 것을 의미한다.  
예를 들어, 정규표현식 `foo(?=bar)`는 "foo"라는 문자열을 찾되, 뒤에 "bar"라는 문자열이 따라오는 경우에만 일치합니다. "foo"와 "bar" 사이에 다른 문자열이 있다면 일치하지 않습니다.  
  
On the other hand, a negative lookahead will look to make sure the element in the search pattern is not there.  
A negative lookahead is used as `(?!...)` where the `...` is the pattern that you do not want to be there.  
The rest of the pattern is returned if the negative lookahead part is not present.
```
let noquit = "qt";
let qRegex = /q(?!u)/;
noquit.match(qRegex); // ["q"]
```
A more practical use of lookaheads is to check two or more patterns in one string.  
Here is a (naively) simple password checker that looks for between 3 and 6 characters and at least one number:
```
let password = "abc123";
let checkPass = /(?=\w{3,6})(?=\D*\d)/;
checkPass.test(password);
```
3개에서 6개의 문자 또는 숫자로 이루어져 있으며, 최소한 한 개 이상의 숫자를 포함해야 한다. 

- Use lookaheads in the `pwRegex` to match passwords that are greater than 5 characters long, and have two consecutive digits.
```
let sampleWord = "astronaut";
let pwRegex = /(?=\w{6,})(?=\D*\d{2})/; // Change this line
let result = pwRegex.test(sampleWord);
```

### Check For Mixed Grouping of Characters
Sometimes we want to check for groups of characters using a Regular Expression and to achieve that we use parentheses `()`.  
  
If you want to find either Penguin or Pumpkin in a string, you can use the following Regular Expression: `/P(engu|umpk)in/g`.  
그룹 내에서 선택할 수 있는 여러 개의 패턴 중 하나와 일치하는지 확인할 수 있다.  
이를 통해 다양한 조건에 따라 패턴을 유연하게 지정할 수 있다.

### Reuse Patterns Using Capture Groups
일치하는 부분을 추출할 수 있다. 
Say you want to match a word that occurs multiple times like below.
```
let repeatStr = "row row row your boat";
```
You could use `/row row row/`, but what if you don't know the specific word repeated? *Capture groups* can be used to find repeated substrings.  
  
Capture groups are constructed by enclosing the regex pattern to be captured in parentheses. In this case, the goal is to capture a word consisting of alphanumeric characters so the capture group will be `\w+` enclosed by parentheses: `/(\w+)/`.  
  
The substring matched by the group is saved to a temporary "variable", which can be accessed within the same regex using a backslash and the number of the capture group (e.g. `\1`).  
Capture groups are automatically numbered by the position of their opening parentheses (left to right), starting at 1.
```
let repeatRegex = /(\w+) \1 \1/;
repeatRegex.test(repeatStr); // Returns true
repeatStr.match(repeatRegex); // Returns ["row row row", "row"]
```
Using the `.match()` method on a string will return an array with the matched substring, along with its captured groups.  

### Use Capture Groups to Search and Replace
You can search and replace text in a string using `.replace()` on a string.  
The inputs for `.replace()` is first the regex pattern you want to search for. The second parameter is the string to replace the match or a function to do something.  
```
let wrongText = "The sky is silver.";
let silverRegex = /silver/;
wrongText.replace(silverRegex, "blue");
```
You can also access capture groups in the replacement string with dollar signs (`$`).
```
"Code Camp".replace(/(\w+)\s(\w+)/, '$2 $1'); // Camp Code
```
### Remove Whitespace from Start and End
```
let hello = "   Hello, World!  ";
let wsRegex = /(\s+)(\w+,\s+\w+!)(\s+)/; // Change this line
let result = hello.replace(wsRegex, '$2'); // Change this line
```
👇 답안 1
```
let hello = "   Hello, World!  ";
let wsRegex = /^\s+|\s+$/g; // Change this line
let result = hello.replace(wsRegex, ""); // Change this line
```






