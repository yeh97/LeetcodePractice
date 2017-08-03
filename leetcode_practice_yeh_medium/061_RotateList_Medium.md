

### Leetcode 61
#### [Rotate List](https://leetcode.com/problems/rotate-list)

  

##### ***Problem:***

    Given a list, rotate the list to the right by k places, 
    where k is non-negative.
    
##### ***Note:***

    1) Given n will be between 1 and 9 inclusive
    2) list : has no loop
    
##### ***Example:***

    Input: 1->2->3->4->5->NULL, 2
        Output: 4->5->1->2->3->NULL


##### *Method #1*
``` java
/*
 *Author: yeh
 *Time: 2017_08_03
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
    public ListNode rotateRight(ListNode head, int k) {
        if (head == null || head.next == null || k == 0) return head;
        //length >= 2
        //tail->head->...->tail
        int length = toLoop(head);
        k = (k % length + length) % length;
        //rotate to the left by length - k
        ListNode newTail = head;
        for (int i = length - k - 1; i > 0; i--) {
            newTail = newTail.next;
        }
        ListNode newHead = newTail.next;
        newTail.next = null;
        return newHead;
    }
    private int toLoop(ListNode head) {
        if (head == null) return 0;
        ListNode tail = head;
        int length = 1;
        while (tail.next != null) {
            tail = tail.next;
            length++;
        }
        tail.next = head;
        return length;
    }
}

```

