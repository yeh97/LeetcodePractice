

### Leetcode 145
#### [Binary Tree Postorder Traversal](https://leetcode.com/problems/binary-tree-postorder-traversal)

  

##### ***Problem:***

    Given a binary tree, 
    return the postorder traversal of its nodes' values.

    
##### ***Example:***

    Input: [1,2,3,4]
        Output: [4,2,3,1]

##### *Method #1*
``` java
/*
 *Author: yeh
 *Time: 2017_08_27
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
    public List<Integer> postorderTraversal(TreeNode root) {
        // L -> R -> N
        List<Integer> list = new ArrayList<Integer>();
        if (root == null) return list;
        Stack<TreeNode> t = new Stack<TreeNode>();
        TreeNode cur = root;
        TreeNode pre = root;
        t.push(cur);
        while (!t.isEmpty()) {
            cur = (TreeNode) t.peek();
            if ((cur.left == null && cur.right == null) 
                || (pre == cur.left || pre == cur.right)) {
                // leaf or child has been read
                t.pop();
                list.add(cur.val);
                pre = cur;
            } else {
                // L -> R --> push into stack : R L
                if (cur.right != null) t.push(cur.right);
                if (cur.left != null) t.push(cur.left);
            }
        }
        return list;
    }
}


```

##### *Method #2*
``` java
/*
 *Author: yeh
 *Time: 2017_08_27
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
    public List<Integer> postorderTraversal(TreeNode root) {
        // L -> R -> N
        List<Integer> list = new ArrayList<Integer>();
        if (root == null) return list;
        Stack<TreeNode> t = new Stack<TreeNode>();
        TreeNode cur = null;
        t.push(root);
        while (!t.isEmpty()) {
            // N -> R -> L
            cur = (TreeNode) t.pop();
            list.add(cur.val);
            // push : L R
            if (cur.left != null) t.push(cur.left);
            if (cur.right != null) t.push(cur.right);
        }
        Collections.reverse(list);
        return list;
    }
}


```

##### *Method #3*
``` java
/*
 *Author: yeh
 *Time: 2017_08_27
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
    public List<Integer> postorderTraversal(TreeNode root) {
        // L -> R -> N
        List<Integer> list = new ArrayList<Integer>();
        postorderTraversal(list, root);
        return list;
    }
    private void postorderTraversal(List<Integer> list, TreeNode root) {
        if (root == null) return;
        postorderTraversal(list, root.left);
        postorderTraversal(list, root.right);
        list.add(root.val);
    }
}

```


