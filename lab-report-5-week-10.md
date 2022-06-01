# Lab Report 5

## Finding tests with different results

Ran `vimdiff` for the 2 result files.

![vimdiff](/report-5/vimdiff.png)

## 1st test file

[510.md](/report-5/510.md)

Expected output (as per the [CommonMark demo site](https://spec.commonmark.org/dingus/))

```java
[]
```

`vimdiff` results:

![vimdiff-510](/report-5/vimdiff-510.png)

My implementation is correct.

Bug in the provided implementation:

![bug-510](/report-5/bug-510.png)

Lines 67 and 68 in `MarkdownParse.java` fail to catch `]` and `(` that are far apart. The method should instead search for the index of `](` to guarantee that the two symbols are adjacent.

## 2nd test file

[577.md](/report-5/577.md)

Expected output (as per the [CommonMark demo site](https://spec.commonmark.org/dingus/))

```
[]
```

![vimdiff-577](/report-5/vimdiff-577.png)

My implementation is correct.

Bug in the provided implementation: 

![bug-577](/report-5/bug-577.png)

Line 60 in `MarkdownParse.java` fails to filter out image links. The index of `nextOpenBracket` must be updated if the character at the index before is an exclamation point.