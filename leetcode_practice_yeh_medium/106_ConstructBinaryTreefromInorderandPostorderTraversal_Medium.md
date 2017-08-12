

### Leetcode 106
#### [Construct Binary Tree from Inorder and Postorder Traversal](https://leetcode.com/problems/construct-binary-tree-from-inorder-and-postorder-traversal)

  

##### ***Problem:***

    Given inorder and postorder traversal of a tree, 
    construct the binary tree.
    
    You may assume that duplicates do not exist in the tree.


##### ***Example:***

    Input: [9,3,15,20,7], [9,15,7,20,3]
             3
           /    \
          9      20
                /  \
               15   7
        Output: [3,9,20,null,null,15,7]

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
    private int p = 0;
    private int i = 0;
    public TreeNode buildTree(int[] inorder, int[] postorder) {
        if (inorder == null || postorder == null) return null;
        // inorder : L -> N -> R
        // postorder : L -> R -> N
        p = i = postorder.length - 1;
        return buildTree(postorder, inorder, Long.MIN_VALUE);
    }
    // similar to : leetcode 105
    private TreeNode buildTree(int[] postorder, int[] inorder, long val) {
        if (p < 0 || inorder[i] == val) return null;
        TreeNode root = new TreeNode(postorder[p]);
        p--;
        // if preorder[k, p - 1] --> rightChild
        // <--> if inorder[i] == preorder[p] leftChild end
        root.right = buildTree(postorder, inorder, root.val);
        // p = k - 1 --> leftChild
        i--;
        root.left = buildTree(postorder, inorder, val);
        return root;
    }
}
```


