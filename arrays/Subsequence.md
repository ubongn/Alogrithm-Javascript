## Subsequence
Given two strings ***s*** and ***t***, return ***true*** if ***s*** is a **subsequence** of ***t***, or ***false*** otherwise.

A **subsequence** of a string is a new string that is formed from the original string by deleting some (can be none) of the characters without disturbing the relative positions of the remaining characters. (i.e., ***"ace"*** is a subsequence of ***"abcde"*** while ***"aec"*** is not).

 

Example 1:

    Input: s = "abc", t = "ahbgdc"

    Output: true

Example 2:

    Input: s = "axc", t = "ahbgdc"

    Output: false

## The code
```
var isSubsequence = function(s, t) {
    // "abc",  "ahbgdc"
    
    // abc       a(h)b(gd)c
    
    let i = 0
    let j = 0
    
    while (i < s.length && j < t.length) {
        if (s[i] === t[j]) {
            i += 1
            j += 1
        } else {
            j += 1
        }
    }
    
    return i === s.length
};

```