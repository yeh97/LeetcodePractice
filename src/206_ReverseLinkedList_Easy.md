


### Leetcode 206
#### [Reverse Linked List](https://leetcode.com/problems/reverse-linked-list)

  

##### ***Problem:***

	Reverse a singly linked list.
	
##### ***Example:***

    Input: 1->2->3->4
        Output: 4->3->2->1

##### *Method #1*
``` java
/*
 *Author: yeh
 *Time: 2018_02_11
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
    public ListNode reverseList(ListNode head) {
        // 2018/2/11 : 0ms
        if (head == null) return null;
        ListNode cur = head;
        ListNode next = null;
        ListNode pre = null;
        while (cur != null) {
            next = cur.next;
            cur.next = pre;
            pre = cur;
            cur = next;
        }
        return pre;
    }
}

```
