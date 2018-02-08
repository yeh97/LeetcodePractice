

### Leetcode 111
#### [Minimum Depth of Binary Tree](https://leetcode.com/problems/minimum-depth-of-binary-tree)

  

##### ***Problem:***

    Given a binary tree, 
    find its minimum depth.

    The minimum depth is the number of nodes along the shortest path 
    from the root node down to the nearest leaf node.


##### ***Example:***

    Input: [1,2]
        Output: 2

##### *Method #1*
``` java
/*
 *Author: yeh
 *Time: 2017_08_13
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
    public int minDepth(TreeNode root) {
        if (root == null) return 0;
        if (root.left == null) return 1 + minDepth(root.right);
        if (root.right == null) return 1 + minDepth(root.left);
        return 1 + Math.min(minDepth(root.left), minDepth(root.right));
    }
}

```


