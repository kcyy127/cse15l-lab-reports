# Lab Report 2

## Change 1

Changes made:

![Diff 1](/images/diff_1.png)

The [test file](https://github.com/kcyy127/markdown-parser/blob/main/test-file2.md) that failed.

The error message:

![Error 1](/images/error_1.png)

Our code failed to account for image links in the file, which look very similar to hyperlinks except for an exclamation point in the front. The symptom of this bug was the parser incorrectly including image links along with hyperlinks, and the failure-inducing input was any file that included images.

---

## Change 2

Changes made:

![Diff 2](/images/diff_2.png)

The [test file](https://github.com/kcyy127/markdown-parser/blob/main/test-file3.md) that failed.

The error message:

![Error 2](/images/error_2.png)

The bug in our code was not verifying that `openParen` and `closeParen` were within bounds before attempting to retrieve a substring between those two indices from the text. The failure-inducing input was a file that contained an incomplete hyperlink (missing "(") and the symptom was an StringIndexOutOfBoundsException.

---

## Change 3

Changes made:

![Diff 2](/images/diff_3.png)

The [test file](https://github.com/kcyy127/markdown-parser/blob/main/test-file4.md) that failed.

The error message:

![Error 3](/images/error_3.png)

Our code did not skip escape characters in the markdown file. The failure-inducing input was a file that contained `\[` or `\]` and the symptom was our program including links it was not supposed to.