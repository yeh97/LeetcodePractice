

### Leetcode 94
#### [Binary Tree Inorder Traversal](https://leetcode.com/problems/binary-tree-inorder-traversal)

  

##### ***Problem:***

    Given a binary tree,
    return the inorder traversal of its nodes' values.
    

##### ***Example:***

    Input: "1, 4, 2, null, 3"
            1
           / \
          4   2
           \
            3
        Output: [4, 3, 1, 2]

##### *Method #1*
``` java
/*
 *Author: yeh
 *Time: 2017_08_10
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
    public List<Integer> inorderTraversal(TreeNode root) {
        List<Integer> ret = new LinkedList<Integer>();
        inorderTraversalDFS(ret, root);
        return ret;
    }
    private void inorderTraversalDFS(List<Integer> list, TreeNode root) {
        if (root == null) return;
        inorderTraversalDFS(list, root.left);
        list.add(root.val);
        inorderTraversalDFS(list, root.right);
    }
}

```


