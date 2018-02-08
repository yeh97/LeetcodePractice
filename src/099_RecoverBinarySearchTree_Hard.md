

### Leetcode 99
#### [Recover Binary Search Tree](https://leetcode.com/problems/recover-binary-search-tree)

  

##### ***Problem:***

    Two elements of a binary search tree (BST) are swapped by mistake.

    Recover the tree without changing its structure.
    
    Need a constant space solution.


##### ***Example:***

    Input: [0, 1]
        Output: [1, 0]

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
    private TreeNode pre = null;
    private TreeNode first = null;
    private TreeNode second = null;
    public void recoverTree(TreeNode root) {
        // only two element are swaped
        searchMistake(root);
        if (first != null && second != null) {
            swapVal(first, second);
        }
    }
    private void searchMistake(TreeNode root) {
        if (root == null) return;
        searchMistake(root.left);
        if (pre != null && root.val < pre.val) {
            if (first == null) first = pre;
            second = root;
        }
        pre = root;
        searchMistake(root.right);
    }
    private static void swapVal(TreeNode a, TreeNode b) {
        int x = a.val;
        a.val = b.val;
        b.val = x;
    }
}

```


