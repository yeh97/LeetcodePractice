

### Leetcode 142
#### [Linked List Cycle II](https://leetcode.com/problems/linked-list-cycle-ii)

  

##### ***Problem:***

    Given a linked list, 
    return the node where the cycle begins. 
    If there is no cycle, return null.

    Note: Do not modify the linked list.
    
    O(1) space

    
##### ***Example:***

    Input: [null]
        Output: null

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
    public ListNode detectCycle(ListNode head) {
        // cycle : A -a-> B -b-> C -c-> B
        // --> cycle begin : B
        // --> C : fast == slow
        // --> 2 * (a + b) = a + b + c + b
        // --> a = c
        // --> length(A -> B) = length(C -> B)
        if (head == null) return null;
        ListNode fast = head;
        ListNode slow = head;
        boolean hasCycle = false;
        while (!hasCycle && fast.next != null && fast.next.next != null) {
            fast = fast.next.next;
            slow = slow.next;
            if (fast == slow) hasCycle = true;
        }
        if (!hasCycle) return null;
        // cur slow = fast = C
        // node = A
        for (ListNode node = head; node != slow; node = node.next) {
            slow = slow.next;
        }
        return slow;
    }
}


```


