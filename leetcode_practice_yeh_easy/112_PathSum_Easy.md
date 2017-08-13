

### Leetcode 112
#### [Path Sum](https://leetcode.com/problems/path-sum)

  

##### ***Problem:***

    Given a binary tree and a sum, 
    determine if the tree has a root-to-leaf path 
    such that adding up all the values along the path equals the given sum.


##### ***Example:***

    Input: [1,2], 1
        Output: false

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
    public boolean hasPathSum(TreeNode root, int sum) {
        if (root == null) return false;
        sum -= root.val;
        if (root.left == null && root.right == null) return 0 == sum;
        return hasPathSum(root.left, sum) || hasPathSum(root.right, sum);
    }
}

```


