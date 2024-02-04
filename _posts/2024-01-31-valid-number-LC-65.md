---
title: "65. Valid Number"
tags: [leetcode, hard]
image: leetcode.png
featured: "true"
---

### | [Valid Number](https://leetcode.com/problems/valid-number/)  | :red_circle: 

A valid number can be split up into these components (in order):

1. A decimal number or an integer.
2. (Optional) An 'e' or 'E', followed by an integer.
   
A decimal number can be split up into these components (in order):
1. (Optional) A sign character (either '+' or '-').
2. One of the following formats:
* One or more digits, followed by a dot '.'.
* One or more digits, followed by a dot '.', followed by one or more digits.
* A dot '.', followed by one or more digits.

An integer can be split up into these components (in order)
1. (Optional) A sign character (either '+' or '-').
2. One or more digits.

Valid             | Invalid |
------------------|--------|0
2   &nbsp; &nbsp;  | e3  
0089 &nbsp; &nbsp; | 99e2.5 
-0.1 &nbsp; &nbsp; | 1a |
+3.14 &nbsp; &nbsp;| 1e | 
+6e-1 &nbsp; &nbsp; | -.9 |
2e10 &nbsp; &nbsp;  | 95a54e53 |
-90e3 &nbsp; &nbsp; | -+3 | 
3e+7 &nbsp; &nbsp;  | --6

###  Notes  

1. Declare 3 variables seenDigit, seenExponent, and seenDot. Set all of them to false.
2. Iterate over the input.
   
> Rules - 
3. If the character is a digit, set seenDigit = true.
4. If the character is a sign, check if it is either the first character of the input, or if the character before it is an exponent. If not, return false.
5. If the character is an exponent, first check if we have already seen an exponent or if we have not yet seen a digit. If either is true, then return false. Otherwise, set seenExponent = true, and seenDigit = false. We need to reset seenDigit because after an exponent, we must construct a new integer.
6. If the character is a dot, first check if we have already seen either a dot or an exponent. If so, return false. Otherwise, set seenDot = true.
7. If the character is anything else, return false.

At the end, return seenDigit. This is one reason why we have to reset seenDigit after seeing an exponent - otherwise an input like "21e" would be incorrectly judged as valid.

**Time Complexity - O(n) since we scanned only once through whole string |** 
**Space Complexity - O(1)**

```java
class Solution {
    public boolean isNumber(String s) {
        boolean seenDigit = false;
        boolean seenExponent = false;
        boolean seenDot = false;

        for (int i = 0; i < s.length(); i++) {
            char curr = s.charAt(i);
            if (Character.isDigit(curr)) {
                seenDigit = true;
            } else if (curr == '+' || curr == '-') {
                // if we see plus, minus,either it should be at first index or
                // item before it should be 'e' or 'E', otherwise its invalid
                if (i > 0 && s.charAt(i - 1) != 'e' && s.charAt(i - 1) != 'E') {
                    return false;
                }
            } else if (curr == 'e' || curr == 'E') {
                // if previously exponent was already seen or
                // if we are seeing it first time but have never seen a digit yet
                // then its invalid
                if (seenExponent || !seenDigit)
                    return false;
                seenExponent = true;
                // if we see a exponent, we have to reset the seenDigit flag
                // because we need to see a new integer once we have seen exponent
                seenDigit = false;
            } else if (curr == '.') {
                // if we already saw Dot or exponent, then we cannot again have a dot
                // only integer is allowed after we saw exponent, not dot
                if (seenDot || seenExponent)
                    return false;
                seenDot = true;
            } else {
                return false;
            }
        }

        return seenDigit;
    }
}

```