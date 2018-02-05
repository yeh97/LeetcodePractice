


### Leetcode 173
#### [Binary Search Tree Iterator](https://leetcode.com/problems/binary-search-tree-iterator)

  

##### ***Problem:***

	Implement an iterator over a binary search tree (BST). Your iterator will be initialized with the root node of a BST.

	Calling next() will return the next smallest number in the BST.

##### ***Notes:***
* next() and hasNext() should run in average O(1) time and uses O(h) memory, where h is the height of the tree.
##### ***Example:***

    Input: [5,2,6,null,4]
        Output: [2,4,5,6]


##### *Method #1*
``` java
/*
 *Author: yeh
 *Time: 2018_02_05
 *Language: Java
 *
 */

/**
 * Definition for binary tree
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */

public class BSTIterator {
    // 2018/2/5 : 6ms
    
    // top of minstack is current smallest elem
    Stack<TreeNode> minstack = null;

    public BSTIterator(TreeNode root) {
        minstack = new Stack<TreeNode>();
        for (TreeNode cur = root; cur != null; cur = cur.left) {
            minstack.push(cur);
        }
    }

    /** @return whether we have a next smallest number */
    public boolean hasNext() {
        return !minstack.empty();
    }

    /** @return the next smallest number */
    public int next() {
        if (!hasNext()) return 0; // err
        TreeNode top = minstack.pop();
        // BSTIterator(top) --> add it (not include top) to minstack
        for (TreeNode cur = top.right; cur != null; cur = cur.left) {
            minstack.push(cur);
        }
        return top.val;
    }
}

/**
 * Your BSTIterator will be called like this:
 * BSTIterator i = new BSTIterator(root);
 * while (i.hasNext()) v[f()] = i.next();
 */

```





