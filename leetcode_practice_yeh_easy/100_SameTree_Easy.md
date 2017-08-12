

### Leetcode 100
#### [Same Tree](https://leetcode.com/problems/same-tree)

  

##### ***Problem:***

    Given two binary trees, 
    write a function to check if they are equal or not.

    Two binary trees are considered equal 
    if they are structurally identical and the nodes have the same value.


##### ***Example:***

    Input: [1], [1]
        Output: true

##### *Method #1*
``` java
/*
 *Author: yeh
 *Time: 2017_08_12
 *Language: Java
 *
 */

/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
public class Solution {
    public boolean isSameTree(TreeNode p, TreeNode q) {
        if (p == null || q == null) return p == null && q == null;
        return p.val == q.val && 
            isSameTree(p.left, q.left) && isSameTree(p.right, q.right);
    }
}

```


