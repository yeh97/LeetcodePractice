

### Leetcode 144
#### [Binary Tree Preorder Traversal](https://leetcode.com/problems/binary-tree-preorder-traversal)

  

##### ***Problem:***

    Given a binary tree, 
    return the preorder traversal of its nodes' values.

    
##### ***Example:***

    Input: [1,2,4,3]
        Output: [1,2,3,4]

##### *Method #1*
``` java
/*
 *Author: yeh
 *Time: 2017_08_26
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
class Solution {
    public List<Integer> preorderTraversal(TreeNode root) {
        // N -> L -> R
        List<Integer> ret = new LinkedList<Integer>();
        preorderTraversal(ret, root);
        return ret;
    }
    private void preorderTraversal(List<Integer> list, TreeNode root) {
        if (root == null) return;
        list.add(root.val);
        preorderTraversal(list, root.left);
        preorderTraversal(list, root.right);
    }
}

```

##### *Method #2*
``` java
/*
 *Author: yeh
 *Time: 2017_08_26
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
class Solution {
    public List<Integer> preorderTraversal(TreeNode root) {
        List<Integer> list = new ArrayList<Integer>();
        if (root == null) return list;
        Stack<TreeNode> t = new Stack<TreeNode>();
        TreeNode cur = null;
        t.push(root);
        while (!t.isEmpty()) {
            // N -> L -> R
            cur = (TreeNode) t.pop();
            list.add(cur.val);
            // push : R L
            if (cur.right != null) t.push(cur.right);
            if (cur.left != null) t.push(cur.left);
        }
        return list;
    }
}

```

