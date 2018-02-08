

### Leetcode 103
#### [Binary Tree Zigzag Level Order Traversal](https://leetcode.com/problems/binary-tree-zigzag-level-order-traversal)

  

##### ***Problem:***

    Given a binary tree, 
    return the zigzag level order traversal of its nodes' values. 
    (ie, from left to right, then right to left for the next level and alternate between).


##### ***Example:***

    Input: [3,9,20,null,null,15,7]
             3
           /    \
          9      20
                /  \
               15   7
        Output: [[3],[20,9],[15,7]]

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
    public List<List<Integer>> zigzagLevelOrder(TreeNode root) {
        List<List<Integer>> ret = new ArrayList<List<Integer>>();
        zigzagLevelOrder(ret, root, 0);
        return (List<List<Integer>>) ret;
    }
    private void zigzagLevelOrder(List<List<Integer>> list, 
                                  TreeNode root, int depth) {
        if (root == null) return;
        if (depth >= list.size()) {
            list.add(new LinkedList<Integer>());
        } 
        if (depth % 2 == 0) {
            ((LinkedList<Integer>) (list.get(depth))).addLast(root.val);
        } else {
            ((LinkedList<Integer>) (list.get(depth))).addFirst(root.val);
        } 
        zigzagLevelOrder(list, root.left, depth + 1);
        zigzagLevelOrder(list, root.right, depth + 1);
    }
}
```


