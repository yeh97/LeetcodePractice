

### Leetcode 143
#### [Reorder List](https://leetcode.com/problems/reorder-list)

  

##### ***Problem:***

    Given a singly linked list L: 
    L0 -> L1 -> … -> Ln-1 -> Ln,
    reorder it to: 
    L0 -> Ln-> L1-> Ln-1 -> L2 -> Ln-2 -> …
    
    O(1) space

    
##### ***Example:***

    Input: [1,2,3]
        Output: [1,3,2]

##### *Method #1*
``` java
/*
 *Author: yeh
 *Time: 2017_08_26
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
class Solution {
    public void reorderList(ListNode head) {
        if (head == null || head.next == null) return;
        ListNode mid = getMidNode(head);
        ListNode prr = reverseList(mid.next);
        ListNode t = null;
        mid.next = null;
        // length(head -> null) >= length(prr -> null)
        for (ListNode node = head; prr != null; node = node.next) {
            t = prr.next;
            prr.next = node.next;
            node = node.next = prr;
            prr = t;
        }
    }
    public ListNode getMidNode(ListNode head) {
        if (head == null) return null;
        ListNode fast = head;
        ListNode slow = head;
        while (fast.next != null && fast.next.next != null) {
            fast = fast.next.next;
            slow = slow.next;
        }
        return slow;
    }
    public ListNode reverseList(ListNode head) {
        if (head == null) return null;
        ListNode phead = head;
        ListNode chead = null;
        while (head != null) {
            phead = head.next;
            head.next = chead;
            chead = head;
            head = phead;
        }
        return chead;
    }
}


```


