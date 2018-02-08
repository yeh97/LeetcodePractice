

### Leetcode 105
#### [Construct Binary Tree from Preorder and Inorder Traversal](https://leetcode.com/problems/construct-binary-tree-from-preorder-and-inorder-traversal)

  

##### ***Problem:***

    Given preorder and inorder traversal of a tree, 
    construct the binary tree.
    
    You may assume that duplicates do not exist in the tree.


##### ***Example:***

    Input: [3,9,20,15,7], [9,3,15,20,7]
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
    public TreeNode buildTree(int[] preorder, int[] inorder) {
        // duplicates do not exist
        if (preorder == null || inorder == null) return null;
        HashMap inorderMap = new HashMap<Integer, Integer>();
        for (int i = 0; i < inorder.length; i++) {
            inorderMap.put(inorder[i], i);
        }
        return buildTree(preorder, 0, preorder.length - 1,
                        inorder, 0, inorder.length - 1, inorderMap);
    }
    private TreeNode buildTree(int[] preorder, int preL, int preR,
                          int[] inorder, int inL, int inR, HashMap inorderMap) {
        if (preL > preR || inL > inR) return null;
        TreeNode root = new TreeNode(preorder[preL]);
        int cutIndex = (Integer) inorderMap.get(preorder[preL]);
        root.left = buildTree(preorder, preL + 1, cutIndex - inL + preL,
                             inorder, inL, cutIndex - 1, inorderMap);
        root.right = buildTree(preorder, cutIndex - inR + preR + 1, preR,
                             inorder, cutIndex + 1, inR, inorderMap);
        return root;
    }
}
```

##### *Method #2*
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
    public TreeNode buildTree(int[] preorder, int[] inorder) {
        // duplicates do not exist
        // preorder : N -> L -> R
        // inorder : L -> N -> R
        if (preorder == null || inorder == null) return null;
        return buildTree(preorder, inorder, Long.MIN_VALUE);
    }
    private TreeNode buildTree(int[] preorder, int[] inorder, long val) {
        if (p >= preorder.length || inorder[i] == val) return null;
        TreeNode root = new TreeNode(preorder[p]);
        p++;
        // if preorder[p + 1, k] --> leftChild
        // <--> if inorder[i] == preorder[p] leftChild end
        root.left = buildTree(preorder, inorder, root.val);
        // p = k + 1 --> rightChild
        i++;
        root.right = buildTree(preorder, inorder, val);
        return root;
    }
}
```


