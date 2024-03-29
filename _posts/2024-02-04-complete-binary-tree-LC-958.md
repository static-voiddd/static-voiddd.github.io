---
title: "958. Check Completeness of a Binary Tree"
tags: [leetcode, medium]
image: leetcode.png
featured: "true"
---

### | [Complete Binary Tree](https://leetcode.com/problems/check-completeness-of-a-binary-tree/)  | :orange_book:

Given the root of a binary tree, determine if it's a complete binary tree.
(Complete if u go left to right and its filled)

Complete Tree             | Not Complete Tree |
--------------------------|-------------------|
<img src="/images/complete-tree.png"> | <img src="/images/incomplete-tree.png"> | 

###  Notes  

> If you ever encounter a NULL node, you must not encounter a non NULL node after that in a Level Order Traversal, this is the definition of a complete Binary Tree.
   
1. Traverse by level using BFS 
2. A flag to track if u have encountered a null so far
3. If we encounter a non null after this flag is true, its not a complete tree

**Time Complexity - O(n) |** 
**Space Complexity - O(n)**

```java
class Solution {
    public boolean isCompleteTree(TreeNode root) {
        boolean nullNodeFound = false;
        Queue<TreeNode> q = new LinkedList<>();
        q.offer(root);

        while (!q.isEmpty()) {
            TreeNode temp = q.poll();

            if (temp == null)
                nullNodeFound = true;
            else {
                if (nullNodeFound)
                    return false;
                q.offer(temp.left);
                q.offer(temp.right);
            }
        }
        return true;
    }
}

```