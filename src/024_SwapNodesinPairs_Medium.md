

### Leetcode 24
#### [Swap Nodes in Pairs](https://leetcode.com/problems/swap-nodes-in-pairs)

    Given a linked list, 
    swap every two adjacent nodes and return its head.
    
***Example:***

    Input: 1->2->3->4
        Ouput: 2->1->4->3
    Input: 1->2->3
        Ouput: 2->1->3

##### *Method #1*
``` java
/*
 *Author: yeh
 *Time: 2017_07_11
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
    public ListNode swapPairs(ListNode head) {
        ListNode phead = new ListNode(0);
        ListNode pre = phead;
        ListNode t1 = null;
        ListNode t2 = null;
        pre.next = head;
        while(pre.next!=null && pre.next.next!=null) {
            //pre -> p1 -> p2 -> p3, t1 = p1
            t1 = pre.next;
            //t2 = p2
            t2 = pre.next.next;
            //pre -> p2 -> p3
            pre.next = t2;
            //p1 -> p3
            t1.next = t2.next;
            //p2 -> p1
            t2.next = t1;
            //pre -> p2 -> p1 -> p3
            //pre = p1
            pre = pre.next.next;
        }
        return phead.next;
    }
}

```
