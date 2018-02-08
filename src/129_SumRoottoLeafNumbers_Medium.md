

### Leetcode 129
#### [Sum Root to Leaf Numbers](https://leetcode.com/problems/sum-root-to-leaf-numbers)

  

##### ***Problem:***

    Given a binary tree containing digits from 0-9 only, 
    each root-to-leaf path could represent a number.

    An example is the root-to-leaf path 1->2->3 which represents the number 123.

    
##### ***Example:***

    Input: [1,2,3,null,4]
        Output: 137 (124 + 13)

##### *Method #1*
``` java
/*
 *Author: yeh
 *Time: 2017_08_22
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
    private int sum;
    public int sumNumbers(TreeNode root) {
        return sumNumbers(root, 0);
    }
    private int sumNumbers(TreeNode root, int prev) {
        if (root == null) return 0;
        prev = prev * 10 + root.val;
        if (root.left == null && root.right == null) {
            return prev;
        } else {
            return sumNumbers(root.left, prev) + sumNumbers(root.right, prev);
        }
    }
}

```


