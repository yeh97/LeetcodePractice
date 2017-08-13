

### Leetcode 110
#### [Balanced Binary Tree](https://leetcode.com/problems/balanced-binary-tree)

  

##### ***Problem:***

    Given a binary tree, 
    determine if it is height-balanced.

    For this problem, 
    a height-balanced binary tree is defined as a binary tree 
    in which the depth of the two subtrees of every node never differ by more than 1.


##### ***Example:***

    Input: []
        Output: true

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
    public boolean isBalanced(TreeNode root) {
        return depth(root) != -1;
    }
    private int depth(TreeNode root) {
        // if unbalanced, return -1
        // else return the height of root
        if (root == null) return 0;
        int ld = depth(root.left);
        int rd = depth(root.right);
        if (ld == -1 || rd == -1 || Math.abs(ld - rd) > 1) {
            return -1;
        } else {
            return 1 + Math.max(ld, rd);
        }
    }
}
```


