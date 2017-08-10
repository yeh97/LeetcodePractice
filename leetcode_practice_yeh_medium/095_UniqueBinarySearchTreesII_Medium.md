

### Leetcode 95
#### [Unique Binary Search Trees II](https://leetcode.com/problems/binary-tree-inorder-traversal)

  

##### ***Problem:***

    Given an integer n, 
    generate all structurally unique BST's 
    (binary search trees) that store values 1...n.
    

##### ***Example:***

    Input: 2
        Output: [[1,null,2],[2,1]]

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
    public List<TreeNode> generateTrees(int n) {
        return (n < 1) ? 
            new LinkedList<TreeNode>() : generateTreesHelper(1, n);
    }
    private List<TreeNode> generateTreesHelper(int s, int e) {
        List<TreeNode> ret = new LinkedList<TreeNode>();
        if (s > e) {
            ret.add(null);
        } else {
            // if i is the root of tree
            for (int i = s; i <= e; i++) {
                List<TreeNode> left = generateTreesHelper(s, i - 1);
                List<TreeNode> right = generateTreesHelper(i + 1, e);
                for (TreeNode l : left) {
                    for (TreeNode r : right) {
                        TreeNode root = new TreeNode(i);
                        root.left = l;
                        root.right = r;
                        ret.add(root);
                    }
                }
            }
        }
        return ret;
    }
}

```


