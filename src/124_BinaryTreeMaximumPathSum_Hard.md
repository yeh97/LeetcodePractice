

### Leetcode 124
#### [Binary Tree Maximum Path Sum](https://leetcode.com/problems/binary-tree-maximum-path-sum)

  

##### ***Problem:***

    Given a binary tree, find the maximum path sum.

    For this problem, 
    a path is defined as any sequence of nodes 
    from some starting node to any node in the tree along the parent-child connections. 
    The path must contain at least one node and does not need to go through the root.


##### ***Example:***

    Input: [1,2,3]
        Output: 6

##### *Method #1*
``` java
/*
 *Author: yeh
 *Time: 2017_08_17
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
    private int maxSum1;
    // private int maxSum2;
    private int maxSum;
    public int maxPathSum(TreeNode root) {
        // note : input : null
        //        output : -2147483648 (Integer.MIN_VALUE)
        //      : input : [-3]
        //      : output : -3 (must need at least a node)
        maxSum = maxSum1 = Integer.MIN_VALUE;
        maxSinglePathSum(root);
        return maxSum;
    }
    private void maxSinglePathSum(TreeNode root) {
        // maxSum1 : 
        // max path sum (node --> root)
        // maxSum2 : 
        // max path sum (node1 --> root --> node2)
        // maxSum : 
        // maxPathSum(TreeNode root)
        if (root == null) {
            maxSum1 = 0;
        } else {
            maxSinglePathSum(root.left);
            int left = Math.max(0, maxSum1);
            maxSinglePathSum(root.right);
            int right = Math.max(0, maxSum1);
            maxSum1 = Math.max(left, right) + root.val;
            // maxSum2 = left + right + root.val;
            maxSum = Math.max(maxSum, left + right + root.val);
        }
    }
}

```


