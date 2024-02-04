---
title: "791. Custom Sort String"
tags: [leetcode, medium]
image: leetcode.png
featured: "true"
---

### | [Custom Sort String](https://leetcode.com/problems/custom-sort-string/)  | :orange_book: 

You are given two strings order and s. All the characters of order are unique and were sorted in some custom order previously.

Permute the characters of s so that they match the order that order was sorted. More specifically, if a character x occurs before a character y in order, then x should occur before y in the permuted string.

Return any permutation of s that satisfies this property.


Input             | Output |
------------------|--------|
order = "cba", s = "abcd" &nbsp; &nbsp;    | cbad  
order = "cbafg", s = "abcd" &nbsp; &nbsp;  | cbad
order = "cbafg", s = "aabcccdfg" &nbsp; &nbsp;  | cccbaafgd |
order = "cba", s = "aabcccdfg" &nbsp; &nbsp;  | cccbaadgf or cccbaagdf (last elements order does not matter) |

###  Notes  

1. Keep a hashmap for count of chars from s, eg a - 2, b - 1 , c-3, d - 1, f- 1, g-1 on 4th example
2. Now loop through 'order', and check for each element of o, on our hashmap what was our key's value.
3. If key exists, then append x times to our string builder, eg - append c 3 times.
4. Once we append, on that loop remove the key
5. Continue through all.
6. At the end if hashmap is not empty, then we have to append remaining chars to our stringbuilder
7. Return the stringBuilder.toString()

> Note- Instead of hashmap we could also use array of 26 chars, where we would write the count on corresponding index. (2nd solution below)

**Time Complexity - O(length of s) since we have to max scan through whole of s |** 
**Space Complexity - Same as time**

```java
class Solution {
    public String customSortString(String order, String s) {
        HashMap<Character, Integer> hashMap = new HashMap<>();
        StringBuilder str = new StringBuilder();

        for(char ch: s.toCharArray()) {
             hashMap.put(ch, hashMap.getOrDefault(ch, 0)+1);
        }

        for (char o: order.toCharArray()) {
            if (hashMap.containsKey(o)) {
                while (hashMap.get(o) > 0) {
                    str.append(o);
                    hashMap.replace(o, hashMap.get(o) - 1);
                }
            }
        }

        //remaining keys with > 0 just gets added at the end
        for (char key : hashMap.keySet()) {
            while (hashMap.get(key) > 0) {
                str.append(key);
                hashMap.replace(key, hashMap.get(key) - 1);
            }
        }
        return str.toString();
    }
}

```
---

```java
class Solution {
    public String customSortString(String order, String s) {
        int[] count = new int[26];
        StringBuilder str = new StringBuilder();

        for (char ch : s.toCharArray()) {
            // ch -'a' gets us the index, we +1 before adding a value to the index
            // since its count of occurence
            // ch - 'a' when char is a is 0,
            // ch - 'a' when char is d is 3
            //System.out.println("Char " + ch + " :" + (ch-'a'));
            ++count[ch - 'a'];
        }
        //count of 'abcdg' = [1,1,1,1,0,0,1,0...0 (till 26)]
        
        for (char c : order.toCharArray()) {
            // while we found the count of char c (-- we are doing -- opposite to above doing ++ )is > 0 
            while (count[c - 'a']-- > 0) {
                str.append(c);
            }
        }

        // remaining items we loop from a to z since count had 26 chars
        // if original count for 'abcdg' = [1,1,1,1,0,0,1,0...0 (till 26)]
        // order was cba
        // at this point, count = [0,0,0,1,0,0,1,0...0 (till 26)]

        for (char c = 'a'; c <= 'z'; ++c) {
            while (count[c - 'a']-- > 0) {
                str.append(c);
            }
        }
        return str.toString();
    }

}

```