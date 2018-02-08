

### Leetcode 82
#### [Remove Duplicates from Sorted List II](https://leetcode.com/problems/remove-duplicates-from-sorted-list-ii)

  

##### ***Problem:***

    Given a sorted linked list, delete all nodes that have duplicate numbers, 
    leaving only distinct numbers from the original list.

##### ***Example:***

    Input: 1->2->3->3->4->4->5
        Output: 1->2->5

##### *Method #1*
``` java
/*
 *Author: yeh
 *Time: 2017_08_08
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
public class Solution {
    public ListNode deleteDuplicates(ListNode head) {
        ListNode preHead = new ListNode(0);
        preHead.next = head;
        ListNode preNode = preHead;
        ListNode nextNode = null;
        int currentVal;
        while (preNode.next != null) {
            if (preNode.next.next == null) break;
            currentVal = preNode.next.val;
            if (preNode.next.next.val == currentVal) {
                nextNode = preNode.next.next.next;
                while (nextNode != null && nextNode.val == currentVal) {
                    nextNode = nextNode.next;
                }
                preNode.next = nextNode;
            } else {
                preNode = preNode.next;
            }
        }
        return preHead.next;
    }
}

```


