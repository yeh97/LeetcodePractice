

### Leetcode 114
#### [Flatten Binary Tree to Linked List](https://leetcode.com/problems/flatten-binary-tree-to-linked-list)

  

##### ***Problem:***

    Given a binary tree, 
    flatten it to a linked list in-place.
    (inorder : n -> l -> r)


##### ***Example:***

    Input: [1,2,null,3,4]
        Output: [1,null,2,null,null,3,4]

##### *Method #1*
``` java
/*
 *Author: yeh
 *Time: 2017_08_14
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
    public void flatten(TreeNode root) {
        // must inorder : N -> L -> R
        while (root != null) {
            //    a         a
            //   / \  ->     \
            //  lc  rc       lc
            //                 \
            //                 rc
            if (root.left != null) {
                TreeNode troot = root;
                TreeNode right = root.right;
                root.right = root.left;
                root.left = null;
                while (troot.right != null) {
                    troot = troot.right;
                }
                troot.right = right;
            }
            while (root != null && root.left == null) {
                root = root.right;
            }
        }
    }
}

```


