

### Leetcode 107
#### [Binary Tree Level Order Traversal II](https://leetcode.com/problems/binary-tree-level-order-traversal-ii)

  

##### ***Problem:***

    Given a binary tree, 
    return the bottom-up level order traversal of its nodes' values. 
    (ie, from left to right, level by level from leaf to root).


##### ***Example:***

    Input: [3,9,20,null,null,15,7]
             3
           /    \
          9      20
                /  \
               15   7
        Output: [[15,7],[9,20],[3]]

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
    public List<List<Integer>> levelOrderBottom(TreeNode root) {
        List<List<Integer>> ret = new ArrayList<List<Integer>>();
        levelOrderBottom(ret, root, 0);
        return ret;
    }
    private void levelOrderBottom(List<List<Integer>> list,
                                 TreeNode root, int depth) {
        if (root == null) return;
        if (depth >= list.size()) list.add(0, new LinkedList<Integer>());
        list.get(list.size() - 1 - depth).add(root.val);
        levelOrderBottom(list, root.left, depth + 1);
        levelOrderBottom(list, root.right, depth + 1);
    }
}
```


