

### Leetcode 116
#### [Populating Next Right Pointers in Each Node](https://leetcode.com/problems/populating-next-right-pointers-in-each-node)

  

##### ***Problem:***

    Given a binary tree : 

    struct TreeLinkNode {
      TreeLinkNode *left;
      TreeLinkNode *right;
      TreeLinkNode *next;
    }

    Populate each next pointer to point to its next right node.
    If there is no next right node, 
    the next pointer should be set to NULL.

    Initially, all next pointers are set to NULL.
    
##### ***Note:***

    1) You may only use constant extra space.
    2) You may assume that it is a perfect binary tree 
       (ie, all leaves are at the same level, and every parent has two children).


##### ***Example:***

    Input:   1
            / \
           2   3
        Output:    1 -> null
                 /   \
                2  -> 3 -> null

##### *Method #1*
``` java
/*
 *Author: yeh
 *Time: 2017_08_14
 *Language: Java
 *
 */

/**
 * Definition for binary tree with next pointer.
 * public class TreeLinkNode {
 *     int val;
 *     TreeLinkNode left, right, next;
 *     TreeLinkNode(int x) { val = x; }
 * }
 */
public class Solution {
    public void connect(TreeLinkNode root) {
        if (root == null) return;
        root.next = null;
        while (root.left != null) {
            TreeLinkNode curParent = root;
            while (curParent.next != null) {
                curParent.left.next = curParent.right;
                curParent.right.next = curParent.next.left;
                curParent = curParent.next;
            }
            curParent.left.next = curParent.right;
            curParent.right.next = null;
            root = root.left;
        }
    }
}

```


