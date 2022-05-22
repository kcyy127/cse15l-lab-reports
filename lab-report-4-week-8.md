# Lab Report 4

## Links to Repos

- My [markdown-parser](https://github.com/kcyy127/markdown-parser)

- The reviewed [markdown-parser](https://github.com/Steven-Hsu1/markdown-parser)

## Making the snippets into JUnit tests

Determined the expected outputs of the snippets by running them on [the CommonMark demo site](https://spec.commonmark.org/dingus/).

Expected outputs:
```
snippet 1
["`google.com", "google.com", "ucsd.edu"]

snippet 2
["a.com", "a.com(())", "example.com"]

snippet 3
["https://sites.google.com/eng.ucsd.edu/cse-15l-spring-2022/schedule"]
```

Turning the snippets into JUnit tests:

![Snippets into Junit tests](/images/report-4/snippet-junit-tests.png)

All 3 tests failed on my markdown-parser implementation:

![Mine failed 1](/images/report-4/my-fail-1.png)

![Mine failed 2](/images/report-4/my-fail-2.png)

All 3 tests failed on the reviewed markdown-parser implementation:

![Reviewed failed 1](/images/report-4/rev-fail-1.png)

![Reviewed failed 2](/images/report-4/rev-fail-2.png)

## Improving the code

### Snippet 1

We can get the code to work with backticks with a small (<10 lines) code change.

We'd need to preprocess the whole markdown String before running the `getLinks` method. 

We would need to first find all the valid backticks (i.e. backticks in parentheses of hyperlinks are not valid) in a line. Then, we would remove the text within the pairs of backticks, and then remove all the valid backticks we found. 

### Snippet 2

We can get the code to work with nested brackets, parentheses, and escaped characters with a small (<10 lines) code change.

The general idea for checking nested links and parentheses is finding the very last possible index of a given symbol without hitting the next hyper link. We would take note of the index of the next open bracket (let's call this `n`), and for all three other symbols ("\]", "(" and ")"), try to find the next valid index of the symbol that did not exceed `n`.

For escaped characters, we'd just check if the character before is a backslash. If a backslash exists there, then the program would search for the next symbol in the text.

### Snippet 3

We can get the code to work with line breaks with a small (<10 lines) code change.

We would first get the indexes of all the line breaks. Then while searching for brackets and parentheses, we would check if any line breaks existed between open bracket and closing parentheses. If a line break existed, we would skip to find the next hyperlink.