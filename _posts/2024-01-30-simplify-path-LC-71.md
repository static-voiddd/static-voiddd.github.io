---
title: "Simplify Path"
tags: [leetcode, medium]
image: leetcode.png
featured: "true"
number: 71
---

### | [Simplify Path](https://leetcode.com/problems/simplify-path/)  | :orange_book:  

Given a string path, which is an absolute path (starting with a slash '/') to a file or directory in a Unix-style file system, convert it to the simplified canonical path.

> "/a/./"   --> means stay at the current directory 'a'

> "/a/b/.." --> means jump to the parent directory
              from 'b' to 'a'

> "////"    --> consecutive multiple '/' are a  valid path, they are equivalent to single "/".

Input             | Output |
------------------|--------|
/home/     | /home 
/a/./b/../../c/ | /c |
/a/.. | /
/a/../ | /
/../../../../../a | /a
/a/./b/./c/./d/ | /a/b/c/d
/a/../.././../../. &nbsp; &nbsp; | /
/a//b//c//////d &nbsp; &nbsp;|     /a/b/c/d

### Notes

1. Split string input with .split(“/”)
2. Loop through the splitted string array
3. Use stack to keep track of each element 
4. Only add to stack if it's anything other than [.. or / or .]
5. If we encounter .., check if stack has any element and pop last one
6. Finally add to stringbuilder using / before every stack read using for loop(if u use for loop, we can read from beginning to top of stack)

**Time Complexity - O(n)** |
**Space Complexity - O(n)**  

```java
class Solution {
    public String simplifyPath(String path) {
        StringBuilder builder = new StringBuilder();
        Stack<String> stack = new Stack<>();
        String[] components = path.split("/");

        for (String dir : components) {
            if (dir.equals(".") || dir.isEmpty()) {
                continue;
            } else if (dir.equals("..")) {
                if (!stack.isEmpty()) {
                    stack.pop();
                }
            } else {
                stack.add(dir);
            }
        }

        for (String dir : stack) {
            builder.append("/");
            builder.append(dir);
        }

        return builder.length() > 0 ? builder.toString() : "/";
    }
}

```