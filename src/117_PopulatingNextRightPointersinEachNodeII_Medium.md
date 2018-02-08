

### Leetcode 117
#### [Populating Next Right Pointers in Each Node II](https://leetcode.com/problems/populating-next-right-pointers-in-each-node-ii)

  

##### ***Problem:***

    Follow up for problem "Populating Next Right Pointers in Each Node".

    What if the given tree could be any binary tree? 
    Would your previous solution still work?
    
##### ***Note:***

    1) You may only use constant extra space.
    

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
        // list : curPrev -> curNode
        TreeLinkNode curPrev = null;
        // TreeLinkNode curNode = null;
        // next list
        TreeLinkNode curNext = null;
        while (root != null) {
            curPrev = curNext = null;
            for (; root != null; root = root.next) {
                if (curNext == null) {
                    curNext = root.left != null ? 
                        root.left : root.right;
                }
                // curNode = root.left != null ? 
                //      root.left : root.right;
                if (root.left != null) {
                    curPrev = curPrev == null ? 
                        root.left : (curPrev.next = root.left);
                }
                if (root.right != null) {
                    curPrev = curPrev == null ? 
                        root.right : (curPrev.next = root.right);
                }
            }
            root = curNext;
        }
    }
}


```


