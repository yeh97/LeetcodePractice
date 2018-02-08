

### Leetcode 141
#### [Linked List Cycle](https://leetcode.com/problems/linked-list-cycle)

  

##### ***Problem:***

    Given a linked list, 
    determine if it has a cycle in it.
    
    O(1) space

    
##### ***Example:***

    Input: [null]
        Output: false

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
 * class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) {
 *         val = x;
 *         next = null;
 *     }
 * }
 */
public class Solution {
    public boolean hasCycle(ListNode head) {
        if (head == null) return false;
        ListNode fast = head;
        ListNode slow = head;
        while (fast.next != null && fast.next.next != null) {
            fast = fast.next.next;
            slow = slow.next;
            if (fast == slow) return true;
        }
        return false;
    }
}


```


