

### Leetcode 101
#### [Symmetric Tree](https://leetcode.com/problems/symmetric-tree)

  

##### ***Problem:***

    Given a binary tree, 
    check whether it is a mirror of itself 
    (ie, symmetric around its center).


##### ***Example:***

    Input: [1,2,2,3,4,4,3]
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
    public boolean isSymmetric(TreeNode root) {
        if (root == null) return true;
        return isSymmetric(root.left, root.right);
    }
    // return a is a mirror of b or not
    private boolean isSymmetric(TreeNode a, TreeNode b) {
        if (a == null || b == null) return a == null && b == null;
        return a.val == b.val &&
            isSymmetric(a.left, b.right) && isSymmetric(a.right, b.left);
    }
}

```


