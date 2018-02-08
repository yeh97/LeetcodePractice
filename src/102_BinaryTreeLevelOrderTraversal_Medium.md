

### Leetcode 102
#### [Binary Tree Level Order Traversal](https://leetcode.com/problems/binary-tree-level-order-traversal)

  

##### ***Problem:***

    Given a binary tree, 
    return the level order traversal of its nodes' values. 
    (ie, from left to right, level by level).


##### ***Example:***

    Input: [3,9,20,null,null,15,7]
             3
           /    \
          9      20
                /  \
               15   7
        Output: [[3],[9,20],[15,7]]

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
    public List<List<Integer>> levelOrder(TreeNode root) {
        List<List<Integer>> ret = new ArrayList<List<Integer>>();
        levelOrder(ret, root, 0);
        return ret;
    }
    private void levelOrder(List<List<Integer>> list, 
                           TreeNode root, int depth) {
        if (root == null) return;
        if (depth >= list.size()) {
            List<Integer> level = new LinkedList<Integer>();
            level.add(root.val);
            list.add(level);
        } else {
            list.get(depth).add(root.val);
        }
        levelOrder(list, root.left, depth + 1);
        levelOrder(list, root.right, depth + 1);
    }
}

```


