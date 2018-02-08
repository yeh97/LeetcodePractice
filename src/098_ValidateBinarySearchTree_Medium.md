

### Leetcode 98
#### [Validate Binary Search Tree](https://leetcode.com/problems/validate-binary-search-tree)

  

##### ***Problem:***

    Given a binary tree, 
    determine if it is a valid binary search tree (BST).
    
    Assume a BST is defined as follows:

    1) The left subtree of a node contains only nodes with keys less than the node's key.
    2) The right subtree of a node contains only nodes with keys greater than the node's key.
    3) Both the left and right subtrees must also be binary search trees.


##### ***Example:***

    Input: "1, 4, 2, null, 3"
            1
           / \
          4   2
           \
            3
        Output: false

##### *Method #1*
``` java
/*
 *Author: yeh
 *Time: 2017_08_11
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
    public boolean isValidBST(TreeNode root) {
        // type of root.val : int
        return isValidBST(root, Long.MAX_VALUE, Long.MIN_VALUE);
    }
    private boolean isValidBST(TreeNode root, long up, long low) {
        if (root == null) return true;
        if (root.val >= up || root.val <= low) return false;
        return isValidBST(root.left, root.val, low) 
            && isValidBST(root.right, up, root.val);
    }
}

```


