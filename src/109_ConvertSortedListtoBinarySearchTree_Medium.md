

### Leetcode 109
#### [Convert Sorted List to Binary Search Tree](https://leetcode.com/problems/convert-sorted-list-to-binary-search-tree)

  

##### ***Problem:***

    Given a singly linked list 
    where elements are sorted in ascending order, 
    convert it to a height balanced BST.


##### ***Example:***

    Input: [3,7,9,15,20]
        Output: [9,3,15,null,7,null,20]

##### *Method #1*
``` java
/*
 *Author: yeh
 *Time: 2017_08_13
 *Language: Java
 *
 */

/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
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
    private ListNode currentNode = null;
    public TreeNode sortedListToBST(ListNode head) {
        this.currentNode = head;
        return sortedListToBST(0, getLength(head) - 1);
    }
    private TreeNode sortedListToBST(int l, int r) {
        if (l > r) return null;
        int mid = l + (r - l) / 2;
        TreeNode left = sortedListToBST(l, mid - 1);
        TreeNode root = new TreeNode(currentNode.val);
        root.left = left;
        currentNode = currentNode.next;
        root.right = sortedListToBST(mid + 1, r);
        return root;
    }
    private int getLength(ListNode head) {
        int ret = 0;
        for (ListNode p = head; p != null; p = p.next) {
            ret++;
        }
        return ret;
    }
}
```


