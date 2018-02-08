

### Leetcode 104
#### [Maximum Depth of Binary Tree](https://leetcode.com/problems/maximum-depth-of-binary-tree)

  

##### ***Problem:***

    Given a binary tree, find its maximum depth.

    The maximum depth is the number of nodes along the longest path 
    from the root node down to the farthest leaf node.


##### ***Example:***

    Input: [1]
        Output: 1

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
    public int maxDepth(TreeNode root) {
        if (root == null) return 0;
        return 1 + Math.max(maxDepth(root.left), maxDepth(root.right));
    }
}
```


